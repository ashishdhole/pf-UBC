<div style="display: flex; align-items: center; gap: 20px; justify-content: left;">
  <img src="/images/logo.png" alt="pf-UBC Logo" class="float-glow-img" width="100">
  <h1 style="margin: 0; font-size: 3em; color: #000000; font-weight: bold;">pf-UBC</h1>
</div>

##<span style="font-size: 1.2em; color: #000000;">Contents of the package</span>
<p style="text-align: justify; text-indent: 2em;">
The pf-UBC (Phase-Field at UBC) simulation toolkit is structured for clarity, modularity, and ease of use. Below is an annotated breakdown of the directory hierarchy:
</p>
<pre>
<span style="color:#ff0000;">             ┌─ <b>pf-UBC</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#ff6600;"><b>Makefile</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#228B22;"><b>launcher</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#0066cc;"><b>bin</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#009999;"><b>generate_micro.sh</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#009999;"><b>generate_micro_3d.sh</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#009999;"><b>gg_run.sh</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#9900cc;"><b>grain_growth.cpp</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#009999;"><b>abnormal_gg_run.sh</b></span>
<span style="color:#ff0000;"> root_folder │     ├─</span> <span style="color:#9900cc;"><b>abnormal_grain_growth.cpp</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#009999;"><b>real_gg_run.sh</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#9900cc;"><b>real_grain_growth.cpp</b></span>
<span style="color:#ff0000;">             │     ├─</span> <span style="color:#009999;"><b>gg_run_3d.sh</b></span>
<span style="color:#ff0000;">             │     └─</span> <span style="color:#9900cc;"><b>grain_growth_3d.cpp</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#009999;"><b>cluster_install.sh</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#009999;"><b>submit.sh</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#009999;"><b>real_submit.sh</b></span>
<span style="color:#ff0000;">             |  ├─</span> <span style="color:#009999;"><b>abnormal_submit.sh</b></span>
<span style="color:#ff0000;">             |  └─</span> <span style="color:#009999;"><b>submit_3d.sh</b></span>
</pre>


##<span style="font-size: 1.2em; color: #000000;">Summary of `pf-UBC` Directory Structure</span>

--> `bin/` — Simulation Scripts & Executables
Contains all executable scripts and C++ simulation code, **clearly organized by simulation type (2D, 3D, abnormal, realistic)**:

- `grain_growth.cpp` → 2D simulation
- `grain_growth_3d.cpp` → 3D simulation
- `abnormal_grain_growth.cpp` → Abnormal grain growth
- `real_grain_growth.cpp` → Realistic grain growth
- Accompanied `.sh` scripts for each type automate execution

--> `Makefile` — Build Automation
Simplifies compilation of all simulation binaries with a single command:

--> `launcher` — Intractive launch execution
launcher serves as the entry point or interface script to guide users through simulation setup.

--> `shell sripts` — Cluster submission scripts
Cluster support is integrated via the submit.sh scripts and cluster_install.sh, making the package suitable for both local and high-performance computing environments.


##<span style="font-size: 1.2em; color: #000000;">Installation</span>
After downloading the simulation toolkit folder from the repository, follow the folling command inside the `pf-UBC` folder
```
make install
```
This will check for all the required packages and if any on them are not installed already it will prompt the user to install on the local system. `cluster_install.sh` make all the shell scripts executable for smooth operation of the toolkit.


##<span style="font-size: 1.2em; color: #000000;">Running Conditions</span>
`pf-UBC` runs on all threads by default. The actual number of threads to use can be set at run stage, using the `OMP_NUM_THREADS` environment variable, as in
```
export OMP_NUM_THREADS=8
```
The environment variable is unset by default.


##<span style="font-size: 1.2em; color: #000000;">Launching the Toolkit</span>
Once the toolkit is successfully installed, you can start the toolkit using launcher file.
```
./launcher
```
You will see the following screen on the terminal.
```

░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░

        Phase-Field Grain-Growth Toolkit       

░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░

 Generate Microstructure 
 1) Generate 2d microstructure
 2) Generate 3d microstructure

 Generate Input Files 
 3) Create model input file
 4) Create real input file

 Grain Growth Models 
 5) Run model grain-growth simulation
 6) Run model 3d-grain-growth simulation
 7) Run abnormal grain-growth simulation
 8) Run real grain-growth simulation

 Exit! 
 9) Exit

░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░▒░

Enter choice [1-9]: 

```

You will observe that there are three sections in the launcher

- Generate Microstructure
- Generate Input Files
- Grain Growth Models

Each section perform the operation as mentioned. The toolkit is made in such a way that you don't have to strictly follow the steps. For example, if you already have a microstructure and an input file ready, you can straight away perform the required grain growth simulation by choosing between 5-6. After every operation, the launcher will show main screen again unless `9) Exit` is chosen.


##<span style="font-size: 1.2em; color: #000000;">Generate Microstructure</span>
Generate Microstructure is a python based tool to create a microstructure of desired domain size and number of grains. By default the domain follows periodic boundary conditions in all directions and cannot be changed from the toolkit. But interested users can do madification in `bin/generate_micro.sh` or `bin/generate_micro_3d.sh` files. 
<br>
This section has two sub-sections
```
 Generate Microstructure 
 1) Generate 2d microstructure
 2) Generate 3d microstructure
```
In `Generate 2d microstructure`, three files are generated, `micro.txt` (Grain ID map — each element in the array represents a grain label (an integer) at a grid point.), `micro.png` and `friction.txt` (A scalar field file representing the spatial distribution of friction pressure or drag resistance, used to control the local evolution of grain boundaries or transformation fronts.). Seed will asked down the line for repeatability.

In `Generate 3d microstructure`, only one vtk file will be generated.

<strong>Note</strong>: You can use the `Generate 3D microstructure` option to create both 2D and 3D initial microstructures by selecting the appropriate configuration. This gives users the flexibility to choose the output format—either .png or .vti — which will be saved in the results/ folder once the simulation begins.

If the user wishes to use another method to generate the initial microstructure, they may do so. However, they must convert it into a Grain ID map, where each element in the array represents a grain label (an integer) at a grid point. The file must be renamed to `micro.txt` (or `micro.vtk`) and saved in the root folder of the toolkit. The toolkit reads only `micro.txt` or `micro.vtk` as valid microstructure inputs.


##<span style="font-size: 1.2em; color: #000000;">Generate Input Files</span>
