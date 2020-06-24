![Image of rlab](https://i.ibb.co/xFQr6QW/Group-1.png)


# Authors

Todd Bryant, Katt Sullivan and Grant Ng

# From the RLab!

To learn more about us visit our website [here](https://www.rlab.nyc/)

## Description
Now with ARKit and an iPhone with a front-facing True Depth camera you can track your facial features allowing you animate digital avatars. The avatars first have to be prepared with point-level animation called blendshapes.  ARKit uses 52 of these to animate the avatar faces.  3D modelling is a craft that takes a long time to master and setting up all of these blendshapes can be daunting, so we’ve developed a workflow to ease the barrier to get your character up and running in a matter of minutes by levering two free avatar creation tools: Adobe Fuse and MakeHuman. Both programs have more than enough blendshapes to animate a face, the just need to be renamed to the ARKit conventions. We’ve developed a simple script to automate of lot of this process.

### Required Software To Be Installed: 
* Fuse downloaded from here: https://www.adobe.com/products/fuse.html
* Need to create a mixamo account (Its free!): https://www.mixamo.com/#/
* MakeHuman downloaded here: http://www.makehumancommunity.org/
* Maya student version download here: https://www.autodesk.com/education/free-software/maya
* Unreal downloaded here: https://www.unrealengine.com/en-US/get-now/agnostic
* Python download here: https://www.python.org/downloads/ **scroll all the way to see how to download properly!
### Software versions:
* Unreal version 4.24 
* Livelink app for iOS (Requires iOS 12.1 or later)
* Maya 2018 or 2019
* Blender 2.83
* Python 3.8  

This tutorial requires some knowledge of using 3D software and game engine mechanics. We will provide more links for beginners that walk you through a more in depth walkthrough. 

### This document will be divided up into sections and address the workflow for converting characters for Face Tracking in both MakeHuman and Fuse in parallel.
1. Exporting Blendshapes from character creator software and importing into Maya
   - Fuse to Mixamo
   - Mixamo to Maya
   - Editing Blendshapes in Maya from Fuse
   - MakeHuman to Blender
   - Blender to Maya
   - Editing Blendshapes in Maya from MakeHuman
   - Merging Blendshapes
2. Python Scripting
   - Knowledge and Filestructuring
   - Renaming the blendshapes
3. Importing in Unreal
   - Importing the FBX
   - Setting up blueprints in Unreal

# Importing and Exporting free 3D characters blendshapes with Maya

First steps you need to have the LiveLink app downloaded onto your iPhone before you start this tutorial. 
There are multiple ways to have a fully rigged character and have a facial rig set up in minutes. 

1. Exporting blendshapes from Fuse and MakeHuman and importing into Maya

#### Adobe Fuse to Mixamo: 
    - Once you have downloaded Fuse, go through the process of creating your custom character. Make your character look however you want. Keep the model simple and avoid facial hair or eyelashes. Once you are at the last step, Fuse has a button at the top of the screen to bring your character into Mixamo. Click on “send to mixamo”



# Python Setup 

Be sure to read our setup [here](https://github.com/RLabNYC/RLab_FaceTracking_RenameScripts)

# Importing into Unreal


