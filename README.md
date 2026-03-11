# AN-RISCV-OS (Developing)

> **"Reinventing the wheel to master the first principles of Operating Systems."**

本项目是一个基于 RISC-V 架构的轻量级内核，参考了 *《Operating System in 1000 Lines》*。我通过“从零实现”的方式，深入理解计算机底层是如何从引导程序（Bootloader）一步步构建出多进程环境的。

## 🚀 当前进度：进程管理 (Chapter 10)

目前我已经实现了内核的核心骨架，重点攻克了**多进程调度**。

### 核心技术点 (Technical Highlights)

* **RISC-V 寄存器上下文保存**：手动编写汇编代码（`switch_context`），在内核态保存/恢复 `s0-s11` 等被调用者保存寄存器，实现硬件级的执行流切换。
* **协作式调度器 (Cooperative Scheduler)**：实现了进程结构体 `struct process`。
* **异常与陷阱处理**：在第08章的基础上，完善了 `trap_handler`，确保时钟中断或异常发生时，进程状态能被正确挂起。
* **从零实现的 C 标准库**：不依赖任何第三方二进制库，手动实现了 `printf`、`memcpy` 等核心函数，确保整个系统的透明度。

### 系统架构

1. **引导 (Boot)**：通过 `kernel.ld` 链接脚本精准控制内存布局，进入 `kernel_main`。
2. **内存分配**：基于页面（Page）的简单分配器，为进程控制块（PCB）和栈空间提供动态支持。
3. **多任务**：目前支持在内核态创建并并发运行多个简单任务。

---

## 🛠 开发环境

* **Architecture**: RISC-V 64-bit
* **Language**: C & RISC-V Assembly
* **Platform**: QEMU virt machine
* **Compiler**: `riscv64-unknown-elf-gcc`

## 📅 下一步计划

* [ ] **Chapter 11-13**: 实现虚拟内存与页表映射，将进程隔离在用户模式。
* [ ] **Chapter 14**: 编写第一个系统调用（Syscall）。
* [ ] **Chapter 15-16**: 实现磁盘 I/O 与简单的文件系统。