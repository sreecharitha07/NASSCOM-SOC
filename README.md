# ***DIGITAL VLSI SOC DESIGN AND PLANNING***

# **Contents**

1. [Introduction](#introduction)
   - [OpenLane](#openlane)
   - [Installation](#installation)

2. [Day 1 - Inception of Open-Source EDA, OpenLane and SKY130 PDK](#day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
   - [Theory](#day-1-theory)
   - [Lab Tasks](#day-1-lab-tasks)

3. [Day 2 - Good Floorplan vs Bad Floorplan and Introduction to Library Cells](#day-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
   - [Theory](#day-2-theory)
   - [Lab Tasks](#day-2-lab-tasks)

4. [Day 3 - DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION](#4-day-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

5. [Day 4 - PRE-LAYOUT TIMING ANALYSIS AND IMPORTANCE OF GOOD CLOCK TREE](#5-day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

6. [Day 5 - FINAL STEPS FOR RTL2GDS USING TRITONROUTE AND OPENSTA](#6-day-5---final-steps-for-rtl2gds-using-tritonroute-and-opensta)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

----------------------------------------------------------------------------------------------------------------------------

## 1. INTRODUCTION
### OPEN LANE

OpenLane is an ASIC infrastructure library based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, KLayout and a number of custom scripts for design exploration and optimization.

For this project, we will be utilizing the OpenLane open-source physical design flow in conjunction with the Skywater 130nm PDK. These tools will be used throughout the entire design and implementation process

### INSTALLATION

By installing Ubuntu through Oracle VM VirtualBox, a virtual Linux environment was created. This setup provides isolation and consistency for development and testing. The entire project will be carried out within this Ubuntu environment.

Below is the screenshot showing the system specifications of the Ubuntu virtual machine set up using Oracle VM VirtualBox.
![image](https://github.com/user-attachments/assets/47777613-abee-4fda-9080-caf427e9eadd)

### COMMONLY USED COMMANDS

**To invoke the docker.**
 1. Go to the below directory: `~/Desktop/work/tools/openlane_working_dir/openlane/`
 2. Enter `docker`
 3. Enter `./flow.tcl -interactive`
 4. Enter `package require openlane 0.9`
 5. For the design if you want to run all the process from the start use `prep -design picorv32a`. If you want to over write your design use `prep -design picorv32a -tag "our runs folder name" -overwrite`
 6. You can access the folder from the below directory:
    Directory: `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/`
    Use `le -ltr` to list the files
    Eg: if your folder name in the runs directory is 13-05_16-48 use `prep -design picorv32a -tag "13-05_16-48" -overwrite`

**Magic tool directories**
1. Floorplan
   `magic -T/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &`

2. Placement
`magic -T/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`


   


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2. DAY 1 - INCEPTION OF OPEN-SOURCE EDA, OPENLANE AND SKY130 PDK

### THEORY
[📄 Day-1.pdf](Day-1.pdf)

### LAB TASKS

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

----------------------------------------------------------------------------------------------------------------------------------------------------------------

## **3. DAY 2 - GOOD FLOORPLAN VS BAD FLOORPLAN AND INTRODUCTION TO LIBRARY CELLS**

### THEORY
[📄 Day-1.pdf](Day-1.pdf)

### LAB TASKS

## FLOOR PLANNING

### Task - 1: To Characterize the Floor planning files

**The steps for the floor planning are as follows**:

Step 1: You can see the README file in the configurations folder in which the switches definations and defaults are set to.
 
 Directory: `~/Desktop/work/tools/openlane_working_dir/openlane/configuration`
 
 use `less README.md` to open the file or `vim README.md`.
 
 <img width="592" alt="image" src="https://github.com/user-attachments/assets/eb970830-e9b5-413a-883a-b8e3f36d5f8a" />


Step 2: The order of precedence of the files needed for floorplan are as follows this order determines the floorplan data. The values of the switches and pins with highest precedence are over written and are stored. (highest to lowest)

   P1. sky130A_sky130_fd_sc_hd_config.tcl          
   
   Directory: `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a`
   
   <img width="672" alt="image" src="https://github.com/user-attachments/assets/b4510b3b-412c-4b2c-b047-38aacb562d2c" />

   
   P2. config.tcl                                   
   
   Directory: `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a`
   
   ![image](https://github.com/user-attachments/assets/6605b91f-54cb-4fb5-b231-e1b7f94b870a)

   
   P3. floorplan.tcl                                
   
   Directory: `~/Desktop/work/tools/openlane_working_dir/openlane/configuration`
   
  <img width="617" alt="image" src="https://github.com/user-attachments/assets/20db777a-79cd-4b23-a374-a69f83703897" />


Step 3: Now we run the command `run_floorplan` in the openlane window. Either overwrite it or run the synthesis again followed by floorplan

<img width="602" alt="image" src="https://github.com/user-attachments/assets/15a6d471-cd67-470f-9db1-034cb3c8f10a" />

<img width="391" alt="image" src="https://github.com/user-attachments/assets/16ab74f1-26b1-423f-873b-60df35be7aef" />

### **Task - 2: To find the Cordinates and area of the die**

Step 1: To find the dimensions of the die we have to locate floorplan def file which gives us the orientations and locations
directory: 

<img width="602" alt="image" src="https://github.com/user-attachments/assets/24dc53dc-602d-4d06-a08c-eeb076aea2ea" />

floorplan def file

<img width="598" alt="image" src="https://github.com/user-attachments/assets/2138ccc3-6c97-48ce-ba44-f6d0b88418e1" />

Step 2: To calculate the dimensions we have:
   1. Units distance microns-> 1000
   2. Die area coordinates representation: (0 0) ->(lower left x value, lower left y value) , (660685,671405) -> (upper right x value, upper right y value)

    `X = upper right x value/Units distance microns , Y = upper right y value/Units distance microns)`
    `X= 660685/1000 , Y = 671405/1000`
    `X = 660.685 , Y = 671.405`

Step 3: To calculate the area of the die.
   `Die Area = X * Y `
   `Die Area = 443587.212425`


### Task - 3: To verify the horizontal and vertical paths in Magic

Step 1: Open magic tool in the below directory and enter the below flow

   Directory: `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-05_16-48/results/floorplan`
   
   Flow : `magic -T/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &`
   
   <img width="490" alt="image" src="https://github.com/user-attachments/assets/b49784fc-9ce4-49ff-9564-a0df254f7b03" />

Step 2: Layout will be opened with the tkcon window(gives us the information about everything in the layout)
  1. To zoom in the layout use 'Z'
  2. To zoom out use 'Shift+Z'
  3. To select anything on the layout use 'left press and right press in the mouse'.
  4. A what command in the tckon window is used to give information of the selected component

Step 3: Vertical and horizontal I/O pins are as fllows:

   <img width="389" alt="image" src="https://github.com/user-attachments/assets/65ab9362-44bd-4fa6-bb5d-36e3060d8a45" />

   <img width="523" alt="image" src="https://github.com/user-attachments/assets/5c34891a-334b-411d-b5af-3c0ef1521fce" />


## PLACEMENT

Step 1: Run the command `run_placement` in the docker window after the floorplan

<img width="533" alt="image" src="https://github.com/user-attachments/assets/9d7a59f1-f873-4954-a74f-815dbc279a39" />

Step 2: We can see the .def file is created in the placement directory

<img width="529" alt="image" src="https://github.com/user-attachments/assets/bba50466-f550-4002-9265-508bdedc9062" />

Step 3: Invoke the magic tool by entering the below directory in the placement folder inside the result folder

`magic -T/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

<img width="425" alt="image" src="https://github.com/user-attachments/assets/51e8886c-029e-4a03-978c-109cd7d796b8" />

The Zoomedin Version gives us the idea about how the standard cells are placed in rows and all the decap , tap cells , I/O pins are all ensured right by floorplan and placement.

<img width="424" alt="image" src="https://github.com/user-attachments/assets/e8157677-e678-4713-8796-2c143d002e91" />

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Day 3 - DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION

### THEORY
[📄 Day-1.pdf](Day-1.pdf)

### LAB TASKS

### Task - 1: To make use of Custom Inverter into our design.

**The Steps to clone the custom Inverter are:**

Step 1: Go to the github clone link `https://github.com/nickson-jose/vsdstdcelldesign.git`

Step 2: Enter this link in the openlane directory as follows and vsdscelldesign has the custom inverter layout

![image](https://github.com/user-attachments/assets/57f9c3bb-c972-45f6-aa60-a13da2f9283d)

Step 3: We need sky130A tech file in the vsdscelldesign folder so we copy it.

![image](https://github.com/user-attachments/assets/7f28aaa0-6692-4cd2-879d-737f38a67e03)

The copied file in the vsdscelldesign folder

![image](https://github.com/user-attachments/assets/7c58661a-d64c-4f63-aa51-854bf01e4b52)

Step 3: Generate the layout of the inverter. Open magic in vsdscelldesign folder 

![image](https://github.com/user-attachments/assets/53f0cead-0ae1-44a9-ac28-c5b93383c33d)

  Layout

![image](https://github.com/user-attachments/assets/e6d432d1-67a3-4182-bac5-6cf608d8140b)

  To know about any component use the tkcon window and the command `what` by selecting that particular component in the layout as seen below:

![image](https://github.com/user-attachments/assets/c1c6e552-c76a-4d0c-96e7-1d27c85474de)

  To see if a component is connected clicl 'S' thrice.

![image](https://github.com/user-attachments/assets/20614f1e-9565-44f8-9cf4-02e737b32ef2)


### Task - 2: To extract the spice netlist.

**The Steps to extract spice netlist are:**

Step 1: Enter the command `extract all` in the tckon window of the inverter layout.

![image](https://github.com/user-attachments/assets/7b71f457-7661-4571-93a2-4b003791c0c3)

We can see the extracted inv file in the vsdstdcell design folder

![image](https://github.com/user-attachments/assets/ac31c6ce-730b-4780-8d81-3f722c542f27)

Step 2: Enter the command `ext2spice cthresh 0 rthresh 0` to convert the extracted filee to spice netlist.We can also see the spice in the folder

![image](https://github.com/user-attachments/assets/eb9ad189-9b81-421d-89f1-f3ce025f1e65)

Step 3: Open the spice netlist using vim to edit

Before change

![image](https://github.com/user-attachments/assets/db8300bd-0380-433a-b500-e8f0a75962af)

 1. To include the .lib files of nmos and pmos in the spice netlist.

![image](https://github.com/user-attachments/assets/a53b20e3-6490-440f-b231-7ca103017739)

2. To make sure we have correct dimensions of the grid , we run a transient analysis and the values VDD , VSS , Va(Input) is given
   
   The Inv Model
   <img width="448" alt="image" src="https://github.com/user-attachments/assets/9b37e0bb-7455-4c49-af3a-ed13457abb67" />
   
   After all the changes we have the below spice netlist.
   
   ![image](https://github.com/user-attachments/assets/6e4b5e4b-0abb-46d5-bac7-568663b5338e)


### Task - 3: Ngspice Simulation and characterization of inverter.

**Steps to generate the ngspice simulation to calculate the delays:**

Step 1: Enter the command `ngspice sky130_inv.spice` to run the ngspice simulation

![image](https://github.com/user-attachments/assets/02c3e537-0bf3-41f9-be88-fdcb67a0d6df)

Step 2: Plot the graph using command `plot y vs time a` -> plot output vs time input.

![image](https://github.com/user-attachments/assets/dfd7af44-c46f-4746-b866-ba808d156659)

![image](https://github.com/user-attachments/assets/718bc093-5e65-4b82-bf54-5b8beba2f2b0)

Step 3: For characterization we need 4 parameters rise transition , fall transition , rise cell delay and fall cell delay. 
        `20 % of 3.3 = 0.66 , 80% of 3.3 = 2.64 , 50% of 3.3 = 1.65`

  1. Rise transition(Rise from 20% to 80%)
     






   




























        

        

        













