# Cliff-Tool

A cliff tool in Houdini based on Ubisoft Far Cry 5 procedural world generation.

## Presentation Slide

### [Here](https://docs.google.com/presentation/d/1ThLG4NI-RBY0QDLCUxiAr70xsRe6HJ0myi9M_S88cLg/edit?usp=sharing)

## Result

### Mesh

|High Res|Low Res|
|-|-|
|![](img/mesh_1.png)|![](img/mesh_2.png)|

### ID Map

|High Res|Low Res|
|-|-|
|![](img/id_1.png)|![](img/id_2.png)|

### Slope

|High Res|Low Res|
|-|-|
|![](img/slope_2.png)|![](img/slope_1.png)|

## Technical Detail

The cliff generation procedure is based on Ubisoft's GDC talk. Only five steps: **Slope Thresholding, Preparing Geometry, Stratification, Split, Shape Construction** are seleted to implement.

### Slope Thresholding

Points with high slope are selected into a group. The threshold is ajustable.

![](img/slope_thresh)

### Preparing Geometry

High-slope-points-containing primitives are selected to be remeshed and subdivided.

|Remesh|Subdivision|
|-|-|
|![](img/remesh.png)|![](img/subdivision.png)|

### Stratification

Primitives after remeshing and subdivision are then converted to point selection. Those points are selected by this [VEX code](VEX/straticification).

The idea is to generate layered and separated boxes to server a the bounding volume in order to select points on cliff.

|Box|Points Selected|
|-|-|
|![](img/stra_box.png)|![](img/stra_points.png)|

### Split

Points with high slope is divided into two goups according to 3D Perlin noise.

![](img/noise_grouping.png)

To have better orgnization, this step actually happens before the stratification step.

### Shape Construction

Shaper construction is extrusion + blur.

|Extrusion|Blur|
|-|-|
|![](img/extrusion.png)|![](img/blur.png)|

## Usability

### Parameter Exposion

The cliff generation network is wrapped in a subnetwork. The adjustable parameters are exposed to the subnetwork leve.

|Subnetwork|Cliff Params|
|-|-|
|![](img/subnetwork.png)|![](img/cliff_param.png)|

|Split Params|Peram Linking|
|-|-|
|![](img/split_param.png)|![](img/parameter_linking.png)|

### Height Field

Height field workflow is Houdini's most powerful terrain editing tool. The tool(as a subnetwork) takes a heightfield as an input.

|Height Field Input|
|-|
|![](img/heightfield_input.png)|


### Output

ID map, heightfield map and cliff mesh are baked using separated nodes. 


## Credits

- [Ubisoft GDC Talk](https://www.youtube.com/watch?v=NfizT369g60)

- [Ubisoft GDC Talk PDF](https://twvideo01.ubm-us.net/o1/vault/gdc2018/presentations/ProceduralWorldGeneration.pdf)

- [Far Cry 5](https://en.wikipedia.org/wiki/Far_Cry_5)
