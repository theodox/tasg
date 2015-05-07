# Rigging fundamentals
* Key concepts: 
	* Spaces: 
		* actions that make sense in one space make no sense in another
		* ++ insert ptolemy trivia here++
		* simple Example: orbit of the moon
		* complex example: walk cycle
		* ++back ref @scope++ a space is another way of referring to a scope; it's the most logical context for an movement
		* The default 'FK' space is not always the right one
			* For example, the head's proper context is usually the world - since a living character is always adjusting their head's position and orientation trying to keep it constant
				* ++ image: cheetah run cycle ++
		* Lots of counter animation is a clue that the controls are in the wrong space
			* Correct spaces mean fewer keys in more consistent scales and timings
		* Once you understand spaces, you also understand the real role of constraints. 
			* constraints: translation between spaces. Get the numbers that make something in space X behave like it's in space Y 
		* Artificial spaces:
			 - sometimes its useful to create a space
			* example: facial animation controls
			* example: barycentric control
			* example: surface constrained control
			* example: blending across a lofted surfac
		* Rigging = helping animators put animations in the right spaces
			* Which is usually not just local rotation space
	 - Kinematics:
		 - How does a motion unfold?
		* Forward kinematics: the motion reflects the physical hierarchy of the model
			* move hips, then spine, then shoulders, etc.
		* Inverse kinematics reverse engineers the rotations needed to produce a movement across a chain
		* In one way kinematics is an extreme example of a space
		* However the difference is so common and so important you need to treat it separately ++ this is a weak point as written++ 
		*  FK vs IK =  directional vs rotational
	* Pose
		* Collection of positions and orientations at a point in time
			* in film this is typically also view dependent
			* in games, usually not
		* Poses have artistic and technical constraints
			* strong v weak, active v passive, etc
			* Symmetry
			* graphic balance
		* Poses are a basic part of the animator's visual toolkit, but poorly represented in animation tools
		* Key idea: POSING != ANIMATING
			* Tools that help with one don't always help with the other
	* Actions 
		* change in the context of a space
		* pose + space + timing
		* the type of change is the character of a motion
		* simple example: the difference between a real blow and a fake one
		* Key ideaa:
			* ANIMATION != POSING.  Animation includes anticipation, hesitation, movement, follow-thru. These are all about timing, 
				* Often overlaps or followthrus cut against poses 
* Rigging: tools of the trade
	*  control rigs and deformation rigs 
		* use similar math and tools but they have different goals
			* Control rigs establish the fundamentals of an action: pose, spaces and timing
			* Deformation rigs make sure the pose is properly rendered:
				* muscle systems
				* cloth systems
				* automatic mixup bones
	* ++ need to coin a definitive phrase to distinguish between control rigs and deformation rigs, then use it consistently throughout so that you can see what's different++
		* Always keep the deformation rig and animation rig orthogonal to each other.
			* control rigs should change to suit animator needs
			* deformation rigs are frequently set in stone by the need for all animations to share bone topology
		* Make sure you understand the constraints of your system. 
			* Is it name matched?
				* .. or topology matched?
			* Is Opt -in ? Or does it need perfect matches? 
				* Opt in: just ignore extra bones
				* perfect matches: won't work unless skeletons are identical
				* Guess? The system will try to add in some default for un-animated bones
					* EG, distributing spine rotations
					* Depending on how smart this system is this may be ok or may not.
	* Control rigs
		* As distinguished from deformation rig. Control rig has two jobs:
			* assist in posing
			* control interpolation
				* or 'guide animation between poses'
		* Components
			* Ultimately, all animation comes down to:
				* transforms:
					* 3d position/rotation/scale
						* These can be nested to create complex spaces
						* Natural example is a skeleton
						* Typically directly manipulated by users
				* parameters
					* numbers that describe how an action or pose will unfold
						* might describe how closely one object tracks another
						* 
				* Operations
					* mathematical operations that drive transforms
						* On transforms
						* driven by parameters or other transforms
					* Can be done directly via expressions or script controllers
					* More commonly done with 'nodes'
						* partly because artists don't like typing
						* partly because nodes execute in determinate order and in optimized code, not in python/mel/mxs  
				* Specialty operators
					* Constraint:
						* convert numbers from one space to another
					* IK:
						* drive a series of rotations to achieve a given position
					* Deformers
						* Specialty 'transforms' which map positions in space to another 
						* Real transforms are affine - shape preserving
						* Deformers are non-linear: they can change the shape of objects
							* Use directly for skinning
							* Or for facial
							* Or special effects
						* 
		 - principles
			  - Directionality
				* To calculate an effect, the system needs to understand all of the operations and transforms which drive the result
				* it must always be clear who is in charge you X's position can;t be dependent on Y's rotation if Y's rotation depends on X's positions
				* It's possible to create situations which look like loops but are not:
					* a's rotation drives' b's position drives a's position
					* Not a good idea when you can design around it -- the software will often spam you with warnings
			 - History independent vs history dependent
				* Ordinary control evaluations have to be history independent - that is, the same set of controls inputs always creates the same set of outputs.
				* Simulations often include an element of  history dependency: what happens now depends on what happened last frame
					* e.g., both parties to a collision get impetus
				* HI and HD are very different beasts - don't confuse them:
					* example, physics sim that adds infinite force due to sudden frame snaps.
					* example: if you want to create an auto-shoulder component it must be driven off the hand OR it must drive the hand; it can't do both
				* HD stuff must always be run sequentially - which means a 'render' step... which is annoying to animators
					* in H'wood this is often hidden by sending the scene to a TD who manages the sims for the animator
					* in Games, not so much
						* know your audiences / budget
		* Understanding transforms
			* it's useful, but incorrect, to think about transforms as nested physical objects with position, scale, and rotation
			* How to build a matrix
				* Local X, Y and Z vectors as the first rows
				* fourth row is the translation
				* fourth column is the 'Homogeneous coordinate'
					* need a good plain english explanation of why
					* practical outcome:
						* XYZ X Matrix = VECTOR
						* XYZW X Matrix = POINT
				* Affine = preserves parallels
				* Uses:
					* transforms
					* But also camera projection
					* Skew deformations
				* 'Soft' deformations can be blends between matrices
					* eg: linear skinning

			* Dot product
				* called the 'scalar' product because it takes two vectors and returns a single number or the 'inner' product
				* Usually used to determine the angle between vectors
					* A * b = cos of the angle between A and B
				* However, it's really a selection function. For example:
					* (1,2,3) dot (0,1,0) = 2
					* (1,2,3) dot (0,0,1) = 3
					* (1,2,3) dot (1,0,1) = 4
				* So you can use it for things like finding one item in a list, or summing up different contributions
				* It's the projection of one vector onto another
				* ++Need a really good reference here++
			* Cross product:
				* the cross product of two vectors is the right angle of the plane they form
				* If they are normalized, the size of the vector is the dot of the the angle between the vectors
				* "Handedness" ++ ??++
				* other uses ++TBD++
				* ++ two or three D only?++
			* 
			* Rotations
				* Euler issues
					* An orientation can be represented by an infinite number of rulers
					* And vice versa
					* Eulers are great because they map onto fcurves
					* But otherwise they stuck
						* Demonstrate Euler vs quat interpolation
						* Gimbal lock
					* Axis order dependency:
						* the meaning of XYZ rotation varies with 
				* twist
					* a visual, not a mathematical concept
				* 
			* Scale / Shear
				* shear is weird
				* uses: control damping
			* 
		 - cookbook
			* arms
				* FK / IK
				* world ik for contact
				* local ik for tight controlled poses
				* local fk for whip action, gestures
				* world fk (rare) for expressive gestures with target component 
			* legs
				* FK/IK
				* spaces - usually world
				* FK/IK switching for dynamics
				* IK for contact most of the time
			* spines
				* 2+1
				* FK
				* Spline
			* heads
				* World FK for most things
				* Local FK for whip
				* IK for spline spines, tracking (snake,etc) or sfx
			* roots
	 - Deformation
		* skinning
			* Linear vs DQ
			* weight tools
			* Fixup bones
		* Blendshapes
		 - Muscle system
	 - management
		* The chicken and egg problem
			* Rig depends on animation needs 
			* animation driven by rig
			* 
	* strategies
		* Retargeting is the heart of good animation pipeline
			* because dependency management is the curse of animation pipelines
			* base models and rigs change all the time
			* ... no pipeline based on "we just won't do that" ever works. It just means "when we do it, it'll hurt".
			* It's better to understand the problem set and plan for tackling it.
			* Minimal retargeting:
				* bake existing animation to a neutral world-space representations
				* Use constraints and fixed settings to drive either the rig or defamation skeleton
				* Minimal retargeting preserves APPEARANCES but not AFFORDANCES
					* This is great for 'done' animations, not so much for others
				* 
		* referencing vs duplication
			* referencing
				* keeps things in sync, but its brittle
					* Changes are propagated by force - which means you have to tackle them when they happen, not when you're ready
					*  pro: Keeps content in sync
				* pro: no room for user error
				* con: unpredictable breakage
				* con: rigidity
				* Great for making sure that the defamation skeleton is always correct
					* because it always matches
				* Less great for rig management
					* con: tends to impose a one-rig-for-all rule
					* con: if reference rig changes, can be hard to retarget
			* If you invest in referencing, invest in transplanting tools: 
				* tools which can adapt existing animation to new rig
				* Some parts will be plug and play - just find existing animation curves and plug them into the right slots
				* Some will need adapters (i.e., "invert this curve" or "add 45 to this curve"
					* Adding appropriate nodes is great, but has a short half-life
					* 
		* duplication 
			* allows for divergences, which is good or bad depending on the back end
				* Do you really want to reexport all existing content because the JO on a pinky is wrong?
				* But... do you want to spend a lot of time auditing existing animations to make sure they are up to spec?
				* Works best if the back end is fault tolerant
				* 

		* referencing
			* * ways to convert existing animations to new controls
				* Baking existing animation to a neutral representation
					* Or using exported animation to generate the neutral version
				* 	        * re-rigging
	        * re-gluing
	* mocap
	    * Mass data management
	    * tagging, etc.
