
如果在调用 `who` 时，`! -f`（不存在）测试失败，则该命令将不会在子 shell 中运行，因为 `test` 已经知道 AND (-a) 表达式为假。这虽然是一个细微的差别，但如果 shell 程序员试图在假设所有内容都在条件测试应用之前运行的情况下，向条件表达式中塞入过多的内容，这可能会让他们困扰。

## 括号

你可以在测试表达式中使用括号来根据需要更改评估顺序；只需确保括号本身被引号括起来，因为它们对 shell 具有特殊含义。因此，要将后来的表达式转换为 `test` 命令，你会写成：

```
[ "$count" -ge 0 -a "$count" -lt 10 ]
```

按照 usual惯例，括号周围必须有空格，因为 `test` 期望将条件语句中的每个元素都视为独立的参数。

## 逻辑或运算符 -O

`-o` 运算符与 `-a` 运算符类似，它仅用于形成两个表达式的逻辑或（OR）。这意味着，如果第一个表达式为真、第二个表达式为真或两者都为真，则该表达式的评估结果将为真。

```
[ -n "mailopt" -o -r $HOME/mailfile ]
```

如果变量 `mailopt` 不为空或文件 `$HOME/mailfile` 对你可读，则该命令将为真。

`-o` 运算符的优先级低于 `-a` 运算符，这意味着表达式

```
"$a" -eq 0 -o "$b" -eq 2 -a "$c" -eq 10
```

被 `test` 评估的方式为

```
"$a" -eq 0 -o "$b" -eq 2 -a "$c" -eq 10
```

当然，如果有必要，你可以使用括号来改变这种顺序：

```
( "$a" -eq 0 -o "$b" -eq 2 -a "$c" -eq 10 )
```

由于优先级在复杂的条件语句中至关重要，你会发现许多 shell 程序员使用嵌套的 `if` 语句来规避问题，而另一些人则使用显式括号来明确解释顺序。仅仅假设内容是从左到右解释的是危险的！

你将在书中看到许多 `test` 命令的用法，因为如果不涉及某种条件语句，编写 shell 程序几乎是不可能的。附录 A 中的表 A.11 总结了所有可用的 test 运算符。

## else 结构

一个名为 `else` 的结构可以添加到 `if` 命令中，其通用格式所示：

```
if command
then
    command
    command
    ..
else
    command
    command
    ..
```

在上述，`command` 被执行并评估其退出状态。如果为真（零），则执行 `then` 代码块（`then` 和 `else` 之间的所有语句），并忽略 `else` 块。
如果退出状态为假（非零），则忽略 `then` 代码块，并执行 `else` 代码块（所有其他内容以及 `fi`）。在任何情况下，只有一组命令会被执行：如果退出状态是执行的，则执行第一组；如果是非零，则执行第二组。

这可以用更简洁的方式表示：

```
if condition then statements-if-true else statements-if-false fi
```

让我们了解 `on` 的一个修改版本。如果请求的用户没有登录，我们不再让程序没有任何输出，而是让程序向用户报告这一事实。

这里是程序的第 3 版本：

```bash
$ cat on
#
# 确定是否有人登录 -- 版本 3
#
user="$user"
if who | grep "$user" > /dev/null
then
    echo "$user is logged on"
else
    echo "$user is not logged on"
fi
$
```

如果作为 `on` 的第一个参数的用户已登录，则 `grep` 将成功并显示消息 `user is logged on`；否则，将显示消息 `user is not logged on`。

146 第 7 章 决策，决策

作为 `on` 的第一个参数的用户已登录，`grep` 将成功并显示消息 `user is logged on`；否则，将显示消息 `user is not logged on`。

谁在登录？

```
$ who
root     tty1
barney   tty2
fred     tty3
joanne   tty4
root     tty5
tony     tty6
lulu     tty7
$ on     tty8
root     tty9
pat      tty10
tony     tty11
lulu     tty12
pat      tty13
root     tty14
tony     tty15
lulu     tty16
pat      tty17
root     tty18
tony     tty19
lulu     tty20
pat      tty21
root     tty22
tony     tty23
lulu     tty24
pat      tty25
root     tty26
tony     tty27
lulu     tty28
pat      tty29
root     tty30
tony     tty31
lulu     tty32
pat      tty33
root     tty34
tony     tty35
lulu     tty36
pat      tty37
root     tty38
tony     tty39
lulu     tty40
pat      tty41
root     tty42
tony     tty43
lulu     tty44
pat      tty45
root     tty46
tony     tty47
lulu     tty48
pat      tty49
root     tty50
tony     tty51
lulu     tty52
pat      tty53
root     tty54
tony     tty55
lulu     tty56
pat      tty57
root     tty58
tony     tty59
lulu     tty60
pat      tty61
root     tty62
tony     tty63
lulu     tty64
pat      tty65
root     tty66
tony     tty67
lulu     tty68
pat      tty69
root     tty70
tony     tty71
lulu     tty72
pat      tty73
root     tty74
tony     tty75
lulu     tty76
pat      tty77
root     tty78
tony     tty79
lulu     tty80
pat      tty81
root     tty82
tony     tty83
lulu     tty84
pat      tty85
root     tty86
tony     tty87
lulu     tty88
pat      tty89
root     tty90
tony     tty91
lulu     tty92
pat      tty93
root     tty94
tony     tty95
lulu     tty96
pat      tty97
root     tty98
tony     tty99
lulu     tty100
pat      tty101
root     tty102
tony     tty103
lulu     tty104
pat      tty105
root     tty106
tony     tty107
lulu     tty108
pat      tty109
root     tty110
tony     tty111
lulu     tty112
pat      tty113
root     tty114
tony     tty115
lulu     tty116
pat      tty117
root     tty118
tony     tty119
lulu     tty120
pat      tty121
root     tty122
tony     tty123
lulu     tty124
pat      tty125
root     tty126
tony     tty127
lulu     tty128
pat      tty129
root     tty130
tony     tty131
lulu     tty132
pat      tty133
root     tty134
tony     tty135
lulu     tty136
pat      tty137
root     tty138
tony     tty139
lulu     tty140
pat      tty141
root     tty142
tony     tty143
lulu     tty144
pat      tty145
root     tty146
tony     tty147
lulu     tty148
pat      tty149
root     tty150
tony     tty151
lulu     tty152
pat      tty153
root     tty154
tony     tty155
lulu     tty156
pat      tty157
root     tty158
tony     tty159
lulu     tty160
pat      tty161
root     tty162
tony     tty163
lulu     tty164
pat      tty165
root     tty166
tony     tty167
lulu     tty168
pat      tty169
root     tty170
tony     tty171
lulu     tty172
pat      tty173
root     tty174
tony     tty175
lulu     tty176
pat      tty177
root     tty178
tony     tty179
lulu     tty180
pat      tty181
root     tty182
tony     tty183
lulu     tty184
pat      tty185
root     tty186
tony     tty187
lulu     tty188
pat      tty189
root     tty190
tony     tty191
lulu     tty192
pat      tty193
root     tty194
tony     tty195
lulu     tty196
pat      tty197
root     tty198
tony     tty199
lulu     tty200
pat      tty201
root     tty202
tony     tty203
lulu     tty204
pat      tty205
root     tty206
tony     tty207
lulu     tty208
pat      tty209
root     tty210
tony     tty211
lulu     tty212
pat      tty213
root     tty214
tony     tty215
lulu     tty216
pat      tty217
root     tty218
tony     tty219
lulu     tty220
pat      tty221
root     tty222
tony     tty223
lulu     tty224
pat      tty225
root     tty226
tony     tty227
lulu     tty228
pat      tty229
root     tty230
tony     tty231
lulu     tty232
pat      tty233
root     tty234
tony     tty235
lulu     tty236
pat      tty237
root     tty238
tony     tty239
lulu     tty240
pat      tty241
root     tty242
tony     tty243
lulu     tty244
pat      tty245
root     tty246
tony     tty247
lulu     tty248
pat      tty249
root     tty250
tony     tty251
lulu     tty252
pat      tty253
root     tty254
tony     tty255
lulu     tty256
pat      tty257
root     tty258
tony     tty259
lulu     tty260
pat      tty261
root     tty262
tony     tty263
lulu     tty264
pat      tty265
root     tty266
tony     tty267
lulu     tty268
pat      tty269
root     tty270
tony     tty271
lulu     tty272
pat      tty273
root     tty274
tony     tty275
lulu     tty276
pat      tty277
root     tty278
tony     tty279
lulu     tty280
pat      tty281
root     tty282
tony     tty283
lulu     tty284
pat      tty285
root     tty286
tony     tty287
lulu     tty288
pat      tty289
root     tty290
tony     tty291
lulu     tty292
pat      tty293
root     tty294
tony     tty295
lulu     tty296
pat      tty297
root     tty298
tony     tty299
lulu     tty300
pat      tty301
root     tty302
tony     tty303
lulu     tty304
pat      tty305
root     tty306
tony     tty307
lulu     tty308
pat      tty309
root     tty310
tony     tty311
lulu     tty312
pat      tty313
root     tty314
tony     tty315
lulu     tty316
pat      tty317
root     tty318
tony     tty319
lulu     tty320
pat      tty321
root     tty322
tony     tty323
lulu     tty324
pat      tty325
root     tty326
tony     tty327
lulu     tty328
pat      tty329
root     tty330
tony     tty331
lulu     tty332
pat      tty333
root     tty334
tony     tty335
lulu     tty336
pat      tty337
root     tty338
tony     tty339
lulu     tty340
pat      tty341
root     tty342
tony     tty343
lulu     tty344
pat      tty345
root     tty346
tony     tty347
lulu     tty348
pat      tty349
root     tty350
tony     tty351
lulu     tty352
pat      tty353
root     tty354
tony     tty355
lulu     tty356
pat      tty357
root     tty358
tony     tty359
lulu     tty360
pat      tty361
root     tty362
tony     tty363
lulu     tty364
pat      tty365
root     tty366
tony     tty367
lulu     tty368
pat      tty369
root     tty370
tony     tty371
lulu     tty372
pat      tty373
root     tty374
tony     tty375
lulu     tty376
pat      tty377
root     tty378
tony     tty379
lulu     tty380
pat      tty381
root     tty382
tony     tty383
lulu     tty384
pat      tty385
root     tty386
tony     tty387
lulu     tty388
pat      tty389
root     tty390
tony     tty391
lulu     tty392
pat      tty393
root     tty394
tony     tty395
lulu     tty396
pat      tty397
root     tty398
tony     tty399
lulu     tty400
pat      tty401
root     tty402
tony     tty403
lulu     tty404
pat      tty405
root     tty406
tony     tty407
lulu     tty408
pat      tty409
root     tty410
tony     tty411
lulu     tty412
pat      tty413
root     tty414
tony     tty415
lulu     tty416
pat      tty417
root     tty418
tony     tty419
lulu     tty420
pat      tty421
root     tty422
tony     tty423
lulu     tty424
pat      tty425
root     tty426
tony     tty427
lulu     tty428
pat      tty429
root     tty430
tony     tty431
lulu     tty432
pat      tty433
root     tty434
tony     tty435
lulu     tty436
pat      tty437
root     tty438
tony     tty439
lulu     tty440
pat      tty441
root     tty442
tony     tty443
lulu     tty444
pat      tty445
root     tty446
tony     tty447
lulu     tty448
pat      tty449
root     tty450
tony     tty451
lulu     tty452
pat      tty453
root     tty454
tony     tty455
lulu     tty456
pat      tty457
root     tty458
tony     tty459
lulu     tty460
pat      tty461
root     tty462
tony     tty463
lulu     tty464
pat      tty465
root     tty466
tony     tty467
lulu     tty468
pat      tty469
root     tty470
tony     tty471
lulu     tty472
pat      tty473
root     tty474
tony     tty475
lulu     tty476
pat      tty477
root     tty478
tony     tty479
lulu     tty480
pat      tty481
root     tty482
tony     tty483
lulu     tty484
pat      tty485
root     tty486
tony     tty487
lulu     tty488
pat      tty489
root     tty490
tony     tty491
lulu     tty492
pat      tty493
root     tty494
tony     tty495
lulu     tty496
pat      tty497
root     tty498
tony     tty499
lulu     tty500
pat      tty501
root     tty502
tony     tty503
lulu     tty504
pat      tty505
root     tty506
tony     tty507
lulu     tty508
pat      tty509
root     tty510
tony     tty511
lulu     tty512
pat      tty513
root     tty514
tony     tty515
lulu     tty516
pat      tty517
root     tty518
tony     tty519
lulu     tty520
pat      tty521
root     tty522
tony     tty523
lulu     tty524
pat      tty525
root     tty526
tony     tty527
lulu     tty528
pat      tty529
root     tty530
tony     tty531
lulu     tty532
pat      tty533
root     tty534
tony     tty535
lulu     tty536
pat      tty537
root     tty538
tony     tty539
lulu     tty540
pat      tty541
root     tty542
tony     tty543
lulu     tty544
pat      tty545
root     tty546
tony     tty547
lulu     tty548
pat      tty549
root     tty550
tony     tty551
lulu     tty552
pat      tty553
root     tty554
tony     tty555
lulu     tty556
pat      tty557
root     tty558
tony     tty559
lulu     tty560
pat      tty561
root     tty562
tony     tty563
lulu     tty564
pat      tty565
root     tty566
tony     tty567
lulu     tty568
pat      tty569
root     tty570
tony     tty571
lulu     tty572
pat      tty573
root     tty574
tony     tty575
lulu     tty576
pat      tty577
root     tty578
tony     tty579
lulu     tty580
pat      tty581
root     tty582
tony     tty583
lulu     tty584
pat      tty585
root     tty586
tony     tty587
lulu     tty588
pat      tty589
root     tty590
tony     tty591
lulu     tty592
pat      tty593
root     tty594
tony     tty595
lulu     tty596
pat      tty597
root     tty598
tony     tty599
lulu     tty600
pat      tty601
root     tty602
tony     tty603
lulu     tty604
pat      tty605
root     tty606
tony     tty607
lulu     tty608
pat      tty609
root     tty610
tony     tty611
lulu     tty612
pat      tty613
root     tty614
tony     tty615
lulu     tty616
pat      tty617
root     tty618
tony     tty619
lulu     tty620
pat      tty621
root     tty622
tony     tty623
lulu     tty624
pat      tty625
root     tty626
tony     tty627
lulu     tty628
pat      tty629
root     tty630
tony     tty631
lulu     tty632
pat      tty633
root     tty634
tony     tty635
lulu     tty636
pat      tty637
root     tty638
tony     tty639
lulu     tty640
pat      tty641
root     tty642
tony     tty643
lulu     tty644
pat      tty645
root     tty646
tony     tty647
lulu     tty648
pat      tty649
root     tty650
tony     tty651
lulu     tty652
pat      tty653
root     tty654
tony     tty655
lulu     tty656
pat      tty657
root     tty658
tony     tty659
lulu     tty660
pat      tty661
root     tty662
tony     tty663
lulu     tty664
pat      tty665
root     tty666
tony     tty667
lulu     tty668
pat      tty669
root     tty670
tony     tty671
lulu     tty672
pat      tty673
root     tty674
tony     tty675
lulu     tty676
pat      tty677
root     tty678
tony     tty679
lulu     tty680
pat      tty681
root     tty682
tony     tty683
lulu     tty684
pat      tty685
root     tty686
tony     tty687
lulu     tty688
pat      tty689
root     tty690
tony     tty691
lulu     tty692
pat      tty693
root     tty694
tony     tty695
lulu     tty696
pat      tty697
root     tty698
tony     tty699
lulu     tty700
pat      tty701
root     tty702
tony     tty703
lulu     tty704
pat      tty705
root     tty706
tony     tty707
lulu     tty708
pat      tty709
root     tty710
tony     tty711
lulu     tty712
pat      tty713
root     tty714
tony     tty715
lulu     tty716
pat      tty717
root     tty718
tony     tty719
lulu     tty720
pat      tty721
root     tty722
tony     tty723
lulu     tty724
pat      tty725
root     tty726
tony     tty727
lulu     tty728
pat      tty729
root     tty730
tony     tty731
lulu     tty732
pat      tty733
root     tty734
tony     tty735
lulu     tty736
pat      tty737
root     tty738
tony     tty739
lulu     tty740
pat      tty741
root     tty742
tony     tty743
lulu     tty744
pat      tty745
root     tty746
tony     tty747
lulu     tty748
pat      tty749
root     tty750
tony     tty751
lulu     tty752
pat      tty753
root     tty754
tony     tty755
lulu     tty756
pat      tty757
root     tty758
tony     tty759
lulu     tty760
pat      tty761
root     tty762
tony     tty763
lulu     tty764
pat      tty765
root     tty766
tony     tty767
lulu     tty768
pat      tty769
root     tty770
tony     tty771
lulu     tty772
pat      tty773
root     tty774
tony     tty775
lulu     tty776
pat      tty777
root     tty778
tony     tty779
lulu     tty780
pat      tty781
root     tty782
tony     tty783
lulu     tty784
pat      tty785
root     tty786
tony     tty787
lulu     tty788
pat      tty789
root     tty790
tony     tty791
lulu     tty792
pat      tty793
root     tty794
tony     tty795
lulu     tty796
pat      tty797
root     tty798
tony     tty799
lulu     tty800
pat      tty801
root     tty802
tony     tty803
lulu     tty804
pat      tty805
root     tty806
tony     tty807
lulu     tty808
pat      tty809
root     tty810
tony     tty811
lulu     tty812
pat      tty813
root     tty814
tony     tty815
lulu     tty816
pat      tty817
root     tty818
tony     tty819
lulu     tty820
pat      tty821
root     tty822
tony     tty823
lulu     tty824
pat      tty825
root     tty826
tony     tty827
lulu     tty828
pat      tty829
root     tty830
tony     tty831
lulu     tty832
pat      tty833
root     tty834
tony     tty835
lulu     tty836
pat      tty837
root     tty838
tony     tty839
lulu     tty840
pat      tty841
root     tty842
tony     tty843
lulu     tty844
pat      tty845
root     tty846
tony     tty847
lulu     tty848
pat      tty849
root     tty850
tony     tty851
lulu     tty852
pat      tty853
root     tty854
tony     tty855
lulu     tty856
pat      tty857
root     tty858
tony     tty859
lulu     tty860
pat      tty861
root     tty862
tony     tty863
lulu     tty864
pat      tty865
root     tty866
tony     tty867
lulu     tty868
pat      tty869
root     tty870
tony     tty871
lulu     tty872
pat      tty873
root     tty874
tony     tty875
lulu     tty876
pat      tty877
root     tty878
tony     tty879
lulu     tty880
pat      tty881
root     tty882
tony     tty883
lulu     tty884
pat      tty885
root     tty886
tony     tty887
lulu     tty888
pat      tty889
root     tty890
tony     tty891
lulu     tty892
pat      tty893
root     tty894
tony     tty895
lulu     tty896
pat      tty897
root     tty898
tony     tty899
lulu     tty900
pat      tty901
root     tty902
tony     tty903
lulu     tty904
pat      tty905
root     tty906
tony     tty907
lulu     tty908
pat      tty909
root     tty910
tony     tty911
lulu     tty912
pat      tty913
root     tty914
tony     tty915
lulu     tty916
pat      tty917
root     tty918
tony     tty919
lulu     tty920
pat      tty921
root     tty922
tony     tty923
lulu     tty924
pat      tty925
root     tty926
tony     tty927
lulu     tty928
pat      tty929
root     tty930
tony     tty931
lulu     tty932
pat      tty933
root     tty934
tony     tty935
lulu     tty936
pat      tty937
root     tty938
tony     tty939
lulu     tty940
pat      tty941
root     tty942
tony     tty943
lulu     tty944
pat      tty945
root     tty946
tony     tty947
lulu     tty948
pat      tty949
root     tty950
tony     tty951
lulu     tty952
pat      tty953
root     tty954
tony     tty955
lulu     tty956
pat      tty957
root     tty958
tony     tty959
lulu     tty960
pat      tty961
root     tty962
tony     tty963
lulu     tty964
pat      tty965
root     tty966
tony     tty967
lulu     tty968
pat      tty969
root     tty970
tony     tty971
lulu     tty972
pat      tty973
root     tty974
tony     tty975
lulu     tty976
pat      tty977
root     tty978
tony     tty979
lulu     tty980
pat      tty981
root     tty982
tony     tty983
lulu     tty984
pat      tty985
root     tty986
tony     tty987
lulu     tty988
pat      tty989
root     tty990
tony     tty991
lulu     tty992
pat      tty993
root     tty994
tony     tty995
lulu     tty996
pat      tty997
root     tty998
tony     tty999
lulu     tty1000
（此处似乎截断了，）

146 第 7 章 决策，决策

谁在登录？

如果作为 `on` 的第一个参数的用户已登录，`grep` 将成功并显示消息 `user is logged on`；否则，将显示消息 `user is not logged on`。

166 退出命令 147

正如你所看到的，缩进对使程序易读性非常有帮助。

## 退出命令

内置 shell 命令 `exit` 允许你立即终止 shell 程序。该命令的通用格式为：

```
exit n
```

其中 `n` 是你返回的状态。如果没有指定，退出状态是最后一个执行命令的状态。请注意，直接从终端执行 `exit` 命令将注销系统。

## 第二次查看 rem 程序

经常被用作终止 shell 程序的方便方法。例如，让我们再次查看 `rem` 程序，它从电话簿文件中删除一个条目：

```bash
$ cat rem
#
# 从电话簿中删除某人
#

grep -v "$1" phonebook > /tmp/phonebook
mv /tmp/phonebook phonebook
$
```

按照编写，如果出现意外情况，该程序可能会产生问题，损坏或清空整个电话簿文件。例如，假设你在 shell 中由于缺少引号向 rem 传递了两个参数。rem 程序将因此删除由 `$1` 指定的所有条目，而从未发现参数过多。

在 `rem` 中可以进行的第一个检查之一是检查参数数量是否正确，就像之前在 `on` 程序中做的那样。这次，我们将使用 `exit` 命令在参数数量不正确时终止程序：

```bash
$ cat rem
#
# 从电话簿中删除某人 -- 版本 2
#

if [ "$#" -ne 1 ]
then
  echo "参数数量错误"
  echo "Usage: rem name"
  exit 1
fi

```bash
grep -v "$1" phonebook > /tmp/phonebook
mv /tmp/phonebook phonebook
$ rem Susan Goldberg
参数数量错误
Usage: rem name
$
```

`exit` 命令返回状态 1，表示失败，以防其他程序想要在条件表达式中检查它。

使用 `exit` 还是 `if-else` 取决于你。有时 `exit` 是快速退出程序的方便方法，特别是在程序早期执行时，而且它还有一个好处是避免了对深度嵌套条件语句的需求。

## elif 结构

随着你的程序变得越来越复杂，你可能会发现自己陷入编写这样的嵌套 `if` 语句：

```
if command,
then
```

