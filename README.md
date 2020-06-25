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
   - Adobe Fuse to Mixamo: 
   - Once you have downloaded Fuse, go through the process of creating your custom character. Make your character look however you want. Keep the model simple and avoid facial hair or eyelashes. Once you are at the last step, Fuse has a button at the top of the screen to bring your character into Mixamo. Click on “send to mixamo”

![mixamo screenshot](https://i.ibb.co/CM961X8/Annotation-2020-02-06-151238.png)

   - After you click on send to mixamo, your internet browser will open up and Mixamo will open automatically. Once mixamo’s algorithm is finished rigging your character, you will see two dropdown selections on the bottom of the screen. 
   
   ![mixamo screenshot2](https://i.ibb.co/n30TyF1/Annotation-2020-02-06-151833.png)

   -For the dropdowns:
     - Make sure facial blendshapes are enabled
     - Skeleton LOD 65 is fine for basic movement. 
     - Hit update rig button and you're free to download your character to your computer! 

Download your character as FBX. It should already be rigged and in a T-Pose.
   - Mixamo to Maya
	  -  Import the FBX into Maya. Choose the Sculpting layout from the top right Workspaces dropdown menu. It will change the layout of Maya to bring up the Blendshapes. This is a screenshot of what the blendshapes will come out as when you open the Fuse FBX file in Maya. You can drag the sliders for each shape and see how it affects the face mesh
	  
![maya screenshot](https://i.ibb.co/SXKrGzw/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-10-18-PM-2.png)

	

# Python Setup 

Be sure to read our setup [here](https://github.com/RLabNYC/RLab_FaceTracking_RenameScripts)

# Importing into Unreal


