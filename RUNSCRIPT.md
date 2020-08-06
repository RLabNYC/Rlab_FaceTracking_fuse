
# Software that should be downloaded already by this page
* Maya 2018 or 2019
* Maya student version download here: https://www.autodesk.com/education/free-software/maya
* Fuse downloaded from here: https://www.adobe.com/products/fuse.html
* Mixamo account has been set up


# Import the FBX from Mixamo

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

When you select the blendshape targets you can move the sliders back and forth and you will be able to see eye’s blinking and the mouth opening and closing.  

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


# Running the script in Maya
This step is after you completed designing your 3D character in your specific software of your choosing. 

# Using Python in Maya
There are no plugins required for this step. To use this script you want to open Maya and open the script editor at the bottom right. 

![Screenshot](https://i.ibb.co/5n74QHS/Screenshot-103-LI.jpg)

Once you have the window open, select the python tab. If you do not see one, hit the "+" and choose python and the tab will have the label Python. 

Now once you name your blendshape group is changed to "Blendshape_mesh" and all the necessary targets are merged you can run our script!

![Maya screenshot](https://i.ibb.co/D9QDx1n/Annotation-2020-02-27-110918.png)

# Running Python

Once you open the script editor there should be a MEL tab and a Python tab. If not you can hit the "+" on the far right of the tabs and select "Python". Open the Python tab and just copy and paste the code below into the maya script editor

![mayascript eiditor](https://i.ibb.co/bBt5vZV/Screenshot-105.png)

Then scroll all the down the code until you see a some yellow and red words, please refer to the screenshot below.

![blendshape rename](https://i.ibb.co/hB0pktX/Screenshot-104.png)

Next, you want insert the "Blendshape_whatever" name in between the '' after you type in the name, you can hit the execute all button at the top.

![excutescreenshot](https://i.ibb.co/0cQm23M/Execute.jpg)

Once the code executes, the specific target blendshapes should have changed to camel case naming convention.

Like so in this screenshot. 

![Blendshaperename](Media/blendshape.jpg)

**Now scroll all the way down this page to see the next steps!**
------------------------------------------------------------------------------------------------------------------------------------------------------------------------

```Python
import maya.cmds

def rename_morph_targets( node_name, attr_dict, quiet = False ):
	# list to catch our failures	
	fail_list = [ ]

	# How many targets there are in the alias list
	number_of_targets = maya.cmds.getAttr( '{0}.weight'.format( node_name ), size = True )

	# Iterate through the weight list
	for index in range( 0, number_of_targets ):
		# Query the name of the current blendshape weight
		old_name = maya.cmds.aliasAttr( '{0}.weight[{1}]'.format( node_name, index ), query = True )

		# If the old name isn't in the attr_dict, we're going to pass on it.
		if old_name in attr_dict.keys( ):
			# We're going to rename
			new_name = attr_dict[ old_name ]
			print 'Found old name: ', index, new_name, old_name
			
			absolute_name = '{0}.weight[{1}]'.format( node_name, index )

			maya.cmds.aliasAttr( new_name, absolute_name ) # Re-aliasing / Renaming occurs here.
			if not quiet:
				print 'Changed {0} -> {1}'.format( old_name, new_name )
				
		# Add the failure to the fail list		
		else:
			fail_list.append( old_name )

	if fail_list:
		maya.cmds.warning( '{0} names were not changed. Check console for details'.format( len( fail_list ) ) )
		for name in fail_list:
			print name

attr_dict = { 'Blink_Left': 'eyeBlinkLeft',
                'Blink_Right': 'eyeBlinkRight',
                'BrowsDown_Left': 'browDownLeft',
                'BrowsDown_Right': 'browDownRight',
                'BrowsUp_Left': 'browOuterUpLeft',
                'BrowsUp_Right': 'browOuterUpRight',
                'Frown_Left': 'mouthFrownLeft',
                'Frown_Right': 'mouthFrownRight',
                'Jaw_Down': 'jawOpen',
                'Jaw_Left': 'jawLeft',
                'Jaw_Right': 'jawRight',
		'Jaw_Up': 'mouthClose',
                'LowerLipDown_Left': 'mouthLowerDownLeft',
                'LowerLipDown_Right': 'mouthLowerDownRight', 
		'NoseScrunch_Left': 'noseSneerLeft',
		'NoseScrunch_Right': 'noseSneerRight',
                'SmileLeft': 'mouthLeft',
                'SmileRight': 'mouthRight',
                'UpperLipUp_Left': 'mouthUpperUpLeft',
                'UpperLipUp_Right': 'mouthUpperUpRight',
		'UpperLipIn': 'mouthUpperUpRight',
		'LowerLipIn': 'mouthRollUpper',
		'MidMouth_Right': 'mouthRight',
		'MidMouth_Left': 'mouthLeft',
		'EyesWide_Left': 'eyeWideLeft',
		'EyesWide_Right': 'eyeWideRight',
		'Squint_Leftt': 'eyeBlinkSquintRight',
		'Smile_Left': 'mouthDimpleLeft',
		'Smile_Right': 'mouthDimpleRight',
                'Squint_Right': 'eyeBlinkSquintLeft'  }

node_name = '' # Insert Blendshape_whatever name of the blendshape between the quotes!!
rename_morph_targets( node_name, attr_dict )
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### After blendshape targets are renamed you can export this model as a FBX and import into Unreal! 

**You can go to file > Export all > make sure the file type is FBX and then save it to a location on your computer.**

# The next steps are [here](https://github.com/RLabNYC/Rlab_FaceTracking_fuse/blob/master/IMPORTING.md)

## If you need to go back to the table of [contents](https://github.com/RLabNYC/RLab_Facetracking). For the Fuse modeling steps go [here](https://github.com/RLabNYC/RLab_Facetracking)


