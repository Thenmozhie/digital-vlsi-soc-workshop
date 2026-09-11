# digital-vlsi-soc-workshop
## DAY 1 Inception of open-source EDA, OpenLANE and Sky130 PDK
As an example, an Arduino board has a processor chip on it.

<img width="601" height="461" alt="image" src="https://github.com/user-attachments/assets/1fda4505-535d-4fb6-aa09-457f6c26f9e1" />

<img width="584" height="329" alt="image" src="https://github.com/user-attachments/assets/5c6b0323-afe2-4f8c-bec8-17ac6ccd42e3" />

If I open the IC, I see input/output ports. Before this workshop, I would call it a "chip"; after the workshop, I now call it a "package" (QFN-48: Quad Flat No-Leads). The pin locations on the package are determined by the Arduino board design.

<img width="576" height="375" alt="image" src="https://github.com/user-attachments/assets/1ec7a491-1e75-4851-a4f9-96ff6075a8bd" />

Inside the Chip

-Pads – Signals going into or out of the chip pass through the pads.

-Core – All the digital logic is placed in this area.

-Die – The physical size of the chip.

<img width="953" height="592" alt="image" src="https://github.com/user-attachments/assets/34f8f25b-d03b-4d78-a2d8-aa26459ef4e3" />

EXAMPLE- RISC V CHIP

<img width="747" height="586" alt="image" src="https://github.com/user-attachments/assets/f808e1e3-0eab-445f-b894-9715f3344c8b" />

**Foundry IPs**

A typical core/chip consists of components such as SoC, PLL, SPI, SRAM, ADC, and DAC — these are called Foundry IPs. Most chips depend on this foundry.

Foundry – The place where chips are manufactured. We communicate with the foundry through an interface file that is given to us or passed through us.

Macros – Digital blocks.

**Difference:**

IP – Some intelligence/technique used to build certain logic.
Macros – Pure digital logic.

<img width="975" height="523" alt="image" src="https://github.com/user-attachments/assets/6645c685-9b8f-4697-9fa0-0bcc6020a15b" />

### Introduction to RISC V ISA
**Software to Hardware Communication**

Software communicates with hardware through an instruction set.

Example: A C program is meant to run on the layout/hardware/chip. The C program is compiled into assembly language (RISC-V), then converted into machine/binary language that the hardware can understand.

The interface between the RISC-V architecture and the layout is HDL. This RISC-V specification needs to be implemented in some RTL (here, the PicoRV32 CPU core), and going from RTL to layout follows the standard RTL-to-GDS flow.

<img width="975" height="515" alt="image" src="https://github.com/user-attachments/assets/731e652c-1a63-4e63-8f19-239bda45f283" />

**Applications to Instructions**

Apps written in C/C++/Java are converted into their respective instructions (.exe file) by a compiler. If the hardware belongs to the RISC-V/MIPS/Intel architecture, the compiler converts the code into the corresponding RISC-V/MIPS/Intel instruction set.

<img width="975" height="592" alt="image" src="https://github.com/user-attachments/assets/6464456d-ed65-4e04-9f50-767ebcd3bca2" />

The output of the compiler depends on the hardware. The assembler's job is then to convert this instruction set into the respective binary language, since hardware understands only 0s and 1s.

<img width="975" height="592" alt="image" src="https://github.com/user-attachments/assets/1c092934-0957-42be-ac7c-a81a7abc32d4" />


This instruction set/specification is implemented in RTL. The RTL is then synthesized into a netlist, and the netlist undergoes physical design implementation.

<img width="975" height="478" alt="image" src="https://github.com/user-attachments/assets/7ba0a022-6ac4-44dc-986d-7962c8e921cd" />



