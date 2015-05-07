# Approach
* The goal of the book is to be a ready reference for working TA
	* Intermediate to advanced
		* assumes you know the basics
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


# Introduction & Outline
* Approach & conventions
	* outline general principles
	* provide one or more specific illustrations
	* interviews / anecdotes from working pros
	* not primarily a tutorial although there will be a lot of code
		* {not sure about code samples atm - don't want to distract but it's useful to have concrete examples. Check how they did it in **Art of Readable Code**}
		* Code primarily python (?)
		* C# when needed
		* MXS sometimes?
* Audience
	* TA's of all experience levels
		* Intro to the field for n00bs
		* Overview guide for intermediates and managers
		* Review text / 'course material' for experienced ta's 
* Organization
	* four big sections:
		* overview of the discipline: history, background, main branches
			* this is intro material which will be most useful for students and newcomers
		* Common core:
			* key techniques for good tool design and pipeline work that are common to all disciplines
		* Discpline specific discussions
			* each includes a 'cookbook' for common problems
* takeaway
	* practical advice
		* but organized around the 3 big themes
	* 4 key themes
		* Tech in the service of creativity 
			* human energy is precious
			* don't waste it on bullshit
		* Diplomacy / hybridity/ one foot in two worlds
			* Ta = link between the two halves of the game dev brain
			* this is a _hard_ niche, requires a lot of work!
				* the few, the proud
			* people skills matter
					* listening to users
					* negotiatiing on their behalf
					* educating
		* Service
			* brilliance is nice, but service is what matters
			* Service, but not servility
				* Don't become a garbageman
					* make things better by helping guide or design around possible problems... not by cleaning up messes or doing drudgework.
		* Responsibility
			* Now that ta is big business, it's important to act like a pro
			* plan for the future 
			* Do things the right way

# 1. Part IA : A brief history of TA
* Why start with history?
	* To illuststrate unique, hybrid nature of a TA
	* To underline the different strands of influence
	* To help offer a working definition, since TA is such a fuzzy term.
* The games industry cladogram
	* production \> programmer
	* programmer \> content guy
	* Next gen and the birth of TA
		* big teams, lots of artists
		* productivity more important
		* production too complex to manage by ear
			* <insert japan example somewhere>
* Enter the ta
	* started off informally
		* evolved from 'power users'
		* usually solving problems the rest of the team ignored
	* became more recognized, important
		* Information sharing -- TA's are more vocal than most artists
			* hat tip to TART, TAO
		* growing complexity of 3d demands drives need for workflows
	* became critical
		* Big budgets, big teams put a premium on productivity
		* More specialization in pipelines and line jobs means more need for glue
		* Games are evolving way faster than DCCs; new functionality comes in house more often than it does from ADSK
* Looking ahead:
	* increasing professionalization
	* more responsibility
	* Identity crisis?
		* Will we turn into vanilla programmers?
		* Will we lose touch with our customers?

# 2.  IB Field guide to technical artists
* TA is not a unified discipline. 
	\*Lots of specialists, sometimes in mutually incomprehensible fields
	* What makes them all alike?
	* How do you switch hit if needed?
* TA specialties outlined
	* detailed later in book, but catalogued here
	* Most people fill one or two niches
		* pros and cons of covering lots of bases
		* Career differences between specialists and generalists
		* **takeaway** follow your passion, but also know your market. And not just today: thinka few years ahead as well!
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
# - IC : Core TA skills
	* Bring it back together: what do all TA's share?
	* DCC wizardry
	    * More than one package
	        * need to know how the other half lives
	        * need to see the answers multiple times to judge them
	    * Patience and sutbborness
	        * Good eye for little known features
	        * a good sense for how to guess the right way to look
	* scripting
	    * Languages.... 
	    *  = which really means 'python' most of the time
	    * 'real' programming a plus, but secondary
	    « this section should include a good bibliography»
	* 3d math and concepts
	    « should include a good biblio...»
	*  Core art skills
	    * Don't have to be a genius, but you do have to be competent
	    * Need to understand what other artists see and say
	* process vision
	    * always look at how things are done and could be better
	    * learn to spot problems before they become routines

# 4. Part II A : Basic TA  survival skills
* Seque: we've identified some of the common skills a TA needs to survive. Now let's talk about the environment where we use these skills
	* Production is crazy! nothing goes according to plan
	* There's always something new and unexpected
	* TA's are always on the front line dealing with the craziness
	* So, you need survival skills
* What are 'survival skills'?
	* **NOTE - it would be great to find a real world survival quote here - someting about seeing beyond the immediate problems to the big issues....**
	* Survival skills are enhancements to the practical skills: how forestall and head off possible problems
		* How to to design possible problems away
		* Howe to _negotiatate_ possible problems away
* There are 3 core survival skills
	* Process analysis:  understanding how data flows through a pipeline so you can design tools that are flexible and iterative
		* Key goal: identify common patterns in production so you can spot possible problems
		* Secondary goal: Design processes first and tools second.  Better processes mean fewer and simple technologies!
	* Defensive design: programming styles that enhance long term maintenance and survivability
	* * Key goal: building robust, reliable tools
		* this is super hard - it's programming where the user can mess around with the memory directly!
	* Secondary goals: 
		* make yourself more productive
	* Service skills:
		* Tech art is a service business. No matter how smart you are, your value is based on how well you help other people do your job.
		* You need to integrate this into what you do.
			* Learning to see problems from the user's side, and also from the consumer's side (aka "talking to artists and programmers"
			* Delivering tools that meet user needs
			* ...On time and reliably
		* Key goal: Use unique TA position to facilitate discuessions between different subcultures
		* Secondary goal: Make your own life easier by taking the drama out of supporting your users
- II.B Process analysis
===================  
\*\* Note lots of new verbiage here at the 0.9 level, needs work
* Process analysis = Understanding data flow
	* learn to see the flow of data for an individual feature or the game as a whole.
	* it should work more or less like a DAG Graph, with all the information flowing one way....
	* Of course, it doesn't
		* for good reasons, like reviews, feedback, and course corrections
		* for bad reasons - like poor design and overconfidence
* Key goal of process analysis: to figure out the _why_ before the _how_
	* "It's too easy to "When you've got a new hammer, everything looks like a nail?" -- drive choices on strategy not on what you know best or what's at hand
	* Classic example: designing levels in Max 'because that's what we know'
	* **TBD: is there a good, non jargony source for this?**
* Important concepts:
	* **Flow** how does information get from one part of the system to another?
		* Is it automatic, as in updating a file?
		* Does it require an export or build?
			* Does that export/build require human intervention
		* What's 'upstream' or 'downstream' -- who makes changes, who consumes them
			* Examples:
				* change the skeleton, the animations change or are invalidated
				* change the uvs, the textures change
				* change import mode of a file, the results change
	* **Dependencies** Can I understand the flow relationships? Can I work back from what I see to what caused it?
		* Clarity and visualization are important for working with dependencies
		* examples:
			* does the animator see or set the value that might speed up his animations in game?  If the animation lenght or art changes, what happens in game?
			* If you change the shader on an object, does that change the build process for a whole level?
			* Key points:
				* explicit dependencies better than implicit ones
				* People who collaborate need to know where they are on the chain!
	* **Scope** What are the ramifications of a change?  Look at the examples above, you can see possiblities of problems because of hidden dependencies
		* If I move a building, do I move it's contents too?
		* If I change an animation, do I have to update a separate file for things to works
		* Visible dependencies are better than invisible ones
			* It makes sense that changing a texture changes model appearance.  It makes less sense that changes in a text file do.
		* logical dependencies are better than illogical ones
		* Small, clear scopes make like easy; big messy ones make life hard!
* Key skills
	* Learn to identify sources of trouble: what operations can't be undone?
		* analogy: construction history
		* simple example: 
			* UV's are downstream of geometry, won't survive major  changes
			* animations are downstream of skeletons, again, wont' survive changes
			* AI navigation is downstream of level layout
		* complex examples:
			* Design input to a game level is downstream of some aspects of layout.  Can it be made more survivable?  If, eg, a mission marker is in a particular building, does it move with the building? Can you move the building and retain it's interior pathing? Etc.
			* Big changes to global lighting will probably involve a lot of shader changes too; the shader settings and the lighting environment are relative to each other.
				* Complex examples are often chicken-and-egg problems; learn to spot and minimize these.
			* There's a difference between changes with simple, mechanical outflows (like relighting a level, which involves a light bake) and those with creative or technical implications (like changing the skeleton of an existing character).  The former are annoyances; you can always throw cpu at the problem.  the latter need human intervention and are more disruptive, more expensive.
* Prioritize tools and processes for art tasks that demand iteration:
	* eg: designing multiplayer levels needs short turn around because of the need for fixes
		* You may have to accept aesthetic tradeoffs: if you need fast turnaround you can't always have perfect control
		* OTOH, if you have an expensive AAA cinematic experience, you can't ship substandard art, so you need to prioritize prettiness and precision
	* eg: get characters built to rough spec and animating before polish
		* That way you can spot things like poor proportions or art \<\> design mismatches early, before wasting a lot of resources
		* See things in context before committing to a 'we won't change this' plan!
* 80/20 rule. Get everything to 80% first, then take 20 % of the finished assets to 100
* When designing a workflow, minimize the number of one-way gates
	* don't rely on 'we won't change it' - that rarely works
	* instead, design data structures or ways of looking at the problem that are survivable
		* example: SOD markup system
			* Changes to geometry and changes to markup live together, it's easy to see and udpate them together
			* Changes are centralized: fix one model, they're all fixed.
			* Tradeoff: Less adaptable to specific circumstances: eg, what happens to the markup if you want to place a chair on it's back?
			* Cheap fix: duplicate the model and mark it up!
				* Minor memory, work costs
				* Not perfect but workable
			* Fancy fix: separate markup editor in between maya and game
				* More flexible, powerful... and expensive
				* is this a 20% case or an 80% case? In our case, 20.
				\* 
		* example: rigging and animating on an animation rig instead of base skeleton
			* Classic game engine problem: skeleton must match between models and animations
			* But they are rarely exported togther
			* Change base, invaliate all
			* Change anim, invalidate one
			* Palliatives:
				* Warn on skeleton changes
					* Avoids accidental changes
					* Maybe queues up automatic re-export?
				* File referencing
					* Keeps files in sync, but needs re-export
					* May break working files
			* Fixes:
				* In-game retargeting
					* Perf tradeoff
				* Offline bulk retargeting
					* Better than nothing, but never perfect
			* Big lesson: this is a tough, tough problem because the dependencies are very hard to teast out
			* **OPEN QUESTIONS**
				* Could you approach this as an analogue to continuous refactoring? Lots of small cheap changes instead of a few big ones?
				* What tools can you build to make this easier?
					* In this case: a custom rerig script specific to your change that can be batch applied
					* World space retargeting that can at least give visually similar results
					* Automated pose comparison tools to compare world-space differences between poses?
			* example: using shader templates
				* Shaders have lots of params
				* Many are intrisincally tied to lighting values
				* So, changes to global lighting can have many ripple effects
				* We'll cover multiple ways to do it
				* Side lesson:
					* As you can see, bulk changes are complex. It's best if shader parameter bundles are NOT part of a larger file:
					* Don't set your game sliders in max/maya!  
				* Options:
					* update hidden constants in the shaders
						* no user input, global
						* results not guaranteed to be indentical
					* manually change shader values
						* High quality
						* expensive, slow, error prone.... boring
					* Templates with variants
						* Shaders know what their 'archetype' is and change if it changes.
						* Settings not included in archetype can be changed any time; those defined in the archetype are relative 
						* Pros: 
							* flexible,  bulk editable
							* semantic: preserves user intent
						* Cons: 
							* up front cost
							*   Needs good UI or users will be confused
					* "Search and replace"
						* smart tools for doing changes
							* ie " if specular \> .5 and diffuse != white, set diffuse to white and reduce specular by half", etc
						* Pros
							* arbitrarily complex changes
							* can be human assisted
							* Works well with source control!
						* Cons:
							* Can go frankenstein, run amok and make lots of changes
							* Very scary for items that are not source controlled properly
* When you see an unavoidable cycle, invest in fixup tools:
	* eg, animation retargeting tools or shader rebuild tools as above
	* eg, distributed light builds
	* automate boring stuff (eg: SOD terrain intersection)
* Always, always prefer open file formats that can be programmatically rewritten as needs change
* Do bulk changes in a source control friendly way!

# 5. II C: Defensive design & TA Coding
* Segue: In some ways, the same principles laid out in Proc.Analysis work for code too:
	* Identify and minimize unneeded dependencies
	* Predict ramifications
	* Minimize costs of making changes
	* Good scope!
* TA's are programmmers where perf is a secondary consideration
	* slower languages
	* maintenance, uptime, flexibility more importance than speed, memory efficiency
		* anecdotes about game programmers & python & eye-rolling
	* With our less demanding environment, we can get sloppy. But we should not
		* We have less choice of environment; typically working with other people's choices
			* eg, the goofy max api or workflow limitations in Maya
		* We don't get help from compilers, etc
		* We don't work in a vacuum. If we screw up, other people pay for it
	* So, it's important to embrace your programmer personality
		* ...without sacrificing your inner artist!
		* this is a _demanding_ role!
* Coding style:
	* OOP vs imperative
		* Most code lying around is jumped-up scripts, not systems
			* over the long term, the balance is shifting
		* short term: what works as long as it's safe
			* Good scope, smart design, simplicity all apply equally to OOP and imp
		* long term: OOP without the fanatacism is the way to go
	* Why OOP?
		* OOP is not about OBJECTS. It's about SCOPES (back XREF)
			* Discuss why the object metaphor is misleading
			* Keep data and code that works on data together
			* bundle data that should cooperate together
			* So oop is a way of ISOLATING problems, not just a slicker way of writing the same functions
		* compartmentalizion: a key survivability feature
			* Battleship principle
			* "Single responsibility" pattern
			* Of course, this doesn;'t solve everything
				* the titanic was unsinkable because of compartmentalization
		* Reuse!  Modular code is much eaiser to adapt and re-use
			* inheritance for customization
			* factory pattern for replacing multiple if/then 
				* **Advice** if statements are the enemy!
			* choices with a single choice of output
			* composition for more features
			* Side note: the 'rule of three' and fully general code. Fully general code is HARD and trying to do it in the abstract is DANGEROUS. 
				* Instead, write 'fairly general code' and try to think about how to make it more general when the needs arises
			* **Advice** if you're cutting and pasting, you're probably doing it wrong.
		* classic OOP applications: 
			* GUI / function split
			* Modular rigging system
		* Less obvious examples:
			* separating the code the reads and writes files from the code that works on data
			* A modular system for metadata that does not know what the data actually means
		* Simple OOP example to make this concrete
			*  \<< side by side comparison of a simple exporter done OOP and imperative style>\>
			* Key features:
				* OOP version can be converted to export different data and different format easily!
		* See the benefits? 
			* OOP is designed for change, expansion
			* no design survives contact with the art staff 
		* Extra bonus: OOP code is testable:
			* short excursus on TDD. Key themes:
				* tests make you keep your promises - they remember when you dont
					* example: my casing change at arena net
				* testable code is better code
					* by definition its more modular and more focused
				* testing in dcc tools is slow and can be irritating
					* but it can be fobbed off on a machine
			* appendix: OOP reference
* * Fault tolerance
	* The biggest knock on TA code is shakiness. "It worked on my machine."
	*   Segue / backref: if you're writing good, tight, well scoped code (OOP or imperative) it's going to be better and less shaky
	* Even so, TA code is hard because it leaves all sorts of data lying around where users can mess with it
		* Real programmers don't need to worry about users manually deleting things from memory, or duplicating named variables or whatever
	* For this reason, you need to design for graceful error handling
		* Which is NOT the same thing as never failing or correctly handling all cases in advance.
	* Error handling
		* Before you can learn what to do, learn how to fail!
			* proper use of try/catch
				* Don't try to catch everything. Exceptions exist for a reason
				* throw low, catch high
				* Don't swallow legitimate errors unless the need is great.
		* What to do with caught errors:
			* log data  for debug purposes
				* via email
					* Importance of real time error logging
				* via database
				* via log file
			* Tell users what you think is wrong
			* Ask users what they were doing
			* BTW, you can do a little stat gathering along the way too!
		* Good logging principles:
			* how the stack works
			* saving stacks
	* What to do with the info?
		* Stats:
			* prioritize fixes
			* identify common user behaviors
		* Get on top of problems ASAP
# 6: II D: TA as service:
* Segue: Instant response to error emails is the best way to build a relationship with your team. And that's the most important thing you can do!
* TA is a service business. Treat it as such
	* The things we've already covered are part of the equation - code quality, well designed processes, etc.
* There's another side to it to - how people get their tools.
* tools have to get to the artists, reliably
	* In the dark ages we mailed scripts around. No more!
	* manual processes are boring & error prone
	* its hard enough keeping a team up and running; when people have lots of different versions concurrently it's extremely hard
	* You need to be safe so you can make sure everybody is on the same version and force-sync them
		* Users will opt out if the reliability is not there. So you need to make the reliability happen.
		* Users will forget, so you need to do it automatically
		* For optional tools, users should not need special instructions to get the right version
* Automatic distribution is big responsibility, so you need to make it safe and easy
* .... So, You need a build process
	* verify code before it goes out to users
	* don't leave old code lying around dormant
	* make sure that the code you THINK you have is the code you really DO have!
* What is a build process?
	* Get a clean copy of source
	* make sure it works
	* package it up into a single deliverable
	* publish it to users
	* Simple build process example:
		* a script that:
			* copies source code into a clean directory
			* makes sure that all the code files are openable
			* makes sure that the DCC tools will load the scripts
			* DOES NOT verify that the code does anything - only that it could work
				* example: Haywood and the Yen symbol
	* Fancier example:
		* a website that:
			* talks to source control, collects the code base and history of recent changes
			* runs a build in a clean environment
			* runs unit tests
			* runs slower acceptance tests
			* automatically presents or checks in a finished build product
			* allows users to see history
			* builds documentation with, eg, epydoc or sphinx
* the end product:
	* You want as monolithic a work product as possible.
		* Should always be able to drop it in and go - no history, no external dependencies
		* especially important if your are supporting outsourcers or remote teams.
		* simple footprint with easy install/uninstall
			* again, especially nice for outsource/remote
	* You want minimal external dependencies
		* requiring external downloads, installs is always a risk
		* You don't know what happens on outside sites - they may introduce a breaking change without your knowledge. Give users a blessed version.
		* Keep user load minimal; many users are not great sysadmins    
		* disk space is cheap - don't worry about redundancy
* Advanced build proceess
	* unit tests- check for subtle bugs
		* back ref to excursus on TDD
		* we need this more than conventional coders, since we have lots more ways to shoot ourselves in the foot
		* tdd catches a lot of 'innocent' bugs before they hatch
		\*Still, it won't catch all bugs
			* can't simulate user craziness
			* can't simulate all complex interactions
		* Despite this it's a GOOD IDEA
	* Smoke tests - checking for major failures
		* eg, a script that runs maya interactively an ensures that the entire environment has loaded correctly
		* fancier still, run headless versions of major tools and check for expected outputs
		* these kinds of tests are complicated and difficult to build well, so they're rare.  A nice luxury if you can afford them.
	* Human factor
		* Automated testing can't catch everything
		* As customer base scales, add formal QA for major releases
		* Don't trust to luck!
		\* 
- III: Discipline - specific tools and tricks
	* This section covers more advanced material for specific disciplines
	* Each section may stand on it's own but they refer back to the core principles in different ways
# - III.A Building pipelines
	* Pipeline design overlaps with many other areas. It's sort of applied process analysis
	* Stress 'pipelines' plural
	    * there are always many
	    * they crop up all the time
	    * Good principles make them easier to make
	* Start with key values
	    * Recapitulate process analysis. Start with that.
	    * Key value: feedback!
	    * key value: human decision making
	        * don't blow it on stupid clerical work
	    * Key value: transparency:
	        * know what you're looking at
	    * Key value: least surprise
	        * the default should just work
	    * Key value: capture intentions
	        * ask users what they want to do, not what settings they want
	            * ie, "I want to make a vehicle"
	            * not "I have a file with rhis naming convention and these 8 settings"
	* Pipeline components
	    * exporter:
	        * Cleans up data. Removes unwanted stuff.
	        * Clarifies intentions
	    * importer: 
	        * Format for target, optimize
	        * Reprocess exported data 
	    * Don't confuse the two!
	        * Better have them be separate - easier to refactor
	    * Exporter
	        * should be as simple as possible
	        * should be self-describing, not convention based
	            * eg: role = root, not 'bone named root'
	            * Why?
	                * Don't put important data where users can change it by accident (ie: names)
	                * Say what you're doing, don't make people guess
	                * Make it inspectable
	            * Should be a future proof as possible (Simplicity helps)
	        * Importer:
	            * this is where the magic happens
	            * this is more likely to be in the hands of engine coders
	            * Frequently changes - that's why we separate it out (human decision: save people from re-exporting)
	            * Important feedback opportunity:
	                * Often, importer is what determines the real cost (transparency)
	                * If you possibly can, report this back to the user - (feedback)
	            * Potentially importers can be multiple (ie, targeting multiple platforms)
	        * Metadata
	            * A key part of every pipeline.
	            * Tracks what's been through the pipeline
	            * Provides info for other tools
	            * Multiple ways to store
	                * databases
	                    + fast, searchable, analytics
	                    - uptime? complexity, disconnected from reality
	                * naming conventions
	                    + easy, universal
	                    - brittle, users can mess with them
	                * exif/metadata files
	                    + can't get lost
	                    - hard to read, must implement for every file
	                * sidecar files
	                    + easy, inspectable, versionable
	                    - synch issues, disconnectable.
	        * Exporter sample:
	            * adding markup data to SOD
	                * YAML exporter
	                * LIBYaml importer
	                * Sidecar file solution
	                * Total time to market \< 1 week
	                \* 
# - III.B Rigging
	* Key concepts: Spaces and actions
	    * Spaces: actions that make sense in one space make no sense in another
	        * simple Example: orbit of the mooon
	        * complex example: walk cycle
	        * constraints: translation between spaces. Get the numbers that make something in space X behave like it's in space Y
	    * Artificial spaces:
	        * sometimes its useful to create a space
	            * example: barycentric control
	            * example: surface constrained control
	            * example: blending across a lofted surface
	            * example: facial animation controls
	    * Key to spaces: They let you describe things with the fewest possible keys
	    * Rigging = helping animators put animations in the right spaces
	        * Which is usually not just local rotation space
	* Kinematics:
	    * How does a motion unfold
	        * Inverse kinematics reverse engineers the rotations needed to produce a movement across a chain
	        * It's also a form of 'space'
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
# - III.C Shaders
* Shaders are an extremely specialized form of programming
	* optimized for massively parallel gpus
		* lots of similar objects being processed side by side
		* limited inputs and outputs
		* you give up complexity for speed
	* It's a very distinct form of programming
* In many companies the final shaders are the the province of specialty graphics programmers
	* This is often a good idea - integrating a full shader pipeline is not trivial 
	* OTOH, graphics programmers often have a hard time knowing what the artists want or need.
	* TA's are well suited to doing prototyping and look development
		* Ex, prototype a look in Maya, going over it with the artists until it's ready, then  go over it with the shader programmer to find a reasonable approximation
		* Ex, prototype a slow, multipass version of the shader
* Shader basics
	* programs come in two flavors
		* vertex programs
			* got limited vertex information
				* position, normal, color, uv channels
				* constants:
					* external data. usually it's camera and model transforms
					* <Backref to 3d math section>

# 9. III.D Effects
* Effects and shaders are really an independent art form, but often they fall to the lot of TA's
	* In a big studio there are dedicated specialists, but in smaller studios it's often the job of the ta
	* We're going to focus on the technical elements rather than the artistic
		* **Need good references**
* Key recipe elements:
	* particles
		* Computationally cheap, but visually rich
			* particles are similar to shaders:
				* unlike traditional programming, everything is _parallel_: particles don't make decisions about other particles
			* Because of the similarities, particles can often be done in hardware for greater performance
			* This takes some getting used to. 
		* The overall effect is the primary artistic result; control is surrendered in the name of complexity 
			* large enough numbers create illusion of complexity
			* basics are very simple
		* visual varieties:
			* points
			* billboards / sprites
			* geometry
			* ribbons / filaments
		* usual inputs:
			* Particle age
			* Velocity
			* Collision
				* reflect / split /kill
			* Vector
			* spin/torque
		* usual outputs:
			* size
			* color
			* transparency
			* velocity/vector
		*   Fields:
			* fields are really just ways of affecting usual inputs in a space:
				* eg, a gravity field just adds something to a vector
* 3D Math basics
* WHERE DOES THIS GO?
* 3d math is daunting but its not that complex.
	* A lot of us learn it piecemeal,  but it's basically stuff we know from high school
	* Trig & linear algebra covers most of it.
	* Basics vocab:
		* Tuples:  in it's most basic, a set of numbers. We usually see it as a vector, ie a translation offset (ie an XYZ movement but tuples could also represent something like a point, a scale, an euler rotation or the
