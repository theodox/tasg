Technical Artists Survival Manual

General notes

Approach
========
* The goal of the book is to be a ready reference for working TA
	* Intermediate to advanced
		* assumes you know the basics
		* 
	* High level introductions to the major problem sets
	* Framework for tackling problems
	* Practical examples
	* Further reading
* It's not a tutorial book
	* tutorials are easy to find
	* books aren't great for up-to-the minute info
	* But they are great at giving a strategic look at stuff
* Emphasis on survival skills:
	* you can look up technical details...
	* we want to give your the right instincts to know where to look


** important note: i'm in the _jotting down_ stage - so don't assume this order or structure is great!!! **

Preliminary outline
===================
* Intro
	* Approach & conventions
	* Audience
	* takeaway
* History of TA
	* production > programmer
	* programmer > content guy
	* Next gen and the birth of TA
		* big teams, lots of artists
		* productivity more important
		* production too complex to manage by ear
			* <insert japan example somewhere>
	* Enter the ta
		* started off informally
		* became more recognized, important
		* became critical
	* Looking ahead:
		* increasing professionalization
		* more responsibility
		* how not to turn into vanilla programmers
* The TA: A field guide
	* TA skills
		* scripting
			* Languages.... python
		* 'real' programming
		* 3d math
		*  art skills
	* TA tools
		* 3d packages
		* scripting languages
		* hardcore programming
   * TA specialties
	   * Pipeline
			* Tools
			* Tech support
	   * Rigging
			* Technical animation
	   * Shaders
			* prototyping
			* shader artists
	   * Effects
			* closest to production
	   * Procedural content
			* small but growing
* Scripting safely
	* Design:
		* compartmentalized
			* GUI / function split
			* design for change
		* SRP and DRY
			* Save time
		* OOP vs imperative
			* what works as long as it's safe
	* distribution
		* build process
		* tdd
		* undoable installation
		* testing, rollouts
	* error handling
		* proper use of try/catch
			* throw low, catch high
	* logging
		* don't overwhelm users, but don't miss good stuff
		* how the stack works
		* saving stacks
		* email, database, messaging etc
* Pipeline design
	* Key values
		* Key value: feedback!
		* key value: human decision making
			* don't blow it on stupid clerical work
		* Key value: transparency:
			* know what you're looking at,
	* Process analysis
		* graph design
		* bottlnecks
		* one-way gates
		* How to invest
			* what saves most time/money
			* what is best for iteration time
			* role of end-user tools
	* Exporting / importing
		* exporter: clean up data
		* importer: format for target
		* Don't confuse the two!
		* Better have them be separate - easier to refactor
		* Exporter
			*  should be as simple as possible
			* should be self-describing, not convention based
				* eg: role = root, not 'bone named root'
				* Why?
					* Don't put important data where users can change it by accident (ie: names)
					* Say what you're doing, don't make people guess
					* Make it inspectable
					* Importance of versioning!
			* Importer:
				* this is where the magic happens
				* this is more likely to be in the hands of engine coders
				* Frequently changes - that's why we separate it out (human decision: save people from re-exporting)
				* Important feedback opportunity:
					* Often, importer is what determines the real cost (transparency)
					* If you possibly can, report this back to the user - (feedback)
	* Discovery
		* databases
		* tagging
* Rigging
	* Spaces and actions
		* Spaces: actions that make sense in one space make no sense in another
			* simple Example: orbit of the mooon
			* complex example: walk cycle
			* constraints: translation between spaces
		* Artificial spaces:
			* sometimes its useful to create a space
				* example: barycentric control
				* example: surface constrained control
				* example: blending across a lofted surface
		* Rigging = helping animators put animations in the right spaces
			* Which is usually not just local rotation space
		* Kinematics:
			* How does a motion unfold:
				* FK vs IK: directional vs rotational
		* Actions = change in the context of a space
			* space + timing
			* the type of change is the character of a motion
			* simple example: the difference between a real blow and a fake one
	* control rigs and deformation rigs
		* Control rigs
			* principles
				* 1 directional evaluation w/o cycles
				* History independent vs history dependent
				* spaces & motions
				* Rotations
					* Euler issues
						* Axis order
						* twist
				* Scale / Shear
					* shear is weird
					* uses: control damping
				* 
 			* cookbook
				* arms
				* legs
				* spines
				* heads
				* roots
		* Deformation
			* skinning
				* weight tools
			* Blendshapes
			* Muscle systems
	* management
		* The chicken and egg problem
		* strategies
			* referencing
			* re-rigging
			* re-gluing
	* mocap
		* Mass data management
		* tagging, etc.
		* 
	* notes on customer service
		* service first
		* trust
		* Sit in their seats
		* 
	