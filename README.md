![Image of rlab](https://i.ibb.co/3zsstG6/Group-3.png)


# Authors

Todd Bryant, Kat Sullivan, Grant Ng and Jiuxin Zhu

# From the RLab!

To learn more about us visit our website [here](https://www.rlab.nyc/)

## Fuse example (added eye movements) 

Here is our example of how the **Fuse** character will move and look like. **Be aware, Fuse will be discontinued by September 2020**

![gif of me](Media/rlabfuse.gif)


### Required Software To Be Installed: 
* Fuse downloaded from here: https://www.adobe.com/products/fuse.html
* Need to create a mixamo account (Its free!): https://www.mixamo.com/#/
* Maya student version download here: https://www.autodesk.com/education/free-software/maya
* Unreal downloaded here: https://www.unrealengine.com/en-US/get-now/agnostic
### Software versions:
* Unreal version 4.25 
* Live Link Face app for iOS (Requires iOS 13.0 or later). Compatable with iPhone, iPad, and iPod touch. 
* Maya 2018 or 2019 

This tutorial requires some knowledge of using 3D software and game engine mechanics. We will provide more links for beginners that walk you through a more in depth overview. 

# Importing and Exporting free 3D characters blendshapes with Maya

### For experienced individuals only!
If you are an already experienced in facial tracking, you can download this repo and it will be ready to work with the livelink app already!

# For Beginners
 - This repo is mainly for beginners who want to get into facetracking for personal projects, virtual production or just for fun. Please keep in mind that this repo is for the Unreal engine. 

 - First, you need to have the LiveLink app downloaded onto your iPhone before you start this tutorial. Then download or clone this repository somewhere on your computer. There are multiple ways to have a fully rigged character and have a facial rig set up in minutes. 

# Setting up with Fuse

**1. Exporting blendshapes from Fuse and importing into Maya**
   - **Adobe Fuse to Mixamo:**
   - Once you have downloaded Fuse, go through the process of creating your custom character. Make your character look however you want. Keep the model simple and avoid facial hair or eyelashes. Once you are at the last step, Fuse has a button at the top of the screen to bring your character into Mixamo. Click on “send to mixamo”. 

![mixamo screenshot](https://i.ibb.co/CM961X8/Annotation-2020-02-06-151238.png)

   - After you click on "send to mixamo", your internet browser will open up and Mixamo will open automatically. Once mixamo’s algorithm is finished rigging your character, you will see two dropdown selections on the bottom of the screen. 

   ![mixamo screenshot2](https://i.ibb.co/n30TyF1/Annotation-2020-02-06-151833.png)

# Exporting the blendshapes
   - **For the dropdowns:**
     - Make sure facial blendshapes are enabled.
     - Skeleton LOD 65 is fine for basic movement. 
     - Hit update rig button and you're free to download your character to your computer! 

Download your character as FBX. It should already be rigged and in a T-Pose.
   - **Mixamo to Maya**
	  -  Import the FBX into Maya. Choose the "Sculpting" layout from the top right "Workspaces" dropdown menu. It will change the layout of Maya to bring up the Blendshapes. This is a screenshot of what the blendshapes will come out as when you open the Fuse FBX file in Maya. You can drag the sliders for each shape and see how it affects the face mesh.
	

![maya screenshot](https://i.ibb.co/SXKrGzw/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-10-18-PM-2.png)

   - After the import in done, there are some textures are transparent. It is an easy fix!
	  - In Maya, just switch workspace modes to "maya classic".
	  - Then select the mesh and select the attribute editor tab on the far right and select the farthest tab. 
	  - You will see a transparency slider grayed out. Right click on it and select "break connection".
	  - And the texture will be fixed! 
	  

![maya screenshot](https://i.ibb.co/3BWk5bL/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-12-06-PM-2.png)

![maya screenshot](https://i.ibb.co/cTY1xX9/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-12-55-PM-3.png)

   - Apply the fix for all the meshes and switch back the workspace to "sculpting".
	  - **Editing Blendshapes in Maya from Fuse:**
If you select the face mesh, you will see all the targets for the facial movements. Fuse will give you three blendshape groups, the last group is the one you want to focus on. If you change the workspace in maya to "Sculpting", you will be able to see the amount of blendshapes easier. 

When you select the blendshape targets you can move the sliders back and forth and you will be able to see eye’s blinking and the mouth opening and closing. Once you have your character all set up in Maya, you can save this file as a Maya Ascii file. Make sure the file is saved with a .ma extension. Make a folder for this project and place this file in it.  For simplicity’s sake use a root directory (D:\BlendshapesFaceTracking) this is  important for the next steps that involve running a python script. 

On the right, you see the name “blendShape1” You can rename these groups like  “_ncl1_1”. The group of **“_ncl1_2”** is where most of the animations are. You need to rename the groups with circle square icons and a little “ +” sign next to it like “_ncl1_2” to Blendshape_[ name of mesh]. 

![Maya screenshot](https://i.ibb.co/D9QDx1n/Annotation-2020-02-27-110918.png)

   - **Merging Blendshapes in Fuse:**
	  - There are three blendshapes that need to be merged in maya, first, you need to identify.
	  - BrowsOuterLower_Lefft and BrowsOuterLower_Right.
	  - MouthNarrow_Left and MouthNarrow_Right.
	  - CheekPuff_Left and CheekPuff_Right.

Once you can see all the blendshapes, shown in the previous picture, scroll all the way down look for three type.

![Maya screenshot](https://i.ibb.co/jwNDpVd/Annotation-2020-02-27-125500.png)

In this example picture you want to select both the Left and Right blendshapes. Be sure to drag the toggles all the way to the right and select both Left and Right blendshapes and right click into one of them and select mirror targets. Once it is merged you need to find the name again, and rename it to cheekPuff, the name has to be exact!

   - **Repeat the process for all three, then rename the merged blendshape to the names in bold:**
	 - BrowsOuterLower_Lefft and BrowsOuterLower_Right = **browInnerUp**
	 - MouthNarrow_Left and MouthNarrow_Right = **mouthPucker**
	 - CheekPuff_Left and CheekPuffRight = **cheekPuff**

![Maya screenshot](https://i.ibb.co/2dZDwgv/Autodesk-Maya-2018-Educational-Version-E-Python-Sripts-Python-Sripts-fuse-RLab-ma-6-24-2020-8-23-29-PM-2.png)

## Setting Up Our Python Script in Maya will be the next steps!

## Link back to table of Content [Here](https://github.com/RLabNYC/RLab_Facetracking)

# For renaming blendshapes and importing into Unreal go to our [Next Steps](https://github.com/RLabNYC/Rlab_FaceTracking_fuse/blob/master/RUNSCRIPT.md).


