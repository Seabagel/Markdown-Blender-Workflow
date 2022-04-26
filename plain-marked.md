# Blender-Non-Destructive-Workflow
Guide to Non-Destructive Workflow for Hard-Surface Modelling and Sculpting. Some shurtcuts, Modifiers, and how to fix weird issues

## Modifiers
### General Mesh Manipulation
  - Mirror = Mirrors an object across X, Y, or Z Axis
  - Subdivision Surface = Create higher resolution by adding points between existing vertices
  ### Hard-Surface Modelling
  - Edge Split = Used to define where smooth shading stops (Also see Mark Sharp)
  - Screw = Create a full object from an edge (Imagine a triangle turning into a pizza from a spiral). Turn on Calc Order and Flip
  - Bevel = Add Bevel to edges. Turn off Clamp Overlap, Profile: 1
  ### Sculpting
  - Multiresolution = Like Subdivision, but in steps. Preserves the lower Subdivisions, and can go back and forth between them. Rebuild Subdivisions can be used to Remesh or Retopologize Higher poly models


## General Mesh Manipulation
### Combining Vertices
- Method 1.
  - Click vertices
  - Press M to merge
  - Merge at center
- Method 2.
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
- Mark Crease =
  - Shift + E
  - Controls how strong an edge is affected by Subdivision Modifier
- Mark Sharp =
  - Can also use Edge Split Modifier
  - Used to define where smooth shading stops

### Smooth Shading
- Click the object
- Go to Object Data > Normals
  - Or right click your object, and Shade Smooth (Turns on the same setting)

### Average Normals (Weird shading)
- Select everything (Press A)
- Mesh > Normals > Average > Face Area
  - Or Shift + N

### Working from Low Poly (Non-destructive)
1. Make a low poly model
2. Subdivision Surface Modifier > Viewport: 2
3. Turn on Uncage
4. Select Edges and Mark Crease
5. Shade Smooth (This will look weird)
6. Two ways to fix this
   1. Select the same edges and Mark Sharp
   2. Use the Edge Split Modifier


## Sculpting
### Shrinkwrap Low Poly to High Poly
- Object Data
  - Normals > Turn Off Auto Smooth
  - Remesh > Smooth Normals
- Shrinkwrap Modifier
  - Wrap Method: Project
  - Axis: Positive & Negative
  - Target: High poly model
  - Turn on Uncage
- Multi-Res Modifier
  - Put it above the Shrinkwrap
  - Subdivide 3 times
- Apply the Shrinkwrap modifier

### Sharpening Edges
- Mesh Filter Tool
  - Go to Sculpt Mode
  - Pick the Mesh Filter Tool
  - Drag the cursor from Left to right until you get the desired sharpness
  - This tool also has Delay Viewport updates, to reduce the amount of times Blender re-renders the high-poly mesh when moving around the viewport

### Retopology
- Method 1. Multi-res Modifier
  - Rebuild Subdivisions
- Method 2. Voxel Remesh
  - Go to Sculpting Mode
  - Remesh Menu
  - Select the resolution
  - Remesh
- Method 3. Instant Meshes
  - https://github.com/wjakob/instant-meshes


### Brush Setting
- Brush > Accumulate: So the brushes would add to the previous stroke continuously
- Falloff: Change the shape and roundness of brush
- Smooth Stroke
- 

## Hair Modelling
### Skin Modifier
- Preferences > Enable Extra Meshes
- Add a single vertices
- Start making a path
- Add Skin Modifier (It'll look like a rectangle)
- Add Subdivision Modifier (This makes the shape rounder)
- Press Ctrl + A to adjust the thickness

### Bezier Curve
- Create a Bezier curve, and shape it to a triangle (Sharp on the top, smooth on the side/bottom, this is the shape of the hair)
- Create a Nurbs Path (Or just a simple path, Curves are harder to control)
- Copy the shape of the Bezier curve to the Nurbs Path
  - Click the path mesh object, switch to Edit mode
  - Under the Object Data Properties, find the Geometry drop down
  - Under Geometry, click on Bevel
  - Switch to Object
  - Change the object to the Bezier Curve you've created
  - Enable Fill Caps so the model isn't hollow/tubular
- Press Ctrl + T  to Twist the hair
- Press Alt + S to make the hair thicker or smaller


## Z-Brush Brushes in Blender
- [Armored Colony - hPolish and Planar sculpting brushes in Blender](https://www.youtube.com/watch?v=gIujBF74FQg)

### hPolish Brush
- Use Scrape Brush
- Duplicate the default preset
- Plane trim = 0.2 m (Controls how deep from the point gets affected)
- Normal Radius = 0.06 (Controls how far the brush radius average the normals)

### Planar
- Use Scrape Brush
- Duplicate the default preset
- Under Advanced, turn ON Use Original Normal and Plane 
- Plane Offset = 0.1 m
- Optional:
  - Hardness = 0.9
  - Under Stroke, Spacing = 4%
  - Turn on Adust Strength for Spacing

## Default Blender Brushes explained (40+ brushes)
- Note: Some brushes are a combination of two/more brushes
- [Noggi - Every Blender Sculpting Brush Explained in 13 Minutes](https://www.youtube.com/watch?v=eFhXnUoxCjw)

### Draw Brush
- Draw = Most basic brush, round shape
  - Draw Sharp = Sharper falloff
  - Clay Strips = Square shape
- Clay Thumb = Pushes mesh like a thumb

### Layer Brush
- Layer = Draw with a consistent height, Persistent option caps how far it can pull the mesh

### Smooth Brush
- Smooth = Smooths jagged meshes
  - Deformation Laplacian smooths the surface and volume, and Surface smooths while perserving volume

### Fill Brush
- Fill = Fills gaps between two different heights to the average height
- Scrape = Like Fill, but moves vertices above it into the average height
  - Invert to Fill setting lets you switch between the Fill and Scrape brush using the Ctrl key

### Pinch Brush
- Pinch = Moves vertices closer to the center of the brush
- Rotate
- Slide Relax - Moves geometry to areas to sculpt that requires more detail, Holding Shift relaxes to sculpt

### Grab Brush
- Grab = Moves the mesh towards the cursor
  - Grab Silhouette constricts the movement to the edge of the visible mesh
- Elastic Deform = Like Grab, but for bigger movement
- Snake Hook - Grabs the mesh and pulls it, but also rotation is included
  - Magnify controls how much volume is lost each stroke
  - Rake controls how much rotation is lost each stroke
  - Deformation Elastic and Deform
- Thumb = Like Clay Thumb but sticks to the surface, without adding volume
- Pose Brush = Moves geometry based on the bones of the object's Armature
  - Deformation includes Rotate/Twist, Scale/Translate, Squash/Stretch
  - Rotation Origins rotates from:
    - Topology (which is automatic based of the volume of the sculpt)
    - Face Sets, which detirmines one bone per Face sets
    - Face Sets FK, which applies Forward Kinematics
  - Lock Rotation When Scaling locks the Axis of the bone when deforming
- Boundary = Detects unconnected edges, and deforms them. Relies on good topology to get good results
  - Deformations include:
    - Bend
    - Expand
    - Inflate
    - Grab
    - Twist
    - Smooth
  - Boundary Fallof detirmines how the Falloff is applied to the edge:
    - Constant = The entire edge
    - Brush Radius = The radius of the brush
    - Loop = Loops the radius of the brush on the entire edge
    - Loop and Invert = Inverted Loop

### Cloth Brush


### Combination Brushes
- Flatten = Combines the Fill and Scrape into one brush
- Clay = Combines the Flatten and Draw brushes
- Multi-plane Scrape = Uses 2 planes to scrape a surface
- Crease = Combines Punch and Draw sharp brush
