survival skills bullet points
{hidden}
> somewhere in here, hopefully note too long, a philosophical
> digression on 'scope' as it relates to both rigging and to
> code.  Good scopes are clear, well chosen and uncluttered; 
> Bad scopes are big, messy and have poorly defined boundaries
	 
* compartmentalized
	* Keep good control of the scope of what you're doing. Lots of little, specific functions are better than big monolithic hunks
		* Little code localises errors well. if something is wrong it's either in the little function or in the context of the function
		* Little code is easier to test. More tests is just better!
			* Testing helps turn work into building blocks for future use.
		* Little code is inherentlty more reusable
		* Build big systems from little ones!
* hierarchical
	* It's imporant to understand where a given bit of code fits into the pecking order. 
		* Decisiions which are appropriate for one level are wrong for another: 
			* eg: user provides and impossible name to a function that wants to save a file? Do you refuse to save, automatically rename, or pop up a dialog? The right answer depends entirely on context:  If you pop up dialogs in a batch app -- or just ignore what the user asked for in a gui app -- hilarity ensues.  Keep decisions in the appropriate scope!
		* Most hard-core code should live in the bottom tiers
		* Crazy application specific stuff is close to the top
		* GUI is almost always on top.
	* top tier: tools
		* here is where you make a actual assumptioins about behavior
			* eg 'i always want to default to this kind of naming scheme' or 'do this if user asks me to do something impossible'
			* This layer faces the users: it's where you use applied psychology
			* This layer is likeliest to be project or product specific
	* middle tier: apis < this might not be right name >
		* here is where you apply your problem-analysis skills. What are the correct verbs and nouns for your particlar problem sets? 
		* Consistency and style count for a lot. Teach users how things work. Provide examples.
		* Tech Documentation really matters here.
	* Bottom tier: functions / classes
		* This is where you a lot of practical stuff - renaming, formatting, finding, etc.
		* This code ought to be maximally re-usable
		* Wherever possible, this code should be borrowed! Ie, don't write your own XML read/write library - that's a done problem.
		* it ought to make the fewest assumptions about context & style
* Plan ahead
	* Code lives a long time
		* Bungie Tool code anecdote
	* It will be be debugged more than written
		* Kernigan quote
	* Design for long term maintenance
		* Avoid magical incantations
			* Document assumptions, workarounds, etc.
		* Avoid hard coded special stuff
			* Where possible, use config files or named constants
			* Include code that knows the magic hoops; use it everywhere instead of short cutting
		* Refactor over and over
			* As you understand the problem better, reflect that in what you do.
			* Lots of small fixes instead of a few big scary ones
			* IDE - Refactor is your friend
			* That said: Refactor to fix problems, not aesthetics
						 
				* Ie, if you have a working functions with the right signature and acceptable perf, it's a very low priority fix
				* OTOH, if you are forced to use 5 lines for 1 all over, that's a good fix candidate
			* Testing and refactoring go together well
			* Refactoring is usually worth it - but it's not free!
				* Apply your problem analysis skills (see XXX) to your public signatures. Are they descriptive? Are they succint? Are they expansible but not overly general?
			* TDD makes refactoring much less scary
	* Good reporting and notification tools are hard to come by - but important
		* In priority order:
			* Real time bug notices. Know what's breaking, with enough context to diagnose and fixt
				*  "context" may be pretty complex:
				* not just what line of code or what error.  What about:
					* User? Machine? OS? DCC version? these may all be useful diagnostic tools
					* Can you get a copy of the bad file? User may have messed with something in a wierd way
						* making people more productive is the core of the TA ethic
					* are you sure user has the right tool version?
			* Good mechanisms for submitting non-crash bugs and suggestions.  This should go into a public queue
				* art tools queue should be in another chapter, include xref
			* Error Stats. It's nice to know which tools/ modules/ functions are the most reliable
			* Usage stats - over the long haul it's good to know which tools do and don't get used
				* of course, stats can be a diversion from the real job too.
* process analysis
	* learn to see the flow of data for an individual feature or the game as a whole.
	* it should work more or less like a DAG Graph, with all the information flowing one way....
	* Of course, it doesn't
		* for good reasons, like reviews, feedback, and course corrections
		* for bad reasons - like poor design and overconfidence
	* Key skills
		* Learn to identify sources of trouble: what operations can't be undone?
			* analogy: construction history
			* simple example: 
				* UV's are downstream of geometry, won't survive major changes
				* animations are downstream of skeletons, again, wont' survive changes
				* AI navigation is downstream of level layout
			* complex examples:
				* Design input to a game level is downstream of some aspects of layout.  Can it be made more survivable?  If, eg, a mission marker is in a particular building, does it move with the building? Can you move the building and retain it's interior pathing? Etc.
				* Big changes to global lighting will probably involve a lot of shader changes too; the shader settings and the lighting environment are relative to each other.
				* Complex examples are often chicken-and-egg problems; learn to spot and minimize these.
			* There's a difference between changes with simple, mechanical outflows (like relighting a level, which involves a light bake) and those with creative or technical implications (like changing the skeleton of an existing character).  The former are annoyances; you can always throw cpu at the problem.  the latter need human intervention and are more disruptive, more expensive.
	* When designing a workflow, minimize the number of one-way gates
		* don't rely on 'we won't change it' - that rarely works
		* instead, design data structures or ways of looking at the problem that are survivable
			* example: SOD markup system
			* example: rigging and animating on an animation rig instead of base skeleton
			* example: using shader templates
	* When you see an unavoidable cycle, invest in fixup tools:
		* retarget animations
		* open file formats that can be programmatically rewritten as needs change
		* automate boring stuff (eg: SOD terrain intersection).