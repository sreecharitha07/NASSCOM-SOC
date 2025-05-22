# ***DIGITAL VLSI SOC DESIGN AND PLANNING***

# **Contents**
1. [Introduction](#introduction)
   - [OpenLane](#openlane)
   - [Installation](#installation)
     
2. [Day 1 - Inception of Open-Source EDA, OpenLANE and SKY130 PDK](#2-day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)
  
3. [Day 2 - GOOD FLOORPLAN VS BAD FLOORPLAN AND INTRODUCTION TO LIBRARY CELLS](#2-day-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)
  
4. [Day 3 - DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION](#3-day-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

5. [Day 4 - PRE-LAYOUT TIMING ANALYSIS AND IMPORTANCE OF GOOD CLOCK TREE](#4-day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

6. [Day 5 - FINAL STEPS FOR RTL2GDS USING TRITONROUTE AND OPENSTA](#5-day-5---final-steps-for-rtl2gds-using-tritonroute-and-opensta)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

----------------------------------------------------------------------------------------------------------------------------

## **1. INTRODUCTION**
### **OPEN LANE**

OpenLane is an ASIC infrastructure library based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, KLayout and a number of custom scripts for design exploration and optimization.

For this project, we will be utilizing the OpenLane open-source physical design flow in conjunction with the Skywater 130nm PDK. These tools will be used throughout the entire design and implementation process

### **INSTALLATION**

By installing Ubuntu through Oracle VM VirtualBox, a virtual Linux environment was created. This setup provides isolation and consistency for development and testing. The entire project will be carried out within this Ubuntu environment.

Below is the screenshot showing the system specifications of the Ubuntu virtual machine set up using Oracle VM VirtualBox.
![image](https://github.com/user-attachments/assets/47777613-abee-4fda-9080-caf427e9eadd)


## **2. DAY 1 - INCEPTION OF OPEN-SOURCE EDA, OPENLANE AND SKY130 PDK**

### **THEORY**
[📄 Day-1.pdf](Day-1.pdf)

### **LAB TASKS**

### Task-1 : To find the flop ratio

        The flop ratio = No. of D flip flops/No. of cells

**The steps for the synthesis which helps us to find the flop ratio is as follows**:

Step 1: Open the openLane directory
<img width="960" alt="image" src="https://github.com/user-attachments/assets/a602e752-3671-4e50-bde4-59ac65aee88b" />

Step 2 : use **"docker"** command which is used to run the OpenLane toolchain inside a Docker container, which provides a pre-configured environment with all dependencies, tools (like Yosys, Magic, KLayout, OpenROAD, etc.), and paths correctly set up.
`docker`

Step 3: **"./flow.tcl -interactive"** command is used to launch OpenLane in interactive mode inside the Docker container.
`./flow.tcl -interactive`
<img width="960" alt="image" src="https://github.com/user-attachments/assets/f6c1e9c2-b933-4341-9442-c168d2f8b8b1" />

Step 4: Enter command **"package require openlane 0.9"** it load the openLane package of version 0.9.
`package require openlane 0.9`

Step 5: Enter the command **"prep -design picorv32a"** is used in OpenLane's interactive mode to prepare the design environment for the flow. This step mereges the .lef files 
`prep -design picorv32a`
        
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d9eae49b-ccb1-4c1b-acf7-21ee202a8dd2" /><br>  
        We can see the merged lef file in the directory shown in below image and .lef can be accessed by the command less merged.lef in the terminal
<img width="960" alt="image" src="https://github.com/user-attachments/assets/3073b8a0-70e4-4d95-9470-6fcedc6fba0e" />

Step 6: Enter the command **"run_synthesis"** to start the synthesis of the design and the below is tha image of successful synthesis.
`run_synthesis`

<img width="960" alt="image" src="https://github.com/user-attachments/assets/00b999a0-6cdd-40ac-9c1a-1d4fc48b3ded" /> <br>                  
        We can see the synthesized verilog file in the below directory,the verilog file contains the logic of our design.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/b36def51-dcee-4e71-b0bf-57c63eedc96b" />

Step 7: We can also see the chip area of picorv32 module
<img width="960" alt="image" src="https://github.com/user-attachments/assets/be542d2c-8217-48ee-bdf4-707170c893d6" />

Step 8: To calculate the Flop Ratio       
         The Number of D FF:
        <img width="960" alt="image" src="https://github.com/user-attachments/assets/39b858f3-ecd2-47e4-902e-ed42e32cc1a7" />       
        The number of cells:
        <img width="960" alt="image" src="https://github.com/user-attachments/assets/8b39cd87-4223-465b-98fc-a24db07f10ab" />  
        **RESULTS:**
        
        Flop ratio: 1613/14876 = 0.108429 
        Flop Percentage : 0.108429*100 = 10.84%



## **3. DAY 2 - GOOD FLOORPLAN VS BAD FLOORPLAN AND INTRODUCTION TO LIBRARY CELLS**

### **THEORY**
[📄 Day-1.pdf](Day-1.pdf)

### **LAB TASKS**
        

        

        













