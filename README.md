# digital-vlsi-soc-workshop

**Table of Contents**

 [DAY 1](#day-1-inception-of-open-source-eda-openlane-and-sky130-pdk)
 
 [DAY 2](#day-2-good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
 
 [DAY 3](#day-3--design-library-cell-using-magic-layout-and-ngspice-characterization)
 
 [DAY 4](#day-4-pre-layout-timing-analysis-and-importance-of-good-clock-tree)
 
 
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

<img width="727" height="792" alt="image" src="https://github.com/user-attachments/assets/8e7c7997-b163-400d-84d0-658df137e7e5" />

**Layout Design** – Using the (Wp/Lp)/(Wn/Ln) values obtained from the previous step, we implement them into the layout.

**Step 1** – Implement the function through MOS transistors.
**Step 2** – Derive the PMOS and NMOS graphs from the design (Euler's path and stick diagram).
Use the results from the input stage — DRC rules, etc. — to create the layout (Tool: Magic).

**Output from Layout Design:**

GDSII
LEF (width and height of the cell)
Extracted SPICE netlist (.cir) — resistance and capacitance of every element.

<img width="829" height="489" alt="image" src="https://github.com/user-attachments/assets/3408de83-3fc1-4467-b4e2-65d394db454f" />

**Characterization**

**Output:** Timing, noise, power (.libs), and functionality of the circuit.

**Steps:**

1. Read the model file.
2. Extract the netlist file.
3. Recognize the behavior of the buffer.
4. Read the sub-circuit of the inverter.
5. Attach the necessary power source.
6. Apply the stimulus.
7. Provide the necessary output capacitance.
8. Provide the necessary simulation command (transient simulation – .tran, DC simulation – .dc).

These inputs (steps 1–8) are fed in the form of configuration files to the characterization software called GUNA.

<img width="869" height="798" alt="image" src="https://github.com/user-attachments/assets/0b8badc4-2b74-4706-9b60-7dd2227a9f04" />v


<img width="869" height="798" alt="image" src="https://github.com/user-attachments/assets/3a522789-5cc5-491d-a355-7cb804f3d6ce" />


The output from GUNA brings the classification of characterization types:

1. Timing characterization
2. Power characterization
3. Noise characterization

**Timing Characterization** – To familiarize ourselves with the tool GUNA, we need to understand some variables that we feed into the software.

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/ea1745e6-c093-494d-86b5-23d292133981" />

<img width="973" height="301" alt="image" src="https://github.com/user-attachments/assets/9b8e20e9-4aa2-41e6-930e-36b1f383837c" />

**Propagation Delay**

Delay = (Time at output threshold) − (Time at input threshold)

<img width="544" height="289" alt="image" src="https://github.com/user-attachments/assets/c13cd967-ec0c-4db2-b273-d0fe6208b5de" />

If the output comes before the input, it gives a negative wire delay, which represents a poor choice of threshold points.

<img width="674" height="438" alt="image" src="https://github.com/user-attachments/assets/02a3923e-de25-4783-91dd-3049ac9cb5bb" />

When two inverters are placed very far apart, we may see negative wire delays even if the output threshold points are correct.

Note: Negative delay indicates greater slew.

<img width="975" height="483" alt="image" src="https://github.com/user-attachments/assets/3ea001a8-e841-4d8e-a816-ec4e3a6eaab4" />


**Timing characterization for Transition Time:**

Note: 20% of Vdd

<img width="974" height="247" alt="image" src="https://github.com/user-attachments/assets/ed8b0536-370b-4932-bc62-43943299e2d4" />

<img width="975" height="335" alt="image" src="https://github.com/user-attachments/assets/3ad2bb66-72c4-40c7-a5d2-4ee457cc9e0b" />


<img width="975" height="440" alt="image" src="https://github.com/user-attachments/assets/612b4720-a0e2-4ff3-8a7a-d58956bf4958" />

## Day 3  Design library cell using Magic Layout and ngspice characterization

**Lab:** IO Placer Revision (IO Placer Tool)

How to make changes to the file: The setting for input/output pins is available in the floorplan.tcl file.

Copy/paste: Select the variable, go to the place where you want to paste it, and press the mouse middle button.

Setting the variable env(FP_IO_MODE) to 2:

set ::env(FP_IO_MODE) 2
run_floorplan


**Voltage Transfer Characteristics (VTC) – SPICE Simulation**

**Step 1:** How to create a SPICE deck for the complete netlist?

**Component Connectivity** – Provide connectivity for the substrate as well, since it is a potential pin on the NMOS/PMOS transistor (it tunes the threshold voltage of the transistor).

<img width="309" height="361" alt="image" src="https://github.com/user-attachments/assets/8199ffdc-05bc-4299-87f1-93cc5fec48b3" />

**Component Values** – Values for PMOS/NMOS. Ideally, PMOS should be twice or thrice the size of NMOS; here, for simplicity, we consider the same values for both PMOS and NMOS.
Voltage Values.

<img width="454" height="389" alt="image" src="https://github.com/user-attachments/assets/3b73145d-fb1f-4523-994f-df155077781c" />

<img width="392" height="309" alt="image" src="https://github.com/user-attachments/assets/39dda5de-df5e-4ea0-a2d1-c1e890d68a9f" />

**Identify Nodes** – One component lies between 2 points. For example, M1 lies between 3 nodes, while a capacitor lies between 2 nodes.

**Name the Nodes** – For example, the load capacitor lies between "out" and "0."

<img width="385" height="339" alt="image" src="https://github.com/user-attachments/assets/57ad5a1c-ac6a-4024-9eb2-36e3f71be246" />


Let's start writing the SPICE deck.

MOSFET Syntax: name drain gate source substrate p/n mos values

<img width="855" height="349" alt="image" src="https://github.com/user-attachments/assets/126de95a-9892-4509-b845-d39f4770d8fd" />

<img width="577" height="440" alt="image" src="https://github.com/user-attachments/assets/94b95b1b-c7d7-4b3a-873f-f382ca0b9964" />

Simulation 1

Steps:

Open the ngspice simulator.

Navigate to the location where the .cir file is stored:
  
   cd <location>

**Source the circuit file:**
  
   source <circuit_file>

**Run the simulation:**
   
   run

**Set the plot:**
   
   setplot
   dc1
   display

**Plot the output vs. input:**
  
   plot out vs in

This gives us the VTC (Voltage Transfer Characteristics) curve.

<img width="567" height="458" alt="image" src="https://github.com/user-attachments/assets/231e4c35-50ec-47ec-9f6e-21013af57836" />

Simulation 2 – simulate following the same steps with pmos width 2.5 time greater
 
<img width="473" height="315" alt="image" src="https://github.com/user-attachments/assets/fa9e209b-3512-4b03-b8a1-85d5d7752d21" />

<img width="858" height="412" alt="image" src="https://github.com/user-attachments/assets/e759027b-8b5e-492e-b47c-893c98edd3d4" />

### Static behavior evaluation: CMOS inverter robustness

**1. Switching Threshold, Vm**

Vm is the point at which Vin = Vout, meaning both MOSFETs are in the saturation region — i.e., both are ON, which leads to leakage current.

Transient analysis,

<img width="698" height="299" alt="image" src="https://github.com/user-attachments/assets/072c3276-4559-4de0-940a-dca464388f15" />

**Finding Rise Delay, Fall Delay, and Switching Threshold (Vm)**

Lab – Extracting a SPICE File from a .mag File for Characterization

Given a .mag file, here's how to extract the SPICE file from it and perform characterization.

git clone <GitHub link>

ls -ltr

cd vsdstdcelldesign

ls -ltr

We will first open the .mag file to view the layers of the inverter — we don't need to build the inverter from scratch.

We need to perform SPICE extraction and post-layout SPICE simulation.

<img width="975" height="380" alt="image" src="https://github.com/user-attachments/assets/902be4f1-559f-4f54-afc5-29d66fd21b00" />

<img width="975" height="664" alt="image" src="https://github.com/user-attachments/assets/fc1d12e0-7beb-4257-89ba-7daedc946fa8" />

<img width="975" height="571" alt="image" src="https://github.com/user-attachments/assets/9b25420f-5fd7-4896-a663-db9c7d940e8f" />

<img width="695" height="819" alt="image" src="https://github.com/user-attachments/assets/d517bdbe-e22b-4db0-ac5d-5bcd8e1b6515" />

<img width="975" height="498" alt="image" src="https://github.com/user-attachments/assets/6bd5b1d2-9ba7-4e06-8836-8c92b2a1809b" />

### 16-mask process(cross sectional view)

**1. Selecting the Substrate**

The substrate is the base on which the complete design is fabricated. The most common substrate is a p-type silicon substrate.

**2. Creating the Active Region for Transistors**

<img width="543" height="283" alt="image" src="https://github.com/user-attachments/assets/b982af59-7a86-4f67-ab38-f94188f68807" />

Photolithography.

Remove the mask — resist is chemically removed.

Place in an oxidation furnace — helps grow oxide in other areas (2nd level of oxidation).

<img width="531" height="248" alt="image" src="https://github.com/user-attachments/assets/30ec4c58-4b85-4745-813c-1f2e8afae551" />

Si₃N₄ is stripped using hot phosphoric acid, providing electrical isolation between the two transistors.

<img width="540" height="189" alt="image" src="https://github.com/user-attachments/assets/4bd1de34-9466-4173-ba24-7413c7c4e966" />


**3. N-well and P-well Formation**

The n-well is used for PMOS fabrication, and the p-well is used for NMOS fabrication. Both cannot be done at the same time — one area must be protected while the other is being fabricated.

<img width="817" height="206" alt="image" src="https://github.com/user-attachments/assets/7f0f7a5b-2b4b-4ead-927d-6a6fff531c96" />

-Expose this layer to UV light (reacts with Red layer) then wash to remove mask2

-Boron (p-type material) – Ion implantation for p-well creation

<img width="498" height="222" alt="image" src="https://github.com/user-attachments/assets/e98ac91e-5336-42db-bc71-6197b3914a53" />

<img width="499" height="226" alt="image" src="https://github.com/user-attachments/assets/35716795-6bcc-44c9-98d1-53673d67b0e7" />

-Expose this layer to UV light (reacts with Red layer) then wash to remove mask3

-Ion implantation – ionization process again for n-well creation

-Phosphorous (n-type material)-heavier than Boron

<img width="447" height="250" alt="image" src="https://github.com/user-attachments/assets/86e71d33-b52f-4032-bcce-b9d8bdf41d55" />

-Put it in the drive in furnace – 110 degree C for 4 to 6 hours

Now forms the clear well of p/n-mos

This is Twin well process

<img width="453" height="266" alt="image" src="https://github.com/user-attachments/assets/19c1752b-062e-45da-bf6e-76c9db9f7842" />

**4.	Formation of ‘gate’**

Gate – control of threshold voltage. This defines the turn on voltage of the transistors. Fab of gate is important.

Doping voltage and oxide capacitance are important to be maintained to get the required threshold voltage.

-Again photoresist then mask4 one of the area, then UV rays exposure, then ionization

-boron

<img width="415" height="214" alt="image" src="https://github.com/user-attachments/assets/5af6d847-4eac-4014-9426-ed849187483f" />

-Again photoresist then mask5 one of the area, then UV rays exposure, then ionization

-Phospherous/Arsenic

<img width="478" height="275" alt="image" src="https://github.com/user-attachments/assets/7167c2ac-c2df-4932-bb09-4ff68fe0e8e6" />

<img width="600" height="237" alt="image" src="https://github.com/user-attachments/assets/fc4d1424-6118-40ed-987f-5f514ec7db31" />

Deposit polysilicon layer

Dop with more impurities

<img width="486" height="237" alt="image" src="https://github.com/user-attachments/assets/18bcde34-bc7c-4964-9a1b-c3bf7f4cd51e" />

Then photoresist then mask6 

<img width="744" height="204" alt="image" src="https://github.com/user-attachments/assets/707a0df2-d733-4467-9aa0-10b890120d36" />

then UV rays exposure, then etching

<img width="848" height="152" alt="image" src="https://github.com/user-attachments/assets/393f325e-6e85-444f-84ed-3f88a808b020" />

**5.	Lightly doped drain(LDD) formation**

Formation order: P+, P−, N / N+, N−, P

Reason for the order of formation: Why include P−/N− in between?

Hot Electron Effect – Electric field: E = V/d. High-energy carriers can break Si–Si bonds.

There is a 3.2 eV barrier between the Si conduction band and the SiO₂ conduction band — a general energy gap maintained between the two conduction bands. If a carrier crosses this barrier, it might enter the oxide layer above the substrate and create reliability issues.

Short Channel Effect – As device size reduces, channels become shorter (i.e., a reduction in gate length). This can cause the drain field/voltage to penetrate into the channel area, making it difficult for the gate to control the source and drain current.

Process for the LDD Structure (Considering These Effects):

- Apply photoresist, then mask one of the areas (Mask 5), followed by UV exposure and ionization.

- Phosphorus/Arsenic — used as n-type impurities.

<img width="549" height="325" alt="image" src="https://github.com/user-attachments/assets/ab90f916-6bf2-4a1e-95de-948f5f9649b2" />

- Again photoresist then mask8 one of the area, then UV rays exposure, then ionization
  
- boron

<img width="546" height="301" alt="image" src="https://github.com/user-attachments/assets/0a46556e-d651-40a0-9c8a-743ab5405edd" />

Lightly Doped (LDD)

How to protect this structure: Create side-wall spacers.

Plasma anisotropic etching.

<img width="608" height="252" alt="image" src="https://github.com/user-attachments/assets/8618ba12-20e4-4637-a9a3-de892ea5747b" />

<img width="608" height="248" alt="image" src="https://github.com/user-attachments/assets/399be45d-2525-4224-a886-c7af17aa0dab" />

**6.	Source and drain formation**

- Add Thin Layer of screen oxide – to avoid the effect of channeling (trying to randomize the direction of Ion)
  
  <img width="551" height="235" alt="image" src="https://github.com/user-attachments/assets/c13a4998-4aff-4408-b1c2-733907de1ff1" />

- Again photoresist then mask9 one of the area, then UV rays exposure, then ionization
  
- Ar exposure

<img width="868" height="246" alt="image" src="https://github.com/user-attachments/assets/b32f67fc-a2a6-4ad7-8873-d23291072e9d" />

- Again photoresist then mask10 one of the area, then UV rays exposure, then ionization
  
- boron
  
  <img width="902" height="253" alt="image" src="https://github.com/user-attachments/assets/cc9d303f-9be6-4386-b954-75248135f83f" />

- put then into High temperature furnace – 1000 degree C
n-type will penetrate more into the p-well and p-type will penetrate more into the n-well. This process is called high temp annealing

<img width="810" height="411" alt="image" src="https://github.com/user-attachments/assets/edc20d11-ab38-4fd1-8480-f1ebb2b85b25" />

**7.	Steps to form contacts and interconnects**

- etch/remove the thin oxide in HF solution – open up the contacts
  
  <img width="717" height="270" alt="image" src="https://github.com/user-attachments/assets/c09d6051-47d1-4777-b932-e8dd612b448e" />

- deposit Titanium – Ti has low resistivity. Using sputtering
  
Sputtering – when Ti is exposed to Argon gas, Ti on the surface will get extracted and deposited on the substrate.

<img width="889" height="205" alt="image" src="https://github.com/user-attachments/assets/c57aa51a-af3d-4234-84cf-02dd2d000349" />

- heated at about 650 – 700 degree C in N2  ambient for 60 sec
  
<img width="665" height="295" alt="image" src="https://github.com/user-attachments/assets/3c6b38d8-456e-4fbc-9e3f-b99237d4a81f" />

- Again photoresist then mask11 one of the area, then UV rays exposure
  
- etching TiN using RCA cleaning
  
RCA is a solution – 

de-ionized water 5part,

ammonium hydroxide 1part, 

Hydrogen peroxide 1 part

<img width="1089" height="228" alt="image" src="https://github.com/user-attachments/assets/1d3f116d-5ee7-4c29-be32-d49e8bf714a2" />

**8.	Higher level metal formation**

- depositing thick layer of SiO2 which is Doped with ph/Boron

<img width="584" height="312" alt="image" src="https://github.com/user-attachments/assets/e68511ee-a292-4551-9bca-02ecec278df3" />

- chemical mechanical polishing (CMP) technique
  
- drilling contact holes – photolithography steps - Again photoresist then mask12 one of the area, then UV rays exposure

  <img width="974" height="236" alt="image" src="https://github.com/user-attachments/assets/f19c288f-9bf8-4238-8726-6b36c6735921" />

 **--1st layer of interconnect--**
 
- Add Ti layer – why – TiN -good barrier layer
  
- deposit Blanket tungsten(W) layer 

<img width="550" height="246" alt="image" src="https://github.com/user-attachments/assets/369de153-d647-4dfc-b1a0-7dfbe0b02065" />

- Chemical mechanical poslishing CMP for planarizing wafer surface

<img width="545" height="241" alt="image" src="https://github.com/user-attachments/assets/02cd87a8-d568-49aa-817e-5375f407e78a" />

- Aluminium metal layer deposition
  
- Again photoresist then mask13 one of the area, then UV rays exposure , remove the resist
  
<img width="975" height="236" alt="image" src="https://github.com/user-attachments/assets/d11fe375-c1c6-46b4-9cbc-040a727948f6" />

-mask 14 to drill the contact holes

<img width="1032" height="263" alt="image" src="https://github.com/user-attachments/assets/f9c21e95-de2e-4a91-a572-61f1ba8c615a" />

**--2nd layer of interconnect--**

- TiN layer – act as the barrio b/w metal layers
  
- tungstun W as contacts
  
<img width="688" height="338" alt="image" src="https://github.com/user-attachments/assets/cbcab753-16f1-4f41-a31a-94c1c57b8402" />

**--3rd layer of interconnect—**

- Al layer (thicker thean bottom later increases from bottom to top)
  
- Again photoresist then mask15 one of the area, then UV rays exposure , remove the resist
  
- Si3N4/SiO2 dielectric layer

<img width="974" height="257" alt="image" src="https://github.com/user-attachments/assets/153e8c54-d38d-4176-890e-dd038e6223ef" />

- Mask 16 – to drill the contact holes

  <img width="725" height="437" alt="image" src="https://github.com/user-attachments/assets/398a7865-4179-4796-879f-d0ddeb74c47e" />

  <img width="727" height="584" alt="image" src="https://github.com/user-attachments/assets/552c1799-b30d-4ff3-8e12-b859e0503736" />

**Lab – Magic Tool: Layout of CMOS Inverter**

**Layers:**

Local Interconnect Layer – Local, shown in blue.

Metal 1 – Purple.

Metal 2 – Pink.

N-well – Shown with solid lines.

**Navigation tips:**

Move the mouse anywhere and press S to select, then click on the Tkcon window and type what to know about the highlighted portion.
Place the cursor at the needed location, then press S twice to know about the connection.

LEF File – Library Exchange Format. Contains all metal layers but no logic; it defines where the pins and boundaries are for placing the cell. Commercially, LEF is referred to as the frame view.

Reference: https://github.com/nickson-jose/vsdstdcelldesign

This GitHub link includes step-by-step instructions for creating a CMOS layout.

<img width="606" height="633" alt="image" src="https://github.com/user-attachments/assets/4b85ec28-b10c-4b69-b424-e24ec3f2151e" />

LLX – Lower-left X value.

URX – Upper-right X value.

Understanding and Modifying the .spice File

<img width="613" height="317" alt="image" src="https://github.com/user-attachments/assets/2211ba56-30ab-4070-aba1-72493d92bd05" />

Updated file: 

<img width="975" height="425" alt="image" src="https://github.com/user-attachments/assets/b870e4d1-65cd-4c6a-93ce-43fc7c79862a" />

- Finding transient response:

  <img width="898" height="538" alt="image" src="https://github.com/user-attachments/assets/b0eb9fcf-38b1-4bc4-b534-6e711810af36" />

Characterizing the Cell

**Finding Delays** – If a particular point is selected, its value is printed in the terminal.

Use this layout to create the LEF file.

**LAB EXERCISE: Magic DRS**

https://opencircuitdesign.com/magic/

https://github.com/google/skywater-pdk

https://skywater-pdk.readthedocs.io/en/main/

## DAY 4 Pre-layout timing analysis and importance of good clock tree

**How to Extract the .lef File**

Convert the grid into track information.

<img width="661" height="190" alt="image" src="https://github.com/user-attachments/assets/b1603a9b-f351-44a5-9431-a8d7b7851514" />

Tkcon:
% help grid

**Steps to Convert Magic Layout to Standard Cell LEF**

Requirements to ensure the standard cell layout meets the PnR tool's specifications:

Input and output ports must be located at the intersection of the horizontal and vertical width/routing grid tracks.
The width of the standard cell should be an odd multiple of the X pitch, and similarly for the height.

Set the layer so that ports are declared as pins of the macro in the .lef file:

% lef write

This will update the .lef file with the same name as the Magic file (i.e., sky130a_vsdinv.mag).

<img width="835" height="195" alt="image" src="https://github.com/user-attachments/assets/d22ba666-589a-458e-b233-7843568ffc0f" />

For STA analysis these 4 .lib file are needed/helpful: 

<img width="975" height="145" alt="image" src="https://github.com/user-attachments/assets/0119b304-256e-4b6d-99e3-e1abb55b2753" />

### Power-Aware CTS

**Clock Gating Technique**

Delay tables exist for buffers of different sizes with their corresponding loads. Similarly, there are delay tables for gates.

<img width="821" height="478" alt="image" src="https://github.com/user-attachments/assets/00c46b22-7722-4656-a49e-a99f230e62e2" />

<img width="811" height="418" alt="image" src="https://github.com/user-attachments/assets/9c32785f-5d9c-479b-aa08-c29db8381020" />

<img width="618" height="322" alt="image" src="https://github.com/user-attachments/assets/8b330760-0f70-4bf3-aff9-2eeeb7506c45" />

**Lab**

<img width="820" height="536" alt="image" src="https://github.com/user-attachments/assets/db271e17-46bc-4649-bdb7-52ff7aa14585" />

**Modifications:**

<img width="444" height="413" alt="image" src="https://github.com/user-attachments/assets/1ee45571-b907-4d48-b515-f11d5a8bee57" />

These settings should create a netlist with reduced slack.

**Result:** Yes — slack was reduced from −15 to −3.

**Timing Analysis (With Ideal Clock)**

**Setup Timing Analysis: Single Clock**

Combinational delay should be less than the clock period.

Setup Analysis

Combinational delay should be less than (clock period − setup time).

Setup Time – The time required by the capture flip-flop to settle the information present at its input.

<img width="760" height="458" alt="image" src="https://github.com/user-attachments/assets/8d1da923-e80a-4463-a533-c470dcbb9c53" />

Temperature variation of the clock (jitter) – Setup uncertainty.

<img width="616" height="197" alt="image" src="https://github.com/user-attachments/assets/1b40b697-6e1e-4eaf-9c5b-298bbc597797" />

<img width="975" height="421" alt="image" src="https://github.com/user-attachments/assets/8431ef8d-95f6-4f2c-9be5-b84fdd15dada" />



