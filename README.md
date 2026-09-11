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

**Summary:** We set the die/core area, aspect ratio, and utilization factor; place the I/O cells; create the power distribution network; and perform macro placement.

The floor plan is now ready for the placement and routing step.

**Lab**

Standard cell placement happens during the placement stage.

OPENLANE/CONFIGURATION$ less README.md

The README file has details on what is being done at each stage (synthesis → floorplanning → placement → CTS → routing). Variables act as switches — each switch specifies what is being done and its default value. We can set values for any of these switches/variables/parameters as per our needs.

There are separate .tcl files that show what default value has been set.

**Priority flow:**

floorplan.tcl → config.tcl → sky130A_sky130_fd_sc_hd_config.tcl

**Inside config.tcl:**

VMETAL Layer – 4
HMETAL Layer – 3

(These layers are 1 more than what you specify.)

**Inside floorplan.tcl:**

VMETAL Layer – 2
HMETAL Layer – 3
run_floorplan
cd logs/floorplan/
ls -ltr
less ioplacer.log

**Check:**

Vertical metal layer: 5
Horizontal metal layer: 4
Core utilization = 50 (incorrect — the design's config.tcl should override the system defaults)

[The system default of 50 (from floorplan.tcl) was overridden by 65 (from config.tcl), and that 65 was in turn overridden by sky130A_sky130_fd_sc_hd_config.tcl.]
1 microns – 1000 database unites

<img width="975" height="83" alt="image" src="https://github.com/user-attachments/assets/5788bc2a-6d56-4f40-bdf7-24d744e4faf4" />

<img width="975" height="82" alt="image" src="https://github.com/user-attachments/assets/47e87727-f880-45aa-9a79-0b39eb9ddb2c" />

**Magic Tool**

Magic will open.

Shift+V – Fit the layout on the screen.

Zoom into a particular portion – Left mouse click, then right mouse click, then press Z.

Tkcon window – Type what to show which layer you are currently in.

<img width="547" height="376" alt="image" src="https://github.com/user-attachments/assets/d96fba4e-3e26-46ea-832c-eb0ea387752c" />

Tap cells are used to avoid latch-up conditions in CMOS devices. They connect the n-well to Vdd and the substrate to ground. They are placed at equal diagonal distances from one another.

### Placement and Routing

**1. Bind the netlist with physical cells.**

In the netlist, the shape of the gate represents its functionality, but in reality, it looks like a box with defined dimensions (width and height).

<img width="582" height="335" alt="image" src="https://github.com/user-attachments/assets/3cd0ec57-211f-4527-ba1f-907018c97fb5" />

<img width="239" height="329" alt="image" src="https://github.com/user-attachments/assets/028992a6-7bec-4cad-966b-456baba6ca70" />

<img width="442" height="254" alt="image" src="https://github.com/user-attachments/assets/03acbb90-e6a4-47e1-8b25-e9e491e27d45" />

**Library**– Contains the width and height, timing and delay information, required conditions (when conditions), and the shape and size of each cell.

We can choose whichever size we want based on the timing condition and the space available on the floorplan.

**2. Placement** 

At this stage, we have the netlist, the floorplan, and the physical view of the logic gates. Now we need to place the netlist within the floorplan.

<img width="947" height="375" alt="image" src="https://github.com/user-attachments/assets/98d8f7fe-cfdf-4ef1-87d0-33cc6aa39adc" />

<img width="779" height="352" alt="image" src="https://github.com/user-attachments/assets/481f98c3-2e41-403b-813d-74c7d700f357" />

**3. Optimized Placement** – There are flip-flops (FFs) placed far away from input and output components. The solution to this distance issue is optimized placement.

At this stage, we estimate wire length and capacitance, and based on that, insert repeaters. Repeaters are buffers used to maintain signal integrity — but more repeaters mean more area used.

Based on the slew value/data transition analysis, we decide whether or not a buffer is needed in the path.

To check if the placements are correct: perform data path and setup timing analysis with an ideal clock.

**Need for Characterization** – Library Characterization and Modeling.

**Step 1 – Logic Synthesis**

Output: An arrangement of gates that represents the original functionality described using RTL.

**Step 2 – Floorplanning**

Import the netlist to decide the width and height of the core and die, depending on the number of gates and the shape and size of the gates in the netlist.

**Step 3 – Placement**

Place the logic cells in a manner that meets initial timing requirements.

**Step 4 – Clock Tree Synthesis (CTS)**

To achieve zero skew.

**Step 5 – Routing**

To route from one point to another, we need to consider certain properties of the cell that must be taken into account.

**Step 6 – STA**

This is the final stage, also called sign-off timing analysis. It determines the setup time, hold time, and the maximum frequency of the circuit.

One common element across all stages is gates/cells (AND, OR, LATCH, BUFFER, DFF, ICG, etc.). To know what a gate is — its timing characteristics, etc. — for the EDA tools, library characterization is important.

**Lab – Checking if Congestion is Reduced**

**Placement**– Standard cell positions are fixed.

Global and detailed placement each require different tools.

**Global Placement** – Focuses on reducing wire length using HPWL (Half-Perimeter Wire Length). No legalization happens at this stage; legalization actually occurs during detailed placement.

**Legalization** – Ensures there are no overlaps between cells, from a timing point of view.

**Cell Design Flow**

<img width="768" height="395" alt="image" src="https://github.com/user-attachments/assets/04caa87e-0ec1-4cae-ad47-bcf63faa3a3f" />

Library – Drive strength, voltage, size, and functionality vary for each element/standard cell.

<img width="693" height="415" alt="image" src="https://github.com/user-attachments/assets/26ec1a92-b719-48a1-8e20-414ceeab2275" />

**Cell Design Flow (For Inverter / NOT Gate)**

**Inputs:**

**DRC & LVS Rules** – Design rules such as poly width (lambda), poly-to-active spacing, etc., are defined in the library files.

**SPICE Models** – Contain formulae for equations such as threshold voltage; the parameters used in these formulae take values from the library.

**Library & User-Defined Specs:**

-Cell height (separation between power and ground) and cell width (based on timing information) to achieve good (high) drive strength.
Supply voltage (considering noise margin).

-Metal layers — certain library elements should be placed on specific metal layers; for example, power layers and contacts should be built on the metal layers specified in the spec.

-Pin locations — the spec may require certain inputs/outputs to be placed near power/ground.

-Drawn gate length (gate length).

**Design Steps:**

Circuit Design – Determines the switching threshold voltage, deriving (Wp/Lp)/(Wn/Ln). The output from circuit design is called the Circuit Description Language (CDL) file.


