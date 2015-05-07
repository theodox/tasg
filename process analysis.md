# Survial skill 1 : Process Analysis
%% Note lots of new verbiage here at the 0.9 level, needs work.  This is long enough that it does not seem to fit into the survival skills 'chapter'... should it stand alone
* Process analysis = Understanding data flow
	* learn to see the flow of data for an individual feature or the game as a whole.
	* it should work more or less like a DAG Graph, with all the information flowing one way....
	* Of course, it doesn't
		* for good reasons, like reviews, feedback, and course corrections
		* for bad reasons - like poor design and overconfidence
* Key goal of process analysis: to figure out the _why_ before the _how_
	* "It's too easy to "When you've got a new hammer, everything looks like a nail?" -- drive choices on strategy not on what you know best or what's at hand
	* Classic example: designing levels in Max 'because that's what we know'
		%% is there a good, non jargony source for this?  it looks like the academic term is 'process algebra' which  has an appealing ring but seems like it will bore readers to death [http://www.pst.ifi.lmu.de/Lehre/sose-2013/formale-spezifikation-und-verifikation/intro-to-pa.pdf][1]
* The basic concepts:
	## * *Flow
		* how does information get from one part of the system to another?
		* Is it automatic, as in updating a file?
		* Does it require an export or build?
			* Does that export/build require human intervention
		* What's 'upstream' or 'downstream' -- who makes changes, who consumes them
			* Examples:
				* change the skeleton, the animations change or are invalidated
				* change the uvs, the textures change
				* change import mode of a file, the results change
	## * Dependencies
		* Can I understand the flow relationships? Can I work back from what I see to what caused it?
		* Clarity and visualization are important for working with dependencies
		* examples:
			* does the animator see or set the value that might speed up his animations in game?  If the animation length or art changes, what happens in game?
			* If you change the shader on an object, does that change the build process for a whole level?
			* Key points:
				* explicit dependencies better than implicit ones
				* People who collaborate need to know where they are on the chain
				* Don’t lie to the users
				* ++Anecdote: bungie tag overrrides++
	## * Scope
		* What are the ramifications of a change?  Look at the examples above, you can see possibilities of problems because of hidden dependencies
		* If I move a building, do I move it's contents too?
		* If I change an animation, do I have to update a separate file for things to works
		* Visible dependencies are better than invisible ones
			* It makes sense that changing a texture changes model appearance.  It makes less sense that changes in a text file do.
		* logical dependencies are better than illogical ones
		* Small, clear scopes make like easy; big messy ones make life hard!
	## * Iteration
		* In theory everything forms a big directed graph
		* In practice, there are always going to be revisions
			* Due to project changes
			* Due to changes in tech
			* Due to art direction
			* Due to random events
		* A process that is unfriendly to iteration is _broken_.
	## * Project cost
		* The cost of a process is the sum of it's outflows.
		* Good understanding of the dependencies is key to getting good cost estimates
			* Example:
				* updating a building which has AI patching that it is maintained separately means not just new model and texture time
					* it also means updating the AI annotation
					* ...And making sure that the people who do the AI know they need to do the changes
					* ... and making sure that QA knows that the changes need to be tested
					* ... and making the costs of doing all these steps more than once if there is some kind of artistic or gameplay intangible involved
				* Scheduling failures frequently come from not counting the secondary costs or iteration costs
			* You can't ever predict costs with perfect accuracy. There are too many variables:
				* Tech problems
				* Different artist skill sets
				* handshake costs between different groups
				* artistic intangibles
			* You can, though, do better
				* Tech art is often the only discipline which knows the whole dependency web
				* Make sure that other groups are aware of the costs of what they want.
				* Keep record! Include 'after action reports' and notes.
					* IE, make sure that somebody who goes to change  model understands what the downstream costs are
					* Make sure other people 
* Key skills
	* _Seeing dependencies_
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
* _Prioritization_
	* Prioritize tools and processes for art tasks that demand iteration:
	* eg: designing multiplayer levels needs short turn around because of the need for fixes
		* You may have to accept aesthetic tradeoffs: if you need fast turnaround you can't always have perfect control
		* OTOH, if you have an expensive AAA cinematic experience, you can't ship substandard art, so you need to prioritize prettiness and precision
	* eg: get characters built to rough spec and animating before polish
		* That way you can spot things like poor proportions or art \<\> design mismatches early, before wasting a lot of resources
		* See things in context before committing to a 'we won't change this' plan!
* _iteration_
* It’s just not possible to solve all your problems in advance
	* it puts the most stress on the time when you know the least - you’re guaranteeing that your most important decisions rate being made in the dark	*  
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
			* Big lesson: this is a tough, tough problem because the dependencies are very hard to tease out
	*  shoot for the 80/20 rule. Get everything to 80% first, then take 20 % of the finished assets to 100
		* Make your polish decisions in the right context
		* Make polish decisions when you can also make cuts
			* At the end of a project you know what matters and what’s disposable
			* ++Anecdote: Half life scripted sequences++
* _Formalize workflows_
* Design tools to manage dependencies
	* "Tools are better than documentation"
	* "Tools _are_ documentation.
	* A good tool can encode dependency information into a human readable format; it provides good context for content decisions
	* Can encode a bunch of operations on the 'graph' into a single, human-understandable operation by a person.
		* Example: 
			* Animation system require several different sets of files to stay in synch:
				* A master animation registry that names and exposes all the files
				* A file of markers for IK targets that uses the names in the animation registry
				* Individual animation files
			* There may be good reasons for keeping all of this separate in the engine - but you can provide a good synthetic view of the whole thing with a tool that reads and writes all of the the files.
				* Minimizes version mismatches
				* provides good context for decision making
				* Minimizes typos
		* Of course this creates a new dependency for the project as a a whole - you need to keep the tool in sync with the process. But it's worth it, since it means that the the  
			*  %%OPEN QUESTIONS
				* Could you approach this as an analogue to continuous refactoring? Lots of small cheap changes instead of a few big ones?
				* What tools can you build to make this easier?
					* In this case: a custom rerig script specific to your change that can be batch applied
					* World space retargeting that can at least give visually similar results
					* Automated pose comparison tools to compare world-space differences between poses?
			* example: using shader templates
				* Shaders have lots of params
				* Many are intrisincly tied to lighting values
				* So, changes to global lighting can have many ripple effects
				* We'll cover multiple ways to do it
				* Side lesson:
					* As you can see, bulk changes are complex. It's best if shader parameter bundles are NOT part of a larger file:
					* Don't set your game sliders in max/maya!  
				* Options:
					* update hidden constants in the shaders
						* no user input, global
						* results not guaranteed to be identical
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
* _Expect problems_
* Nothing ever works as expected. No matter how hard you try to avoid process cycles and dead ends, things will change
	* for creative reasons
	* for business reasons
	* because of bugs
	* Just because
* When you foresee a particularly expensive, hard to iterate process: invest in fix-up tools:
	* eg, animation retargeting tools or shader rebuild tools as above
	* eg, distributed light builds
	* automate boring stuff (eg: SOD terrain intersection)
	* Always, always prefer open file formats that can be programmatically rewritten as needs change
	* Do bulk changes in a source control friendly way!
		* Create named changed lists - fewer the better
		* If possible, share (with shelve or similar) to other machines to see how these work with other kinds of state
		* Do bulk changes on up to date trees!
* _Refactor_
* No tool is ever done. Don’t let be afraid to rethink an old approach
	* Legacy tools can be a cost of their own
	* A tool is always in danger of becoming an obstacle to work
	* Example:
		* Bungie Guerrilla - the one tool to rule them all
			* It wasn't there to make work easier, it was only a tax of different tasks
				* Limited UI
				* No automation
				* opaque file formats
			* hard to extend, fix, maintain
		* Perfect example of the need to split UI from   functionality
	* **need to go deeper here....**
	* Example:
		* Unreal Ed 4
			* Slicker, faster, better --- but less flexible.
			* locks users away from data
	* General rule:
		* Split data format from tool just like you split functionality from UI
		* Tools can live a long time

[1]:	http://www.pst.ifi.lmu.de/Lehre/sose-2013/formale-spezifikation-und-verifikation/intro-to-pa.pdf