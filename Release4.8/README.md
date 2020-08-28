# LS-PrePost 4.8

**Release Data**:

**Major new features of the 4.8 series, compared to 4.7:**

[toc]



## Geometry

1. Curve-Sketch

   Modify Ellipse editor in Curve-Sketch.

2. B-Spline Curve

   Draw aux projecting lines in B-Spline Curve->Respace Para.

<img src="pictures/bspline.png" alt="Alt text" style="zoom:75%;" />

3. Converting Ref-Coordinate System to keyword coordinate system in Feature Tree.

   <img src="pictures/convert_coord.png" alt="Alt text" style="zoom:75%;" />

4. Add “Standard”, “End Point Constraint” and “Mixed” three algorithm options into Shape Offset->Edge on Face.

5. Add Angle by 3 Points measure in Geometry Measure.

6. Add “Sweep Mode” in Curve->Middle Curve->Axis of Pipe to extract axis from FEM parts using sweeping algorithm.








## New keywords and improvement

### New keywords

**233 new keywords** have been added into LS-PrePost4.8. some of them has been added into LS-PrePost4.7. A lot of keyword have been updated. 

Four keyword groups have been added

* **BATTERY**

  The keyword *BATTERY provides input data for the electrochemistry solver

* **COSIM**

  The keyword *COSIM allows LS-DYNA to co-simulate with other software. Currently, co-simulation only works through the functional mock-up interface (FMI). 

* **DUALCESE**

  The keyword *DUALCESE provides input data for the dual Conservation Element/Solution Element (dual CESE) compressible fluid solver.

* **IGA**

  The *IGA keywords set up and control the isogeometric-related capabilities of LS-DYNA.

New keyword see [NewKeyword.pdf](https://github.com/LSPrePost-Development-Group/LSPrePost-Release/tree/master/Release4.8/NewKeyword.pdf)



### Keyword Reading 

1. speed up of reading keyword file by improve the process of remove space characters of each line.
2. speed up the process of include transform, especially for model which has too many *include_transform subsystems.
3. speed up the process of pre-comment.

---







## General Preprocessing

### Entity Display

support multiple ids in "Keyin" of entity selection panel

<img src="pictures/keyword_feature01.png" alt="Alt text" style="zoom:60%;" />

### Part SortBy

support popup keyword form when right click on the cell of SortBy dialog

<img src="pictures/keyword_feature02.png" alt="Alt text" style="zoom:60%;" />

### Entity Creation

support create *INITIAL_VELOCITY in EntCreation dialog

<img src="pictures/keyword_feature03.png" alt="Alt text" style="zoom:60%;" />

### Identify dialog: 

support pop-up keyword form of selected Entity(node/element/part)

<img src="pictures/keyword_feature04.png" alt="Alt text" style="zoom:60%;" />

Keyword Input Form

### support "PLOT" of *DEFINE_CURVE_DUPLICATE.

<img src="pictures/keyword_feature05.png" alt="Alt text" style="zoom:60%;" />

### Keyword Manager

right menu of *DEFINE_CURVE to load curve from xydata file, “Load Curve” will load curve data from file and create *DEFINE_CURVE, “Load curve to table” will also use these curve ids to create *DEFINE_TABLE.

<img src="pictures/keyword_feature06.png" alt="Alt text" style="zoom:60%;" />

### Model Compare

support "Diff Parts" on model compare dialog, compare the selected two models and find out parts that are different or only exist in one model, then highlight these parts and set others as transparent.

<img src="pictures/keyword_feature07.png" alt="Alt text" style="zoom:33%;" />

### Shell splitting

Description: split quad elements into tria elements so that their diagonals create a unionjack pattern.

<img src="pictures/shell_splitting_01.png" alt="Alt text" style="zoom:30%;" />

Advantage: this split seems to provide slightly better stability when we crush the honeycomb barriers.

Implement: this feature can be activated from “element editing dialog” -> ”Split/Merge” -> ”Split Operation:Shell” -> ”unoinjack icon”,if the additional “Propagate” checkbox is checked,the splitting will propagate to the entire part.

<img src="pictures/shell_splitting_02.png" alt="Alt text" style="zoom:30%;" />



### Set-segment creation

support element with both 8 or 20 nodes

<img src="pictures/set_segment_creation.png" alt="Alt text" style="zoom:60%;" />



### Find

Add CNRB option to find out CNRB as well when finding neighbor elements.

<img src="pictures/find_cnrb.png" alt="Alt text" style="zoom:60%;" />



### Dummy Position

support soft angle parameter (S. Limit = 1) for a child assembly



### Material Direction

mat-36E, mat-274



### Move Copy

support Penta element.



### Element Generation

1. Element Generation -> Shell -> Tunnel.

   Given a batch of section coordinates (such as X, Y or Z coordinates) and profiles’ parameters (such as circle’s area, radius, perimeter, or square’s area, side length, diagonal length), it construct a revolve shell mesh. Here provides a “Sample” button to load a sample data.

   <img src="pictures/element_generation01.png" alt="Alt text" style="zoom:75%;" />

   Here you can select “Tunnel Direction” to change revolve axis direction. Define “Segments” to set number of sampling points in section plane. Set “Extra Section” to interpolate more points in profile.

   <img src="pictures/element_generation02.png" alt="Alt text" style="zoom:75%;" />

   We also provide two options “Refit Section” and “Linear Profile”. “Refit Section” will fit a b-spline curve by raw section position. During meshing, all section points will be sampled from the b-spline curve and raw section points will not be kept. “Linear Profile” will sample profile points from polygon’s profile instead of b-spline profile.

   <img src="pictures/element_generation03.png" alt="Alt text" style="zoom:75%;" />

2. Element Generation -> Shell -> Fan Mesh.

   Given a center point and several boundary points, it construct a shell fan mesh.

   <img src="pictures/element_generation04.png" alt="Alt text" style="zoom:75%;" />

   To construct fan mesh easily, here we provide a “Auto Pave” option and “N-Side Center” button. In the following example, we pick three nodes to “Boundary Points”, and click “N-Side Center” to calculate the fan center, check “Auto Pave” to pave other nodes in fan mesh.

   <img src="pictures/element_generation05.png" alt="Alt text" style="zoom:75%;" />

3. Element Generation -> Shell -> Voxel Mesh

   Given several closed 2D curves, it construct a structure mesh on grids’ region. 

   <img src="pictures/element_generation06.png" alt="Alt text" style="zoom:75%;" />

   For curvature closed curves, we will try to fit a b-spline surface as background surface. The following pictures show voxel mesh from two closed curvature loops. To get better mesh result, you need to adjust “Rotation Angle” in view region.

   <img src="pictures/element_generation07.png" alt="Alt text" style="zoom:75%;" />

   To get boundary voxel mesh, check “Only Outline Voxel”.

   <img src="pictures/element_generation08.png" alt="Alt text" style="zoom:75%;" />

   It also can construct a structure mesh on the surfaces.

   <img src="pictures/element_generation09.png" alt="Alt text" style="zoom:75%;" />

4. Element Generation -> Solid -> Voxel Mesh

   Given a geometry solid shape, it construct a structure hex mesh on 3D grids’ region.

   <img src="pictures/element_generation10.png" alt="Alt text" style="zoom:75%;" />







## General Post-processing

### Vector Plot

print the vector scalar on the screen

<img src="pictures/vectorplot.png" alt="Alt text" style="zoom:60%;" />



### Measure

Measure->Area->Nd

<img src="pictures/measure_area_nd.png" alt="Alt text" style="zoom:48%;" />



### New XY Plot

1. support for the splitwindow state about "Plot" and "New" of history dialog.

2. support for draw the annotation in split window and main window by changing the annotation functions based on port area.

   <img src="pictures/newxyplot_01.png" alt="Alt text" style="zoom:75%;" />

3. support for the rubber band for annotation link line.

4. improve the annotation text boundary.

   <img src="pictures/newxyplot_02.png" alt="Alt text" style="zoom:75%;" />

5. support for the splitwindow state to fix "Comment by Shi. split window, draw histroy plot, then close lspp, crash".

6. support for the splitwindow state about "Plot" of history dialog. 

7. improve enter and exit annotation state both of them will refresh the xyplotting zone. 

8. support for showing the XYPlot on the split window state.

9. fix print bug when annotation notes on the screen.

10. Add the enter label callback function to improve the UE.

11. change default font size to smaller.

12. Add without arrow on annotation for like label to curve.

13. Add the boundary of label on annotation.

14. improve the move port on main when out of the main window boundary, Shift+ctrl+mouse left button to drag the port on main window.

15. improve the move port on main to add return default position function.

    <img src="pictures/newxyplot_03.png" alt="Alt text" style="zoom:60%;" />

16. support for the cross2d for all curves in different ports.

    <img src="pictures/newxyplot_04.png" alt="Alt text" style="zoom:60%;" />

17. Add the "X" button to exit window when crossing results. 

18. support for drawing the port with model when getting curves from external file.

19. [Bug 16213] New: Problem with x-axis label when saving FLD curve.



### Old XY plot

1. support for the crossing curves with different x range when interpolation.

2. support for the saej211.

   <img src="pictures/oldxyplot_01.png" alt="Alt text" style="zoom:60%;" />

3. support for interface of prepare for define curve.

4. support for the legend on XYPlot dialog and fix plotting csv file bug.

5. fix bug of loading the empty csv file.

6. Fix the filter problem when GUI operated and send command results are different.

7. improve the efficient problem of drawing all of curves in file.

---



### 3DGraphics

1. support for visualizing DEFIND_TABLE_2D.

2. support for visualizing DEFIND_TABLE_3D.

   <img src="pictures/3dgraphics_01.png" alt="Alt text" style="zoom:60%;" />

3. fix DefTable crashing bug when no data is loaded.

4. improve the GUI.



### NVH-panel contribution

Description: provide tools for acoustic panel contribution analysis.

Implement:this application can be activated from “LS-PrePost” -> “Main menu” -> “Application” -> “NVH“-> “Panel Contribution”

<img src="pictures/nvh_panel.png" alt="Alt text" style="zoom:33%;" />

1. Load binout file
2. Set the number of top contributions.Only the panels of which contribution ranked top “n” will be shown.For example,Enter “2” and press “Enter” button on the keyboard,only top 2 panels are displayed.
3. Select frequency.Three ways to select which frequency to show.
   * *Select frequency on the choice widget.*
   * *A sliding bar can be pulled back and forth to change the frequency.*
   * *A pair of buttons to select previous frequency and next frequency.*

4. Select field point.The data on this Field Point will be loaded and plotted.
5. XYplot window with panel contributions ratio for whole range of frequencies.
6. A circle to show the vector of panel contribution (magnitude and phase for each panel).
7. XYplot window with both magnitude and phase angles for whole range of frequencies.
8. A bin plot to show panel contribution percentage.



### Binout Fringe

1. Tprint Fringe

   fringe component->LSDA->Load.

   Type: switch element type.

   Index: switch ipts.

   For K file:

   Animate by fringe dialog animate bar.

   support step forward, step backward, stop operation.

   <img src="pictures/tprint_fringe.png" alt="Alt text" style="zoom:76%;" />

2. Elout Fringe

   fringe component->LSDA->Load.

   Type: switch element type.

   Index: switch ipts.

   For d3plot:

   animate by lspp Animate bar.

   For K file:

   Animate by fringe dialog animate bar.

   <img src="pictures/elout_fringe.png" alt="Alt text" style="zoom:75%;" />



### Fast Render

1. Modify light model of fast render mode to make it seems consistent with normal render. Remove highlight in previous state.

   <img src="pictures/fast_render.png" alt="Alt text" style="zoom:75%;" />

2. Tet10 render for fast render.


### S-ALE 

S-ALE data is much smaller the old type, LS-Prepost 4.8 fully support to read it, unpackage it, render, pick, and transparency.

<img src="pictures/sale01.png" alt="Alt text" style="zoom:75%;" />

<img src="pictures/sale02.png" alt="Alt text" style="zoom:75%;" />

<img src="pictures/sale03.png" alt="Alt text" style="zoom:61%;" />

### MS-Post

1. Follow Function

   support follow function for structural part for MS-POST. From Post->Follow set “Follow Point” or “Follow Plane”.

   <img src="pictures/ms_post01.png" alt="Alt text" style="zoom:61%;" />

2. Cylinder

   support cylinder section for MS-POST. Create a section plane on an object, switch section type to “cylinder”, set value of “radius”, then update the section plane.

   <img src="pictures/ms_post02.png" alt="Alt text" style="zoom:61%;" />

3. Fringe by Fringe Dialog

   fringe by fringe dialog for MS-POST. select the variable to be fringed, if this variable exists for multisolver part, it will be fringed, if not, the color will reset to original part color.

   <img src="pictures/ms_post03.png" alt="Alt text" style="zoom:61%;" />

4. MSASCII

   support icfd_steady_residual type for MSASCII plot. From MS-POST-> MSASCII, switch “file type” to “ICFD”, select “icfd_steadyresidual” from the list, load the file to be plot, the select variables to be plot.

   <img src="pictures/ms_post04.png" alt="Alt text" style="zoom:61%;" />



### Media Tool

1. Update media load panel, delete two media compare

   <img src="pictures/move01.png" alt="Alt text" style="zoom:48%;" />

2. Use a new control panel

   * *The new panel was divied to 3 parts. Each part has their own control button.*
   * *Left part is used to control media. User can change media start frame, last frame. So active frame could equal model active frame.*
   * *Right part is used to control model.*
   * *Common part: Used to control both Media and Model. Only media and model active frame equal, common part will be enable.*

   <img src="pictures/move02.png" alt="Alt text" style="zoom:48%;" />

3. Horizontal

   <img src="pictures/horizontal.png" alt="Alt text" style="zoom:60%;" />

4. Vertical

   <img src="pictures/vertical.png" alt="Alt text" style="zoom:61%;" />

5. Overlap

   <img src="pictures/Overlap.png" alt="Alt text" style="zoom:61%;" />

6. Add movie format(H264)



### Split Window

<img src="pictures/split_window.png" alt="Alt text" style="zoom:61%;" />







## General

### Sort by Size/Extend

Add “Sort by Size” and “Sort by Extend” options in Feature Tree (size Extend in X,Y,Z, Area, Volume, Length).

<img src="pictures/sort_by.png" alt="Alt text" style="zoom:75%;" />



### Color Box

Add color box in Feature Tree.



### Background Color

Add background color in Active Label.



### Statistical Information

List all parts’ elements and nodes number in Statistical Information panel when selecting multiple parts in Feature Tree.



### DES

overall support for genselect, fringe and history plot.



### Trace

Speed up the Trace Node for big model.



### Adaptive

support adaptive SPH model.



### View

Show Deleted Element Only and No Coord. Update.



### Section Plane

overall support for clip mode with beam, sph and deletion data.

---







## Scripting Command Language and Python Language

### Scripting Command Language

1. support for the "scalar" component name to get the node scalar and element scalar results.
2. support for element deletion.
3. update scl samples of control macro with file.
4. fix int array bugs to deep copy the int array results.
5. Save result node id of the command "ident xyzpt" to get ready for SCLCmdResultGetValue in SCL.
6. fix bug of xyplot related functions when no model loaded.
7. retrieve selected parts and nodes from genselect.

More examples see [SCLExamples](https://ftp.lstc.com/anonymous/outgoing/lsprepost/SCLexamples/SCL_Examples.zip)



### Python Language

At the moment, the Python language is also used as the scripting language of LS-PrePost. The user can use Python scripting in LS-PrePost. The Python modules that LS-PrePost provides include "DataCenter" and "LsPrePost", more details see [lsppscripting.pdf](https://ftp.lstc.com/anonymous/outgoing/lsprepost/SCLexamples/lsppscripting.pdf)

**How to use Python Scripting in LS-PrePost**

Firstly the user should set own Python home path(LS-PrePost4.8 only supports Python36) by using LS-PrePost command:

`setpythonhome "python/home/path"(like D:\Python36)`

<img src="pictures/python_01.png" alt="Alt text" style="zoom:75%;" />

The Python home path will be automatically saved to the config file.

And then run Python scripting with the regular LS-PrePost command, or within the command file, use the runpython command to execute the Python scripting, parameters can also be passed to the script.

The syntax:

`runpython "pythonscriptingname" optional parameters`

<img src="pictures/python_02.png" alt="Alt text" style="zoom:75%;" />

Example: the following command file will execute the script that creates a X-Y curve with the parameters defined in the command file.

```
parameter  pa 9.0E+07
parameter  pb 7000.0
parameter  pc  4.0E+07
parameter  npt  300
parameter  xmin  0.0
parameter  xmax  0.00126
runpython "customcurve.py"  &npt &pa &pb &pc &xmin &xmax
```

More examples see [PythonExamples](https://github.com/LS-PrePost/Release/tree/master/Release4.8/python_examples/)

---







##  Multiphysics Solution

### Open

1. Open the “Multiphysics Solution” interface by checking on the “Solution Explorer” item under the “View” menu.

   <img src="pictures/ms_open01.png" alt="Alt text" style="zoom:33%;" />

2. Pop up the solution explorer file operation menus by right clicking on the top tree item in the solution explorer.

   <img src="pictures/ms_open02.png" alt="Alt text" style="zoom:33%;" />

   * *“New Solution” can create a new solution file.*

   * *“Save Solution” can save the current solution data to the already named solution file.*

   * *“Save Solution As...” can save the current solution data to a new solution file with a new name.*

   * *“Load Solution...” can load a saved solution file to the solution explorer.*

   * *“Recent” can list the latest 5 opened solution files.*

   * *“Run” can open the “LS-Run” and call the “LS-DYNA” solver to solve the defined solution file.And this item can also save the solution data to a “.solution” file and a corresponding keyword file.*

   * *“Export Keyword File...” can save the solution data to corresponding keyword file.*



### Create New Solution

1. Select the “New Solution” menu item and pop up the “New Solution” interface.

   <img src="pictures/ms_create01.png" alt="Alt text" style="zoom:60%;" />

   * *This interface can name the new solution file and set the working directory.*

   * *When the current model data is not the correct one for the new solution file, user can use the “Keyword Data” option to load a keyword file.*

   * *The unit system is based on the loaded keyword file or the current opened model data in LS-Prepost.*

   * *Solution Explorer can support “Mechanical”, “ICFD”, “Thermal(structure)” and “Structured ALE” four case types. User can choose the right one to define the whole solution tree structure.*

     

### Solution Tree Structure

1. The tree structure contains three layers:

   * *The top layer is called “Multiphysics Solution”, in this layer user can set the unit system and keyword data version for the whole analysis.*

   * *The second layer is called “Case”.*

     <img src="pictures/ms_solution01.png" alt="Alt text" style="zoom:60%;" />

   * *Different cases have the same model data(the materials of parts in different case can have different properties.), connectors data and contact data if these tree items exist in one case. So the case operations in right-clicked menu of the case item can copy the case data to other cases which can be added before or after the current case. User can choose to call the “LS-DYNA” solver from any case by clicking on the “Run...” menu item. If user choose to run from a selected case, a “.lsda” file which is got from the previous case is necessary.*

   * *The third layer is different case types. Different case types may have different tree structures. User select correct case type when create a new solution file from the “New Solution” interface, LS-Prepost will build whole tree structure automatically.*

2. The solution data contains two parts, one is the tree node in the tree structure and the other one is called property gird which is attached to the corresponding tree node. User can select different tree nodes and set their related property data in the property gird.

   <img src="pictures/ms_solution02.png" alt="Alt text" style="zoom:60%;" />



### Mechanical and Thermal Case

1. For “Mechanical” and “Thermal” case types, the whole tree structure both contains three parts:Analysis, Model,Output. It can be built like the following picture.

   <img src="pictures/ms_mechanical01.png" alt="Alt text" style="zoom:60%;" />

2. In the “Analysis” item user can set the solver data, time step data, and integration data. For “Mechanical”, the solution only support the “Nonlinear Implicit” solver for now. If user select the “Mechanical” and “Thermal” case type, the tree data under the “Analysis” item is like what the picture shows.

3. The “Model” item contains fem model data, initial conditions data, boundary conditions data, prestress data, contact data, connector data.

   * *Different analysis type mean different boundary conditions data. The “Node Constraints”, “Force/Moments”,”Pressures” and ”Prescribed Motions” belong to “Mechanical” analysis. And “Convection”, “Temperature”, “Flux” and “Radiation” are related to “Thermal” analysis.*

   * *The material property in part item is defined by a new material library. In LS-Prepost executable folder, LS-Prepost add a sample material database file called “material.xml”. It is in XML and keyword format. Users can add their own material databases as the LS-Prepost “built-in” database format. The thermal material data will be shown when the thermal analysis exists in the solution tree structure.*

     <img src="pictures/ms_mechanical02.png" alt="Alt text" style="zoom:60%;" />

   * *Contact item only support “Sliding Contact”, “Tied Contact” and “Transducer” three types for now. The data for thermal analysis is in every contact item property gird.*

4. The “Output” item can output the defined “Node Data” and “Element Data” and some default result files like “glstat”, “rcforc”, “bndout”, ”spcforc”, “matsum”, “secforc” , “sleout” and so on.

5. For now, the post analysis is added into the property grid for part items and contact items. And user can switch the item property between “pre” and “post” button. If users change any “pre” data, they need to rerun the current case to update the post data. When users choose to rerun the case, the case data after the selected one will be updated too.

   <img src="pictures/ms_mechanical03.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_mechanical04.png" alt="Alt text" style="zoom:33%;" />

   

### ICFD

The ICFD type may build a tree structure as the following picture shown. It uses the same solution data format(tree nodes and related property grid). ICFD has its special items which are related to the ICFD analysis.

1. Now solution explorer supports these six analysis types, and they are “Turbulent”, “Thermal”, “FSI”, “DEM Coupling”, “Free Surface” and “RTM”. Different analysis types have different properties.

2. Users need to define their own materials under “Material” item and mesh data under the “Mesh” item.

3. The model data is came from the loaded keyword file in “New Solution” interface or the current opened model data in LS-Prepost.

4. In “Output” item, users can set the output result data for ICFD analysis.

5. Support the initial condition of "initial free surface" for ICFD Pre-processing in solution explorer.

   <img src="pictures/icfd_01.png" alt="Alt text" style="zoom:30%;" />

   * *Initial Free Surface is available if “Free Surface” is defined.*

   <img src="pictures/icfd_02.png" alt="Alt text" style="zoom:30%;" />

   * *Generated an initial levelset surface by a box*

   <img src="pictures/icfd_03.png" alt="Alt text" style="zoom:30%;" />

   * *The defined box will be drawn on the canvas*

### Structured-ALE

The Structured-ALE type may build a tree structure using the same solution data format(tree nodes and their related property grid) as the following picture shown.

<img src="pictures/ms_structuredALE01.png" alt="Alt text" style="zoom:60%;" />

1. If users want to do a “FSI” analysis, they need to load the fem keyword data when create the new solution file or use the already opened model data in LS-Prepost. The “FSI” analysis data can be set under the “FSI” items.

2. The “Trim”, “Volume-Filling”, “Initial Conditions” ,“Boundary Conditions” are all based on the defined “Mesh”. And the properties about the mesh is like below picture.

   <img src="pictures/ms_structuredALE02.png" alt="Alt text" style="zoom:33%;" />

3. The “Boundary Conditions” can support six different types: “Pressure”, “Node Constraint”, “Prescribed Motion”, “Ambient Element”, “Hydro static” and “Non Reflecting”.

   

### Solution Property

Solution explorer defines some properties which will call the LS-Prepost other powerful functions.

1. Define Set Data: clicking the first button will list all defined set data in current model and clicking the second button will confirm what data users have selected on the model.

   * *Node Set:* 

     <img src="pictures/ms_property01.png" alt="Alt text" style="zoom:60%;" />

   * *Part Set:* 

     <img src="pictures/ms_property02.png" alt="Alt text" style="zoom:60%;" />

   * *Shell Element Set:* 

     <img src="pictures/ms_property03.png" alt="Alt text" style="zoom:60%;" />

   * *Segment Set:* 

     <img src="pictures/ms_property04.png" alt="Alt text" style="zoom:60%;" />

2. Define Local Coordinate System: clicking the first button will list all the defined local coordinate system in current model and clicking the second button will pop up the “Define Local Coordinate System” interface. 

   <img src="pictures/ms_property13.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property05.png" alt="Alt text" style="zoom:60%;" />

3. Define Material: clicking the button will pop up the “Material Library” interface and list all the material databases in LS-Prepost.

   <img src="pictures/ms_property14.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property06.png" alt="Alt text" style="zoom:60%;" />

4. Define Curve: clicking the first button will switch current property among constant, curve, curve function, function four types, and clicking the second button will list all the defined curve data, clicking the third button will pop up a interface to input all the curve data.

   <img src="pictures/ms_property07.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property08.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property09.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property10.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property11.png" alt="Alt text" style="zoom:60%;" />

   <img src="pictures/ms_property12.png" alt="Alt text" style="zoom:60%;" />

---





## ASCII and Binout

### ASCII

1. support for the new component in the sbtout branch.

   <img src="pictures/ascii_01.png" alt="Alt text" style="zoom:60%;" />

2. support for PBLAST_SENSOR branch.

3. support for swfore about OPT=9 of *MAT_100.

4. fix crashing bug when elout including Elastic materials have no history variables.

5. fix boundary array problem.

6. fix problem of FreeNSetAsciiMemory.



### Binout

1. support for the new component in the sbtout branch. 

   <img src="pictures/binout_01.png" alt="Alt text" style="zoom:60%;" />

2. support for the sphflow branch.

3. support for pblast_sensor branch.

4. support for the hex assembly with binout of area selection.

5. Model selection the spotweld to highlight binout dialog's id list related and highlight on model when selected on binout dialog id list.

   <img src="pictures/binout_02.png" alt="Alt text" style="zoom:75%;" />

6. support for highlight the define coordinate entity when clicking the swforc solid assembly.

7. support for picking define coordinate and update the binout swforc id list.

8. support for outputting curvout to ascii file.

9. fix the rwforc bug when multiple selecting ids and components.

10. fix the bug of showing curve after the element is deleted.

11. update l2a for sphflow and pblast_sensor branches.

12. [Bug 16272] New: lspp fails to read a large binout file Ticket#2019120410000167

13. fix bug of selected multiple components to plot set id data.

14. Disbout: consider deletion data in plotting disbout components.

---



## Femzip

1.  improve the efficient problem of loading the first state to draw model.
2.  fix problem of loading model and fringe.
3. fix crash of setting the SPH surface.
4.  support progress bar in reading file.

---



## File Reading and Writing

1. Optimize STL writer module for large model.
2. Support loading batch of STL files.
3. Apply multi-thread tessellation during reading IGA pre model.



## Command File

1. Retrieve ids with “#var1,#var2 or #var3” appearing in the command statement after issuing command “range identmax 3”



