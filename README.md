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

### 1. IO Placer Revision

One of the features of OpenLANE is that we can make changes on the fly.

To see this, we are going to change the placement of Input-Output pins (IO placer).

First, we will figure out what key value needs to be updated; we can get this information in the "README.md" file in the configuration folder.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/ad150f8f-bfda-460d-9ebc-8db598de9632)

Now, we will set the key with a different value in the openlaneFlow window and execute the floorplan command again.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/770619bf-7333-40a8-ae3e-8c8856a79880)

Once this is complete, we can verify changes in the new floor plan using Magic.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/42b77bdd-65de-4be8-9062-5f4930b5c0f6)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/8e487766-c1ec-43b1-9b81-f70771335a9b)

The above image shows that the IO pins have changed their position compared to the first floorplan.

### 2. Cloning a Git File.

For this lab, we have to clone a git file that contains the required information and files for standard cell designs.

To get this data, we will go to a Git hub repository whose address is mentioned below.

```https://github.com/nickson-jose/vsdstdcelldesign```

To copy the git link, press on Code. After that, a dropdown tab will appear; click the copy option to copy the URL.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/f2f97c76-ca7e-4d8c-8587-eb40809e9542)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/8380c73d-269e-4625-88b6-b0d91ee24804)

After this step, go on your virtual machine, and in the openLANE Directory type the below command :

```git clone https://github.com/nickson-jose/vsdstdcelldesign.git```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/652d71f0-c7ae-473c-8f5d-3647eefa524f)

To view the copied inverter file, we will use magic. We have copied the tech file to current directory. 
The command for magic:

```magic -T sky130A.tech sky130_inv.mag &```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/81fde5f2-b15b-41e5-a131-316ef40a4d10)

Once the layout is opened, we can use Magic GUI to learn about layers in the mask layout. We can select/deselect layers by clicking icons on the right-hand side

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/0a0bbe65-662d-45be-9852-d85c1c6b7b72)

We can get to know about the device type just by dragging the cursor over the required region, pressing s (which selects the area), and then typing the prompt “what” in the tkon window.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/8670622d-39f9-470c-998d-720b50f6748d) ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/708211b9-efd7-4b20-97b5-9e26e6cb45fc)


We can also check the connectivity of the pins by dragging the cursor over the required region, pressing "sss" ( three times s) .

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c3ae0275-9b25-43c3-b9ac-67dcf738ee0d)

### 3. Extracting Netlist from Layout File

For extracting Netlist we will use the below commands in the tkon window:

```
extract all
ext2spice cthresh0 rthresh0
ext2spice
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/337ddfaa-301a-4f32-bce3-7ebb15868984)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c8f6e1cc-49d0-46ca-ac62-793781eb132f)

The generated netlist is shown below:

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/32f6a1df-8c8d-46b9-ab7c-89801cf669fa)

The Extracted Parastics are shown below:

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/5074641f-6188-47a4-97c6-c458729a85cc)

### 4. Creating Final SPICE deck using Sky130 tech and simulating through ngspice.

Once we have extracted the SPICE file, we have to make some changes highlighted in the image below.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/e9e69305-1862-4f3b-af90-7ccd86d57f01)

After spice file is edited we can run the simulation using below command:

```
sudo apt-get install ngspice
ngspice sky130_inv.spice
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/b7a0a2c2-b074-4f03-aa55-d1e3370b5ce1)

Once Simulation is completed , excute the bleow command to plot graph.

'''plot Y vs time A'''

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6149db6e-0df6-4ac5-b81b-7fb732623118)

Now Right click to zoom 

1. Rise time transition 20%-0.66 to 80%-2.64
   
   ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/76480d87-4d50-4b77-bae5-a8e9ec2e8179)

   Rise Time = 0.05ns

2. Fall time transition 80%-2.64 to 20%-0.66
   
   ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/b81b4704-cd7d-4a33-9cfd-3a530649c448)

   Fall Time = 0.02ns

3. Cell rise delay 50%-1.65
   
   ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/332bac11-4d78-400a-b10c-8154259cbf71)
   
   Cell rise delay = 0.05ns

4. Cell fall delay 50%-1.65
   
   ![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/200ceca5-d300-4ec2-9eaf-35d2f2a953a0)
   
   Cell fall delay = 0.02ns

### 5. Magic DRC

We will download the setup for the GitHub repository for this lab and unzip it.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1edcbc90-b35e-419a-8f2a-a3bba15a1f0a)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/07ff60bd-e8e8-4478-bc31-1533c5135275)

Command for invoking Maic is :

```magic -d XR &```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6c425237-e458-4234-9480-f29859a6d83d)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/588482a9-2b50-445c-b220-fda9629c1438)

We can use the File > Open ,option to open any layout file

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/380a092f-8347-4a58-84e0-f399445e4dba)

DRC errors are highlighted in white shade on layout , we can see the excat error in tkon window by selecting the cell and excuting command "drc why ".

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1f6cb142-b485-482e-88a8-b373e2547427)

### DRC EXCERSISE 1

Open layout file "poly.mag"

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/8a7b4730-aac4-4c87-95b2-bdc5101b9fac)

In this file we will be working on "poly.9" layout

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6d43eccb-e1cb-4345-9ddd-5824b2dcfca6)

As we can see, no DRC errors are visible in the above layout, but there are some DRC errors. We must make changes to the "sky130A.tech" file to fix this.

```gedit sky130A.tech```

Changes done are highlighted in the below image.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c60add31-bc14-484c-9270-20571b8f5483)
![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/908b1d29-a103-4d89-80c8-a9aee63ecc38)

After changes are made, Magic will not need to restart. We can just run the below command in the tkcon window to refer to the rules, and DRC checks are reflected in the layout view.

```
tech load sky130A.tech
drc check
drc why
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6a914963-48b0-49a1-a9be-663b5a6635a9)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/168d2f05-9d32-49b3-8c4c-a9801e302e44)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/ff334310-1013-4c8c-8bd7-bd3402d3c64c)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/a0fe5fa4-8129-478f-9866-1e2042eaec13)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/b2925474-2ab5-4249-805f-4183490fe267)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/0b89c627-4c2e-4e94-ba8b-16c650a1d0c6)

### DRC EXCERSISE 2 - Fix Missing Rules

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/f0a6f51e-ffd0-478e-9208-2169afe32672)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1915b34b-ba10-404a-84f7-6bb98e760c10)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c3b3ea2f-c948-4efe-a7ba-090c250e08a5)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/af866d20-dd6e-4180-b8d0-ba7d91c80447)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/8ac1eb22-0a0f-452f-be76-9496a0be4bce)




























  
















































  
  









