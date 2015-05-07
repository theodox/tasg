# Pipeline TA fundamentals
* Pipeline design overlaps with many other areas. It's sort of applied process analysis
* Stress 'pipelines' plural
	 - there are always many
	* they crop up all the time
	* Good principles make them easier to make
* Start with key values
	 - Recapitulate process analysis. Start with that.
	* Key value: feedback!
		* Clear, human readable explanations of what is going on
		* Not too much warning spew
		* Bad example:
			* Socom exporter generating 10k warnings per export 
				* and we had to raise the warning cap
			* Crytek importer generating detailed error messages about geometry falures-
				* but not using the same indices as the maya  file, so that the artists could never figure out which one was the real culprit
	* key value: human decision making
		* don't blow it on stupid clerical work
		* A bad example: special characters n material names
			* Lots of complex rules to make up for lack of characters
			* Intentions were simple, but the rules were not
			* Copy-paste errors could create problems
	* Key value: transparency:
		 - know what you're looking at: "this is a vehicle", not "this object ob-type-code is 005"
		* A bad example: Placing references in Halo
			* original system: artist places geometry in level,
				* Game checks geometry name; if it had special characters it tries to treat the geometry as an instance
				* If it has the right name, check the geometry checksum and try to match up to the matching model
				* Problems:
					* Names could go bad
					* Artists could edit geometry so their instances no longer matched
					* It wasn't clear when the process worked and when it did not.
	* Key value: least surprise
		* the default should just work
			* Bad example: exporter which allows you the export a skinned mesh as a static model and vice-versa 
			* Good example: preflight checklist
				* Don't make the user go to the engine to catch something that's obviously wrong
	* Key value: capture intentions
		 - ask users what they want to do, not what settings they want
		   - ie, "I want to make a vehicle"
		* not "I have a file with this naming convention and these 8 settings
			* Good example: wizard style asset creation
			* bad example: Typical FBX import dialog with hundreds of switches and flags which matter to the engine team but not the artist
	* Key value: responsiveness
		* Long bake times = bad. 
			* Not primarily because of the time... the real cost is breaking attentions spans
				* if it takes longer than 15 seconds, you may lose your users!
			* Strategies for minimizing times:
				* Good code
					* watch for dumb loops
						* trolling same list many times
					* Cache expensive operations
					* When can order help you out
						* e.g., throwaway tests before processing
					* Use profiling to help out
				* Threading to maintain responsiveness
					* Use only when needed
					* threading makes code harder to write
					* and python threading is not always cost effective
						* Usually only helps when IO is the blocker.
					* But threads can be great for keeping user involved
					* And multiprocessing is good for data hungry tasks
				* iterative feedack
					* Use power-of-two resolution so users can do tests quickly  and then refine
						* Example, light baking
							* start with low res / single bounce and work up
						* Example, animation compression
							* Keep uncompressed data side by side with uncompressed for comparison
					* Don't make user start from scratch every time
						* Auto-recompress with last settings at export time 
						* cache useful info so the compression can be tweaked faster
			* "One button export" wherever possible
		* Key value: Focus
			* Don't pester users with too much information
				* It should be there when they want it
				* But keep to the minimal working set as much as possible
					* Example: One button exporter
						* Users typically don't want to tweak a lot of settings every times
						* Good workflow:
							* "What is this", set good defaults
							* Then add custom tweaks
							* Remember settings
							* after that, just execute
								* Until user explicitly wants to change.
* Pipeline components
	 - exporter:
		* Cleans up data. Removes unwanted stuff.
		* Gives the importer enough data to work om
		* Minimizes guesswork for the importer
		*  Real job of the exporter: Clarify intentions

	* importer: 
		* Format for target, optimize
		* Reprocess exported data 
		* Real job of importer: format data for efficient use by the engine
	* Don't confuse the two!
		* Better have them be separate - easier to refactor
		* The common language is the data format
			* Make it clear and simple!
	 - Exporter implementation
		* should be as simple as possible
			* better for maintenance
			* easier future proofing
		* should be self-describing, not convention based
			* eg: role = root, not 'bone named root'
			   - Why?
				* Don't put important data where users can change it by accident (ie: names)
			   - Say what you're doing, don't make people guess #transparency
		 - Make it inspectable
			* If possible, human readable
	   - Importer:
		   - this is where the magic happens
		* this is more likely to be in the hands of engine coders
		* Potentially importers can be multiple (ie, targeting multiple platforms)
		* This is the code that cares about the low-level arrangement of data
		*  May change during production
			*  that's why we separate it out (human decision: save people from re-exporting)
			* Should be batch-able so we can rebuild the data without re-exporting 
		 - Important feedback opportunity:
			* usually, importer is what determines the real cost  #transparency
			* e.g.: meshes get split buy material assignment or vertex-weighting groups
		* If you possibly can, report this back to the user right away
			* partly for #transparency
			* partly to make sure they have early warning of mysteries
			* talk to importer team and establish a common standard for error reports, warnings , etc
				* Warnings should be few!
				* Errors should be clear
					* If possible, don't cascade them

	* Metadata
		* A key part of every pipeline.
		* Tracks what's been through the pipeline
		  - Provides info for other tools
		* Multiple ways to store
			   - databases
				* pro
					*  fast
					* searchable
					* analytics
				* con
					* uptime? 
					* complexity
					*  can get disconnected from reality
			 - naming conventions
				* pro
					* easy
					* universal
				* con
					* brittle
					* data easy to get at & mess up
					* typo prone
			* exif/metadata inside files
				* pro
					*  can't get lost or out of 
				* con
					* hard to read
					*  must implement for every file type
					* No one-size-fits-all standard

			* sidecar files
				* pro:
					+ easy 
					+ inspectable 
					+ versionable
				* Cons
					* synch issues / access contention
					* disconnectable.
	* Case studies
		* some concrete examples to illustrate the points
			* adding markup data to SOD
			* Why?
				* Data belongs in Maya, because it should be the same everywhere
				* We compromised on some degree of flexibility to make the process efficient
					* By comparison, the AI markup which had to be done in the Engine was a huge pain in the butt
				* Key goals: speed, simplicity
			* How?
				* YAML exporter
					* text based, declarative, and simple
				* Real data format != the artist format
					* volumes vs edges
				* LIBYaml importer
					* easy to use lib
					* contents negotiated (and
				* YAML as Sidecar file
					* No need to touch existing pipeline
					* Easy updated 
					* Total time to market \< 1 
					* Cons
						* Sidecar solution = no bulk reimport
			* adding effect targets to Daeomon
				* why?
					* Effects artists needed to be able to target bones or things-near-bones
					* Do it in Maya because the bones are not the same between characters
					* And the bones don't convey the shape
					* Maya tool can 'auto populate' - using bone names / fbik 
						* this way artists can handle exceptions instead of making the code do it.
				* How?
					* Custom attributes on FBX
					* Strip out Maya markers, replace with game entities
					* Do it on import, so there are no synch issues.
