# ***DIGITAL VLSI SOC DESIGN AND PLANNING***

# **Contents**

1. [Introduction](#1-introduction)
   - [OpenLane](#open-lane)
   - [Installation](#installation)
   - [Commonly used Commands](#commonly-used-commands)

2. [Day 1 - Inception of Open-Source EDA, OpenLane and SKY130 PDK](#2-day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
   - [Theory](#theory)
   - [Lab Tasks](#lab-tasks)

3. [Day 2 - Good Floorplan vs Bad Floorplan and Introduction to Library Cells](#3-day-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
   - [Theory](#theory-1)
   - [Lab Tasks](#lab-tasks-1)

4. [Day 3 - DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION](#4-day-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
   - [Theory](#theory-2)
   - [Lab Tasks](#lab-tasks-2)

5. [Day 4 - PRE-LAYOUT TIMING ANALYSIS AND IMPORTANCE OF GOOD CLOCK TREE](#5-day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
   - [Theory](#theory-3)
   - [Lab Tasks](#lab-tasks-3)

6. [Day 5 - FINAL STEPS FOR RTL2GDS USING TRITONROUTE AND OPENSTA](#6-day-5---final-steps-for-rtl2gds-using-tritonroute-and-opensta)
   - [Theory](#theory-4)
   - [Lab Tasks](#lab-tasks-4)

7. [References](#7-references)
8. [Acknowledgement](#8-acknowledgement)

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

## 3. DAY 2 - GOOD FLOORPLAN VS BAD FLOORPLAN AND INTRODUCTION TO LIBRARY CELLS

### THEORY
[📄 Day-2.pdf](Day-2.pdf)

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

## 4. Day 3 - DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION

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

Step 3: For characterization we need 4 parameters rise transition , fall transition , rise cell delay and fall cell delay. We take the height of the graph from 0V to 3.3V

        `20 % of 3.3 = 0.66 , 80% of 3.3 = 2.64 , 50% of 3.3 = 1.65`

  1. Rise transition(Rise from 20% to 80%)

     Rise At 20%

     ![image](https://github.com/user-attachments/assets/c6667217-bc25-4cec-8da8-030235048983)

     Rise At 80%

     ![image](https://github.com/user-attachments/assets/ff7f43db-498e-455a-954d-2ffd43a62bc6)

     `X0 = The difference between the Rise transition at 20% and 80% of x0 values`
     
     `X0 = 2.24655-2.1824`
     
     `X0=0.064ns`
     
     ![image](https://github.com/user-attachments/assets/0c9d4302-9494-449c-bc1f-c0b791b92d2d)

3. Fall transition(Fall from 80% to 20%)

   Fall at 80%

   ![image](https://github.com/user-attachments/assets/b09e618d-f025-4a63-801a-fda1d45263c6)

   Fall at 20%

   ![image](https://github.com/user-attachments/assets/7b4cbf10-59b0-4e37-94a7-94aec950ce08)

     `X0 = The difference between the Fall transition at 20% and 80% of x0 values`
   
     `X0 = 4.0964-4.0531`
   
     `X0 = 0.0433ns `
   
   ![image](https://github.com/user-attachments/assets/79980371-fbc1-4e34-bbc2-e57b8e8926ec)

5. Rise delay(Rise at 50% of the output)

   ![image](https://github.com/user-attachments/assets/870cd1f7-6dcd-4278-a7de-272c2a21778b)

    `X0 = The difference between the Rise of Input and output at 50% of x0 values`
   
     `X0 = 2.211-2.15`
   
     `X0 = 0.062ns `

7. Fall delay(Fall at 50% of the output)

![image](https://github.com/user-attachments/assets/bb36db75-3f95-40a9-8e73-4b547e4bd6ab)


    `X0 = The difference between the Fall of Input and output at 50% of x0 values`
    
     `X0 = 4.077-4.050`
     
     `X0 = 0.027ns `

### Task - 4: To work on Met3 mag file in magic from drc_test folder .

Step 1: After the characterization of the inverter load the wget again to open the magicrc file to locate where the .tech file. We download the lab files from the below directory copy this in the command window as seen below
Lab files: `wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz`

Commad to extract the drc_tests `tar xfz drc_tests.tgz`.
Go to the directory `cd drc_tests.tgz.1`

![image](https://github.com/user-attachments/assets/fe1374af-9115-4589-9afc-f8aa8cf2bab3)

We can observe that Metal layers drawn for the layout in the drc_test folder

![image](https://github.com/user-attachments/assets/5ebe168c-0f83-4cb7-9563-66a76800c656)

Open magic rc in the drc_test folder using the command `vi .magicrc`

![image](https://github.com/user-attachments/assets/2f75730b-0628-4bdd-ae85-7fce01218505)

Inside the magicrc file, We see the Sky130A tech file

![image](https://github.com/user-attachments/assets/d02a9572-8fff-4e96-a76c-ad07653707be)


Step 2: Open Magic in the drc_test folder using the command `magic -d XR`

![image](https://github.com/user-attachments/assets/5b34fafa-c30e-4eb0-ab28-f022a750f290)

Step 3: Load the met3.mag file in layout from File(left corener)->open-> choose met3.mag file.

![image](https://github.com/user-attachments/assets/f7244884-3f26-41a3-93b3-fc21a5dff3b4)

In tckon window `drc why` after selecting a component gives you about the drc information of that component

![image](https://github.com/user-attachments/assets/dfe7dc2b-3010-4a0f-b3c8-223223e017fe)

Step 4: We create a component to check the layers and its properties on how they work and what they are. To create a component use your mouse left press and right press to make a box like structure

We fill the box with metal 3 contact layer using the command `paint m3contact` to paint and crate the cuts.
Command `cif see VIA2` is used visualize a specific layer here VIA2 is a derived layer that is filled with contact cuts

![image](https://github.com/user-attachments/assets/20c54b4d-60d3-4b0a-b288-0a5334a8a7b1)

To know the dimensions of a component select that compoment and use command `box`

![image](https://github.com/user-attachments/assets/dcc90a43-d778-430b-bee0-6acb4fa88eaa)

To clear feed use command `feed clear`

![image](https://github.com/user-attachments/assets/aa767d5a-c8e4-4590-b7dc-09ab071a4513)


### Task - 5: To fix the poly.9 eroor in sky130 tech file .

Step 1: Look into the poly.9 error from the guide `https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html`

![image](https://github.com/user-attachments/assets/42034734-09ec-463f-9c29-2e2f873e99ac)

Step 2: load the ploly from the tckon window using `load poly` command

![image](https://github.com/user-attachments/assets/ac339bd3-1e52-4046-ab4f-88f9c82a8579)

After loading poly we have

![image](https://github.com/user-attachments/assets/fc8e72b2-1078-4dab-bf04-2b80a7ab909d)

Step 3: Identifying the poly.9 error. The spacing should be min of 0.480 with no overlap or to different tap.

Incorrect component with poly.9 error

![image](https://github.com/user-attachments/assets/a9ddee33-ac1a-4efd-a518-b4805d8b6838)

We see it clearly violates the 0.480 spacing error from below after checking the spaceing between the two.

![image](https://github.com/user-attachments/assets/e57de293-3a81-4230-b9f7-af85b548c2a6)

Step 4: Fixing the poly.9 error. Go to the drc_tests directory and open the sky130A.tech file in edit mode

![image](https://github.com/user-attachments/assets/1deea9b9-b241-45b8-a531-2e13477105d2)

search `:/poly.9` to loacte to the error in sky130A file and to make changes use `i` - insert to edit

![image](https://github.com/user-attachments/assets/f2e71957-353f-40db-b7fa-04780d15e188)

After adding new line for fixing the drc error we have the below

![image](https://github.com/user-attachments/assets/e4796530-c9aa-4dc6-997b-382b68982139)

Step 5: AFter fixing the error check again in the tckon window invoke using the magic command mentioned above 
Command to run in tckon window 
`tech load sky130.tech` -> load the tech file

`drc check` -> Run the drc to check the updated spacking

`drc why` -> Gives you the information about drc

`box` -> gives you the dimensions of the selected component

<img width="448" alt="image" src="https://github.com/user-attachments/assets/e80b29f0-e25f-4acb-a77a-fc7ccb2d994f" />

Laod metal contact file to magic and check if it still has violations.

![image](https://github.com/user-attachments/assets/a6bf4051-b95c-4af2-a3d8-6b2ca33b8dec)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 5. Day 4 - PRE-LAYOUT TIMING ANALYSIS AND IMPORTANCE OF GOOD CLOCK TREE

### THEORY
[📄 Day-1.pdf](Day-1.pdf)

### LAB TASKS

### Task - 1: Convert grid to track info and to ensure if the layout follows the guidelines of pnr rules while making a standard cell.

**The Steps and guidelines are as follows:**
Step 1: Open tracks information is in the below directory
     ![image](https://github.com/user-attachments/assets/b1c3352f-1cee-4898-87b4-8f2949f39b9c)

   Inside tracks.info file
     
   ![image](https://github.com/user-attachments/assets/cf6791be-2b4e-4a76-998a-839cba4d74b5)

Step 2: Open layout using magic
command: `magic -T sky130A.tech sky130_inv.mag`

![image](https://github.com/user-attachments/assets/bf0fdca5-567e-4381-9bda-771f08ba1fcd)

Step 3: To ensure by following the guidelines if our standard cell is as per the pnr rules we do the following:

  1. Check tracks and enable the grids by typing `G`.
     
     ![image](https://github.com/user-attachments/assets/fd191453-d38b-4ad6-b57e-4dd47ea0fd1b)

  2. Guideline 1: The input and output ports should be at intersection of horizontal and vertical lines. Give the dimensions of the tracks from the tracks file seen before in the syntax given 
    below in tckon window.

   Syntax : `grid[xspacing[yspacing[xorigin yorigin]]]`

   ![image](https://github.com/user-attachments/assets/d23effe7-7400-4fb4-be3f-910ccbda9511)

   Doing this ensures that I/O ports are placed at intersection show in below image (arrow pointed)

   ![image](https://github.com/user-attachments/assets/1c39b6c6-6643-4922-9792-4ab79a25fb14)

 3. Guideline 2: Required width of the standard cell should be in odd multiples x direction pitch of that layer( x pitch is 0.46)

    The Width is 3 boxes here. Ensuring the guideline
   
   ![image](https://github.com/user-attachments/assets/f5b1964d-a647-4cf4-b5d7-50f52f0aa11e)

 4. Guideline 3: Required height of the standard cell should be in odd multiple

   ![image](https://github.com/user-attachments/assets/4393235c-37f8-4787-84df-16fe1bc18301)

### Task - 2: To write lef file of the standard cell, to copy the files in src directory and make changes in config.tcl file for synthesis process. 

**The Steps are as follows:**

Step 1: In the same layout window ad above we convert the labels to ports if not converted already such that lef could read our layout and generate a file

![image](https://github.com/user-attachments/assets/4ffa1945-963d-4517-813d-dfe06ea1d19b)

Step 2: Save the layout with a different name so that its easier for us to locate this file in the tkcon window.
Command: `save sky130_vsdinv.mag`

![image](https://github.com/user-attachments/assets/91556af4-20df-4211-bd85-8b4421417c0d)

Step3: Write lef in the tkcon window. 

Command:`lef write`

![image](https://github.com/user-attachments/assets/255d98ab-6e5a-47d4-b4f3-e80a75be6a59)

We can locate our lef file vsddtscelldesign folder as shown below:

![image](https://github.com/user-attachments/assets/d802ee7e-a709-43c0-88b0-babeea7dd41b)

Inside .lef file

![image](https://github.com/user-attachments/assets/7e70046d-7a23-4eb8-98a6-bb44c4185ef3)

Step 4: We copy the lef file to src directory use `cp command and the file directory` to copy as shown below:

![image](https://github.com/user-attachments/assets/7996fbb3-6702-4541-b479-ba1857542f63)

All the lib files needed are in src folder such that synthesis can map during the flow

![image](https://github.com/user-attachments/assets/cc8698ff-6706-447e-ab14-6c81c9d61aa0)

![image](https://github.com/user-attachments/assets/a7535e48-48f0-48a4-a677-41888d7ecafa)

Step 5: We modify the config.tcl file by adding all library paths.

Directory

![image](https://github.com/user-attachments/assets/9392db2b-c28e-4387-8b70-a3bbfedc5d44)

Modified file

![image](https://github.com/user-attachments/assets/aa35aee7-dbeb-4332-9a70-53806147efe2)

Step 6: Invoke docker and follow the basic commands for openlane mentioned in Introduction section(commonly used command) above.

Overwrite our runs file

![image](https://github.com/user-attachments/assets/4dc975da-e842-43cc-9722-15eb1d8df09c)

Commands to be used addtionally:
`set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs`

![image](https://github.com/user-attachments/assets/c8fbb213-75ea-41d6-b4b4-091620877146)

Run the command `run_synthsis`. It will be reading the config.tcl file we modified bylinking to the libraries we have added.

![image](https://github.com/user-attachments/assets/bb6bb45a-933d-49f8-8e3b-96d42439346b)

Chip area

![image](https://github.com/user-attachments/assets/0856b173-34b1-42b4-829e-5e91db4b4b0a)

Slack[wns->Worst Negative Slack , tns ->Total Negative Slack]

![image](https://github.com/user-attachments/assets/680e42d4-6fec-41bb-a419-dfd9b825f7f2)

As both the slacks are high we have to improve them by modifying. 


### Task - 3: To improve the slack and re-run synthesis process.

### SYNTHESIS

**The Steps are as follows:**

Step 1: Go to the README file and check out the SYTH_STRAGEY this helps us to modify the changes

![image](https://github.com/user-attachments/assets/f2d55eae-a7fc-41b7-af47-48421c0eff8f)

Step 2: Invoke docker and overwrite the file for the design step before running synthesis follow the commands below

   1. Additional commands to include newly added lef to openlane flow merged.lef
      `set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
      add_lefs -src $lefs`
   2. Command to display current value of SYNTH_STRATEGY
      `echo $::env(SYNTH_STRATEGY)`
   3. Command to set new value for SYNTH_STRATEGY
      `set ::env(SYNTH_STRATEGY) "DELAY 3"`
   4. Command to display current value of SYNTH_BUFFERING to check whether its enabled
      `echo $::env(SYNTH_BUFFERING)`
   5. Command to display current value of SYNTH_SIZING
      `echo $::env(SYNTH_SIZING)`
   6. Command to set a new value to SYNTH_SIZING
      `set ::env(SYNTH_SIZING) 1`
   7. Command to display currennt value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
      `echo $::env(SYNTH_DRIVING_CELL)`
   8. Command to Run synthesis
      `run_synthesis`

![image](https://github.com/user-attachments/assets/7ba35ebd-1195-4fff-8fc6-309c32cf7dd4)

Step 3: After ruuning synthesis we have the following results:

Area is increased as the usage of extra space for reducing the timing

![image](https://github.com/user-attachments/assets/d9a59e20-d82b-40bf-8fac-54369ad228ee)

Slack is reduced entirely

![image](https://github.com/user-attachments/assets/92cfd8be-9926-4bd2-937d-7be35fca24f3)

Step 4: Verifying if our chaged inv file is present in merged.lef

Directory

![image](https://github.com/user-attachments/assets/fe2347ef-adeb-4b9c-86c5-3563358ad30f)

The vsd inv is shown below

![image](https://github.com/user-attachments/assets/4612883d-25b9-4ee2-811f-9722b5cee36c)

### Task - 4: To run floorplan and placement with the above changes. 

### FLOORPLAN

**The Steps are as follows:**

Step 1: Run floorplan using the below commands:

`init_floorplan`

![image](https://github.com/user-attachments/assets/ae8798b2-0997-4496-8f64-3cf116966e50)


`place_io `

![image](https://github.com/user-attachments/assets/03e8f7ee-a576-45c0-9d28-c26c425821f3)


`tap_decap_or`

![image](https://github.com/user-attachments/assets/bcb576af-d438-44f9-9a34-c8e6e9114385)


### PLACEMENT

Step 2: Run the placement command

command: `run_placement`

![image](https://github.com/user-attachments/assets/5f07a5a4-47f3-416e-82d8-21a5c6ecef36)

Step 3: We can see our layout in the magic tool after synthesis,floorplan and placement

Command directory: `magic -T/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

Directory

![image](https://github.com/user-attachments/assets/5ba44b49-bd17-4d88-b697-e49105e5d3da)

![image](https://github.com/user-attachments/assets/422df6a3-eb21-447e-aacd-b616e17ea2bc)

Zoom in version of layout 

![image](https://github.com/user-attachments/assets/d52dcc75-21a4-4fb3-b5a1-7c479bd5b507)

Select the inv cell and use command `expand` in tkcon window to see the layout of inverter

![image](https://github.com/user-attachments/assets/26180c53-2896-4638-b4f4-d02e5692814a)

![image](https://github.com/user-attachments/assets/42e00694-e56d-4a7d-a7ac-f20faf8148f2)


### Task - 5: To run STA analysis.

### STA

We have made the changes and modified the during the synthesis process to get good timing analysis. Now we redo the whole synthesis process to get the original timing such that timing analysis can be done and rectified as such

**The Steps are as follows:**

Step 1: Invoke the docker command and do the pre runs till synthesis.

`set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`

`add_lefs -src $lefs`

`set ::env(SYNTH_SIZING) 1`

![image](https://github.com/user-attachments/assets/e4eab56b-c57e-4894-8ed5-971b88236fc4)

After synthesis

![image](https://github.com/user-attachments/assets/4cc2d4b1-2afd-4700-b764-05ea7893575e)

Step 2: To create a base sdc file based on the custom .sdc file

   1. Custom base.sdc file

      directory

      ![image](https://github.com/user-attachments/assets/1a250891-ef60-4a70-9a3e-106e0c4f83c4)

      Inside Custom base.sdc

      ![image](https://github.com/user-attachments/assets/6bbc0d24-6887-4a5b-a8ed-3ab68c287c3a)

   2. Create a new base sdc file named my_based.sdc using `vim` command

      Directory:
      
      ![image](https://github.com/user-attachments/assets/c16d6be7-8ebd-4c19-87af-bf253498415a)

      After modifying my_base.sdc we have the below file

      <img width="545" alt="image" src="https://github.com/user-attachments/assets/13b95425-71b9-45fc-8609-3d06e6ba4832" />

Step 3: To create a pre sta conf file which will do the pre layout analysis

Directory:

![image](https://github.com/user-attachments/assets/9a7b5a95-a61d-43a3-bcd3-38142cfcc54b)

Inside pre_sta.conf

![image](https://github.com/user-attachments/assets/7c647632-0e46-4d8f-83c5-ec45d2375297)

Step 4: Run the sta analysis. Use the command `sta pre_sta.conf` in openlane directory

Directory:

![image](https://github.com/user-attachments/assets/c2ae59c4-2135-4c0b-86fe-ca9d652ad14f)

We see the same slack which was during the synthesis this is due to that fan out delays

![image](https://github.com/user-attachments/assets/2a209f36-3db6-4c55-9575-5a464c2f807d)


### Task - 6: To improve the timing of STA analysis.

**The Steps for improving the timing analysis are as follows:**

Step 1: We run the synthesis process again to see the correct fan out delay. Invoke the docker command and rewrite the design file and run synthesis follow the below commands:

 1. Additional commands to include newly added lef to openlane flow merged.lef
      `set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
      , add_lefs -src $lefs`

 2. Command to display current value of SYNTH_SIZING
      `echo $::env(SYNTH_SIZING)`
    
 3. Command to set a new value to SYNTH_SIZING
      `set ::env(SYNTH_SIZING) 1`

 4. Command to set a new value to SYNTH_MAX_FANOUT
      `set ::env(SYNTH_MAX_FANOUT) 4`

 5. Command to display currennt value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
      `echo $::env(SYNTH_DRIVING_CELL)`

 6. Run the synthesis
      `run_synthesis`

![image](https://github.com/user-attachments/assets/bf3c07cc-f04a-4985-8ff1-92a56b892230)

![image](https://github.com/user-attachments/assets/af5c0be0-48d0-4079-a271-5cc396d39633)

![image](https://github.com/user-attachments/assets/d04f4b2a-165a-4c9e-81eb-d3115194ac7f)

You can see that the slack is reduced from -711 to -710

![image](https://github.com/user-attachments/assets/c276696c-b72e-4e2e-9634-569b45f3aa13)

Step 2: Now verify the same by running sta in openlane directory

Command : `sta pre_sta.conf`

![image](https://github.com/user-attachments/assets/1682a1ae-78ef-4c67-bde0-90fe72263ad2)

![image](https://github.com/user-attachments/assets/cae26adc-fb4b-4513-8caf-512fb888c41d)

Same slack as the synthesis 

![image](https://github.com/user-attachments/assets/259fd48e-244e-4a23-ba24-bcca9cf1ddb5)

Step 3: To improve the slack we make chages with regard to fan outs by increasing the drive strengths where ever the delay is more and when its driving more number of inputs and we check the sta again if the slack is improved.

1. Commands used:

   1. To report the net `report_net -connections _net number_`  Eg: report_net -connections _11672_
    
   2. To replace cell we have `replace_cell _driver pin number_ sky130_fd_sc_hd__cellname_drivestrength`  Eg: replace_cell _12510_ sky130_fd_sc_hd__or3_4

   3. To obtain results run the sta analysis after change :

      Directory:
      `~/Desktop/work/tools/openlane_working_dir/openlane`

      Command:
      `sta pre_sta.conf`

   2. Change 1
     
     ![image](https://github.com/user-attachments/assets/2d6f6112-44f6-44b8-bab0-104775007df8)

     Its driving 4 pins so increasig the drive strength is better

     ![image](https://github.com/user-attachments/assets/64e4e50b-89f5-4ff1-b847-a73b04acb637)

     Replacing with 4x:
     
     ![image](https://github.com/user-attachments/assets/fa878317-66ab-4fd3-b0a0-ec403f0a821d)

     RESULTS:

     Change in fanout

     ![image](https://github.com/user-attachments/assets/51aec5eb-71a9-45be-9489-c7447a3de533)

     Slack is decreased from the original

     ![image](https://github.com/user-attachments/assets/617e1dff-252a-4975-8f27-da9c047440d6)

   3. Change 2

      ![image](https://github.com/user-attachments/assets/7fc64cda-f492-42f0-ab7f-e9b956e736d7)

     Replacing with 4x:

      ![image](https://github.com/user-attachments/assets/7c837c12-56b6-44a6-909c-c0a268956acb)

     RESULTS:

     Slack is decreased Compared to that last change

      ![image](https://github.com/user-attachments/assets/f3d3eeab-bd72-4769-9081-e9a1d2b0dd52)

   4. Change 3
  
      ![image](https://github.com/user-attachments/assets/bec7f2a7-adc2-4703-8e62-704621f6548d)

      Its driving 4 pins so increasig the drive strength is better , Replacing with 4x:
   
       ![image](https://github.com/user-attachments/assets/467f527b-ff47-4b0d-bbf5-40401cbd2d48)
        
      RESULTS:

      Slack is decreased Compared to that last change
      
      ![image](https://github.com/user-attachments/assets/70f5d25f-ebf8-443a-87dd-fbbe7b70a62c)

   5. Change 4
        
        ![image](https://github.com/user-attachments/assets/c590fbcc-fe98-4b3c-831c-95e6d45726e9)

        Replacing with 4x:
  
         ![image](https://github.com/user-attachments/assets/c30a9a93-5931-42d4-8623-69ea7274c4ba)

        RESULTS:
   
        Change in fanout
      
         ![image](https://github.com/user-attachments/assets/665764d8-d02e-4518-8e00-6a852bcac084)

        Slack is decreased

         ![image](https://github.com/user-attachments/assets/5dcf231d-0592-45cc-8ce0-135b90f1739b)


    6. Change 5
  
        ![image](https://github.com/user-attachments/assets/f3a29e29-5bd4-4b47-a476-4f8f20e51d82)
   
        Replacing with 4x:
  
         ![image](https://github.com/user-attachments/assets/32efa20e-9a54-403d-b484-6b3b23d29bee)
   
        RESULTS:

         Change in fanout
      
         ![image](https://github.com/user-attachments/assets/d42ab584-0812-4b07-8dea-0073db06bf2a)
   
        Slack is decreased

         ![image](https://github.com/user-attachments/assets/70391047-58d8-4baf-a6b8-3fbca2e6466b)

    7. Change 6
  
        ![image](https://github.com/user-attachments/assets/1fb67fa7-a72d-44ba-a955-7d355b03568c)
   
        Replacing with 4x:
        
         ![image](https://github.com/user-attachments/assets/4f10397c-f00e-44b2-82a0-6db046964fd2)

        RESULTS:
   
        Change in fanout
   
        ![image](https://github.com/user-attachments/assets/c06d4c81-2517-4716-8c87-e7aabac16bed)

        Slack is decreased  
      
         ![image](https://github.com/user-attachments/assets/f78f0d3a-b583-45ad-af08-07c1e6f34979)


### Task - 7: To Replace the old netlist file after the timing ECO fixing.

**The Steps are as follows:**

Step 1: In the openlane directory after runnin the sta pre_sta.conf command use the below command

Directory: `~/Desktop/work/tools/openlane_working_dir/openlane`

To run sta :  `sta pre_sta.conf`

To rewrite the verilog file use below:

`write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-05_18-08/results/synthesis/picorv32a.synthesis.v`

![image](https://github.com/user-attachments/assets/8361b600-6872-472b-9a69-ac2a13c2b594)

Step 2: To verify if its overwritten go to the below directory and open the picorv32a.synthesis file and search for the last pin you have modified for fixing the timing error. 

![image](https://github.com/user-attachments/assets/5a8c8441-0aa6-4988-bdbd-024f867b97b7)

Pin _15168_ was changed from drive strength 2 to 4. we can see that below

![image](https://github.com/user-attachments/assets/e88bf39c-57af-427c-bff8-07e0edb91f47)


### Task - 8: To Implement floorplan,placemet,cts(Clock tree synthesis) after fixing the timing and rewriting the verilog file

**The Steps are as follows:**

Step 1: Invoke docker and overwrite the design

![image](https://github.com/user-attachments/assets/42b088d1-5826-4f14-8e84-80ad42a6c4df)

<img width="555" alt="image" src="https://github.com/user-attachments/assets/a5e14636-551e-473e-9eb7-2122f64ed337" />

Step 2: Run synthesis

![image](https://github.com/user-attachments/assets/e218707b-1494-458e-921a-3938d3bceb56)

![image](https://github.com/user-attachments/assets/0c1b1beb-43f8-4a9d-8938-d5d901221e6f)

Step 3: Run floorplan

![image](https://github.com/user-attachments/assets/21eabf1f-67e5-4b6b-bce1-8ecd0a7286f5)

![image](https://github.com/user-attachments/assets/b125eca3-a22a-4c86-97a0-409d216bddd0)

![image](https://github.com/user-attachments/assets/7017db61-3d87-4499-9ec1-3feb4f6db033)

Step 4: Run placement

Command : `run_placement`

![image](https://github.com/user-attachments/assets/df4df732-1d61-41c6-b25e-3c69ce97760c)

Step 5: Run cts

Command : `run_cts`

![image](https://github.com/user-attachments/assets/5dc6fd95-63c7-4ac0-9f43-e2696c73d978)

![image](https://github.com/user-attachments/assets/cc59139c-0af8-49ca-9c3a-25e397ca6fdf)

Step 6: We can see the .v file in the below directory after cts run

![image](https://github.com/user-attachments/assets/b37bc11d-f394-40bf-9282-f90607fb30e0)


### Task - 9: To verify CTS

**The Steps are as follows:**

Step 1 : To see how openlane take the procs from ie., the procedure for running a command go to the below directory

Directory:

![image](https://github.com/user-attachments/assets/8bdbe25e-297f-4774-9f70-68ca6232dc9d)

Taking cts tcl file using the command `less cts.tcl` here to check how the proc works. It shows the procedure on how it runs one by one when run_cts is invoked.

![image](https://github.com/user-attachments/assets/54cc7bc1-18e0-45ec-8b6b-e226627bfdd0)

### ABOUT OPENROAD
Step 2 : Open the openroad in the below directory. Openroad is a EDA tool inside openlane

why is there no file related to synthesis? Openroad runs Floorplan, placement, CTS, routing, STA in a TCL-based scripting

![image](https://github.com/user-attachments/assets/6d742894-12fb-4d0f-9b73-b0140aaadd4c)

Inside or_cts.tcl file. Command `less or_cts.tcl`

![image](https://github.com/user-attachments/assets/2eaabd91-f587-490c-890f-bc11297b4a6d)

![image](https://github.com/user-attachments/assets/d08d100e-dcbd-417e-99f5-b2a7a5861f2e)

Step 3: Go back to the openlane docker window after running till cts we run the below commands 

   1. To show the current def : `echo $::env(CURRENT_DEF)`

      ![image](https://github.com/user-attachments/assets/bf5da2eb-b17e-4975-b4d6-aff2daa5716a)

  2. To display the branch buffer cells : `echo $::env(CTS_CLOCK_BUFFER_LIST)`

      ![image](https://github.com/user-attachments/assets/d8a6801e-9526-4466-8424-5d7a9eec2809)

  3. To display the Maximum capacitance of the output pin of the clock buffer 16 : `echo $::env(CTS_MAX_CAP)`

     ![image](https://github.com/user-attachments/assets/d9db3053-be9a-42d9-86c1-b139a8d5fb9c)

Step 4: All the paramenters and variables in or_cts.tcl are typical parameters so they can be verified from typical.lib from the below directory

![image](https://github.com/user-attachments/assets/09fe320d-f633-42db-832b-54df22344680)

Inside sky130_fd_sc_hd__typical.lib 

We can see the clk buf 16 cell

![image](https://github.com/user-attachments/assets/be74da53-a303-4d5a-a8d8-597410d54560)

For output pin the below is the capacitance as mentioned above in or_cts.tcl in openroad file

![image](https://github.com/user-attachments/assets/afdb9692-d475-41c2-a94b-dbe1da7d0c7d)


### Task - 10: To analyze Timing analysis with real clocks using OpenSTA

**The Steps are as follows:**

Step 1: Open openroad insise openlane docker window.

Command to run OpenROAD tool

`openroad`

![image](https://github.com/user-attachments/assets/c2f050d0-d7ac-4cd4-9100-dd9f4530a3c3)

Step 2: Read lef file 

`read_lef /openLANE_flow/designs/picorv32a/runs/18-05_18-08/tmp/merged.lef`

![image](https://github.com/user-attachments/assets/1d1092df-55b5-4286-9029-4e37d4afd57e)

Step 3: Reading def file

`read_def /openLANE_flow/designs/picorv32a/runs/18-05_18-08/results/cts/picorv32a.cts.def`

![image](https://github.com/user-attachments/assets/f3dce53d-ee70-4a06-a732-c0c4129d9a77)

Step 4: Creating and reading an openroad database 

`write_db pico_cts.db`

`read_db pico_cts.db`

![image](https://github.com/user-attachments/assets/0f752626-2c5c-4180-b540-976ffb53155f)

We can see it is created in the below image

![image](https://github.com/user-attachments/assets/efd92480-c513-45ce-9740-9b43a26ccf2b)

Step 5: Read netlist post CTS

`read_verilog /openLANE_flow/designs/picorv32a/runs/18-05_18-08/results/synthesis/picorv32a.synthesis_cts.v`

![image](https://github.com/user-attachments/assets/96022937-67d1-4817-b964-68a0b29b2b81)

Step 6: Read library for design

`read_liberty $::env(LIB_SYNTH_COMPLETE)`

![image](https://github.com/user-attachments/assets/283753f1-4d53-45f0-a838-3f11c4ef8d16)

Step 7: Read in the custom sdc we created

`read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`

![image](https://github.com/user-attachments/assets/0a9fa9d1-0448-43ea-aec4-b943383af48a)

Step 8: setting all clocks as propagated clocks

`set_propagated_clock [all_clocks]`

![image](https://github.com/user-attachments/assets/762090f5-c262-4bb8-95d5-f6d60c6244fd)

Step 9: Generate the custom timing report

`report_checks -path_delay min_max -format full_clock_expanded -digits 4`

![image](https://github.com/user-attachments/assets/ea177f43-c9be-4d5e-b661-6178a22a1d16)

Hold slack

![image](https://github.com/user-attachments/assets/585df64d-92b0-49d7-a9ba-fe160ae8383f)

Setup slack

![image](https://github.com/user-attachments/assets/34d21dcb-08fd-4f7d-abf2-a4ae608b8121)

Step 10: To report the skew of slack use the below commands

   `report_clock_skew -hold`

   `report_clock_skew -setup`

   ![image](https://github.com/user-attachments/assets/0812a44e-a7bb-4bdd-8d9f-14b43c90fc21)

Step 11:To exit to Openroad flow
 `exit`

 
### Task - 11: To improve Timing analysis by removing the clock buffer

**The Steps are as follows:**

Performing the below steps in docker window after running cts

Step 1: Check the current .def file used it should be placement def file

`echo $::env(CURRENT_DEF)`

![image](https://github.com/user-attachments/assets/1f66c016-e66a-4f3d-aaea-13c157778f9a)

Step 2: Update the .def file & verify the buffer list if clk_buff_0 is removed.

`set ::env(CURRENT_DEF) directory of placement.def file`

`echo $::env(CTS_CLK_BUFFER_LIST)`

![image](https://github.com/user-attachments/assets/b2ddbb22-8b6c-4793-bfaa-d277784b5fe5)

Step 3: Run cts again `run_cts`

![image](https://github.com/user-attachments/assets/1e104ee0-4396-4882-a998-48e61085cf83)

Step 4: Follow the below steps in openroad ie., enter the command openroad inside the openlane docker terminal after running the above cts command

   1. Command to run OpenROAD tool

      `openroad`

   2. Read lef file 

      `read_lef /openLANE_flow/designs/picorv32a/runs/18-05_18-08/tmp/merged.lef`

   3. Read lef file 

      `read_lef /openLANE_flow/designs/picorv32a/runs/18-05_18-08/tmp/merged.lef`

   4. Creating and reading an openroad database [As its modified write a new file again]

      `write_db pico_cts1.db`
      
      `read_db pico_cts1.db`

   5. Read netlist post CTS

      `read_verilog /openLANE_flow/designs/picorv32a/runs/18-05_18-08/results/synthesis/picorv32a.synthesis_cts.v`

   6: Read library for design

      `read_liberty $::env(LIB_SYNTH_COMPLETE)`

   7. Link design and library

      `link_design picorv32a`

   8. Read in the custom sdc we created

      `read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`

   9. setting all clocks as propagated clocks

      `set_propagated_clock [all_clocks]`

   10.  Generate the custom timing report

      `report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4`

   ![image](https://github.com/user-attachments/assets/923c7950-9ba8-4668-aad4-0395e6d28868)

   RESULTS

   Hold slack

   We observe from the below figure that there is no buf 1 as we removed it from buffer list
   
   ![image](https://github.com/user-attachments/assets/e15d1824-06d9-41c9-b6c4-b4140aaec7cd)

   Hold slack is increased from 0.0772 to 0.2456 as the area increased

   ![image](https://github.com/user-attachments/assets/e4f23313-708c-46f4-b07e-acb8665cb8ee)

  Setup Slack

   We observe from the below figure that there is no buf 1 only buf 2,4,6 is there as we removed it from buffer list
   
  ![image](https://github.com/user-attachments/assets/f2405536-aa25-4aa2-9394-4f519542917f)

  Setup slack remains the same
  
  ![image](https://github.com/user-attachments/assets/9fd83f5c-1659-47dd-9486-f168ef46e3a1)


Step 5: The reports for setup and hold

  `report_clock_skew -hold`

   `report_clock_skew -setup`

![image](https://github.com/user-attachments/assets/6197daf1-df88-4e23-9b81-cc8f3c61022f)

Step 6: If we want to add back the buf 1 to the list follow the below

Command : `set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]`

![image](https://github.com/user-attachments/assets/a6c1d541-5095-4d10-bfa3-6910c6ce7730)

Step 7: To Exit from openroad 

 `exit`

 -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## 6. Day 5 - FINAL STEPS FOR RTL2GDS USING TRITONROUTE AND OPENSTA

### THEORY
[📄 Day-1.pdf](Day-1.pdf)

### LAB TASKS

### PDN(POWER DISTRIBUTION NETWORK)

### Task - 1: Power distribution

**Steps for the pdn are as follows:**

Step 1: In the openlan terminal invoke docker and our runs folder for design

   `docker`

   `./flow.tcl -ineractive`

   `prep -design picorv32a -tag 18-05_18-08` -> dont overwrite as till cts everything is done we can run pdn continuing from cts

   `echo $::env(CURRENT_DEF)` -> to check if the def file is cts. If not we have to update it to cts by using the set command and the directory in which cts def file is located

   ![image](https://github.com/user-attachments/assets/cac05b7a-de1b-4ae6-b2e9-94c146a3300e)

Step 2: Run pdn 

`gen_pdn`

![image](https://github.com/user-attachments/assets/0ede28f2-b762-471a-ab3c-c120936360f7)

Loads the below files

![image](https://github.com/user-attachments/assets/27c36fb3-aaed-4c0d-aaac-12b626de0aa5)

Created the standard cells grids ie., the power and ground for stdcells

![image](https://github.com/user-attachments/assets/14a5c86e-191c-4b19-a657-3b3a54dd526a)

![image](https://github.com/user-attachments/assets/87582d6b-ee51-4aec-9f39-c0d11c091ce8)

Here by using the echo command we can see our .def file is changed from cts to pdn ad pdn is run successfully

![image](https://github.com/user-attachments/assets/fe384b5b-b47f-4d39-bce6-dca0573b86f0)

Step 3: View in Magic

`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 17-pdn.def`

![image](https://github.com/user-attachments/assets/90d569e0-12dd-48cd-bb92-a95839c2a16d)

Layout of our inv cell. We can see a grid like structure in bluish green color

![image](https://github.com/user-attachments/assets/2163696c-4fee-43b9-89ca-c7dfc81dc4eb)

Vdd and gnd rails can be observed

![image](https://github.com/user-attachments/assets/2927c49c-a8d4-4a8b-a13c-b63df9b9cdeb)

Vdd rail

![image](https://github.com/user-attachments/assets/925bceaf-b681-459f-9467-e3d4f142795c)

Gnd rail

![image](https://github.com/user-attachments/assets/80265ec0-3da3-4211-9860-d21b2ed010fc)

Std cells

![image](https://github.com/user-attachments/assets/099c97ee-bd10-4ee0-8f69-0d1391ddf318)


### ROUTING

### Task - 1: Perform routing

**Steps for the routing are as follows:**

Step 1: Switches for routing can be observed in the following directory

![image](https://github.com/user-attachments/assets/f35ffe4e-caaa-4aea-bb95-074d665e0c34)

Inside READmE file

![image](https://github.com/user-attachments/assets/72b723ee-6608-4b13-a4b5-2f7504de4ae9)

Step 2: After generating pdn in openlane docker terminal run routing 

`run_routing`

![image](https://github.com/user-attachments/assets/1c3a1aac-eb10-4662-8e2a-2baaac33b5a7)

![image](https://github.com/user-attachments/assets/90ae4b78-15e0-4a4b-ba79-2456e843bba8)

Step 3: View in magic

`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../../tmp/merged.lef def read picorv32a.def &`

Directory:

![image](https://github.com/user-attachments/assets/54b39328-97ed-41f7-968e-be8ce97baa5b)

Layout

![image](https://github.com/user-attachments/assets/87bab45b-d390-4517-9521-08fc2a0bb96e)

The routing is done

![image](https://github.com/user-attachments/assets/372f50a4-0198-48b6-8288-29762f79274c)

![image](https://github.com/user-attachments/assets/2210f777-4beb-4e34-9988-ce1e16ee15f0)


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 7. REFERENCES

   1. Google. SkyWater Open Source PDK. GitHub. Available at:

      https://github.com/google/skywater-pdk
      
   2. Nickson Jose. VSD Standard Cell Design. GitHub. Available at:

      https://github.com/nickson-jose/vsdstdcelldesign

   3. NGSpice. Open Source Circuit Simulator. SourceForge. Available at:

       https://sourceforge.net/projects/ngspice/

   4. GitHub. Explore and Discover Open Source Projects. Available at:

      https://github.com/

   5. SkyWater SKY130 PDK Authors. Periphery Rules Documentation . Available at:

      https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## 8. ACKNOWLEDGEMENT

I would like to sincerely thank Mr. Kunal Ghosh, Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd., and Mr. Nickson Jose for their outstanding mentorship and engaging delivery during the DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING workshop. Their depth of knowledge and ability to clearly explain complex concepts made a significant impact on my understanding of physical chip design using OpenLANE and other advanced tools. The workshop was thoughtfully structured and exceptionally informative. I’m truly grateful to both Mr. Ghosh and Mr. Jose for their dedication and for generously sharing their expertise, which made this learning experience both insightful and inspiring























      








   
























      


     




































 


     


























     






   




























        

        

        













