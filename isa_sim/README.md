# RISC-V Instruction Set Simulator

A simple RISC-V instruction set simulator for RV32IM.

## Building

Dependancies;
* gcc
* make
* libelf

To build the executable, type:
```
make
````

## Usage

The simulator will load and run a compiled ELF (compiled with RV32I or RV32IM compiler options);
```
./riscv-sim -f firmware.elf
```

There is an example ELF provided.

## Extensions

The following primitives can be used to print to the console or to exit a simulation;
```

#define CSR_SIM_CTRL_EXIT (0 << 24)
#define CSR_SIM_CTRL_PUTC (1 << 24)

static inline void sim_exit(int exitcode)
{
    unsigned int arg = CSR_SIM_CTRL_EXIT | ((unsigned char)exitcode);
    asm volatile ("csrw mscratch,%0": : "r" (arg));
}

static inline void sim_putc(int ch)
{
    unsigned int arg = CSR_SIM_CTRL_PUTC | (ch & 0xFF);
    asm volatile ("csrw mscratch,%0": : "r" (arg));
}
```
