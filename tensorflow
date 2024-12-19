.section .data
    cpu_info_msg: .asciz "CPU Usage:\n"
    ram_info_msg: .asciz "RAM Info:\n"
    total_ram_msg: .asciz "Total RAM: %lu bytes\n"
    free_ram_msg: .asciz "Free RAM: %lu bytes\n"
    cpu_stat_path: .asciz "/proc/stat"
    sysinfo_syscall: .asciz "sysinfo"

.section .bss
    total_ram: .space 8
    free_ram: .space 8
    cpu_usage: .space 8
    buffer: .space 256

.section .text
    .global _start

_start:
    // Infinite loop to check every second
.loop:
    // Get RAM info
    mov x0, total_ram
    mov x1, free_ram
    bl get_ram_info

    // Get CPU info
    bl get_cpu_info

    // Print RAM info
    ldr x0, =ram_info_msg
    bl print_string
    ldr x0, =total_ram_msg
    ldr x1, =total_ram
    bl print_long
    ldr x0, =free_ram_msg
    ldr x1, =free_ram
    bl print_long

    // Print CPU info
    ldr x0, =cpu_info_msg
    bl print_string
    ldr x0, =cpu_usage
    bl print_long

    // Sleep for 1 second
    mov x0, 1          // seconds
    bl sleep

    b .loop            // Repeat

// Function to get RAM info
get_ram_info:
    // Call sysinfo to get RAM info
    mov x8, 99         // syscall number for sysinfo
    svc 0              // make syscall
    // Store total and free RAM
    ldr x0, =total_ram
    str x0, [x0]
    ldr x0, =free_ram
    str x1, [x0]
    ret

// Function to get CPU info
get_cpu_info:
    // Read from /proc/stat (not implemented in this example)
    // Placeholder for CPU usage logic
    mov x0, 0          // Placeholder for CPU usage
    str x0, [cpu_usage]
    ret

// Function to print a string
print_string:
    mov x1, x0        // string to print
    mov x0, 1         // file descriptor (stdout)
    mov x2, 256       // length of string
    mov x8, 64        // syscall number for write
    svc 0
    ret

// Function to print a long integer
print_long:
    // Placeholder for long integer printing logic
    ret

// Function to sleep
sleep:
    mov x8, 35         // syscall number for sleep
    svc 0
    ret
