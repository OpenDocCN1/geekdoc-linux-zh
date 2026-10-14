
图 24.33 vm86 系统调用的返回值

37 此宏掩码掉低字节以外的所有位，给出返回值的类型。

38 此宏将高字节移动到低字节位置，给出返回值的参数。

40 返回是由于信号引起的。它似乎从未被使用过。

41 这意味着通用保护异常是由一个操作数引起的，而 `handle_vm86_fault()` 中没有该操作数的句处理程序。它在第 24.6 节中被使用。

42 如果指定要在保护模式下处理向量中断（第 24.6.3 节），或 `do_int()` 函数由于某种原因无法处理向量中断（第 24.7.1 节），则返回此值。在这种情况下，返回值的高字节将包含向量号。

43 如果 `EFLAGS` 中的 `IF_MASK` 位被置位，则返回此值（参见第 24.2.5 节）。这意味着通过 `STI` 或 `POPF` 或 `IRET` 启用了虚拟中断，这三者都会从栈弹出到标志寄存器。

48 如果用户指定的来自可编程控制器 (PIC) 的硬件中断在 32 位模式下处理，且 `IF_MASK` 位被设置，则返回值为 `VM86_PICTURETURN`（参见第 24.6 节）。

49 如果发生了陷阱 1 (debug) 或断点 3 (breakpoint)，则为此值（参见第 24.5 节）。

# 索引

- `_ALIGN_STR` 360
- `_build_read_lock` 126, 128–30
- `_build_write_lock` 126, 131–2
- `_cpu_bh_enable` 582–3
- `_cpu_raise` 559
- `_DO_ACTION` 441–2
- `_down(read)` 157–8
- `_down(write)` 157–6
- `_global_restore_flags` 502–3
- `_global_save_flags()` 501–2
- `_list_add_function` 74–5
- `_list_del_function` 75
- `_read_lock(IRQ)` function 440–1
- `_prepare(ICR)` function 132–4
- `_run_task(queue)` function 578–9
- `_RWSEM_INITIALIZER` 154
- `_save_init_f` 345
- `_SEMAPH_INITIALIZER` 136–7
- `_ser_IPL_short` 437
- `_set_current_state` 557,558
- `_set_gate_macro` 272
- `_set_personality()` function 227–9
- `_setup_APIC_LTT` 449–50
- `_tasklet_handle` function 564–5
- `_tasklet_schedule` 564–4
- `_up(read)` function 160–2
- `_up(write)` function 162–3
- `_wait_event_interrupt` macro 87–8
- `_wait_queue_struct` 63–6
- `_wait_queue_head_struct` 73
- `_WAIT_QUEUE_HEAD_INITIALIZER` macro 65
- `_WAITQUEUE_INITIALIZER` macro 62
- `_wait_up` macro 88–90
- `_wait_up_common()` function 90–2
- `_wait_up_sync_macro` 88–90
- `_write_lock_failed` 132–4
- `_xchg()` function 107–8
- 8259 可编程控制器
- `acknowledgement` 392–6
- `data structure` 386–8
- `disabling an IRQ line` 391–2
- `enabling an IRQ line` 390–1
- `initialising` 388–90
- `IO APIC` and 453
- `overview` 384–6
- `pending IRQ` 396–7
- `shutdown` 390
- `startup` 390
- `abort exception` 272
- `accounting system` 参见 accounting
- `acct(function)` 755
- `acct_process()` function 246–7, 761–2
- `acct_timeout()` function 758
- `ack_edge_oopic_irq()` 486
- `active_irq_field(task_struct)` 22, 52, 193–4
- `add_to_irq(function)` 469–70
- `add_to_runner()` function 534–5
- `add_to_queue()` function 93–4
- `add_wait_queue()` function 69
- `add_wait_queue_exclusive()` function 70
- `add_wait_queue_tail()` function 71
- `addr_limit field(task_struct)` 16, 52
- `address space` 16
- `advanced programmable interrupt controller (APIC)`
- `acknowledging an IRQ` 429
- `arbitration registers` 410–11
- `calculating words` 440–1
- `controller function` 424–6
- `disabling` 428
- `enabling` 419–20
- `error handling` 422–3
- `identification` 418–9
## 高可编程中断控制器 (APIC)

（续)
- `identification registers` 410–11
- `initialising` 418–24
- `instantiating handlers` 441–3
- `interrupt call function` 331–3,445–6
- `error` 450
- `interprocessor` 431–41
- `reschedule` 441–5
- `timer` 443–44,8
- `interrupt command` 413–5
- `interrupt handling registers` 411–3
- `interrupt sources` 409–10
- `IO APIC` and 453
- `local APIC` 369, 370, 372, 409–110
- `local vector` 415–7, 422, 426–8
- `manipulating the APIC` 426–9
- `read before writing` 430–1
- `sensing an IRQ` 451
- `sanity checking` 418–9
- `setting up` 420–2
- `setting up` 449–50
- `signal_return` 305–7

# 索引

- 预定义 572–3
- 时钟中断向量 369
- 移除 573–4
- clone 标志 226–7, 222–229, 231–2
- 软件中断 549, 560
- (clone) 系统服务 213, 243
- 定时器 59–80
- cmaj, fjt 字段 (task_struct) 27
- 另请参 dimmer bottom
- cmin_ft 字段 (task_struct) 27
- 越界异常 299, 300
- CMOS 芯片 320
- 分支方向 6
- nsswap 字段 (task_struct) 27
- 断点异常 299, 300
- collect_signal(function) 659–70
- BSD 计数 16
- task_struct 719
- bug 模拟标志 719
- 兼容字段 (virtual 8086) 767–805
- BUG 宏 68, 117, 188, 418, 419
- 完成 Linux 内核 5–9
- BUILD_COMMON_IRQ 宏 360–1
- 完成回调函数 173–4
- BUILD_IRQ 宏 361–2
- 完成阶段 26, 273–15, 216–8–7
- bust_spinlocks 宏 349
- 信号量隐喻 172–5
- 等待繁忙 109
- 连续符号链接 31
- do..while(construct) 6–7
- 上下文 193, 195–206, 334–354
- FASTCALL 5–6
- convert_fsr_user(function) 699–701
- likely 宏 6
- convert_fsr_to_user(function) 685–7
- unlikely(function) 6, 189, 190, 192, 193
- 协处理器异常处理程序 296–38
- calc_load(function) 512, 527–8
- 协处理器段处理程序 300
- 调用中断 431, 435–6
- copy_flat 227
- 门 278–287
- copy_info_struct 634
- call_data_struct 433, 435–4
- copy_sigahand(function) 231–2
- call_do_IRQ 360–1
- copy_siginfo_to_user(function) 679–80
- 回调函数 617–8
- copy_thread(function) 234–2
- can_scheduler 191, 196, 201, 207–8
- copy_to_user(function) 269
- cap_combin 707–7–8
- count_active_tasks(struct) 528–9
- cap_drop(function) 709–10
- counter_field(task_struct) 18, 52, 178, 190, 192
- cap_effective(task_struct) 28–29, 52, 706–9
- se_alloc quantum
- cap_inherable(task_struct) 28–29, 706–9
- CPU 是处理器
- cap_intersect(function) 709
- CPU_curr 宏 185, 207–8, 208–11
- cap_permitted(task_struct) 28–29, 52, 706–9
- cpu_has_apic 宏 343, 346
- cap_set_all 711–12
- cpu_has_pru 宏 343, 346
- cap_set_pg 712
- cpu_has_xmr 宏 343, 348
- 能力
- cpu_idle function 56
- 检查 712–15
- cpu_logical_map function 180, 209
- 常量 703–72
- cpu_number_acpi function 180
- 操作 707–11
- cpu_raise_ofstruct(function) 559
- 概述 28–9, 703
- cpu_relax_marco 265–6
- 安全 74–5
- CPU 生成的错误 599–601
- 设置掩码 712
- allowed_field(task_struct) 21, 52, 92
- 类型 706–9
- cpu_runnable_field(task_struct) 21, 52, 199, 204, 205
- 可能力的 216–7, 248, 250, 626, 712–13
- 206
- cascade_index 370
- CT_TO_SECS 宏 268–9
- check_free_space(function) 759–61
- CT_TO_USECS 宏 268–9
- clear_bit(function) 699
- 调试头部 298, 314–5
- cf_fput(function) 699
- 调试 register 314–5
- cf_IF(function) 779–8
- DEBUG_SPINLOCK 宏 109–11
- clear_IO_APIC(function) 482
- 调试
- IO_IN(function) 482
- 信息 74–53
- cf_TF(function) 779–8
- register 203–4
- 简单步进 317
- 另请参阅 tracing
- DECLARE_WAIT_HEAD 65
- DECLARE_WAITQUEUE 宏 62, 256–7
- default_handler 722–3
- del_from_queue 94–5
- del_timer 538–9
- del_timer_sync 246–7
- deliver_signal 648
- dequeue_signal 648, 655–7
- desc_struct 272
- descript_format 273
- descriptor_table 248
- descriptor_table, 中断
- detach 339, 544, 545
- del_edge_field (task_struct) 248
- del_event 327–40
- del_if_kernel 339, 348–9
- del_8259a_irq 391–2
- del_enable_atomic_irq 485–6
- del_io_APIC 481–2
- del_irq 353, 354–3
- del_irq_nosync 381–2
- del_level_io_irq 487
- disconnect_bis_APIC 417
- div_error_handler 293–6
- dev_ac_process 769
- del_oco_coprocessor 335
- del_debug 315–8
- DO_ERROR 宏 309–11
- DO_ERROR_INFO 309–10, 311
- dn_exit 224, 243
- dn_fork 215, 25, 243
- dn_general_processor 225, 552, 553
- dn_int 799–8
- dn_IRQ 360, 1–362, 5
- dn_it_proof 508, 511–1
- dn_it_timer 508, 509–10
- dn_rmalloc 318–24
- dn_notify_parent 249, 51, 641–3
- dn_process_timer 508–9
- dn_sicitation 611–63
- dn_signalkaft 619–21
- dn_signal 305, 306, 647–55
- dn_some_coprocessor 338–40
- dn_softirq 552, 55
- dn_spurious_interrupt_bug 327
- dn_sys_vm86(i) 786–9
- dn_timer 506
- dn_trap 311, 312–4
- dn_VM86_ERROR 309, 10–311–2
- dn_VM86_ERROR_INFO 309, 311–2
- dn_wait_for_consort 6–7
- DOS 模拟器 (dosemu) 767
- down 139, 140, 146–151
- down_interruptible 140–1, 143–146–151
- down_trylock 141, 144, 151–2
- EAX 寄存 6, 163, 243, 274–5, 277–8, 287–290–2, 332–3
- EBX function 200–1, 235, 643–4, 290
- ECX function 271, 275–332
- edged_interrupt 484–6, 489
- EDX 寄存 120–1, 274–5, 277–8, 332–3
- EFLAGS 寄存 288–4, 208–343, 349, 375–7
- egeid_field (task_struct) 288
- EIP 寄存 215
- EIISA_ELCR(i) function 461–462
- enabled_8259a_irq 390–1
- enable_edge_intopic_irq 485–6
- enable_io_APIC 475–6
- enabled 353, 354, 383–4
- enabled_level_io_irq 487
- encode_comp_it 765–6
- end_8259a_irq 396
- end_level_io_irq 487
- end_of_interrupt_mode 398–9, 392, 394
- ENTRY 290–294, 296, 300, 303
- bad_fork_count 220–1, 224
- bad_fork_count_mem 220–21, 224
- bad_fork_free 216–17, 224
- bad_free_out 215–24, 225
- Intel binary 287
- ret_from_call 235, 236
- SPARK_binary 287
- sys_call 290
- sys_system 289
- traceys 292
- traceys_exit 235, 236
- sie_end_of_interrupt_mode 422–3
- error_status (ESR) 241–4
- ESI 寄存 241–4
- ESP 寄存 200, 235
- r_disable(i) 418, 419
- egeid_field (task_struct) 287
- adding a timer 534–5, 536
- cascading 335–6
- changing a timer 335–6
- data structure 720–1
- deleting a timer 538–9
- expired 543–7
- initial 533
- synchronising 545–6
- abort 272
- fault 271
- trap 271
- exception handler 30–10
- alignment check 30
- bounds exceeded 299, 300, 309–10
- breakpoint 299, 300, 309–10
- coprocessor 296–8, 300, 103–550
- coprocessor overrun 300, 309–10
- debug 299, 315–8
- device not available 309–10, 333–5
- divide error 293–6, 309–10
- double fault 309–4
- general protection 325–7
- generic
- invalid TSS 309–10
- invalid-opcode check 300, 327–33
- numeric error 296–8, 309, 10, 335–8
- overflow error 296–8, 309, 299, 300–10
- overview 309
- segment present 309–45
- spurious bug 300, 327
- stack check 309–10
- exect 16, 30
- excl_domain(task_struct) 16, 52, 268, 288
- exception domain
- data structure 720–1
- default handler 722–3
- list 721–2
- registering 723–5
- tracking 725
- unregistering 725–6
- execution unit 4
- exit system service 15, 19, 245
- exit code_field(task_struct) 14, 24, 246–7
- exit_notify() 246–7, 248, 251
- exit_sighand(function) 246–7, 613–14
- exit_signal_field(task_struct) 246–7
- exit_thread() 246–7
- FASTCALL 5–6, 163–4, 200, 306
- fault exception 271
- flz(function) 102–1
- file descriptor table 36–7
- file system 30–1, 35–6
- fields(task_struct) 36–7, 52, 215
- find_irq_entry() 457–8
- find_isa_irq_pin() 458–9
- find_task_by_id()function 50
- flags field(task_struct) 15–16, 52, 227
- floating point 333–50, 346, 3–8
- flush_signal_handlers() 616
- flush_signal(s) 615–16
- flush_asynchronous() 314–15
- for_each_task_macro 529
- force_sig_info() *struct 312, 314, 316, 317, 341,
- force_sig_info()function 312, 314, 316, 317, 341, 342, 635–6
- fort_original_parent()function 24
- fork() system service 16, 19, 25, 26, 213, 235–6
- fork_init()function
- fork_out_entry 215–16, 224
- free_irq() 378–8
- free_uid() 242
- fs field(task_struct) 35–6, 52, 215
- fs fluid 288
- fuser()function
- down_read 157
- down_write 158
- global_restore_flags 502–3
- global_save_flags 501–2
- list_add() 74–5
- list_del() 775
- prepare_IC() 440–1
- run_task_queue() 578–9
- save_init_put() 435
- set_current_state 557, 558
- set_personality() 727–9
- set_UP_LL() 449–50

# 索引

- function(续) 106
- atomic_inc_and_test() 106
- atomic_read() 216–27
- atomic_set() 432, 433
- atomic_sub() 103–04
- atomic_sub_and_test() 104
- bad_signal() 625–66
- bh_action() 562, 574–75
- block_all_signals() 617
- calc_load(712) 512, 137–58
- call_do(IRQ) 360–61
- can_schedule() 190, 191, 196, 207–08
- cap_commit() 708–09
- cap_drop() 709–10
- cap_intersect() 709
- cap_invert() 710
- cap_all() 711–12
- cap_table() 216–27, 248, 250, 626, 712–733
- check_free() 759–761
- clip_fpu() 669
- clip_if() 779–80
- clear_IO_APIC() 482
- clear_IO_APIC_pin() 482–83
- clear_tf() 779–80
- collect_signal() 773
- copy_from_from_user() 699–701
- copy_from_to_user() 685–87
- copy_flags() 227
- copy_sig_info() 634
- copy_signbit() 231–32
- copy_sign_to_user() 679–80
- copy_thread() 223–24
- copy_to_user() 269
- count_active_tasks() 528–59
- cpu_idlet() 56
- cpu_logical_map() 280
- cpu_number_map() 186
- cpu_raise_softirq() 559
- default_handler() 722–73
- del_from_user() 94–95
- del_timer_set() 246–47
- del_delivery() 663
- dequeue_signal() 648, 655–57
- detach_timer() 712
- diet() 327, 349–50
- die_if_kernel() 339, 348–49
- disable_8259IRQ() 391–92
- disable_edge_io_irq() 485–86
- disable_IO_APIC() 481–82
- disable_set() 353, 342, 381–82
- disable_irq_nsync() 381
- disable_level_io_irq() 487
- disconnect_bsp_APIC() 483
- do_acct_process() 762–65
- do_coprocessor_error() 335
- do_debug() 315–18
- do_exit() 245–48
- do_fork() 215–25, 231, 243
- do_general_protection() 325–27
- do_int() 799–80
- do_IRQ() 360–61, 362–65, 552, 553
- do_it_prof() 508, 510–11
- do_it_virt() 508, 509–10
- do_mmi() 318–320
- do_notify_parent() 249, 51, 641–43
- do_process_timer() 508–59
- do_signaled() 611–13
- do_signlist_ack() 619–22
- do_signal() 305, 306, 647–55
- do_simd_coprocessor() 338–40
- do_softirq() 552, 554–58
- do_spurious_interrupt() 327–29
- dys_vs_irq() 786–89
- do_timer() 506
- do_tripl() 311, 312–14
- do_down() 139, 140, 146–51
- down_interruptable() 140–41, 143, 146–51
- down_downlock() 141, 144, 151–52
- down_EISA() 461–52
- enable_8259IRQ() 390–91
- enable_edge_io_irq() 485–86
- enable_IO_APIC() 475–76
- enable_level_io_irq() 487
- encode_comp() 765–76
- enable_level_io_irq() 487–89
- esr_disable() 418, 419
- exec() 160
- exit() 15, 19
- exit_notify() 246–47, 248, 51, 254
- exit_sigand() 246, 713, 641–43
- exit_thread() 246–47
- fuzz() 102–101
- find_irq_query() 457
- find_isa_iq_pin() 458–59
- find_task_by_id() 50
- flush_signal_handler() 616
- flush_signal() 615–16
- flush_softirq() 614–45
- force_sig() 312, 314, 339, 640–45
- force_sig() 312, 314, 317, 342, 635–36
- forget_original_parent() 24
- fork() 16, 19, 25
- fork_id() 214
- free_irq() 379–81
- free_uid() 242
- fussert() 715
- get_sigframe() 671, 672, 677–78
- get_current() 180
- get_esc_alt() 726–27
- get_fpu_cwd() 336, 337–348
- get_fpu_msr() 340, 341
- get_fpu_swd() 336, 337–348
- get_irlock() 495–96
- get_pid() 228–31
- get_stack_long() 744
- get_vflags() 778
- get_ret() 742–44
- get_usage() 260–69
- goodness 190–196, 118–255
- hand_IRQ_event() 363, 365–66
- hand_signal() 653, 464–66
- hand_stop_signal() 626–27
- hand_vm86_fault() 339, 792–801
- hand_vm86_trap() 789, 791, 800
- has_pending_signals() 646–67
- has_stopped_joblist 225
- hash_fn 47
- hw_interrupt_type 352
- hw_resend_iri() 452
- 8259A_iri_pending 397
- signed_signal 629
- immediate_bhi 580
- init_kernel 279
- init 11
- init_8259A 388–392
- init_b_hi 11, 511–573
- init_b_APIC 423–44
- init_fpu 333, 334–34
- init_IRQ 367–70
- init_ISA_irq 370–11
- init_sigpending 217–18, 595
- init_timer 219, 534–537
- init_timerc 11, 533–34
- init_machine_check 328–321
- internal_add_timer 536–38
- IO_API_IRQ_trigger 467–68
- hio_api_read 493
- hio_api_syncl 494
- hio_api_write 493–44
- irq_exit 586
- irq_pin_list 468–69
- irq_polarity 499, 585–86
- irq_running 254
- is_orphaned_prgt 254
- is_reveCTED 801–82
- it_real 542–43
- kernel_thread 243–44, 555–56
- kill_pgll 248, 250, 644–55
- kill_pg_info 636–67
- kill_proc 645
- kill_proc_once 638–69
- kill_sl 644–55
- kill_sl_info 637–38
- kill_something_info 639–641
- ksftout 556–58
- list_add 75, 537, 538
- list_add_tail 74–75
- list_del 729, 575
- list_del_init 76
- list_empty 76
- list_splice 76–77
- list_modscr 344
- list_douget 262–64
- local_bb_enable 582–83
- local_irq_disable 567, 568, 570
- local_irq_enable 568, 570
- lock_kernel 246–47
- lookup_exe_dense 729–731
- mark_bhi 575
- mask_and_AK_8259 392–95
- mask_and_IO_irq 489–591
- mask_evaluator 335–37
- mask_error 337
- mask_error_iri 373–74
- mask_state_restore 334–35
- mask_bit 204–05
- mod_timer 535–36
- move_last_runqueue 94
- BIOS_policy 463–65
- BIOS_trigger 465–67
- next_signal 657–59
- nnotify_parent 644
- non_on_stack 622
- ofopensirq 551, 552
- outb 388–89
- outb_p 368, 370
- panic 329, 331
- p_2_irq 459–61
- prepare_to_stack 193–94
- process_limit 542
- process_attach 733–35
- process_detach 736–37
- process_disable 737–38
- process_readd 738–89
- process_write 739–40
- put_stack_long 744
- put_reg 258, 260
- queue_task 576–77
- rave_softinq 558–59
- read_lock 126
- read_unlock 127
- recalc_sigpending 646, 750, 791
- register_denom 724–75
- release_irq 496–97, 585–86
- release_task 204–05, 258, 261, 263–65
- remove_bht 573–74
- remove_wait_queue 72
- rep_not 265–66
- request_irq 374–76
- reschedule_rdd 207–08
- restore_fpu 334, 346
- restore_1387 697–698
- restore_1387_fsave 698–699
- restore_1387_fxsave 699
- rwsem_sigcontext 802–83
- return_to_32bit
- rm_from_queue 627–28
- rm_sig_queue 575, 577–580
- run_task_queue 453
- run_timer_list 534–34
- rwsem_atomic_add 171
- rwsem_atomic_update 172
- rwsem_create 15–16
- save_1370 682
- save_1387_isave 683–84
- save_1387_fxsave 684–85
- save_init_fpu 340, 341, 345
- save_v6_state 803–04
- sched_init 10–11, 47
- sched_setparam 187–95, 246, 248, 557
- sched_sched 194, 205, 204–236
- sched_time_out 540–42
- send_overflow 541, 519, 523–26
- send_imita 137–38
- send_ipi_all 435–36
- send_ipi_alloc_list 434–45
- send_ipi_mask 438
- send_ipi_mask_atomic 439–40
- send_ipi_mask_sequence
- send_ipi_self 436
- send_sig_22 252–53, 309, 510, 644–55
- send_sig_info 621, 625–560
- send_signal 631–63
- send_bit_set 97–98
- send_call_gate 278–281
- send_itf 779–88
- send_intr_gate 278, 381, 369
- send_ioaptic_affinity 492–93
- send_system_get 278–381
- send_vflags_long 778–79
- send_vflags_short 777–78

# 索引

- 输入/输出高级可编程控制器 (IO APIC) 全局中断请求锁 494–9
- 全局中断操作 499–501
- 初始化 175–481
- 中断配置表 453–61
- 中断描述符表 (IDT) 358, 359–475
- 电平中断 IDT 486–9
- 操作寄存器 489–93
- 非屏蔽中断 320–3
- 校验和错误 319
- 读取一个 493 470–5
- 返回 PIC 模式 483

- 入口阶段 287–93
- 错误 450
- 退出阶段 302–7
- 查找当前进程 285–1
- ignore_int 274, 275–6
- icall27 280–129
- icall27 260–1,289
- 非屏蔽中断 (NMI) 298–3,218
- 概述 2
- 处理器异常 301–2
- 重新调度 441–445
- 恢复寄存器 285
- 从硬件中断返回 305–5
- 从系统调用返回 303
- 从异常返回 303–5
- 保存寄存器 284–5
- 服务阶段 293

- 输入/输出进程
- 实例化 401
- 超过 400–1
- 暂停 406–7
- 读取 401–3,405
- 写入 403–4,406
- 服务中请求 (ISR)
- Intel 特尔二进制规范 (IBCS) 入口 287–9
- intel_machine_check() 函数 328–31
- inter_add(timer) 函数 536–8
- 处理器间中断 (IPI) 调用函数 431–3
- 超过 208, 369
- 重新调度 431
- 快捷寻址 434–40

- 边沿触发 484–6,489
- 全局操作 499–501
- 本地请求锁 494–9
- 电平触发 486–9
- 定时器 2,205–47
- 类型 271
- 中断配置表 453–61
- 参见可编程控制器中断计数器 584–6
- 中断描述符格式 273
- 中断描述符表 (IDT) 创建条目 276–81
- 数据结构 272–3
- 硬件处理中断 358–9
- 初始化 274–5
- 为 IO APIC 初始化 475
- 初始化硬件中断 367–74
- 中断门 272–3,274–278
- 下半部 11,397,433,498
- 调用函数 431–3,445–6
- 默认 274,275

- SIMD-控制系统调用 270, 287–23
- 解耦定时器 443–4,446–48, 50–547
- 参见 异常处理程序、硬件中断、可编程控制器、软件中断
- 中断线 IRQ
- 中断请求掩码 (IMR) 385
- 中断请求 (IRQ) 386
- 中断请求统计 580–6
- 中断服务程序
- 中断处理程序
- 中断状态 747–99
- 中断向量 372
- 中断安全锁 397–400, 433, 512, 578
- 无效选项处理程序 300
- IO-事件-输出高级可编程中断控制器

- IO_APIC_irq_trigger() 467–8
- IO_APIC_read_entry() 472–3
- IO_APIC_route_entry 结构 494
- IO_APIC_sync_event() 494
- IO_APIC_write() 493–4
- IPI 参见处理器中断
- IRQ 中断描述符表 (IDT) 358, 967–74
- IO APIC 和 453–504
- 线 351, 358, 384–4
- 未注册的 357
- IRQ 宏 358–99
- irq_2_pin_fault 353–49
- irq_desc_t_struct 365–6
- irq_enter_macro 365–6
- irq_event(function) 586
- irq_exit_function 366–77
- irq_exit(event) 386
- IRQ_NAME 宏 361
- irq_put_list(function) 468–9
- irq_polarity(function) 463
- at_stat 数组

- 中断函数 353, 355, 370
- IRQLIST 管理 358-9
- irq_running() 函数 499, 586-1
- ISR 参见中断请求寄存器 386
- is_orphaned(j pgrp) 函数 254
- is_reverted() 函数 801-2
- ISR 参见服务中寄存器 386
- it_procr_field(task_struct) 26
- it_profi_value_field(task_struct) 74
- it_26_value_field 540-32
- it_real_incr_field(task_struct) 26
- it_real_value_field(task_struct) 26
- it_virt_inner_field(task_struct) 26
- it_virt_value_field(task_struct) 26
- journal_info(task_struct) 39, 53
- keep_capabilities field(task_struct) 29, 52
- 编译 5
- 创建线程 243-4
- 启动 9-10
- 线程化
- 内核代码
- 多处理器实现 120-3
- 单处理器实现 120
- 内核模式 235, 245, 284, 289–90, 304, 312, 339, 349, 448, 553, 667, 689, 702-1
- 信号量
- 能够 141, 144, 151
- 汇器实现 135
- 初始化 137
- 初始化 136
- 概述 135
- 将进程休眠 146-51
- 触发 141, 146
- 操作 139–41, 143-4
- 唤醒进程 6
- 内核栈 281, 4-288
- 内核状态 186
- 内核线程 243, 4-555-8
- 性能分析器 448–9
- kernel_stat_struct 186
- kernel_thread() 243, 4-555-6
- nmk_regs 结构 771, 772, 773
- nmk_restore_struct 771-2, 774
- kill_pg() 248, 250, 644-5
- kill_pginfo() 636–7
- kill_proc() 645
- kill_gro_info() 638–9
- kill_sl() 644-5
- kill_sl_info() 637–8
- kill_something_info() 639–41
- ksftirqd(root) 556-8
- last_pid 214
- LATCH 368, 370
- callit27 中断处理程序 280-1, 289
- ledev_interrupt(task_struct) 219-20, 246–7
- 电平触发中断 486–9
- 轻量级进程 222
- 可能的 6
- link_count field(task_struct) 31
- Linux 内核结构 74
- 列表处理代码 73-9
- list_add() 函数 75, 537, 538
- list_add_tail() 函数 74-5
- list_add 75, 539
- dist_del_init() 函数 76
- list_empty() 函数 76
- list_entry 宏 78, 190, 191
- list_for_each 宏 78-90, 191
- list_HEAD 宏 74
- list_head_struct 73, 191, 576
- list_HEAD_INIT 宏 73
- list_spc() 函数 76
- lock_count 函数 344
- load_debugb() 函数 202-4
- 本地中断 420-1
- 本地向量表 (LVT) 415, 422, 426-8
- lock_bh_disable 结构 398–400
- lock_bh_enable enable 398–400
- lock_bh_enable() 函数 582-3
- lock_dirq_struct 398–400
- lock_disable() 函数 567, 570, 582
- lock_irq_struct 398–400
- lock_irq_enable() 函数 568, 570
- lock_irq_restore_struct 398–400
- local_pages field(task_struct) 22
- 本地锁函数 102–99
- LOCK 宏 102, 103, 104, 105, 106, 107
- lock_depth_field(task_struct) 175
- lock_kernel() 函数 246-7
- 锁定机制中断安全 397–400, 533, 578-9
- 锁定机制内核锁 120-3
- 锁定机制读写锁 109, 123-34
- 锁定机制自旋锁 109-119
- locks field(task_struct) 31
- lookep_exit_denom() 729-31
- machine-check 异常处理程序 300
- 机器特有寄存器 331-3
- 宏（续）

- _cpu_raise_softrq 559
- _DO_ACTIONIT 491–2
- _SEMAPHORE_INITIALIZE 136–7
- set_gate 277
- wait_event_interruptible 87–8
- _WAIT_QUEUE_HEAD_INITIALIZER 65
- _WAKE_UP_INITIALIZER 62
- wake_up 88–9
- wake_up_sync 88–90
- ALIGN(7)
- atomic_write() 418, 419, 420, 423
- atomic_INIT 102
- atomic_read 109
- atomic_set 277
- barrier 119, 565
- BUG(68, 117, 418)
- BUILD_COMMON_IRQ 360
- BUILD_IRQ 361
- bust_spinlocks 349
- cpu_curr 185, 207–808–11
- cpu_has_apc 341
- cpu_has_fpu 343, 345
- cpu_has_mm 339, 333, 348
- cpu_rel 265–6
- CT_TO_SECS 268–109
- DEBUG_SPINLOCK 109–113
- DECLARE_WAKE_QUEUE 65
- DO_ERROR 309–311
- DO_ERROR_INIT 309, 310–2
- ENTRY 290, 294, 296, 298, 300, 303
- GET_CURRENT 285–6
- idle_wait 191, 195, 204–5
- for_each_each 285–6
- next_thread 2529
- in_interrupt 553, 584
- INIT_LIST 74, 207
- INIT_TSS 184
- IRQ 258–9
- IRQ_NAME 361
- IRLIST 358–9
- irq_event 365–6
- irq_exit 366–77
- list(6)
- list_entry(each) 78, 190, 191
- list_for(each) 78–190, 191
- LIST_HEAD 74
- LIST_HEAD_INIT 234
- loundsement 69
- local_bh_disable 398–400
- local_bh_enable 398–400
- local_irq_disable 398–400
- local_irq_enable 398–400
- local_irq_restore_struct 398–400
- local_irq_save 398–400
- local_pages field(task_struct) 22
- local lock functions 102–99
- lock_count 344
- lock_depth_field(task_struct) 175
- lock_kernel() 246-7
- LOCK 102, 103, 104, 105, 106, 107
- locks field(task_struct) 31
- popb 783
- popl 784–5
- popw 783–4
- pubb 780–1
- pushl 781–2
- pushw 781
- rdmr 229, 330, 332–3
- read_lock 123–4, 529
- read_lock_398–400
- read_irq_restore 398–400
- read_unlock 123–4
- read_unblock 398–400
- read_unlock_irqrestore 398–400
- reschedule 307
- RESTORE 285,303
- RWLOCK_MAGIC 125
- SAVE_ALL 284–5
- spin_lock 398–400
- spin_lock_init 112–113, 215–218
- spin_lock_string 118–9
- spin_lock_wait 118–9
- spin_irq_init 398–400
- spin_irq_restore 398–400
- spin_irq_save 399–400
- set_current_state 85
- setup_jit 274–3
- signal_restore 305–7
- softirq_pending 559
- spin_in_unlocked 18–9
- spin_unlock_bh 398–400
- spin_unlock_irqrestore 398–400
- struct_cpu() 234–5
- switch_gate 277
- SPIN_LOCK_MAGIC 114–5
- SPIN_LOCK_UNLOCKED 114–5, 228
- switch_to 194, 195, 200–2

# 索引

- pid 字段 (task_struct) 24, 246
- didash_next_prev 字段 (task_struct) 26, 46–50
- didash_pprev 字段 (task_struct) 26, 46–50
- pin_2_trq() 函数 459–61
- pi_entry_array 475, 447
- policy_field (task_struct) 18–19, 52, 177, 192, 193
- popb_macro 783
- popl_macro 784–5
- popw_macro 783–4
- PPS 信号每秒脉冲系统
- prepare_to_switch() 函数 193–4
- prev_task (task_struct) 22, 41, 43–4, 52, 215
- 权限 16
- 进程
    - 访问资源 2
    - 分配 755–66
    - 创建任务 214–16
    - 分配标识符 227–31
    - 分配锁 187
    - 能力 28–9, 703–15
    - 子线程 232–5
    - 创建 26
    - 凭证 27–30
    - 释放分配 245, 613–16
    - 定义 2
    - 错误处理 223–5
    - 事件计时器 530–47
    - 示例 3
    - 文件描述符表 36–7
    - 文件系统信息 35–6
    - 固定优先级 26
    - 组标识符 28
    - 哈希表 46–50
    - 空闲 24
    - 初始 0–6
    - 初始化 216–221
    - 插入 43–5, 47–9
    - 中断处理 271–307
    - 内核模式 689–702
    - 限制 508–9
    - 链接 41–6, 221
    - 里程碑 15
    - 互斥 97–134, 135–75
    - 通知 248–53
    - 重启 253–4
    - 待处理信号 645–55
    - 优先级 190–1, 88
    - 移除 42–39
    - 在 Linux 中的表示 13–39
    - 重新调度 307
    - 资源限制 29
    - 运行队列 93–5
    - 调度函数 187–95
    - 查找 45–6, 50, 90–2
    - 信号机制 587–702
    - 睡眠 80–33, 83–135, 540–3
    - 状态 14–15
    - 统计 266–9, 507–8
    - 停止 254–5
    - 终端设备 31
    - 终止 245–69, 348–50
    - 线程 32–5, 52, 347–50
    - 时间片 178–222
    - 跟踪 2, 17, 200, 733–57
    - 用户标识符 28
    - 用户态栈 618, 666, 679–90
    - 胜利 61–255
    - 唤醒 88–50
    - 僵尸 14–15
- 另见 also_task
- 进程会计
- 节省空间 755–6
- 数据结构 755–6
- 释放磁盘空间 758–61
- 概述 30
- 状态标志 758
- 写入 761–5
- 进程控制块 13
- 进程描述符 13
- 进程组 24, 25
- 进程标识 24
- process_timeout() 函数 542
- 处理器
- 寻找一个 207 12
- 内核模式 3
- 开销 4
- 寄存器 4
- 租赁 206
- 用户态 3
- 进程异常处理器 301–2
- 进程_字段 (task_struct) 21, 199
- 可编程中断控制器 (PIC)
- 8259 384–37
- 数据结构 353–6
- 哑处理程序 356–7
- 入口点 360–1
- 处理程序栈 359–60, 361
- 处理请求 355–77
- 初始化 370–1, 372–4
- 中断描述表 (IDT) 358, 359, 374–6
- 大小 351–2
- 查看可编程中断控制器
- 控制器
- pt_regs_struct 232–2, 282–4, 287, 296–3
- 指针库 213
- ptrace_field (task_struct) 17, 235, 260–1
- 用户系统 17
- ptrace_attach(task) 函数 733–5
- ptrace_detach(task) 函数 736–7
- ptrace_disable() 函数 737
- ptrace_read() 函数 738–9
- ptrace_write() 函数 739–40
- 每秒脉冲(PPS) 526–7
- push 780–1
- pushl 781–2
- pushmw 780–1
- put_stack_long() 函数 744–5
- put_user() 函数 258, 260
- putreguf() 函数 740–2
- 量子 19, 17, 188–90, 192, 198–508
- queue_task() 函数 576–7
- raise_sortq() 函数 558–9
- dmr 329, 330, 332–3
- read_load_macro 123–4, 529
- read_load() 函数 126, 255, 257, 259
- read_lo_bh 398–400
- read_lo_iqq_macro 398–400
- read_iqq_macro 398–400
- read_unblock_macro 123–4
- read_unblock() 函数 127, 255, 261
- read_unblock_bh_macro 398–400
- read_unblock_iqq_macro 398–400
- read_unblock_macro 398–400
- read_write_lock 124–255
- 中断安全 397
- 多处理器实现 124–358
- 调度器 181
- 多处理器实现 123–24
- write_queue 79–80
- write_semaphore atomic_operation 171
- 获取读 157–8
- 获取写 158–60
- 租赁读 160–2
- 租赁写 162–3
- 跟踪 155–6
- 等待 164–77
- 唤醒 167–71
- 就绪函数 ready-use_user 531
- 实时模式 274, 667
- real_field(task) struct, 26, 52
- rescheduling_sync() 函数 646, 656, 790, 791
- 递归共生链接 31
- APIC 仲裁 410–111
- 标识 410–111
- 中断命令 413–5
- 中断处理程序 411–3
- 调试 203–4
- 显示内容 751–3
- EAX 6, 163, 200–1, 234, 277–8, 287–8, 290–2, 332
- EBX 200–1, 225–6, 243–290
- ECX 6, 275
- EDX 6, 200–1, 254, 577–8, 332
- EFLAGS 283–4, 288, 303–4, 339, 375
- EIP 235
- 错误状态 422–2
- ESI 243–4
- ESP 200–235
- 浮点数 346, 347–8
- 服务中 413–2
- 通用 470–1
- 路由 471–5
- 机器特定 331–3, 344, 348, 182, 200
- register_ee_domain() 函数 724–5
- lease_unlock() 函数 496–7, 585–6
- release_read() 函数 204–558, 281, 261–3
- release_thread() 函数 264, 265
- remove_bh() 函数 573–4
- REMOVE_LINKS 42–9
- remove_wait_queue() 函数 722, 262
- rep_pop() 函数 265–6
- request_intr() 函数 374, 441–5
- 重新调度中断 371
- reschedule_deci() 函数 207, 212, 369
- 资源分配_stack 54
- 资源分配_unit 4
- 资源限制 29, 55
- 责任 2
- RESTORE_ALL_mask 284-5
- restore_f_free() 函数 340, 344
- restore_id387_fpu() 697
- restore_fpu() 697–8
- restore_id387_fpu() 698–9
- restore_context() 函数 543
- return_to_sys() 函数 235, 236
- return_to_id 802
- rusage_struct 768
- rlim_field(task) struct, 21, 52, 94
- rm_from_queue() 函数 627–8
- rm_sig_from_queue() 函数 627
- rt_priority(task) struct 666–7
- rt_signfield_struct 666–7
- run_task() 函数 575, 577–8, 580
- run_timer_list() 函数 543
- runqueue 14, 19, 53–178, 179, 181, 192, 198–508
- rusage_struct 257, 267–8
- rw_semaphore_struct 152–3
- rw_lock_init_macro 123–4
- RWLOCK_LOCK 125
- RWLOCK_MAGIC_INIT 125
- rwlock_t struct 125
- rwsem_atomic_add() 函数 171
- rwsem_atomic_update() 函数 172
- rwsem_mutex_struct 155
- ransentract() 155–6
- sleep_time 22, 94
- sprint 181
- static data_struct 181–2
- switching context 193–1, 199–206
- task segment enlist 182–4
- scheduling policy 19, 17–8
- second_overflow() 函数 514, 59–21, 523–6
- self_exec_id (task_struct) 39
- semat_init() 137–8
- 信号量
- completion 175–4
- sas_size_field (task_struct) 38
- sas_sp_field (task_struct) 38
- SAVE_ALL_mask 284-5
- save_i387() 函数 697
- save_id387_fave() 函数 683–4
- save_id387_fave() 函数 684
- save_f_free() 函数 340, 344
- save_v_struct 779
- hash_pid() 47
- sched_LINKS 42
- sched_init() 378, 49
- sched_function() 1195, 246, 252
- sched_data_struct 185
- sched_tail 194, 204
- sched_timeout() 函数 540
- sched_state 85
- sched_trap_get() 278–8
- sched_v_struct 779
- set_frame_link()  6114

# 索引

sigtext context 667–8
sigframe structure 666–7, 671–4
siginfo struct 593–4, 595–8
sigmask_lock field (task_struct) 38, 52
signal
- 拷贝处理器 231–2
- 异常处理程序 312–14
- 处理 663–6
- 等待, 16, 53–30, 745–55
- 进程组 24
sigCHILD 601–2
- 标准 588–91
- 另见信号处理程序、机制、信号
处理信号处理器
- 对齐检查 309–2
- 上文信息 667–9, 692–702
- 释放内存 213–16
- 浮点区域 669–71, 696–702, 611–13
- 调用 663–7
- 内核模式 689–693
- 段寄存器 696
- 栈帧 666–78, 679–89
- 标签值 687–9, 699
task_struct 38–7
- 类型 309–10
- 用户模式 663
- 用户栈栈 67–9, 689–90
- 用户定义 653–4
信号机制
- 位图图 603–11
- 数据结构 587–602
- 处理器类型 593–4
- 安装处理器 611–13
- 调用处理器 663–702
- 通知用户 617–18
- 等待队列 594–5
- 进程特定信息 591–4
- 代码 598–602
- sigLL 602
- 栈 618–22
- 标准信号 588–91
- 另见信号处理器、信号处理
信号处理:
- 默认处理器 631–3
- 递送 630–34
- 强制递送 635–6
- 忽略信号 650–1
- 发送 623–30
- 从队列移除 655–61
- 启动系统调用 654–5
- 结束 636–45
- 用户定义 653–4
- 另见信号处理器、信号机制
信号栈 618–22
signal_pending(function) 189, 190, 645–6, 656
signal_return 宏 305–7
signal_struct 231–2, 591–2
signal_type(function) 629–30
signal_wake_up(function) 634–5
signal 字段 (task_struct) 16, 652–65
signal struct 594–5
SIMD 处理器中断 338–342
SIMd_math_error(function) 339, 340–42
sleep(调试模式) 81–3
SLEEP_ON_HEAD 宏 81–3
SLEEP_ON_TAIL 宏 81–3
SLEEP_ON_VAR 宏 81–3
sleep_time (task_struct) 22, 94
SMP 对称多进程处理 432–4, 434
smp_call(function) 451
smp_call_interrupt(function) 457
smp_inner_interrupt(function) 450
smp_timer_interrupt(function) 447–8
smp_processor_id 宏 10, 319, 321, 328, 330, 418, 419, 507
smp_stack_id(function) 450, 567–570, 574, 634, 635
smp_spurious_interrupt(function) 451
softq_struct 550, 552, 554
softq_init 函数 551
softq_pending 宏 559
softq_pending(function) 552, 553
软件中断
- 半部 577–52
- 数据结构 551–1
- 初始化机制 551–2
- 内核线程 555–8
- 概述 11, 397, 549–50
- 预递送 558–1
- 上升 558–9
- 请求统计统计 580–6
- 运行一个 552–5
- 任务队列 757–780
- tasklet 队列 560–72
SPARC 二进制入口点 289
spawn_queue(function) 555–6
spin_unlocked 宏 118–9
spin_lock(function) 116–7
spin_lock_bh 宏 398–400
spin_lock_init_macro 112, 115, 217–18
spin_lock_init(function) 219–20
spin_lock_irq 宏 349, 399, 400
spin_lock_irqsave_macro 398–400
spin_lock_string_macro 118–9
SPIN_LOCK_UNLOCKED 宏 114, 5, 228–229, 349
spin_try(function) 115–6
spin_unlock(function) 117–8
spin_unlock_bh_macro 398–400
spin_unlock_irq_macro 398–400
spin_unlock_irq_restore 398–400
spin_unlock_wait_atomic 118–9

自旋锁
- 8259A 可抢占中断控制器 386–7, 392, 393, 394
- 占用 115–6
- 数据结构 114
- 释放 117–8
- 初始化 114–5
- 层级 0 109–110
- 层级 1 111
- 层级 2 113–3
- 多处理器分配 114–9
- 调度器 181
- 接入 116–7
- 单处理器分配 109–114
- 等待队列 70–89
SPINLOCK_MAGIC_INIT_macro 114–5
- spinlock_t1 114
- 悬疑扩展处理器 300

查看 栈值 749–51
start_kernel() 9, 214, 551
start_time_field (task_struct) 277
8259A,irq_function 390
start_level_of_irq_function 484
state_field (task_struct) 14, 52, 85, 90, 217
state 254–5
流 341, 343, 404–483
wait_queue 61–3
wait_queue_head 63
acct 755–758–6
call_data_struct 433, 445
completion 26, 173, 215–216
desc_struct 272
exec_dev 721–0
hw_interrupt_type 424, 484, 486
idt 272
10_APIC_entry 472–3
irq_desc 353–4
action 355, 350, 185–6
kernel_sel 185
kernel_vm86_struct 771, 772, 773
kernel_vm86_struct 771–2, 774
list_head 73, 190
mm_struct 199–21, 193–4
mpc_config_intsrc 454, 456
mpc_config_iac 454, 555–6
no_irq_type 356–7, 371
pt_regs 232–3, 282–447, 289, 362
revored_struct 768
rt_significance 666, 669–7
usage 257, 268
schedule_data 185, 188, 192–3
sigance 592–3
systemcontext 667, 671–4, 690
signinfo 592–4, 595–8
signal_struct 231–2, 591–2
sigpending 594–5
softir_action 550, 553, 554
task_struct 10, 11, 39–23, 21, 507
tasklet_struct 560
thread 774–5
timer_list 531–3, 376
timer_vec 532–3
timer_rec 532–3
timeval 267, 513, 514
tq_struct 577–
uss_struct 182–3, 216–7
user_struct 267, 79
vm86_regs 768–9
vm86_struct, 769–7
vm86_plus_info 770–1
vm86_struct 770–1
struct_cpy_struct 28
suid_field (task_struct) 28
superuser_privilege 16
user(struct) 713–4
swap_space 27
swappable_file (task_struct) 27
switch_to_mapper 194, 195, 200–2
switch_isr 202–4
SYMBOL NAME 7, 8–1, 200
SYMBOL_NAME_LABEL 78
symmetric_multiplying 4
sys_call_table_entry 290
sys_call(task_struct) 246
syscall_trace(function) 746–7
system_call_entry_point 289–93
system_call_handler_interrupt_handler
system_service
clone() 213, 243
default_handler 722–3
entry_point 290–2
exit() 245
fork() 213, 215, 235–6
oldvm86() 785–6
ptrace() 17, 235, 236

# 索引

- used_math 字段 (task_struct) 30
- 用户添加 238–41
- 缓存 236–43
- 释放内存 241–2
- 哈希表 237–8, 240–1, 242–3
- user 字段 (task_struct) 29, 236–7
- 用户标识符 28
- 用户 3, 329, 289–90, 304, 587, 663, 679
- user_mode 宏 284
- user_struct 结构 29, 216–7, 236–8
- v6flags 字段 (thread struct) 775–80
- 变量
    - ast_pid 214
    - max_threads 214
    - nr_running 214
    - nr_threads 214, 216, 218
    - total_fork 214
- 向量中断 799–802
- vfork() 系统服务 172
- vfork_done 字段 (task_struct) 26
- 8086 模式
    - 控制信息 677–75, 770–1
    - CPU 时间 769–70
    - 数据结构 776–75
    - 模拟 PUSH 783–4
    - 模拟 PUSH 780–2
    - 进入 785–9
    - 异常处理程序 791–8
    - 标志寄存器 775–80
    - 退出 802–5
    - 读取内存 783–4
    - 寄存器保存 768–9, 772, 773, 774
    - 返回值 809
    - 栈布局 768–9, 771–5, 775–6
    - 线程结构 774–5
    - 陷处理 789–9
    - 向量中断 799–802
    - 写入内存 780–2
    - 用户写入空间 803–4
- 虚拟机角色 423–4
- vmk6() 系统服务 785–6
- vmk6_regs 结构 768–9
- vmk6_struct 结构 768
- vmk6_plus_info_struct 770–1
- vmk6_plus_struct 结构 770–1
- 等待队列
    - 检查项 733
    - 条件调度进程 83–8
    - 数据结构 616–6
    - 调试器 66
    - 查找进程 90–2
- 函数
    - __wake_up_common() 90–2
    - 等待队列，查找进程（续）
    - add_wait_queue() 69, 256–7
    - add_wait_queue_exclusive() 70
    - add_wait_queue_tail() 71
    - remove_wait_queue() 72
    - try_to_wake_up() 92–3
    - waitqueue_active() 73
    - 插入项 — 69
    - 锁 65
    - 锁架构 79–80
- 宏 wait_event_interruptible 87–8
- _WAIT_QUEUE_HEAD_INITIALIZER 65
- _WAIT_QUEUE_INITIALIZER 62
- _wake_up 88–90
- _wake_up_sync 88–90
- BUG() 68
- DEARE_WAIT_QUEUE_HEAD 65
- DECLARE_WAIT_QUEUE 62, 256–7
- set_current_state 85–6
- set_task_state 85
- SLEEP_ON_HEAD 81–3
- SLEEP_ON_TAIL 81–3
- SLEEP_ON_VAR 81–3
- wait_event 83–8
- wait_event_interruptible 86–7
- WAITQUEUE_DEBUG 62, 63, 64, 65, 66,–72
- 移除项 — 71–2
- TASK_INTERRUPTIBLE 状态 14
- 无条件睡眠进程 80–33
- 唤醒进程 88–93
- wait() 系统服务 15, 26, 245, 255–
- wait_childext 字段 (task_struct) 26, 52, 218
- wait_event_macro 84–5
- wait_event_interruptible 宏 86–7
- wait_for_completion() 函数 174–5
- wait_on_irq() 函数 497–9
- waitqueue_active() 函数 73
- WAITQUEUE_DEBUG 宏 62, 63, 64, 65, 66,–72
- wake_up_parent() 函数 643
- wake_up_process() 函数 558, 634, 635
- wake_up_sort_irq() 函数 558, 559
- wait_time 513
- will_become_orphaned, prngp 函数 253–4
- WQ_FLAG_EXCLUSIVE 123–4
- write_lock_宏 126
- write_lock_bb_macro 398–400
- write_lock_irq_macro 398–400, 512
- write_trylock() 函数 127
- write_unlock_macro 123–4
- write_unlock_bh_macro 398–400
- write_unlock_irq_macro 398–400, 512
- write_unlock_irq_restore_macro 398–400
- wrmsr 宏 332–3
- x86_do_profile(it) 函数 448–9
- XBUILD_SMP_INTERRUPT 宏 442–3
- XBUILD_SMP_TIMER_INTERRUPT 宏 443–4
- xchg 宏 107, 108
- 僵尸进程 14
