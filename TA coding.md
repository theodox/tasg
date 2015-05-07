
# Survival Skill 2: Defensive design: TA coding
* Segue: In some ways, the same principles laid out in process analysis work for code too:
	* Identify and minimize unneeded dependencies
	* Predict ramifications
	* Minimize costs of making changes
	* In other words: it’s all about
		* Scope
		* Dependencies
		* and Flow
* TA's are programmers where perf is a secondary consideration
	%% is there a good place in here to discuss the similarities between TA coding and web dev?
	* slower languages
	* maintenance, uptime, flexibility more important than speed, memory efficiency
		++anecdotes about game programmers & python & eye-rolling
	* With our less demanding / more iterative environment, we can get sloppy. But we should not
		* We have less choice of environment; typically working with other people's choices
			* eg: the goofy max api or workflow limitations in Maya
			* e.g., lots of our critical data sits out where users can get at it.
		* We don't get help from compilers, etc
		* We don't work in a vacuum. If we screw up, other people pay for it
	* So, it's important to embrace your programmer personality
		* ...without sacrificing your inner artist!
		* this is a _demanding_ role!
* Coding style is driven by these needs:
	* optimize for flexibility, expansion, and maintenance.
	* OOP vs imperative
		* Most code lying around is jumped-up scripts, not systems
			* over the long term, the balance is shifting
		* short term: what works as long as it's safe
			* Good scope, smart design, simplicity all apply equally to OOP and imp
		* long term: OOP without the fanaticism is the way to go
	* Why OOP?
		* OOP is not about OBJECTS. It's about SCOPES ++ xref to discussion of scopes++
			* Discuss why the object metaphor is misleading
			* Keep data and code that works on data together
			* bundle data that should cooperate together
			* So OOP is a way of ISOLATING problems, not just a slicker way of writing the same functions
		## * compartmentalization: 
			* A key survivability feature
				* Battleship principle
			* Of course, this doesn't solve everything
				* the titanic was unsinkable because of compartmentalization
			* "Single responsibility" principle
				* Do one thing, do it well
			* Advantages:
				* Lots of little, specific functions are better than big monolithic hunks 
				* Little code localises errors well. if something is wrong it's either in the little function or in the context of the function
				* Little code is easier to test. More tests is just better!
					* Testing helps turn work into building blocks for future use.
				* Little code is inherently more reusable
				* Build big systems from little ones!

		## * Reuse!  
			* Modular code is much easier to adapt and re-use ++need good example here; maybe the YAML exporter from SDO++
			* "DRY" principle for both economy of effort and higher quality code
				* more often the code gets called, the better it is 
			* inheritance for customization
			* factory pattern for replacing multiple if/then 
				* **Advice** if statements are the enemy! [^1]
			* choices with a single choice of output
			* composition for more features
			* Don't go crazy with re-usability and generality:
				* the 'rule of three' and fully general code. Fully general code is HARD and trying to do it in the abstract is DANGEROUS. 
					> There are two "Rules of Three" in reuse: (a) It is three times as difficult to build reusable components as single use components, and (b) a reusable component should be tried out in three different applications before it will be sufficiently general to accept into a reuse library. [^2]
				* Instead, write 'fairly general code' and try to think about how to make it more general when the needs arises
			* **Advice** if you're cutting and pasting, you're probably doing it wrong.
		* So, OOP is not a technique for writing functions, it's a technique for better problem solving and analysis
		* classic OOP applications: 
			* GUI / function split
			* Modular rigging system
		* Less obvious examples:
			* separating the code the reads and writes files from the code that works on data
			* A modular system for metadata that does not know what the data actually means
		* Simple OOP example to make this concrete
			 %% side by side comparison of a simple exporter done OOP and imperative style would work well here
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
## * Fault tolerance
	* The biggest knock on TA code is shakiness. "It worked on my machine."
		* some of this is not our fault. 
			* We work in a weird environment, with our data lying around where users can poke  at it.
			* We are dependent on lots of other people's choices
			* Lots of configuration mishaps possible
	*  ++backref to @compartmentalization++ If you're writing good, tight, well scoped code (OOP or imperative) it's going to be better and less shaky
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

* Organization
	* It's imporant to understand where a given bit of code fits into the pecking order.
	* In well compartmentalized code, split over many files, this is particularly important
	* top tier: tools
		* here is where you make a actual assumptions about behavior
			* eg 'i always want to default to this kind of naming scheme' or 'do this if user asks me to do something impossible'
			* This layer faces the users: it's where you use applied psychology
			* This layer is likeliest to be project or product specific
			* It’ss also the one where there are lots of design and UI problems to solve
		* The majority of the code here is UI and application specific.  Most of the real work is done in lower level code.
		* Most tools are themselves split between the functionality and the UI
			* Often, a ‘Tool’ in the top tier is a thin wrapper around an API; it might be little more than a dialog that setup a request.

			* Most tools should be designed to run headless
				* this is how Maya and to a lesser degree max both with
			* it gives you much more flexibility to automate your processes - you never want to be scripting button pushes
			* It also gives you more freedom to refine your UI; ui is always fiddly and iterative.
	* middle tier: apis and libraries
		* This is the code that coordinates lots of smaller pieces into working toolkits for dealing with problems
		* This is the most technically demandig layer of your code!
			* here is where you apply your problem-analysis skills. 
			* What are the correct verbs and nouns for your particular problem sets?
			* Good design here makes for stronger tools
			* Mistakes here will dog all of the code that connects here
		* May be completely standalone, or depend on other pieces
			* examples
				* mGui
				* rPyc
				* BeautifulSoup
		* In python, particularly, this tier often contains lots of 3rd party modules and libraries
			* Use these when you can - it’s always best to leverage proven systems instead of reinventing the wheel
			* ++xref to @picking ads party modules++

		* Consistency and style count for a lot. Teach users how things work. Provide examples.
			* Tech Documentation really matters here.
		* for our purposes, lets say an API is a collection of modules, functions and classes that work together as part of a system, while a ‘module’ is just a collection of functions and classes that are related by subject matter:
			* lxml is an api: a way of working with xml
			* a bunch of functions that happen to  deal with and live in the same file XXXX are a module
			* Api’s, clearly are the stronger form of organization
			* But module have their place too, since they can provide a degree of organization to a code base which staves off  chaos
	* Bottom tier: functions / classes
		* This is the the place where actual work gets dome: the actual functions and classes which make things happen
			* Could be as simple as a short specialty function that correctly formats email addresses
			* Or as complex as a sophisticated geometry processing algorithm 
		* The key here is good scoping:
			* This code ought to be maximally re-usable
			* it ought to make the fewest assumptions about context & style
			* There is tension between maximum reuse and tight scoping: massive reuse means massive coupling, but on the other hand keeping your tools completely isolated makes for massive duplication
				* Example: a file path formatting module can be a big time saver - who want’s to write a zillion meaningless variations on a  + “/“  + b, etc?
				* On the other hand, do you want to import that modules into dozens of others?
			* While there’s is not one rule to tell you what to do, you can follow a few rules of thumb: 
				* The more often an module is imported elsewhere, the fewer modules it should import itself.
					* For example, a path formatting module is likely to be used in a lot of places, so it should probably be written with nothing but the standard library
					* An animation retargeting library, on the other hand, probably includes a lot of other code. So you don’t want to import it in a lot of places
					* If it base lots of pieces you want maybe they should be broken out into their own modules
			* Packages and subpackages
				* ++ need good reference here, or maybe a boxout, on packages and sub packages and how they relate to this++
		* Look at the system from the _other_ end : 
			* Tools are the end result of hundreds and hundreds of smaller pieces. 
			* APIs group the functions into collections that work together in an organized way
* At all 3 levels, the same basic principles apply:
	* Understand your scope
	* Work in the smallest scope you can
		* at each level, good code reads almost like pseudocode

[^1]:	[http://www.antiifcampaign.com/][1]

[^2]:	[http://www.codinghorror.com/blog/2004/09/the-delusion-of-reuse.html][2]

[1]:	http://www.antiifcampaign.com/ "Anti If Campaign"
[2]:	http://www.codinghorror.com/blog/2004/09/the-delusion-of-reuse.html