cmake_minimum_required(VERSION 3.20)

set(CMAKE_TRY_COMPILE_TARGET_TYPE "STATIC_LIBRARY")
set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR riscv)

set(CMAKE_C_COMPILER riscv64-unknown-elf-gcc)
set(CMAKE_ASM_COMPILER riscv64-unknown-elf-gcc)

project(ANOS C ASM)

set(COMMON_FLAGS "-march=rv32imac -mabi=ilp32 -mcmodel=medany -std=c11 -O2 -g3 -Wall -fno-stack-protector -ffreestanding -nostdlib -fno-pie")

set(CMAKE_C_FLAGS "${COMMON_FLAGS}")
set(CMAKE_ASM_FLAGS "${COMMON_FLAGS}")

set(CMAKE_EXE_LINKER_FLAGS "-Wl,-T${CMAKE_CURRENT_SOURCE_DIR}/kernel.ld -nostdlib")

add_executable(kernel.elf
        kernel.c
        common.c
        kernel.h
        common.h
)