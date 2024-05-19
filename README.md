# Kashyap_NASSCOM_VSD_SOC_Design_PD

# **Introduction**

This workshop offers hands-on experience designing an Application Specific Integrated Circuit (ASIC) using open-source processes. I will learn about physical design and how to create a chip layout, going from a high-level description (RTL) to a final design file (GDSII) suitable for fabrication. The workshop leverages Google's open-source resources for the design process.
This workshop will use OpenLANE and Sky130 nm PDK to generate standard cells.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/2b2c1f19-45db-4cb2-9b61-a31ce33678ee) 

Below, I will upload the lab contents of what I have learned in this workshop.

*****************************************************************************************************************************************************************************************************************************************

# **Day 1**

### 1.Locating Openlane work Directory and exploring files.

  OpenLANE operates in a Linux-based OS environment, so we access it through a virtual environment using VirtualBox, with Ubuntu as the installed OS.

  The below is the path where openLANE is located

  ```cd Desktop/work/tools/```

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/92f2f866-f235-41ed-9fb0-babc8fb63c6b)

  ```cd openlane_working_dir/openlane```

  In this directory we can find all type of support and required files 
  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/5fb6c57c-455e-4943-b5f6-51ae587d1380)


  ```cd Desktop/work/tools/openlane_working_dir/pdks```

  In this directory, you will find PDK files that include all the necessary supporting files, such as timing data and more.

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/514a2c58-c9d7-4ef5-9835-57816de52ecb)
  
  ```cd Desktop/work/tools/openlane_working_dir/pdks/sky130A```

  The folder /sky130A contains two subfolders: /libs.ref and /libs.tech. The /libs.ref folder holds all the reference files, while the /libs.tech folder contains tool-specific files.

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/58b50ad6-e362-483d-b386-389bb1cb322b)

  The PDK variant which we will be using is "sky130_fd_sc_hd" which is highlighted in the above image.
  explaination of the abbreviation Sky130_fd_sc_hd is given below:

  Sky130: This refers to the process technology used, likely the 130nm process from SkyWater Technologies.

  fd: This stands for "foundry," indicating SkyWater Foundry is responsible for creating and maintaining the library.

  sc: This is short for "standard cells," which are pre-designed building blocks used to construct digital circuits.

  hd: This signifies "high density," meaning the library offers more compact standard cells compared to non-HD libraries.

  Therefore, Sky130_fd_sc_hd describes a collection of high-density, pre-designed digital circuit elements built by SkyWater Foundry using their 130nm process. This library allows designers to quickly and efficiently create complex  digital circuits.

### 2. Invoking OpenLANE 

  First, navigate to the directory where OpenLANE is located:

  ```cd Desktop/work/tools/openlane_working_dir/openlane/```

  Then, use the `docker` command to invoke OpenLANE:

  ```docker```

  To open OpenLANE in interactive mode, use the following command:

  ```./flow.tcl -interactive```

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c5ab3bd8-baed-49a3-8c3a-6ab6ea260ec8)

### 3. Now we will run simulations on synthesis of picorv32a.

  It consist multiple stages:
  a. Design Preparation stage
  command to run preparation stage :
  
  ```prep -design picorv32a``` where "picorv32a" is the folder name

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/902eb09e-b3d4-4472-9645-9eebc8954e7e)

  After running the preparation command, we can see changes in the "runs" folder of picorv32a; in this folder, all the reports and results are generated from the ongoing simulation.

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/9e0b852f-3498-4f4d-8f37-7185493fa740)

  b. Design Synthesis Stage
  command to run synthesis stage :

  ```run_synthesis```

After running this command, the synthesis will take a few minutes. After completion, an error will pop out if it is present or will give us a successful completion of the synthesis text.  

  ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/a69e1013-2213-4ccf-a018-bdc93c671a36)

  If we scroll up on the terminal window, we can see the results generated or go to the "/runs" folder to view the generated reports and results.
  
![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/5cf0937b-876a-4cfa-b161-b87d22a500c6)


## **Workshop Objective 1**
Calculate the flop ration i.e. number of D Flipflops in the generated netlist.

We will use the "Number of cells: " and "sky130_fd_sc_hd__dfxtp_2" generated in the synthesis report.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/11f90e98-d1c8-48e2-b7fa-823e34f70b9c)

Flop Ratio = (Total No. of D Flipflops)/(Total No. Cells) = 1613/14876 = 0.1084

%Flop Ratio = 0.1084 * 100 = 10.84

Therefore the Flop ratio is 10.84%.

*****************************************************************************************************************************************************************************************************************************************

## **Day 2**

### 1. Running Floorplan in OpenLane

Before running the floor plan, we must check all the configuration files; the data in this file is used to set important parameters like die size, aspect ratio, utilization factor, etc.
We can find these configuration files at the location below.

```./openlane/configurations ```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/5c8950c3-aad3-439c-82ab-9a8ebd18698c)

The "README.md" files contain the information of a set of switches that are required to be set in the configuration files (*.tcl)
The configuration file for the floorplan is named "floorplan. tcl," and its contents are shown in the below image.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/ee6cc837-b7aa-44dd-8109-52aec03ebc09)

After all the required Changes, we can run the Floorplan step with the below command:

```run_floorplan```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/f09dbb25-cd46-4632-8bda-64440fbc7713)

The image below shows that this step is completed without any errors.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1d8f1bca-d795-4b9a-90bd-06cd607a858d)

We can view the generated floorplan data on the path given below :

```./openlane/designs/picorv32a/runs/<date-on-which-simulaion-executed>/results/floorplan``` 

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/db7e878d-f6e8-475c-8424-9ee16cd63aab)

we can check the data in "picorv32a.floorplan.def"

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/31da20f0-17e4-4a31-ac8a-a0fa024d3f50)

## **Workshop Objective 2**
Calculate the Area of the Die

From the above output data we get ,

Unit Distance Microns 1000

Die Width = 660685/1000 = 660.685 Microns

Die Height = 671405/1000 = 671.405 Microns

Therefore, Area of the Die = Width * Hieight = 660.685 * 671.405

**Area of the Die = 443,587.212425 Sq. Microns**

### 2. Review floorplan layout in Magic

The command used to invoke maic is given below

```magic -T <technology_file_path> lef read <path_for_meged.lef_file> def read <path_for_*.def_file> & ```

Therefore the customized command which I used was:

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &```

After executing this command, Magic is invoked, and we can see the floorplan of your design.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/05674c69-9d84-4e94-9f72-a7914cebb930)

By using Tkcon window, we can check what cell it is

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/140166b8-7371-4c86-a8df-8f1a4f2cdddb)

### 3. Running Placement in OpenLANE

We use the below command to run placement.

```run_placement```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1c30319b-7a9b-46bc-8530-3cfc9f604a95)

Once Placement is done, we can view our schematic in Magic. We will use the same command format used earlier to invoke Magic and make the required changes and execute on the correct file path.

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/16315a5c-e826-4c50-b0e0-75e7b5f56ddc)

Maic Window

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/f665f5a5-033f-408f-a23f-d3dbb930c065)

We can see placement of Blocks in Row Format

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/17cd9a85-bf59-4018-85e8-f56da096c7b5)

*****************************************************************************************************************************************************************************************************************************************

## **Day 3**

### 1.






  
  









