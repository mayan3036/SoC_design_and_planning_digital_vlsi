# SoC Design and Planning

## Day 1: Synthesis for PicoRV32A Design

<details>
  <summary><strong>Day 1 Theory</strong></summary>

### Introduction
This project demonstrates the process of designing an ASIC using the **OpenLane** flow, focusing on the synthesis of the **PicoRV32A** design and the calculation of the **Flop Ratio**. The flow follows the **RTL-to-GDSII** process, utilizing open-source tools and libraries to complete the design and verification.

---

### QFN-48 Package

A **QFN-48 (Quad Flat No-Lead)** package is a surface-mount integrated circuit package with 48 leads or pads. It is compact and thermally efficient, ideal for high-performance applications requiring a small form factor.

---

### Package, Pads, Die, Core, and Chip

- **Package**: The physical housing of an integrated circuit, protecting the chip and providing connectivity to external circuits.
- **Pads**: Metal terminals on the die's edges used for electrical connections to the package or external circuit.
- **Die**: The silicon wafer piece containing the integrated circuit (IC).
- **Core**: The central functional part of the die, such as the CPU or processing unit.
- **Chip**: The complete semiconductor device, including the die and the package.

### Relation:
The **package** houses the **die**, which contains the **core**. The **pads** on the edges of the die enable electrical connections between the die and the package or external circuit.

---

### Foundry IPs and Macros

**Foundry IPs** are pre-designed blocks provided by semiconductor foundries:
- **PLL**: Phase-Locked Loop for clock generation and synchronization.
- **ADC**: Analog-to-Digital Converter for signal conversion.
- **SRAM**: Static Random-Access Memory for fast, volatile storage.
- **DAC**: Digital-to-Analog Converter for signal conversion.

**Macros** are high-level, pre-designed components used in chip design:
- **RISC-V SoC**: A system-on-chip based on the RISC-V instruction set architecture.
- **SPT**: Single Processing Thread, referring to specialized processing architectures.

---

### RISC-V ISA

**RISC-V** is an open-standard Instruction Set Architecture (ISA) based on the principles of reduced instruction set computing. It’s designed to be simple, extensible, and open, providing an excellent foundation for building custom processors and microcontrollers.

---

### ASIC Design Flow: RTL to GDSII

![](./images/GENERAL_ASIC_FLOW.png)

1. **Synthesis**:  
   - Converts RTL (written in HDL) into a circuit using components from the standard cell library.  
   - **Standard Cells**:  
     - Have a regular layout.  
     - Each cell comes with different models/views:  
       - **Functional Model**: Describes cell behavior.  
       - **Timing Model**: Captures timing constraints and delays.  
       - **Power Model**: Details power consumption.  
       - **Physical Layout**: Describes the geometrical arrangement for placement and routing.

2. **Floor/Power Planning**:  
   - **Chip Floor Planning**: Divides the chip die among different system building blocks.  
   - **Macro Floor Planning**: Specifies dimensions, pin locations, row definitions, and routing tracks.  
   - **Power Planning**: Constructs a power network to deliver power effectively across the design.

3. **Placement**:  
   - Places standard cells on the floor plan rows aligned with wiring.  
   - Includes:  
     - **Global Placement**: Finds optimal positions for all cells, allowing overlaps and potential illegal placements.  
     - **Detailed Placement**: Adjusts the global placement minimally to ensure legality (e.g., no overlaps).  

4. **Clock Tree Synthesis (CTS)**:  
   - Distributes the clock signal to all sequential elements with minimal skew and in a balanced shape.  
   - Common structures include **H-tree** and **X-tree** architectures.

5. **Routing**:  
   - Implements interconnects using available metal layers to connect cells.  
   - **SkyWater 130nm PDK Example**:  
     - Defines 6 routing layers, the lowest is made of **titanium**, and the rest are **aluminum**.  
     - Metal tracks form a large routing grid; the **divide-and-conquer** approach is used to manage complexity.

6. **Sign-Off**:  
   - Ensures the design is fabrication-ready and meets specifications.  
   - Includes:  
     - **Physical Verification**: Checks physical integrity and correctness.  
     - **DRC (Design Rule Checks)**: Verifies compliance with process design rules.  
     - **LVS (Layout vs. Schematic Check)**: Ensures the physical layout matches the schematic.  
     - **Static Timing Verification**: Confirms timing constraints are met.


### ASIC Design Flow: RTL to GDSII

![](./images/OPENLANE_ASIC_FLOW.png)

</details>

---

<details>
  <summary><strong>Day 1 Labs</strong></summary>

### Task: Synthesis for PicoRV32A Design
- Perform synthesis for the **PicoRV32A** design.  
- From the synthesis output, calculate the **Flop Ratio**, which is defined as:  

    **Flop Ratio** = (Number of D Flip-Flops) / (Total Number of Cells)


---

### Lab Process Steps

1. **Initial State of Terminal**  
![](./images/1.PNG)
   In this image, we see the initial state of the terminal where we will access the **OpenLane** directory and begin the process.

2. **Entering the OpenLane Directory** 
![](./images/2.PNG) 
   Here, we have navigated to the **OpenLane** directory, where we will start working with the design flow.

3. **Invoking OpenLane Flow with Docker**  
![](./images/3.PNG)
   At this step, we invoke the **OpenLane** flow using the **Docker** command to set up the required environment for synthesis.

4. **Dealing with the `flow.tcl` File in Interactive Mode**  
![](./images/4.PNG)
   Inside the OpenLane flow, we work with the **flow.tcl** file to process the design in **interactive mode**. Here, we also bring in the necessary packages to ensure proper functionality.

5. **Preparing the Initial Design from PicoRV32A Directory**  
![](./images/5.PNG)
   In this image, we prep the initial design by navigating to the **PicoRV32A** design directory, where we will work on synthesis.

6. **Preparation Complete, Running `run_synthesis` Command** 
![](./images/6.PNG) 
   Here, the preparation is complete, and we run the **`run_synthesis`** command to initiate the synthesis step.

7. **Synthesis Complete, Analyzing Results**  
![](./images/7.PNG) 
   The synthesis step has completed, and we are now ready to examine the results, including calculating the **flop ratio**.

8. **Total Number of Cells: 14,876** 
![](./images/8.PNG)  
   The total number of cells in the design is **14,876**.

9. **Total Number of D Flip-Flops: 1,613**  
![](./images/9.PNG) 
   The total number of D Flip-Flops in the design is **1,613**.

10. **Viewing Flop Ratio Statistics**  
![](./images/10.PNG) 
![](./images/11.PNG) 
![](./images/12.PNG) 

11.  **Flop Ratio Calculation**  
    Now, we calculate the **flop ratio** using the formula:  
    Flop Ratio = (Number of D Flip-Flops) / (Total Number of Cells)  
    Substituting the values:  
    Flop Ratio = 1613 / 14876 ≈ **0.1088**  
    Next, to find the **percentage of D Flip-Flops**, we multiply the result by 100:  
    Percentage of D Flip-Flops = 0.1088 × 100 = **10.88%**
---
</details>

## Day 2: Floorplanning, Placement, and Library Cells

<details>
  <summary><strong>Day 2 Theory</strong></summary>

### Floorplanning

**Floorplanning** is the step in the physical design process where the layout of the chip is determined, including the dimensions, placement of macros, standard cells, and power planning. It sets the foundation for efficient placement and routing.

#### Steps of Floorplanning

1. **Define Width and Height of Core and Die:**
   - Establish the dimensions of the core and die to accommodate all components.

2. **Define Locations of Pre-Placed Cells:**
   - Place large macros and cells that are fixed due to design constraints.

3. **Use of Decoupling Capacitors:**
   - Place decap cells to manage voltage fluctuations.

4. **Power Planning:**
   - Create a grid of **VDD** and **VSS** lines to ensure proper power delivery.

5. **Pin Placement:**
   - Position input/output pins for efficient routing.

6. **Logical Cell Placement Blockage:**
   - Define areas where standard cells should not be placed to avoid congestion.

---

### Placement and Routing

**Placement** involves assigning precise physical locations to standard cells within the core area, while **routing** connects these cells using metal layers. The placement process ensures optimal performance and minimal congestion.

#### Steps of Placement and Routing

1. **Bind Netlist with Physical Cells:**
   - Map logical design components to physical cells in the library.

2. **Placement:**
   - Perform global and detailed placement to ensure optimal positions.

3. **Optimized Placement:**
   - Refine cell locations to enhance performance and reduce routing complexity.

---

### Standard Cells, Cell Design Flow, and Need for Characterization

During each step of physical design, standard cells like gates, buffers, inverters, and flip-flops are commonly used. A collection of these cells forms the **library**, which is essential for EDA tools to interpret and implement the design. Libraries include cells of varying sizes, functionalities, and threshold voltages.

#### Cell Design Flow

Each standard cell is created using a defined process:

1. **Input:**
   - **PDKs:** Process Design Kits containing DRC and LVS rules, SPICE models.
   - **Library Specifications:** User-defined constraints and functionality.

2. **Design Steps:**
   - **Circuit Design:** Define the electrical behavior.
   - **Layout Design:** Create the physical representation.
   - **Characterization:** Evaluate timing, noise, and power.

3. **Output:**
   - **Circuit Description Language (CDL):** Output of circuit design.
   - **GDSII, LEF, Extracted SPICE Netlist:** Outputs of layout design.
   - **Timing, Noise, Power .LIBs:** Outputs of characterization.

#### Characterization Flow

Characterization evaluates the performance of cells in terms of **timing**, **power**, and **noise**. This step often uses tools like **GUNA** to generate accurate metrics for library cells.

</details>

---

<details>
  <summary><strong>Day 2 Labs</strong></summary>

### Task

1. Running floorplanning step for **PicoRV32A**.
2. Accessing the die size and calculating its area.
3. Using Magic tool to view and explore the floorplan.
4. Running placement step for **PicoRV32A**.
5. Using Magic tool to view and explore the placement.

---

### Lab Process Steps

1. **Run the `run_floorplan` Command**
   - This step is performed after running the `run_synthesis` command (refer to Day 1 Lab).

   ![](./images/13.PNG)
   ![](./images/14.PNG)
   ![](./images/15.PNG)

2. **Access the `picorv32a.floorplan.def` File**
   - Navigate to the relevant directory as shown below.

   ![](./images/16.PNG)

3. **Calculate Die Area**
   ![](./images/17.PNG) 
   - Inside the `.def` file, note the die dimensions:
     - **Die Width = 660685 units**
     - **Die Height = 671405 units**
   - Using the formula:
     
     \[
     \text{Die Area (in units)} = \text{Die Width} \times \text{Die Height}
     \]
     
     Convert to microns:
     \[
     \text{Die Area (in microns)} = \frac{\text{Die Area (in units)}}{10^6}
     \]

   - Die Area = **443.555 mm²**.

4. **Use Magic Tool for Floorplan Visualization**
   - Command to open Magic for graphical exploration.

   ![](./images/18.PNG)

5. **Floorplan Results**
   - **Floorplan DEF in Magic:**
     ![](./images/19.PNG)
   - **Port Layers:**
     ![](./images/21.PNG)
     ![](./images/22.PNG)
   - **Equidistant Ports:**
     ![](./images/20.PNG)
   - **Decap Cells and Tap Cells:**
     ![](./images/23.PNG)
   - **Unplaced Standard Cells:**
     ![](./images/24.PNG)

6. **Run the `run_placement` Command**
   - Command to perform placement step.

   ![](./images/25.PNG)
   ![](./images/26.PNG)
   ![](./images/27.5.PNG)

7. **Use Magic Tool for Placement Visualization**
   - Open Magic to view placement results graphically.

   ![](./images/27.PNG)

8. **Placement Results**
   - **Placement Results in Magic:**
     ![](./images/28.PNG)
     ![](./images/29.PNG)

</details>
