# NASSCOM-SOC
## **OPEN LANE**

OpenLane is an ASIC infrastructure library based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, KLayout and a number of custom scripts for design exploration and optimization.

For this project, we will be utilizing the OpenLane open-source physical design flow in conjunction with the Skywater 130nm PDK. These tools will be used throughout the entire design and implementation process

## **INSTALLATION**

By installing Ubuntu through Oracle VM VirtualBox, a virtual Linux environment was created. This setup provides isolation and consistency for development and testing. The entire project will be carried out within this Ubuntu environment.

Below is the screenshot showing the system specifications of the Ubuntu virtual machine set up using Oracle VM VirtualBox.
![image](https://github.com/user-attachments/assets/47777613-abee-4fda-9080-caf427e9eadd)


## **DAY 1 - INCEPTION OF OPEN-SOURCE EDA, OPENLANE AND SKY130 PDK**

### Introduction
[📄 Day-1.pdf](Day-1.pdf)

### Task-1 : To find the flop ratio
The steps for the synthesis which helps us to find the flop ratio is as follows:

Step 1: Open the openLane directory
<img width="960" alt="image" src="https://github.com/user-attachments/assets/a602e752-3671-4e50-bde4-59ac65aee88b" />

Step 2 : use **"docker"** command which is used to run the OpenLane toolchain inside a Docker container, which provides a pre-configured environment with all dependencies, tools (like Yosys, Magic, KLayout, OpenROAD, etc.), and paths correctly set up.

Step 3: **"./flow.tcl -interactive"** command is used to launch OpenLane in interactive mode inside the Docker container.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/f6c1e9c2-b933-4341-9442-c168d2f8b8b1" />

Step 4: Enter command **"package require openlane 0.9"** it load the openLane package of version 0.9.

Step 5: Enter the command **"prep -design picorv32a"** is used in OpenLane's interactive mode to prepare the design environment for the flow.
        This step mereges the .lef files 
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d9eae49b-ccb1-4c1b-acf7-21ee202a8dd2" />   
         We can see the merged lef file in the directory shown in below image and .lef can be accessed by the command **"less merged.lef"** in the terminal
<img width="960" alt="image" src="https://github.com/user-attachments/assets/3073b8a0-70e4-4d95-9470-6fcedc6fba0e" />

Step 6: Enter the command **"run_synthesis"** to start the synthesis of the design and the below is tha image of successful synthesis.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/00b999a0-6cdd-40ac-9c1a-1d4fc48b3ded" />
        We can see the synthesized verilog file in the below directory,the verilog file contains the logic of our design.
        <img width="960" alt="image" src="https://github.com/user-attachments/assets/b36def51-dcee-4e71-b0bf-57c63eedc96b" />

        













