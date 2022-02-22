# Blender-Non-Destructive-Workflow
Guide to Non-Destructive Workflow for Hard-Surface Modelling and Sculpting. Some shurtcuts, Modifiers, and how to fix weird issues


## Modifiers
### General Mesh Manipulation
- **Mirror =** Mirrors an object across X, Y, or Z Axis
- **Subdivision Surface =** Create higher resolution by adding points between existing vertices
### Hard-Surface Modelling
- **Edge Split =** Used to define where smooth shading stops (Also see *Mark Sharp*)
- **Screw =** Create a full object from an edge (Imagine a triangle turning into a pizza from a spiral). Turn on Calc Order and Flip
- **Bevel =** Add Bevel to edges. Turn off Clamp Overlap, Profile: 1
### Sculpting
- **Multiresolution =** Like Subdivision, but in steps. Preserves the lower Subdivisions, and can go back and forth between them. Rebuild Subdivisions can be used to Remesh or Retopologize Higher poly models


## General Mesh Manipulation
### Combining Vertices
- **Method 1.**
  - Click vertices
  - press M to merge
  - Merge at center
- **Method 2.**
  - Go to Tools
  - Options
  - Automerge
  - Turn Snap on > Set to Vertex
  - Press GG to slide vertex to the other vertices

### Extrude Along Normals
- Alt + E
- Extrude Along Normals

### Joining Objects
- Shift Click 2 objects (The order is important, last object is the destination object)
- Press E

### Seperating Objects
- Select Faces
- Press P > Seperate by selection

### Select Similiar
- Select an edge
- Shift + G
- Crease, Seam, Sharpness

### Fix Circle Merged at Center
- Select the weird faces
- Dissolve Edges
- Poke Face

### Apply All modifiers
- Select All (Press A)
- Space or F3
- Search "Convert to Mesh"
  - Or Menu > Object > Convert to > Mesh


## Hard-Surface Modelling
### Sharpening Edges
- **Mark Crease =**
  - Shift + E
  - Controls how strong an edge is affected by Subdivision Modifier
- **Mark Sharp =**
  - Can also use *Edge Split Modifier*
  - Used to define where smooth shading stops

### Smooth Shading
- Click the object
- Go to Object Data > Normals
  - Or right click your object, and Shade Smooth (Turns on the same setting)

### Average Normals (Weird shading)
- Select everything (Press A)
- Mesh > Normals > Average > Face Area
  - Or Shift+N

### Working from Low Poly (Non-destructive)
1. Make a low poly model
2. Subdivision Surface Modifier > Viewport: 2
3. Turn on *Uncage*
4. Select Edges and *Mark Crease*
5. Shade Smooth (This will look weird)
6. Two ways to fix this
   1. Select the same edges and *Mark Sharp*
   2. Use the *Edge Split Modifier*


## Sculpting
### Shrinkwrap Low Poly to High Poly
- Object Data
  - Normals > Turn Off Auto Smooth
  - Remesh > Smooth Normals
- Shrinkwrap Modifier
  - Wrap Method: Project
  - Axis: Positive & Negative
  - Target: High poly model
  - Turn on *Uncage*
- Multi-Res Modifier
  - Put it above the Shrinkwrap
  - Subdivide 3 times
- Apply the Shrinkwrap modifier

### Sharpening Edges
- **Mesh Filter Tool**
  - Go to Sculpt Mode
  - Pick the Mesh Filter Tool
  - Drag the cursor from Left to right until you get the desired sharpness
  - This tool also has *Delay Viewport updates*, to reduce the amount of times Blender re-renders the high-poly mesh when moving around the viewport

### Retopology
- **Method 1.** *Multi-res Modifier*
  - Rebuild Subdivisions
- **Method 2.** *Voxel Remesh*
  - Go to Sculpting Mode
  - Remesh Menu
  - Select the resolution
  - Remesh
- **Method 3.** *Instant Meshes*
  - https://github.com/wjakob/instant-meshes
