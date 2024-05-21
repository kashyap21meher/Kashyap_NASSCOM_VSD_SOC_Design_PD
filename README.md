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

*****************************************************************************************************************************************************************************************************************************************

## **Day 4**

### 1. Lab steps to convert grid info to track info

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/b7def3b7-49bb-47c4-b32c-7155e5d8f5d3)

A track info is used to route the metal routes. its located in  

```
cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd
cat tracks.info
```

With the help of ``help grid``` we get to know what all arguments does the grid command take.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/06975d7d-c7e4-4bd4-ab11-50ad1cf90647)

Once make the required changes and press ENTER , the grid size changes as per the value entered.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1167cfaf-c1fe-4487-95aa-d1d3c1112135)

### 2. Step to Convert Layout to ".lef" file

For naming a port , first select a pin to assign a port .Then go to Edit > text and to required changes.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/3b7adea2-d5f0-400e-8e0b-b9b90c69c8f5)

Now we need to define ports assign them as input, output and inout pins , this is done selecting the port an execting the below command :

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7a07833e-fa22-4ecf-bc0b-28c09c7ca42e)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/5ff695bf-da28-4930-b350-f680fc52e062)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/93585022-acae-43a0-85b2-90bd5bbe4ac9)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/d2182a94-efc7-4fcf-bc76-4573ee021711)

Now we are ready to extract the ".lef" file.

First we will save the edited ".mag" file with different name.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/93a3d6e7-ea73-40ed-ba43-cfd646aba52b)

then we will open the edited .mag file. and execte "lef write" which will create a ".lef" file 

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/a015d574-66ae-4906-b752-0d4f78486517)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/679a2290-5073-4733-bed5-fb848797160f)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/2d4a26b1-e7c6-459f-b3c6-54b62ac4ba79)

Now we wll copy nescessary files to "picorv32a" designs folder.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6937b5ef-c988-4ed2-86fa-a852f69b9565)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/0da7980f-1010-4b38-9147-ba9c184b7b9e)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/650a27b0-85a1-4cf9-b4f5-e5fd53dcc295)

Now we need to modify our "config.tcl"

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1278d181-19f4-434f-8b3b-06a8abfb8ee2)

```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Now we will Invoke openlane in interactive mode and ececute the below command (prp to synthesis)

```
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/41406001-dc2b-4c24-8a8b-2e85d537ea26)

Now we have to take care of slew , we will set some reqired keys to improve overall specs.
We will execute commands in the following order

```
prep -design picorv32a -tag 21-05_08-49 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
echo $::env(SYNTH_STRATEGY) # Command to display current value of variable SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3" # Command to set new value for SYNTH_STRATEGY
echo $::env(SYNTH_BUFFERING)# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_SIZING) # Command to display current value of variable SYNTH_SIZING
set ::env(SYNTH_SIZING) 1 # Command to set new value for SYNTH_SIZING
echo $::env(SYNTH_DRIVING_CELL) # Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
run_synthesis
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/a8890c03-20e7-4b9c-b5fb-2f9614832039)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/61fd81b5-10f1-4ab2-aaf2-eb4b4540476f)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/0ba7efe7-d872-463c-8a9a-4bc72c3c2461)

The area has increased, and the worst negative slack has improved to 0.

Now ,we will run floorplan 

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/356bdeb5-c90a-48bb-bca1-37017f67f967)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/e93e288a-f383-44a0-8500-3e536891cfe1)

There is a error for running floorplan , therefore we are excuting the below command.

```
init_floorplan
place_io
tap_decap_or
run_placement
```
Now Placement step is completed.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/fa228545-53ff-47a0-bc2b-1ff4eeb56aa0)

We will now invoke Magic to view the Placement of our cell in the design.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/3cf4488e-f224-4752-9094-b40800bf56a6)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/b6390f70-15e7-4885-839b-589c552f7ce3)

We can see our custom inverter been placed in the design

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/4faff06b-8629-4784-bfbb-67444ce84137)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/90679565-742c-4fec-b46a-839d277918d6)

### 3. Steps to configure OpenSTA for post-synth timing analysis

Since we have achieved a worst negative slack (WNS) of 0 after the improved timing run, we will now perform timing analysis on the initial synthesis run. This initial run had many violations and no parameters were added to improve timing.

First we will creat pre_sta. conf file in the openlane directory.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/032a9140-2aa2-4203-a023-aa6cf4727ca6)

Then we will create a my_base.sdc file which is based on openlane/designs/picorv32a/src directory based on the file openlane/scripts/base.sdc for STA analysis.

```
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 24.73
#set ::env(SYNTH_DRIVING_CELL) sky130_vsdinv
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.653
set ::env(IO_PCT) 0.2
set ::env(SYNTH_MAX_FANOUT) 6

create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
set input_delay_value [expr $::env(CLOCK_PERIOD) * $::env(IO_PCT)]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $::env(IO_PCT)]
puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"

set_max_fanout $::env(SYNTH_MAX_FANOUT) [current_design]

set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]
#set rst_indx [lsearch [all_inputs] [get_port resetn]]
set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]
#set all_inputs_wo_clk_rst [lreplace $all_inputs_wo_clk $rst_indx $rst_indx]
set all_inputs_wo_clk_rst $all_inputs_wo_clk

# correct resetn
set_input_delay $input_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
#set_input_delay 0.0 -clock [get_clocks $::env(CLOCK_PORT)] {resetn}
set_output_delay $output_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]

# TODO set this as parameter
set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]
set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
puts "\[INFO\]: Setting load to: $cap_load"
set_load  $cap_load [all_outputs]

```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/8b8caaa3-70c0-48cb-bb2f-788eba6dda0e)

Then we will run pre design and synthesis with required changes.

```
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
run_synthesis
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/59023ded-eefb-42d2-866c-fd1a0709f60a)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/e293fa4f-1ffe-4b09-9a0a-0d8d000bb29a)

Now , we are ready to run STA for the changes we have done.

```sta pre_sta.conf```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/4cea7322-92dc-4b5e-86ef-1d75c43c9561)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6ffcdf9b-f070-4afe-9d91-0782269006ac)

### 4. Steps to optimize synthesis to reduce setup violations

Since increased fanout is causing more delay, we can add a parameter to reduce fanout and perform synthesis again.

```
prep -design picorv32a -tag 21-05_14-41 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
set ::env(SYNTH_MAX_FANOUT) 4
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6bbf3571-4c59-4ce2-a696-e9916d85a794)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/4635fa45-81ec-40b1-a7ba-6dc0e9a86b87)

Now we will re run ```sta pre_sta.conf```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/6c28d89f-1d3e-4a63-aab3-76b92b06d1a5)

In the report we can see that , an OR gate of drive strenght 2 is driving 4 fanouts.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/07f40b8c-ce08-4805-b767-cd0db13cd2fc)

Commands to analyze and optimize timing by replacing with an OR gate of drive strength 4.

```
report_net -connections _11672_
help replace_cell
replace_cell _14510_ sky130_fd_sc_hd__or3_4
report_checks -fields {net cap slew input_pins} -digits 4
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7671eb12-8b96-4458-8e16-8b75492dc4ec)

We can see overall slack reduced

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/11a1216b-f975-4573-a16d-9eac18a16127)

In the report we can see, Another OR gate of drive strength 2 is driving 4 fanouts

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/4ec6e77f-8b77-407e-9bef-e44852abe618)

Commands to analyze and optimize timing

```
report_net -connections _11675_
replace_cell _14514_ sky130_fd_sc_hd__or3_4
report_checks -fields {net cap slew input_pins} -digits 4
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7c86c406-8132-48d9-ae0e-e922389d6f2a)

We can see overall slack reduced again.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/786e2756-252a-4849-bd2a-587fec1f62a6)

### 5. Steps to do basic timing ECO

In the report we can see that , OR gate of drive strength 2 driving OA gate has more delay.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/3ddf88fc-c356-478f-82c2-c76877c077d3)

Commands to analyze and optimize timing

```
report_net -connections _11643_
replace_cell _14481_ sky130_fd_sc_hd__or4_4
report_checks -fields {net cap slew input_pins} -digits 4
```

We can see overall slack reduced again.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/34c296cc-18be-4710-8a21-8b1ab20e5f7e)

Another OR gate of drive strength 2 driving OA gate has more delay

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7e84f61c-c1e0-47cd-bade-3c0b30374a5e)

Commands to analyze and optimize timing

```
report_net -connections _11668_
replace_cell _14506_ sky130_fd_sc_hd__or4_4
report_checks -fields {net cap slew input_pins} -digits 4
```

We can see overall slack reduced again.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/64766039-50b3-4a93-9592-2b058505cf45)

Verify instance 14506 is replaced with sky130_fd_sc_hd__or4_4

```report_checks -from _29043_ -to _30440_ -through _14506_```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/eb7dcd72-ae9c-4f6d-9f86-e8d8d2be36b2)

In total of 1.2827 violation was reduced (23.90 - 22.6173)

### 6. Clock tree synthesis TritonCTS and signal integrity

Steps to run CTS using Triton

we wll replace the old netlist with the new one which was generated after after timing ECO fix.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/dcf31381-66f0-415a-93ea-8ef573b13d24)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/cee37ea0-3c18-49e7-bf09-fda576ea3aa5)

Now once all the required changes are done , we will not run synthesis again , 

We will run floorplan > Placement > cts.

command for CTS ```run_cts```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1b759662-cd04-4236-b131-162924cdc336)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/0ed392ac-80a6-4353-a7a5-0188965b6817)

We can see a CTS file is generated.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1edef4db-0ea4-45c5-88cd-1dd3a2324f7b)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/bef33b1c-d62d-4b95-a67c-de7e5c6dad46)

Steps to verify CTS runs

From the below commands we can verify the CTS operations

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/2eda28ad-b2d4-41de-9203-53f27f911f13)

```
echo $::env(LIB_SYNTH_COMPLETE)
echo $::env(LIB_TYPICAL)
echo $::env(CURRENT_DEF)
echo $::env(SYNTH_MAX_TRAN)
echo $::env(CTS_MAX_CAP)
echo $::env(CTS_CLK_BUFFER_LIST)
echo $::env(CTS_ROOT_BUFFER)
```

### 7. Timing analysis with real clock using openSTA

In this we will use "openroad" instead of "openSTA".
Open road can be invoked inside openlane

```openroad```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/a9d026bd-6771-41ac-a1b4-dc7f8ad9f466)

below are the commands to setup openroad.

```
read_lef /openLANE_flow/designs/picorv32a/runs/21-05_14-41/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/21-05_14-41/results/cts/picorv32a.cts.lef
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/21-05_14-41/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
help report_checks
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```
![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7be77789-23d0-43c6-b1f5-a5b103db997b)

Steps to execute OpenSTA with right timing libraries and CTS assignment.

Steps to observe impact of bigger CTS buffers on setup and hold timing

*****************************************************************************************************************************************************************************************************************************************

## **Day 4**

### 1. Steps to build power distribution network

command :  ```gen_pdn```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c055c9de-0327-4b5a-b0f1-cbca08fe2f88)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/499b2e8e-f3f1-4d7c-9ecf-072650548ecb)

Viewing the Floorplan with pdn init.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/a117ceb8-f9a2-447f-8999-8774e26b64da)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/43acae2d-5af3-4ceb-9223-8aeae9db772a)

### 2. Steps for Detailed routing using TritonRoute and explore the routed layout.

command : ```run_routing```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/65370927-6cb9-4898-846a-3276c8a17943)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/88eb34d6-97a2-4498-8eb4-f6c5b4fd3c4a)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/9aa7fb92-21fc-4816-8766-5bfc7e62e6d7)

We can see the routed layout using magic.

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/847d40af-440f-44e3-91a1-000185074503)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/ded637da-c2d4-48c1-a8c9-7ebd90e2be9b)

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/21-05_14-41/tmp/routing
gvim 20-fastroute.guide
```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/fea360fe-4c77-452b-8aaa-a12d11d76a32)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7b03a614-405b-4e58-81bd-57ba42b736fe)

### 3. Post-Route parasitic extraction using SPEF extractor & Final Layout.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/5c845b7a-910c-4447-bc70-d385b42e35df)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/1b9a2527-b2ea-487e-a85c-4b296ea29900)

### Final Layout - A Beauty ,A Art work

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/40c62d35-8470-4eab-9ed1-e630837da38e)

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/7a082cc4-f584-4501-8ab2-3310a81c43e8)













 


































































  
















































  
  









