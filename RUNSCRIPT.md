```
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

attr_dict = { 'brow_outer_down_left': 'eyeBlinkLeft',
                'brow_outer_down_right': 'eyeBlinkRight',
                'brow_mid_down_left': 'browDownLeft',
                'brow_mid_down_right': 'browDownRight',
                'brow_outer_up_left': 'browOuterUpLeft',
                'brow_outer_up_right': 'browOuterUpRight',
                'mouth_down_left': 'mouthFrownLeft',
                'mouth_down_right': 'mouthFrownRight',
                'mouth_open': 'jawOpen',
                'mouth_down_left': 'jawLeft',
                'mouth_down_right': 'jawRight',
                'mouth_corner_down_left': 'mouthLowerDownLeft',
                'mouth_corner_down_right': 'mouthLowerDownRight', 
                'mouth_corner_in_left': 'mouthLeft',
                'mouth_corner_in_right': 'mouthRight',
                'lips_mid_lower_up_left': 'mouthUpperUpLeft',
                'lips_mid_lower_up_right': 'mouthUpperUpRight',
                'brow_squeeze': 'browInnerUp'  }

node_name = 'CC_Base_Body_ncl1_1'or '' # Name of the blendshapes
rename_morph_targets( node_name, attr_dict )
```
