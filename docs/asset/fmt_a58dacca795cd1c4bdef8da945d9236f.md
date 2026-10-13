
古典音乐爱好者会立即发现这张 CD 的数据库条目存在小问题；该盘的 1-15 节与拉威尔的《西班牙狂想曲》完全无关。无论如何，`tracknames.pl` 在目录中留了一个名为 `backup.sh` 的小脚本，包含一组命令。列表 11 显示了该盘的内容。

# 使用 cdda2wav 为音频 CD 准备 WAV 镜像

## 列表 11.4 `tracknames.pl` 的结果。

```
mv audio_01.wav Rapsodie_Espagnole-01-Promenade.wav

mv audio_02.wav Rapsodie_Espagnole-02-Gnomus.wav

mv audio_03.wav Rapsodie_Espagnole-03-Promenade.wav

mv audio_04.wav Rapsodie_Espagnole-04-Il_vecchio_castello.wav

mv audio_05.wav Rapsodie_Espagnole-05-Promenade.wav

mv audio_06.wav Rapsodie_Espagnole-06-Tuilleries.wav

mv audio_07.wav Rapsodie_Espagnole-07-Bydlo.wav

mv audio_08.wav Rapsodie_Espagnole-08-Promenade.wav

mv audio_09.wav \
Rapsodie_Espagnole-09-Ballet_des_Petits_Poussins_dans_leurs_Coques.wav

mv audio_10.wav Rapsodie_Espagnole-10-Samuel_Goldberg_und_Schmuyle.wav

mv audio_11.wav Rapsodie_Espagnole-11-Limoges_Le_Marchi.wav

mv audio_12.wav Rapsodie_Espagnole-12-Catacombee_Sepulchrum-Romanum.wav

mv audio_13.wav Rapsodie_Espagnole-13-comortuis_in_lingua_morta.wav

mv audio_14.wav \
Rapsodie_Espagnole-14-La_Cabane_de_Baba_Yoga_des_Pattes_de_Poule.wav

mv audio_15.wav Rapsodie_Espagnole-15-La-Grande_Porte_de_Kiev.wav

mv audio_16.wav Rapsodie_Espagnole-16-Pavane_de_La_Belle_au_Bois_Bormant.wav

mv audio_17.wav Rapsodie_Espagnole-17-Petit_Poucet.wav

mv audio_18.wav Rapsodie_Espagnole-18-Laideronette_Impratrice_des_Pagodes.wav

mv audio_19.wav Rapsodie_Espagnole-19-Entretiens_de_La_Belle_et_la_Bjte.wav

mv audio_20.wav Rapsodie_Espagnole-20-Le_Jardin_Fierique.wav

mv audio_21.wav Rapsodie_Espagnole-21-Prilude_la_Nuit.wav

mv audio_22.wav Rapsodie_Espagnole-22-Malaguena.wav

mv audio_23.wav Rapsodie_Espagnole-23-Habanera.wav

mv audio_24.wav Rapsodie_Espagnole-24-Feria.wav
```

# 第 11 章 / 刻刻光盘

```
mv audio_19.wav Rapsodie_Espagnole-19-Entretiens_de_la_Belle_et_Bjte.wav
mv audio_20.wav Rapsodie_Espagnole-20-Le_Jardin_Fierique.wav
mv audio_21.wav Rapsodie_Espagnole-21-Prilude_la_Nuit.wav
mv audio_22.wav Rapsodie_Espagnole-22-Malaguena.wav
mv audio_23.wav Rapsodie_Espagnole-23-Habanera.wav
mv audio_24.wav Rapsodie_Espagnole-24-Feria.wav
```

此脚本没有设置执行权限，因此最简单的运行方法是：

```
sh rename
```

该脚本对于第 3 到第 5 节以外的所有轨道都会失败，导致大量的错误信息。如果你打算立即将这些 WAV 文件写入 CD-R，你可能不想运行此脚本。`tracknames.pl` 不移动与每个 WAV 文件关联的 `.inf` 文件。`.inf` 文件包含预间隙信息，可以在写入空白 CD-R 时使用。

`cdrecord` 分发的未来版本可能具有增强的 CDDB 功能。由于 CDDB 数据库不是免费的，`cdrecord` 分发中的程序将使用 `www.cdindex.org`。当你读到这里时，支持可能已经发生了变化。

## 使用 cdrecord 将音频镜像刻入 CDR

一组 WAV 文件（以 44.1 kHz 的正确频率和正确的属性记录）可以通过以下形式调用 `cdrecord` 刻录到空白 CD-R：

```
/opt/schily/bin/cdrecord -v speed=2 dev=0,0,0 -pad -useinfo \
-audio *.wav
```
