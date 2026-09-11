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

**SoC Design using OpenLane**

OpenLane was meant to automate entire RTL to GSD to flow

SoC Design using OpenLane
OpenLane was meant to automate entire RTL to GSD to flow

<img width="778" height="267" alt="image" src="https://github.com/user-attachments/assets/9e493a59-378a-473a-8e54-5d977223786e" />

**Tools**

RTL Design – librecores.org, opencores.org, github.com

EDA Tools – Flow, OpenROAD, OpenLANE

PDK Data – Initially, the design of an IC was tightly integrated with the manufacturing process available within each company. Lynn Conway and Carver Mead envisioned the need to separate design from technology, introducing a structured design methodology based on lambda-based rules.

Since then, we have seen the emergence of pure-play fabs and fabless design companies.

PDK – The interface between designers and fabs is a set of data files and documents referred to as Process Design Kits (PDK).

Includes – Libraries, etc.

Google released an open-source PDK under the Apache 2.0 license — a FOSS 130nm production PDK.

<img width="975" height="1047" alt="image" src="https://github.com/user-attachments/assets/de670e5d-89d6-4c86-8785-c8ea6c27a881" />

**Simplified RTL to GDSII Flow**

<img width="864" height="314" alt="image" src="https://github.com/user-attachments/assets/30fbfb69-55a9-4239-b094-c59ccc57273a" />

**Physical Design Flow**

**Synthesis** – RTL is translated into a circuit using the standard cell library.

**Standard Cells** – Have a regular layout.

**Floorplanning + Powerplanning (FP+PP)** – Planning the silicon area, dimensions, and pin locations.

**Power Planning** – Designing the power distribution network.

**Place** – Placing the cells on the floorplan. This involves two steps: global and detailed placement.

**Clock Distribution Network** – Delivers the clock to all sequential elements.

**Routing** – Implements the interconnect using the available metal layers.

6 routing layers; the lowest is the local interconnect layer, and the other 5 are aluminum layers.
Global routing – Generates routing guides.
Detailed routing – Uses the routing guides to implement the actual wiring.

**Sign-off:**

Physical Verification – Design Rule Checking (DRC) and Layout vs. Schematic (LVS).
Timing Verification – Static Timing Analysis (STA).

**Open Source ASIC Flow – Openlane pdk**
**OPENSOURCE SoCs – StriVe family (Open PDK, Open EDA, Open RTL)**

<img width="795" height="555" alt="image" src="https://github.com/user-attachments/assets/1d62e618-8c25-4164-af50-09aeec537361" />

**Goal** – Produce a clean GDSII with no human intervention.

"Clean" means: No LVS, DRC, or timing violations.

<img width="863" height="492" alt="image" src="https://github.com/user-attachments/assets/39a4f205-ad67-4232-876c-f051a584edf3" />

**Synthesis Exploration**

**Design Exploration Utilities** – Generates reports on violations (helps find the best design configurations) and is also used for regression testing.

**Testing After Fabrication (DFT)** – Includes Scan Insertion, Automatic Test Pattern Generation (ATPG), Test Pattern Compaction, Fault Coverage, and Fault Simulation.

**Physical Implementation** – The OpenROAD app performs automated place and route. It covers:

-Floorplanning/Power Planning
-End Decoupling Capacitors and Tap Cell Insertion
-Placement: Global and Detailed
-Post-Placement Optimization
-Clock Tree Synthesis (CTS)
-Routing: Global and Detailed

Dealing with Antenna rule violations – 

<img width="811" height="495" alt="image" src="https://github.com/user-attachments/assets/98b3ea33-f822-4ceb-9ea2-2ed03e40eff1" />

**2 solution :**

1-	Bridging – attaches higher layer intermediary (Reuires Router Awareness)

2-	Add antenna diode cell

<img width="858" height="563" alt="image" src="https://github.com/user-attachments/assets/be08b154-29ae-4be0-84bb-751fd8fe26a3" />

**Open Source Tools**

**Antenna Check** – Fake antenna diodes are used; the antenna checker (Magic) is run on the routed layout.

**STA** – OpenSTA (part of OpenROAD).

**Physical Verification** – Magic performs Design Rule Checking (DRC) and SPICE extraction from the layout. Magic and Netgen are used for LVS.

**OpenLANE Directory Structure (in detail)**

The Skywater 130nm PDK is used in this workshop.

**Open PDK** – Timing, tech files, etc. — scripts that convert foundry-level IP PDK files to be compatible with open-source EDA tools like Magic and Netgen. Magic is used for layout.

**Skywater PDK** – One of the variants.

libs.ref

libs.tech

<img width="975" height="602" alt="image" src="https://github.com/user-attachments/assets/cc9c4b4e-1e95-4b55-b3fd-1ee98b62b803" />

```tcl
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```
<img width="975" height="742" alt="image" src="https://github.com/user-attachments/assets/a756d4fa-b186-4847-a285-382484027559" />

Useful link-
https://github.com/efabless/openlane

**Objective of the Workshop:** Calculate the flop ratio, which is the number of D-flip-flops (D-FF) divided by the total number of cells.

## DAY 2 Good floorplan vs bad floorplan and introduction to library cells

### SKY130_D2_SK1 - Chip Floor planning considerations: 

**1.Define the width and height of the core and die.**

We are dependent on the dimensions of the netlist (flops/logic gates) — only standard cells are considered at this stage, not wires.


<img width="517" height="302" alt="image" src="https://github.com/user-attachments/assets/ce3a02dd-d4d4-4014-b5f4-7383cb996cfa" />

4 SQ UNIT

<img width="298" height="235" alt="image" src="https://github.com/user-attachments/assets/5dd162b1-e6da-43f9-9039-0872eab09659" />

<img width="533" height="175" alt="image" src="https://github.com/user-attachments/assets/4f564095-744c-4bd3-a042-382de7acc058" />

<img width="536" height="240" alt="image" src="https://github.com/user-attachments/assets/3fa438b1-e63b-44a4-8d3e-5497e224abd4" />

**Utilization Factor = Area occupied by the netlist / Total area of the core**

= (4 × 1 sq. unit) / (2 unit × 2 unit)
= 4 sq. units / 4 sq. units
= 1

This means 100% utilization. Usually, we aim for 50–60% utilization.

Aspect Ratio = Height / Width = 2 unit / 2 unit = 1

A ratio of 1 means it is in a square shape; if not 1, it means it's a rectangular shape.

**IF THE CHIP IS BIGGER:**

<img width="636" height="384" alt="image" src="https://github.com/user-attachments/assets/cd6ec3fe-8f0b-4011-a6b2-0e46caed3827" />

UF = 0.5, AR = 2/4 = 0.5

**2. Define the location of pre-placed cells.**

Pre-placed cells – Implemented as black boxes and used multiple times, though the functionality is implemented only once.

Similar IPs – Memory, Clock-Gating, Comparator, MUX — are implemented once and can be instantiated multiple times in the netlist. The functionality is implemented only once.

The arrangement of these IPs in the chip is called floorplanning. Since they are placed in the chip before automated placement and routing, they are called pre-placed cells.

<img width="501" height="551" alt="image" src="https://github.com/user-attachments/assets/e391fff6-53c7-45cb-928f-6be4c23c5329" />

**3. Surround pre-placed cells with Decoupling Capacitors**

Switching operations demand switching current.

0 → 1: Requires power.

1 → 0: Discharges power.

Decoupling Capacitor – Decouples the circuit from the main power supply. It is added in parallel to Vdd and placed close to the circuitry. Whenever the circuit switches, it draws current from the decoupling capacitor (Cd) instead of the main supply.

<img width="605" height="317" alt="image" src="https://github.com/user-attachments/assets/1deb0182-9af9-4054-a8d9-e2c22c7e9ed3" />

Decoupling capacitors keep the circuit charged. Whenever there is switching activity, the decoupling capacitor loses some amount of charge to the circuitry; whenever there is no switching activity, the decoupling capacitor spends its time replenishing its own charge. This takes care of local communication.

<img width="415" height="266" alt="image" src="https://github.com/user-attachments/assets/bd74371c-a2fa-4c5b-8ef5-1acc0c54fa07" />

**What about global communication?**

**4.	Power planning**

Problem: The supply is provided only from one point

<img width="462" height="334" alt="image" src="https://github.com/user-attachments/assets/16d0e21f-19d4-4ecd-89bc-a4537c2bc15f" />

 1->0  ground bounce

 <img width="599" height="379" alt="image" src="https://github.com/user-attachments/assets/20b032d0-4208-4ec8-8c3e-537b8b3bc685" />

0 ->1 voltage drops

<img width="595" height="358" alt="image" src="https://github.com/user-attachments/assets/3546e3b6-acc3-49ca-9219-2dc5c3ef485e" />

**Solution:** Multiple power supplies — multiple Vdd's and Vss's. This is called a mesh.

<img width="511" height="411" alt="image" src="https://github.com/user-attachments/assets/8bad69ba-b3ee-471a-b1ad-bc6990e0b7cd" />

<img width="518" height="391" alt="image" src="https://github.com/user-attachments/assets/27695164-e299-48f4-90a9-ecb2a306b3dd" />

Any logic in that area will take current from the nearest power supply or dump its current into the nearest ground.

**5. Pin placement**

Considering below image as netlist:

<img width="575" height="396" alt="image" src="https://github.com/user-attachments/assets/029b8736-761b-4740-8bb9-d54468f415c0" />

<img width="508" height="355" alt="image" src="https://github.com/user-attachments/assets/39652193-5a5c-4609-8f02-a03adb1bff98" />

**Observations:**

-I/O ports are placed in the area between the core and the die.

-I/O ports can be placed anywhere, in any order, based on the designer's choice.

-The ordering of Din/Dout is not fixed — it depends on where the cells are placed. For example, if block A is driven by Din1 and Din2, we try to place it close to those ports. Similarly, if block B is directly connected to the clock output, placing it too close might require additional decoupling capacitors — so instead, we keep it where it is and use buffers to route the signal out to the clock output.

-No cell/flip-flop can be placed in the occupied area — ports must remain outside of this area.

-Functional understanding is important for pin placement.

-Clock ports are larger in size compared to I/O ports. This is because the clock drives the entire chip continuously and needs the lowest-resistance path possible. A larger size means lower resistance.

**6. Logical Cell Placement Blockage** – The automated place-and-route tool should not place any cell in this area, as it is reserved for pin locations. The area (orange-shaded) is blocked off for the automated place-and-route tool. This is done through logical cell placement blockage.

<img width="446" height="324" alt="image" src="https://github.com/user-attachments/assets/637e561c-0ed4-40b7-a5d8-a8f365c2b16c" />










