
```
wget ftp://ftp.ncbi.nlm.nih.gov/all/GCA/000/401/GCA_000001405.15_GRCh38/seqs_for_alignment_pipelines.ucsc_ids/GCA_000001405.15_GRCh38_no_alt_analysis_set.fna
```

使用此参考基因组的程序需要索引，所以让我们创建它们。

```
gunzip GCA_000001405.15_GRCh38_no_alt_analysis_set.fna
bwa index GCA_000001405.15_GRCh38_no_alt_analysis_set.fna
samtools fixidx GCA_000001405.15_GRCh38_no_alt_analysis_set.fna
```

现在我们有了一对 FASTQ 文件、一个参考基因组、BWA 比对结果以及将 FASTQ 比对到参考基因组的 Samtools 命令，并将输出直接管道到 Samtools 以进行压缩：

```bash
outputfile=my_fastq.bam
infile1=my_fastq.R1.fastq.gz
infile2=my_fastq.R2.fastq.gz
ref_fasta=ref.GCA_000001405.15_GRCh38_no_alt_analysis_set.fna
NCPUS=4 # 为了减少执行时间，尽可能使用所有可用 CPU
ID=HILLUMINA2AB1C4 # Illumina 平台单元，可能包含流式细胞和通道
PU=HILLUMINA2AB1C4:MY_SAMPLE_1 # Illumina 平台单元，可能包含流式细胞、通道和样本
LB=20200101 # 文库准备 ID
PL=ILLUMINA # 用于测序的平台技术
SM=SAMPLE_1_ # 样本标识符
read_group="@RG|ID:$ID|CPU:$PU|LB:$LB|tPL:$PL|tSM:$SM" #这将附加到输出中的每个读取，这样当读取来自时，下游质量控制算法就能正常工作
```

```bash
bwa mem -t $NCPUS -R "$read_group" $ref_fasta $infile1 $infile2 | samtools view -b - -o $outfile
```

# 第 8 章 处理序列数据

如第 4 章所述，制表符分隔的条目表示序列标识符（两个成对 read 相同，即该 read 及其配对）、该 read 映射到的染色体和位置、该 read 配对的相同信息、CIGAR 字段、标记（flag）、比对质量评分以及原始片段的长度。

在这里，我们的示例样本映射到 7 号染色体的位置 117559573，其配对映射到同一染色体（= 字段）的位置 117559783。CIGAR `67M3D83M` 表示 67+3D 个碱基与基因组完美匹配（M），中间有一个 3bp 的缺失（D）。标记 99 表示这是该配对中的第一个 read，且两个 read 都已映射。比对质量评分 60（最高分）表示具有极佳的比对质量，片段大小估计为 400 个碱基，这处于正常范围内。

BAM 文件的定义可以在 [`samtools.github.io/hts-specs/SAMv1.pdf`](https://samtools.github.io/hts-specs/SAMv1.pdf) BAM 文件规范的第 6 页找到。标记值在 [`broadinstitute.github.io/picard/explain-flags.html`](https://broadinstitute.github.io/picard/explain-flags.html) 中解释。输入 `sam_flag` 值，让我们为您解释该特定值。

## 对 BAM 文件中的比对 read 进行调整和优化

我们广泛遵循 Broad（Broad Institute）开发并推荐的最佳实践，并使用 Genome Analysis Toolkit (`GATK`) 软件处理比对过的序列 read。

让我们下载并安装 `GATK` 软件。访问 [`github.com/broadinstitute/gatk`](https://github.com/broadinstitute/gatk)，右键点击 `gatk` zip 文件并复制链接地址，下载 `GATK` 软件软件包。

```
wget https://github.com/broadinstitute/gatk/releases/download/4.3.0.0/gatk-4.3.0.0.zip
unzip gatk-4.3.0.0.zip
cd gatk-4.3.0.0
```

你将在 `README.md` 文件中看到 `GATK` 需要 Java 8 版本。如果你还没有安装 Java 8，请安装它。

```
sudo apt install openjdk-8-jre
```

在执行 `MarkDuplicates` 步骤的最佳实践中，测序的片段可能会被测序多次，例如 PCR 重复或光学重复。`MarkDuplicates` 会识别这些额外的 read 并将它们标记为重复，以便下游处理能够考虑此因素。我们为什么要考虑这一点呢？一个例子是，当软件进行变异检测时，必须判断 read 是否包含变异，以及是否有一半的 read 包含参考基因组值（如果变异在一条染色体上而在另一条上没有，这就是预期的结果）。如果包含变异的 read 存在额外的 PCR 或光学重复，而软件不知道它们是重复的，它就会错误地得出变异存在于两条染色体上的结论，而实际上它只位于其中一条染色体。

以下命令运行 `MarkDuplicates` 步骤。如果你由于有多个对 FASTQ 输入文件而有多个输入 BAM，那么在这里通过将所有文件作为输入输入到 `MarkDuplicates` 步骤来合并它们。

```
infile=my_bam.bam
outfile=my_bam_markdup.bam
```

```
java -server jar gatk-package-4.3.0.0-local.jar \
MarkDuplicates \
INPUT="$infile" \
OUTPUT="$outfile" \
METRICS_FILE=output_MarkDuplicatesMetrics.txt \
VALIDATION_STRIGENCY=SILENT \
OPTICAL_DUPLICATE_PIXEL_DISTANCE=2500 \
ASSUME_SORT_ORDER=queryname \
MAX_FILE_HANDLES=1000 \
MAX_RECORDS_IN_RAM=5000000 \
CLEAN_DT=false \
ADD_PG_TAG_TO_READS=false
```

```
# 如果有多个 bam 文件，请将上面的 INPUT 行替换为：
# INPUT=my_bam1.bam INPUT=my_bam2.bam INPUT=my_bam3.bam
```

检查 `MarkDuplicates` 步骤是否工作正常。

```
cat output_MarkDuplicatesMetrics.txt
```

如果 `MarkDuplicates` 步骤工作正常，上一个 `cat` 命令的输出如下：

No errors found

如果 `MarkDuplicates` 步骤工作正常，你可以删除它的输入文件以释放磁盘空间。

```
rm my_bam.bam
```

现在按染色体和坐标对 `MarkDuplicates` 的输出 bam 进行排序，以便其可以被 `SetNmAndUqTags` 步骤进行处理：

```
infile=my_bam_markdup.bam
outfile=my_bam_markdup_sort.bam
```

```
gatk SortSam \
  --INPUT "$infile" \
  --OUTPUT "$outfile" \
  --SORT_ORDER "coordinate" \
  --COMPRESSION_LEVEL 2 \
  --CREATE_INDEX false \
  --CREATE_MD5_FILE false
```

接下来，在 `SetNmAndUqTags` 步骤中，我们在 BAM 文件中添加额外的标签，这些标签将用于下游处理。

```
infile=my_bam_markup_sort.bam
outfile=my_bam_markup_sort_tags.bam
ref_fasta=GR38.fasta
```

```
gatk SetNmAndUqTags \
--INPUT "$infile" \
--OUTPUT "$outfile" \
--CREATE_INDEX true \
--REFERENCE "$ref_fasta"
```

验证我们的 BAM 文件以确保其正常。
