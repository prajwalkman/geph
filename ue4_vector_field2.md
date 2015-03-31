In Editor Vector Field Design for UE4
=====================================

Goal: To expose an interface in UE4 that allows developers to author and modify vector fields entirely within UE4, by placing primitives / splines within a bounding box, which affect the voxels inside to create a vector field.

SubTasks:
---------

* Reverse engineer the `.fga` vector field file type (refer UE4 plugin for Maya).
* Implement Vector Field generation by extending base mesh/box classes.
* Implement an editor tab/window to expose all necessary features/options.

Stretch goals:
--------------

* Investigate if the vector field can be modified at run time (not rotation/translation of the bounding box, but actual modification of vector fields inside it). If possible, this would be a completely new feature for UE4.


Implementation:
---------------

* First version will be a editor plugin based on Rama's editor extension template. This version will be authoring the vector field within the scene view.
* Second version will use info from Twitch broadcast on UE4 editor extension to build a separate editor window for this.
* The actual generation will work by creating new classes deriving from `FBoxCenterAndExtent` (boundingBoxes), and `UStaticMesh` (primitives), and raymarching within the bounding box.


References:
-----------

* Rama's editor extension template (https://wiki.unrealengine.com/Rama%27s_Vertex_Snap_Editor_Plugin#Core_of_Making_Your_Own_Editor_Mode)
* Basic intro to gpu particles in UE (http://youtu.be/DcesEW380lc)
* More detailed video of making and using vector fields (http://youtu.be/POyYZJWPVng)
* A much longer video about extending the UE4 editor (http://youtu.be/zg_VstBxDi8)
* UE4 Maya Velocity Grid exporter (UnrealEngine\Engine\Extras\MayaVelocityGridExporter\)
