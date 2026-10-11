and add the line

```rust
use panic_halt as _;
```

to `main.rs` immediately below the existing use statement. The code should now build without errors, and the binaries for your target should be in the `target` subdirectory. You can install some further tools to check their validity. Run the following commands:

```
```bash
rustup component add llvm-tools
cargo install cargo-binsight
```

This installs the standard LLVM tools and a wrapper that Cargo uses to call them. If you type

```bash
cargo size -- -Ax
```

you will get some information about how the code is laid out in memory (see Listing 1). It shows that the vector table is located at the start of the flash memory, the program code (`.text`) 0x400 bytes later, and it’s all of 0x8e bytes in size. Any variables (`.data`) would be located in RAM, though in this case, with the program being so simple, the `.data` segment has zero size.
```

# Programming the Target

To program your microcontroller with this code, you need one further tool, `cargo embed`. This tool talks over USB to the companion processor on the target board, which in turn manages programming the microcontroller. You can no longer install cargo embed directly as it is now part of a project called probe-rs. Follow the instructions at the project website [13], which just amounts to running a `cur` command. Let’s first check that probe-rs supports our target:

```
```bash
$ probe-rs chip list | grep STM32L476
...
STM32L476RCTX
STM32L476RET
STM32L476RGT
...
```

The output shows it supports many variants of the STM32L476, including our target. Now connect the target board to a USB socket on your host. The power LED should light. Type `probe-rs list` and you should see that it has detected the target board. Our output may vary, depending on the exact configuration:
```

```
```text
The following debug probes were found:
[0]: STM32 V3 -- 0403:3753:0000002737 5650132903558 (ST-LINK)
```

Let’s try programming the target:

```bash
cargo embed --chip STM32L476RGT
```

You should see an output similar to that in Figure 2 – success: your code runs! Note that the proper launch command was `cargo embed` and not `cargo run`, which would attempt to run your program on the host.
```

![](bbox=[0.35, 0.09, 0.61, 0.19])

To complete the project configuration, you can add the chip information to an `Embed.toml` file in the project’s root folder, so you don’t have to provide all the details every time:

```
```toml
[default.general]
chip = "STM32L476RGT"

[default.rtt]
enabled = false

[default.reset]
halt_afterwards = false
```

Then typing `cargo embed` will be enough to program and run your code on the target.
```

# Runtime Debugging

Before diving into programming the microcontroller’s I/O, I’ll deal with a debugging technique which allows you to print data back to your host’s console. The first step is to add another crate with

```
```bash
cargo add rtt-target
```

(which provides a feature called real-time transfer, RTT) and a new statement to the program:

```rust
use rtt_target::{rprint!, rtt_init_*
print!};
```

Modify the `Embed.toml` file you created above, and set `enabled` to `true` in the `default.rtt` section. Then you can add some `print` statements to your code (see source code `file main-02.rs`). This will fail to link, producing an undefined symbol error. You can fix it by adding a feature to the `cargo` `make` crate. Change the appropriate line in Cargo.toml to this:
```

```
```toml
[dependencies]
cortex-m = { version = "0.7.7", features = ["critical-section-single-core"] }
```

Modify `main.rs` so it looks like Figure 3 (`main-03.rs`). This should clear your terminal and print a list of ascending numbers. As this data is exchanged
```

# Listing 1: Output of "Cargo Size"

|               | size | addr |
|---------------|------|------|
| .vector_table | 0x500 | 0x08000000 |
| .text         | 0x8e  | 0x0800046c |
| .rodata       | 0     | 0x0800046c |
| .data         | 0     | 0x20000000 |
| .gnu.sections | 0     | 0x20000000 |
| .bss          | 0     | 0x20000000 |
| .uninit       | 0     | 0x20000000 |
| .debug_abbr   | 0x11ab | 0x0  |
| .debug_info   | 0x2237 | 0x0  |
| .debug_ranges | 0x1248 | 0x0  |
| .debug_frame  | 0x199f | 0x0  |
| .debug_str    | 0x3B8d | 0x0  |
| .comment      | 0x40   | 0x0  |
| .ARM.attributes | 0x3a | 0x0  |
| .debug_frame  | 0x1154 | 0x0  |
| .debug_line   | 0x1f26 | 0x0  |
| .debug_loc    | 0x529  | 0x0  |
| Total         | 0x56c275 | |

```
```rust
1 //no_std
2 #fn_main
3 extern crate cortex_ms
4 use cortex_m_rtsentry;
5 use panic_halt as _;
6 use rtt_target::{rprint!, rtt_init_*
print!};

8 #entry
9 fn entry_point() -> !{
10     rtt_init_point!();
11     let mut i = 0;
12     loop { //
13         rprint!("{}\n", i);
14         i += 1;
15         cortex_ms::delay(2_000_000);
16     }
17 }
```

Figure 3: Real-time transfer lets you see output from the embedded device (`main-03.rs`).
```