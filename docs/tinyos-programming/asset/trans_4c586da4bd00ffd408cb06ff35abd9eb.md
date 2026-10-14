

将数据存储在 Block 存储卷中。它随后会将此样本的摘要记录到循环日志中。因此，系统将始终具有最新的全保真度测量值，以及若干个保真度降低的旧测量值。

对于用于防盗应用的同一 mts300 传感器板的 micaz，以下 volumes 文件指定了 FlashSampler 的日志和块卷——64 kB 用于最新样本（SAMPLES），其余用于长期日志（SAMPLELOG）：

```
<volume_table>
    <volume name="SAMPLES" size="65536"/>
    <volume name="SAMPLELOG" size="458752"/>
</volume_table>
```

与其它存储抽象类似，块存储是通过实例化 BlockStorageC 组件并使用其 BlockRead 和 BlockWrite 接口来访问的，其中使用卷标识符：

```
generic configuration BlockStorageC(volume_id_t void) {
    provides interface BlockWrite;
    provides interface BlockRead;
}
```

Listing 6.33 BlockStorageC signature

要采样到闪存，我们使用 BlockWrite 接口：

```
interface BlockWrite {
    command error_t write(storage_addr_t addr, void* buf, storage_len_t len);
    event void writeDone(storage_addr_t addr, void* buf, storage_len_t len, error_t error);

    command error_t erase();
    event void eraseDone(error_t error);

    command error_t sync();
    event void syncDone(error_t error);
}
```

Listing 6.34 The BlockWrite interface

所有命令都是分阶段的：erase 在首次使用前擦除闪存，write 写入一些字节，sync 确保所有未完成的写入都物理存在于闪存上。

FlashSampler 使用 BlockWrite 和我们之前看到的 ReadStream 采样接口，同时采样并将结果保存到闪存。为此，它需要使用两个缓冲区：当一个缓冲区正在被采样时，另一个缓冲区被写入闪存。因此，最大采样率将同时受传感器最大采样率和闪存最大写入速率的限制。该方案在以下 AccelSamplerC 组件中实现，作为 Sample 接口提供的分阶段 sample-to-flash 命令（未显示）：

```
```nesc
// in flashSampler.h:
enum {
  SAMPLE_PERIOD = 1000,
  BUFFER_SIZE = 512,       // samples per buffer
  TOTAL_SAMPLES = 32768,   // must be multiple of BUFFER_SIZE
};

module AccelSamplerC
{
  provides interface Sample;
  uses interface ReadStream<uint16_t> as Accel;
  uses interface BlockWrite;
}
implementation
{
  uint16_t buffer1[BUFFER_SIZE], buffer2[BUFFER_SIZE];
  uint8_t nbuffers;  // how many buffers have been filled

  command void Sample.sample() {
    // Sampling requested, start by erasing the block
    call BlockWrite.erase();
  }

  event void BlockWrite.eraseDone(error_t ok) {
    // Block erased. Post both buffers & initiate sampling
    call Accel.postBuffer(buffer1, BUFFER_SIZE);
    call Accel.postBuffer(buffer2, BUFFER_SIZE);
    nbuffers = 0;
    call Accel.read(SAMPLE_PERIOD);
  }

  event void Accel.bufferDone(error_t ok, uint16_t *buf, uint16_t count) {
    // A buffer is full. Write it to the block
    call BlockWrite.write(nbuffers * sizeof *buffer1, buf, sizeof buffer1);
  }

  event void BlockWrite.writeDone(storage_addr_t addr, void *buf,
                                  storage_len_t len, error_t error) {
    // Buffer written. TOTAL_SAMPLES is multiple of BUFFER_SIZE,
    // once we've posted TOTAL_SAMPLES / BUFFER_SIZE buffers we're done.
    // As we started by posting two buffers, the test below includes a -2
    if (++nbuffers <= TOTAL_SAMPLES / BUFFER_SIZE - 2)
      call Accel.postBuffer(buf, BUFFER_SIZE);
    else if (nbuffers == TOTAL_SAMPLES / BUFFER_SIZE)
      // Once we've written all the buffers, flush writes to the buffer
      call BlockWrite.sync();
  }
}
```
```

```
event void BlockWrite.syncDone(error_t error) {
  signal Sample.sampled(error);
}
```

```
event void Accel.readDone(error_t ok, uint32_t usActualPeriod) {
  // If we didn't use all buffers something went wrong, e.g., flash writes were
  // too slow, so the buffers did not get reposted in time
  signal Sample.sampled(FAIL);
}
```

## Listing 6.35 Simultaneously sampling and storing to flash (most error checking omitted)

FlashSampler 的第二部分读取采样块，对其进行汇总，并将其写入循环日志。摘要仅为原始样本的 128 倍下采样（通过平均），因此长度为 512 字节。

读取块使用 BlockRead 接口完成：

```
interface BlockRead {
  command error_t read(storage_addr_t addr, void* buf, storage_len_t len);
  event void readDone(storage_addr_t addr, void* buf, storage_len_t len,
    error_t error);

  command error_t computeCrc(storage_addr_t addr, storage_len_t len,
    uint16_t crc);
  event void computeCrcDone(storage_addr_t addr, storage_len_t len,
    uint16_t crc, error_t error);

  command storage_len_t getSize();
}
```

## Listing 6.36 The BlockRead interface

它提供分阶段命令用于从块中读取和计算 CRC。日志抽象同时支持循环日志和线性日志，但选择必须在编译时按卷进行：

```
generic configuration LogStorageC(volume_id_t volId, bool circular) {
  provides interface LogWrite;
  provides interface LogRead;
}
```

## Listing 6.37 LogStorageC signature

