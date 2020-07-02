![Image of rlab](https://i.ibb.co/3zsstG6/Group-3.png)


# Authors

Todd Bryant, Katt Sullivan and Grant Ng

# From the RLab!

To learn more about us visit our website [here](https://www.rlab.nyc/)

## Description
Now with ARKit and an iPhone with a front-facing True Depth camera you can track your facial features allowing you animate digital avatars. The avatars first have to be prepared with point-level animation called blendshapes.  ARKit uses 52 of these to animate the avatar faces.  3D modelling is a craft that takes a long time to master and setting up all of these blendshapes can be daunting, so we’ve developed a workflow to ease the barrier to get your character up and running in a matter of minutes by levering two free avatar creation tools: Adobe Fuse and MakeHuman. Both programs have more than enough blendshapes to animate a face, the just need to be renamed to the ARKit conventions. We’ve developed a simple script to automate of lot of this process.

![gif of me](ft5.gif)

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

First steps you need to have the LiveLink app downloaded onto your iPhone before you start this tutorial. Then download or clone this repository somewhere on your computer. 
There are multiple ways to have a fully rigged character and have a facial rig set up in minutes. 

**1. Exporting blendshapes from Fuse and importing into Maya**
   - **Adobe Fuse to Mixamo:**
   - Once you have downloaded Fuse, go through the process of creating your custom character. Make your character look however you want. Keep the model simple and avoid facial hair or eyelashes. Once you are at the last step, Fuse has a button at the top of the screen to bring your character into Mixamo. Click on “send to mixamo”

![mixamo screenshot](https://i.ibb.co/CM961X8/Annotation-2020-02-06-151238.png)

   - After you click on send to mixamo, your internet browser will open up and Mixamo will open automatically. Once mixamo’s algorithm is finished rigging your character, you will see two dropdown selections on the bottom of the screen. 
   
   ![mixamo screenshot2](https://i.ibb.co/n30TyF1/Annotation-2020-02-06-151833.png)

   - **For the dropdowns:**
     - Make sure facial blendshapes are enabled
     - Skeleton LOD 65 is fine for basic movement. 
     - Hit update rig button and you're free to download your character to your computer! 

Download your character as FBX. It should already be rigged and in a T-Pose.
   - **Mixamo to Maya**
	  -  Import the FBX into Maya. Choose the Sculpting layout from the top right Workspaces dropdown menu. It will change the layout of Maya to bring up the Blendshapes. This is a screenshot of what the blendshapes will come out as when you open the Fuse FBX file in Maya. You can drag the sliders for each shape and see how it affects the face mesh
	  
![maya screenshot](https://i.ibb.co/SXKrGzw/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-10-18-PM-2.png)

   - After the import in done, there are some textures are transparent. It is an easy fix!
	  - In Maya, just switch workspace modes to "maya classic"
	  - Then select the mesh and select the attribute editor tab on the far right and select the farthest tab. 
	  - You will see a transparency slider grayed out. Right click on it and select "break connection".
	  - And the texture will be fixed! 
	  

![maya screenshot](https://i.ibb.co/3BWk5bL/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-12-06-PM-2.png)

![maya screenshot](https://i.ibb.co/cTY1xX9/Autodesk-Maya-2018-Educational-Version-untitled-6-24-2020-8-12-55-PM-3.png)

   - Apply the fix for all the meshes and switch back the workspace to "sculpting"
	  - **Editing Blendshapes in Maya from Fuse:**
If you select the face mesh, you will see all the targets for the facial movements. Fuse will give you three blendshape groups, the last group is the one you want to focus on. If you change the workspace in maya to Sculpting, you will be able to see the amount of blendshapes easier. 

When you select the blendshape targets you can move the sliders back and forth and you will be able to see eye’s blinking and the mouth opening and closing. Once you have your character all set up in Maya, you can save this file as a Maya Ascii file. Make sure the file is saved with a .ma extension. Make a folder for this project and place this file in it.  For simplicity’s sake use a root directory (D:\BlendshapesFaceTracking) this is  important for the next steps that involve running a python script. 

On the right, you see the name “blendShape1” You can rename these groups like  “_ncl1_1”. The group of **“_ncl1_2”** is where most of the animations are. You need to rename the groups with circle square icons and a little “ +” sign next to it like “_ncl1_2” to Blendshape_[ name of mesh]. 

![Maya screenshot](https://i.ibb.co/D9QDx1n/Annotation-2020-02-27-110918.png)

   - **Merging Blendshapes in Fuse:**
	  - There are three blendshapes that need to be merged in maya, first, you need to identify
	  - BrowsOuterLower_Lefft and BrowsOuterLower_Right
	  - MouthNarrow_Left and MouthNarrow_Right
	  - CheekPuff_Left and CheekPuff_Right

Once you can see all the blendshapes, shown in the previous picture, scroll all the way down look for three types 

![Maya screenshot](https://i.ibb.co/jwNDpVd/Annotation-2020-02-27-125500.png)

In this example picture you want to select both the Left and Right blendshapes. Be sure to drag the toggles all the way to the right and select both Left and Right blendshapes and right click into one of them and select mirror targets. Once it is merged you need to find the name again, and rename it to cheekPuff the name has to be exact!

   - **Repeat the process for all three, then rename the merged blendshape to the names in bold:**
	 - BrowsOuterLower_Lefft and BrowsOuterLower_Right = **browInnerUp**
	 - MouthNarrow_Left and MouthNarrow_Right = **mouthPucker**
	 - CheekPuff_Left and CheekPuffRight = **cheekPuff**

![Maya screenshot](https://i.ibb.co/2dZDwgv/Autodesk-Maya-2018-Educational-Version-E-Python-Sripts-Python-Sripts-fuse-RLab-ma-6-24-2020-8-23-29-PM-2.png)


**Be sure to save this file as a “.ma” (maya ASCII) file for running python script later on!**


**2. Exporting blendshapes from Fuse and importing into Maya**
  - **Getting the Blendshapes out of MakeHuman/Blender:**
     - The MakeHuman and Blender workflow integrates these two open source software platforms to extract the blendshapes associated with all of the parametric sliders for crafting your avatar.  You’ll need to install two plugins to MakeHuman and one to Blender. Both are free downloads and have robust communities.
  - **Editing Blendshapes in Maya from MakeHuman:**
     - Once you make the switch, you will see a bunch of orange targets, these are the blendshapes. You can toggle between how strong you want each target to be for animation purposes. It’s basically like a light dimmer. 
  -[Makehuman](http://www.makehumancommunity.org/content/downloads.html) (new link for community [edition](http://download.tuxfamily.org/makehuman/nightly/makehuman-community-1.2.0-alpha4-win32.zip))
  -[Blender](https://www.blender.org/download/)

![make human screen shot](https://i.ibb.co/8zsWQsh/Make-Human-Community-1-2-0-Beta1-HEAD-748a570b-Untitled-6-25-2020-5-08-27-PM.png)

**Installing the Plugins**
Once both are installed let’s grab the plugins and turn them on.

All the plugins needed are [on one page](http://www.makehumancommunity.org/content/plugins.html)

Under the Plugins for MakeHuman section download MHAPI and Forked MHX2. The Forked MHX2 has both the plugin for MakeHuman and Blender.

   - In MakeHuman:
    - [From the MakeHuman Documentation](http://www.makehumancommunity.org/wiki/FAQ:I_downloaded_a_third_party_plug-in._How_do_I_install_it%3F) 
    - On PC the Plugins go in the “plugins” folder wherever you installed MakeHuman.

![mkhu pc set up](https://i.ibb.co/bH5HNKH/Work-flow-for-facial-tracking-Google-Docs-Google-Chrome-6-25-2020-6-36-48-PM-2.png)

   - On Mac the Plugins go inside the MakeHuman.app. Navigate to your Applications folder and right-click on your MakeHuman.app and select “Show Package Contents” and then put the plugins in this location. Note that it goes into the plugin folder in Resources, not the Plugin folder in the root Content folder

![mac set up](https://i.ibb.co/DMpjfbW/Work-flow-for-facial-tracking-Google-Docs-Google-Chrome-6-25-2020-6-37-28-PM-2.png)

   - Copy the 9_export_mhx2 folder and paste it in the plugins folder where MakeHuman is installed.
   - Unzip MHAPI and copy the folder 1_mhapi in the same plugins folder where MakeHuman is installed. 

 - **In Blender:** 
    - Zip up the folder import_runtime_mhx2 and open the Blender application. Go to Edit -> Preferences -> Add-ons. Select “Install” and look for the zipped folder.
![blender set up](https://i.ibb.co/khfv10x/Work-flow-for-facial-tracking-Google-Docs-Google-Chrome-6-25-2020-6-59-29-PM-2.png)

    - Exporting from MakeHuman
    - Create your avatar in MakeHuman. Put your character into a T-Pose before exporting.  Go to Files -> Export and Select MakeHuman Exchange (mhx2), then check the box for Poses on the right Options menu.  Blendshapes are called Targets in MakeHuman and they are used in the Poses.  If you do not see these options, check your plugin installation.

![Make human export](https://i.ibb.co/vQXVNdX/Work-flow-for-facial-tracking-Google-Docs-Google-Chrome-6-25-2020-7-36-36-PM-2.png)

  - **Importing into Blender**
  - Now Open Blender and navigate to File -> Import -> MakeHuman (.mhx2).  On the import window select your file from MakeHuman and Check the box on the right for Override Exported Data.  Under Import Human Type check Face Shapes. Under Rigging choose the Rig Type Humanik.

![Blnder set up](https://i.ibb.co/W54b0YG/blendersetup.png)

![Blender import](https://i.ibb.co/4gvR1gm/Blender-6-23-2020-8-21-51-PM-2.png)

  - Export as FBX from Blender. Turn off “Apply Modifiers” in the Geometry section of the FBX export options.
  - **In Maya from MakeHuman/Blender:**
After you created the model in Blender, and it is exported as a FBX, open the file in Maya. Make sure to delete the default cube, light, and camera from the Blender scene first.

Once you import the model in Maya you should scale the bone joint size. In the toolbar look for Display > Animation > Joint Size. Scale it down to whatever is comfortable for you. This is to make it easier to see the animation of the blendshapes. 

Then switch the workspace mode to sculpting this will layout the blendshapes in a easier way to see. 

  - **Editing Blendshapes in Maya from MakeHuman:**
  - Once you make the switch, you will see a bunch of orange targets, these are the blendshapes. You can toggle between how strong you want each target to be for animation purposes. It’s basically like a light dimmer.

![makehuman blendshapes](https://i.ibb.co/YfqrB1Z/Autodesk-Maya-2018-Educational-Version-untitled-6-23-2020-8-33-46-PM.png)

When you open up the model in maya, you should see one blendshape group, in this example its called “Body_ncl1_4” rename it to **Blendshape_mesh**

![blend shape group](https://i.ibb.co/D9QDx1n/Annotation-2020-02-27-110918.png)

   - **Merging Blendshapes in MakeHuman:**
      - The two blendshapes that need merging are:
         - mouth_narrow_left and mouth_narrow_right = **mouthPucker**
         - cheek_balloon_left and cheek_balloon_right = **cheekPuff**

Be sure to rename Brow_squeeze = **browInnerUp**  This one is already merged! But just needs to be a different name so it can work with Apple!!

In maya, you want to locate these two pairs of blendshapes and merge them. In order to merge the two targets correctly you will need to select them both, for example “mouth_narrow_left and mouth_narrow_right” and drag the toggles all the way to the right and right click into them and hit merge.  Once they are merged you need to look for it again and there will only be one name, select it and rename it mouthPucker, it has to be exactly spelled like that.  Repeat the steps for cheek_balloon_left and cheek_balloon_right. 

![merge targets](https://i.ibb.co/jwNDpVd/Annotation-2020-02-27-125500.png)

Now that you have all the blendshapes renamed and the merged blendshapes working, you can export this file as a fbx 2018 file and import it into Unreal!


# Setting Up Our Python Script

Be sure to read our setup [here](https://github.com/RLabNYC/RLab_FaceTracking_RenameScripts)


Python download here: https://www.python.org/downloads/ **scroll all the way to see how to download properly!**

![python screenshot](https://i.ibb.co/5RYbr30/Inkedwin-installer-LI.jpg)

**Make sure you check off "Python version number to PATH"**

# Installing Pandas

Open the terminal into where python is installed into your computer. In case panda is not installed already.

  - **Run command:**

```
pip install pandas
```

# Installing pip

Installing with get-pip.py
To install pip, securely 1 download get-pip.py by following this link: get-pip.py. Alternatively, use curl:

```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
```

Then run the following command in the folder where you have downloaded get-pip.py:
```
python get-pip.py
```

## How To Run Our Script

Here is the link to the files for the [python scripts](https://drive.google.com/file/d/1doMe8WIUbqdsxNHbB--hBKqrz7n8hjyf/view?usp=sharing). After you extract the files from the zip folder, make sure you save the .ma files into this same folder that you created for this tutorial. Then import the Fuse or MakeHuman CSV files into the same folder:

  - [Fuse CSV](https://drive.google.com/open?id=1xSIUFs7t_SA1iKy8z1C6dZr_NC3nmUk7)
  - [Make Human CSV](https://drive.google.com/open?id=1_eibyGkDRUnFtG_fo79H6KKyiKjnk3E6)

In order to have the blendshapes register in Unreal, the blendshapes needs to be named in a specific way for Apple’s ARKit to work on the new model. 


  - The file structure should look this
![file screen shot](https://i.ibb.co/4SBsmSY/Python-Sripts-6-25-2020-3-40-32-PM-2.png)

You will need to change directory in Terminal or Command Prompt to the folder that your files and Pythons scripts are in. 

Make sure all three files are in the same folder before you run the script. This is basically reading the CSV file and replaces all the fuse blendshape names with the apple blendshape names in the .ma file.

  - **For  WINDOWS Users:**
     - Open the command prompt as admin, you can search for it.
     - Navigate to the folder with the python scripts (cd into the folder). 
In the command line, type in: 
```
runme.bat
```
  - **For MAC Users:** 
     - open terminal, search for” terminal” in the finder. 
     - Navigate to the folder where the python scripts live (cd into the folder). 
Open the terminal and type in: 
```
	source runme.sh
```
Once the program runs make sure to type in: 
```
deactivate
```
![file screen shot](https://i.ibb.co/ynLk4ys/Command-Prompt-runme-bat-6-24-2020-8-21-21-PM.png)


# Download Our Repo

**3. Importing into Unreal**
   - You should have our project downloaded or cloned on your computer by this point.
   - Once the project is downloaded make sure you save it a place where you can find it easily. Please refer to Unreal’s documentation on setting up the Unreal environment and selecting the map for prototyping. Here is the link again https://docs.unrealengine.com/en-US/Platforms/AR/HandheldAR/FaceARSample/index.html 

      - When you open the faceAR project in Unreal again, import the FBX into Unreal with these settings:

![import screenshot](https://i.ibb.co/LnhVCvm/Screen-Shot-2020-02-10-at-5-05-25-PM.png)



  - Need to make sure that “Import Morph Targets”  is checked off. Once it is imported as a mesh and as skeletal, the import default settings should take care of itself. 

If you need further assistance, refer to this documentation from Unreal: https://docs.unrealengine.com/en-US/Engine/Content/FBX/MorphTargets/index.html

Once it is imported into Unreal. You should be able to open up the skeletal mesh asset and see the renamed blendshapes. Test the sliders to see if they work on the model. 

### Fuse example
![unreal fuse blendshapes](https://i.ibb.co/6R2XJRH/Annotation-2020-02-11-105608.png)

### Makehuman example
![ unreal mkhuman blendshapes](https://i.ibb.co/m8K1n8s/Annotation-2020-02-28-115732.png)

If you see an error or the blendshapes are named differently, make sure to double check the grouping name of the blendshapes, this is the group that should be named “Blendshape_mesh” 

![Maya screenshot](https://i.ibb.co/D9QDx1n/Annotation-2020-02-27-110918.png)

In this example, the “Body_ncl1_4” needs to be renamed to Blendshape_mesh

Our repo will have everything set up for you to test the Livelink app on yor phone with our Unreal sample project.

## Enabled plugins in Unreal 

   - Make sure these plugins are enabled in Unreal. 
   - **Livelink** 
![plugins](https://i.ibb.co/j8J5xKY/Rlab-facetracking2-Unreal-Editor-6-29-2020-3-00-28-PM.png)
   - **Apple ARkit**
![Appleplugins](https://i.ibb.co/N1KPM8W/Rlab-facetracking2-Unreal-Editor-6-29-2020-3-00-37-PM-2.png)

   - **LiveLink**
     - Make sure you are able to see your phone
![Livelink](https://i.ibb.co/02n2Xvq/Rlab-facetracking2-Unreal-Editor-6-29-2020-3-19-35-PM-2.png)



## Blueprints in Unreal

- Check out our blueprints that should be set up for you already. Make sure our level blue print has a *Start-AR-Session* node connected to *Event Begin Play* 
- You should see two sample characters in the project. Go into their animation blueprints and see how they are set up. 

- We have already prepared the sample blueprints for you in this project.

**Use the Unreal documentation for a more detailed set up.**

Steps for getting the iPhone to control facial movements in Unreal. 
Please refer to the documentation from Unreal to setup the face tracking from scratch here:
https://docs.unrealengine.com/en-US/Platforms/AR/HandheldAR/FaceARSample/index.html

Here is a link to Apple’s blendshape guidelines: https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation

   - **Here is a simplified list of the setup:**
     - Make sure the blendshapes are named correctly. 
     - Enable face tracking in the Defaultengine.ini file. 
     - Create and apply the data asset
     - Create a sessionAR function in the level blueprint 

     - Create an animation blueprint that connects livelink node and set the name to “iPhoneXFaceAR” exactly. 
       - Right click in the content browser in an empty space > go to “Animation” > select “Animation blueprint” > Under parent class Select “anim instance” > Under target skeleton select the name of your imported fbx file > click “ok” and rename it and make sure you know where it is. 

   - **Level Blueprint**
     - ![LevelBlueprint](https://i.ibb.co/Lk6RV6j/RLab-Sample-map-6-29-2020-3-44-14-PM-2.png)
   - **Animation Blueprint**
   - **Fuse**
      - ![Anim blueprint](https://i.ibb.co/dM0D37F/ABP-fuse1-6-29-2020-3-46-53-PM.png)
   - **Makehuman**
      - ![Anim blueprint](https://i.ibb.co/w7gffd9/Rlab-facetracking2-Unreal-Editor-6-29-2020-3-45-28-PM.png)



# Download The App

Look on the app store on your iPhone and download the *LiveLink UE MoCap* app. 

  - Type in your ip adress
  - To find out what your ip adress is:
On PC: Open the command line and type in
```
ipconfig
```
On Mac type in 
```
ifconfig
```
Or go into your "system preferences" click on "Network" and then you will see the ip address on the right. 


# Almost Done! 

  - Make sure your phone and computer are connected on the same network!
  - On the app click connect and then press play in Unreal, while it's running, you might need to click again on the phone app and you will start to the faces move!

  **Congratualtions!** You just completed facial tracking in Unreal for free!
