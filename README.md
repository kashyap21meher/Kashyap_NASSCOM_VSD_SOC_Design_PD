# Kashyap_NASSCOM_VSD_SOC_Design_PD

**Introduction**

This workshop offers hands-on experience designing an Application Specific Integrated Circuit (ASIC) using open-source processes. I will learn about physical design and how to create a chip layout, going from a high-level description (RTL) to a final design file (GDSII) suitable for fabrication. The workshop leverages Google's open-source resources for the design process.
This workshop will use OpenLANE and Sky130 nm PDK to generate standard cells.

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/2b2c1f19-45db-4cb2-9b61-a31ce33678ee) 

Below, I will upload the lab contents of what I have learned in this workshop.

**Day 1**

1.Locating Openlane work Directory and exploring files.

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

Therefore, Sky130_fd_sc_hd describes a collection of high-density, pre-designed digital circuit elements built by SkyWater Foundry using their 130nm process. This library allows designers to quickly and efficiently create complex digital circuits.

2. Invoking OpenLANE 

First, navigate to the directory where OpenLANE is located:

```cd Desktop/work/tools/openlane_working_dir/openlane/```

Then, use the `docker` command to invoke OpenLANE:

```docker```

To open OpenLANE in interactive mode, use the following command:

```./flow.tcl -interactive```

![image](https://github.com/kashyap21meher/Kashyap_NASSCOM_VSD_SOC_Design_PD/assets/169720302/c5ab3bd8-baed-49a3-8c3a-6ab6ea260ec8)

3. 









