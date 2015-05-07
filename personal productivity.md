# Survival Skill 4: Personal productivity
%%
* Chaos Control
	* TA work life is extremely interrupt driven
		* fix this bug!
		* Solve this mystery!
		* Prove this concept
	* All these random tasks put a premium on organization
		* ++ include some cog sci research on task switching costs++
		* Steve jobs closet example
		* bad day at work example
		* It also puts the TA in a tough spot
			* frequently, the TA is the ‘institutional memory’ for a whole company - the only person who recalls the reasons why some crazy thing is being done
			* This is great for job security - but a lost way to live
				* for one thing, it’s stressful
				* for another, it’s usually harder than it seems
					* short term memory is very vivid
					* long term memory is unreliable
* Key tool: Documentation
	* Documentation is THE HARDEST part any technical job
	* There’s a reason there are technical writers!
		* Clear documentation for the public is  a full time job
		* The truth is always changing and always relative to other things
		* the whole system is in flux, keeping it up to date is hard
	* Many teams opt for the easy way out: no documentation
		* tribal knowledge decays over time
		* it’s not uncommon for people to become ‘gatekeepers’ for a process or a tool
			* ++anecdote: Paul Vosper++
		* Fiefdoms and tribal knowledge are bad things
			* communication delays
			* politics
			* What happens if they get run over by a bus?!
	* A partial solution: literate tools
		*  Build important knowledge directly into the tools
			* ++anecdote : the crytek exporter checklist.  Way too much crap for anybody to sit down and memorize (and we didn’t know the whole problem set to begin with anyway). Instead of writing documentation, it became part of the tool itself.  This educates the users by sheer repetition. It also stays current since you have to maintain it.++ 
			* Link directly to the wiki from inside your tools; use wiki as the ‘display’ for your help links etc
	* A partial solution: the wiki
		* A good wiki is a great thing
			* fast to edit
			* flexible
			* communal
		* Unfortunately, it’s not perfect
			* only 10% of users will actively contribute
			* Stale knowledge piles up
			* important info can get lost
		* Unless you’re on a big team with dedicated tech writers, don’t assume the entire wiki is authoritative
			* Identify the key parts which must be up to date and keep them up to date
				* New user docs
				* Critical path procedure docs
				* ideally “doc tests”
			* Encourage users to contribute
				* “Can you write down what you’re doing so I can show it to XXX” is a key part of the discover process
			* Encourage users to comment if they don’t contribute
				* “Can you put a comment about that on the XXX wiki page until I get it fixed?” Should be a standerd part of bug triage
			* Teach everybody to use links!
				* link to your backlog
				* link to bugs
				* link to ‘authoritative docs’
			* Treat wiki fail as bugs!
	* A partial solution: Multimodal communication
		* Nobody reads anything
		* … until they need it
		* Don’t rely on any single mode of communication!
			* Send emails
				* with links to wiki pages
			* Include doc links inside your tools
			* Do videos
			* Do seminars
			* Do tooltips 
			* Provide ‘message of the day”
		* None of these individually is going to reach everybody
			* Collectively, though, you can make sure that knowledge is well diffused
			* Ideally, if user X doesn’t know user Y can point to the right link/email/wiki page before they call you
			* Encouraging users to share 
		* A partial solution: API Docs
			* Code comments are controversial among programmers
				* Some say they are redundant 
				* Others make then a fetish
				* Personally, I feel like there’s a big difference between tactical and strategic documentation
					* Tactical:
						* “loop over these items, finding the ones which are templates and have more than 50 vertices, then prep them for export…”
					* Strategic:
						* “This module provides two tools for managing animation retargeting.  The RetargetPose function is used for (example here) and provides (YYY) functionality.  The ZZZ tool, on the other hand, is used for QQQ….”
					* Tactical documentation is mostly a luxury: in most cases, a new programmer reading the code is going to have to sort through the details= anyway so this is often redundant
					* Strategic docs on the other hand and very important: they  mean you don’t have to read the whole library through in order to use it. 
						* This is is especially important if you have a big team where lots of people will be touching the code.
						* You want to lower the barrier to reuse so that people find it easier to use library code than to reinvent the wheel
						* You want to make it clear how a set of tools is intended to be used so users can tell when the tools aren’t working!
				* Depending on the nature of the team, python docstrings may be enough
					* it matters a lot if you have search-in-files functionality!
					* In languages which don’t support docstrings  - e.g. mxs — a similar convention is a good idea
						* ++anecdote: Scripthelp++
				* On big teams it becomes more important to provide discoverability; using something like sphinx or epydoc to generate Searchable docs is a great  tool for helping users know of the existence of tools and code they may not have written themselves.
	* _Key Tool: Backlog_
		* Backlogs are great 
			* They show other people what you're up to
				* Make it public!
			* They reflect the real truth: you only do one thing at a time.
			* Return to the backlog every week or so
				* Don't be afraid to reprioritize: thing change all the time.
			* Trello, text files, fog bugs, whatever
		* even if your team doesn't do agile!
		* keep track of all your recursion levels
		* You think you'll remember - but you won't.  Write it down!
			* Provide context where you can
	* Time is a fixed resource
		* decide how and when to tackle a problem - don't drop everything automatically!
			* how you prioritize is up to you
			* but here are some things to consider
				* task switch costs
					* it's easier to jump between tasks if they are at least related, e.g., put off all your lighting problems until next week and then hit them in a block
				* relative priorities
					* What's blocking other people?
					* What's important to the project?
					* What has long term implications?
					* Down at the bottom: 
						* what's cool?
						* what's interesting?
						* what's fun?
					* this is sad, but it's also the difference between a talented hobbyist and a pro.
					* Plus, good prioritization helps you earn the freedom to pick your projects.
* Detective skills
	* A lot of TA work is forensic: figuring out why things went wrong
	* You're likely to be the first person asked when something doesn't work
		* You want to either find an answer or find the person who knows it... quickly
		* Mysteries are bad for business
			* Artists can be superstitious
				* Once knew an artist who was mortally convinced his problems stemmed from how close he put his keyboard to his monitor
				* Many artists stop using something when it breaks and never check for the fix
				* This is one of the differentiators between TAs and line artists.
					* Don't get snarky about it!
					* Line guys have problems you don't like finicky art directors and looming deadlines
	* How can you be a good detective?
		* Ask good questions
			* create and refine a standard set of questions
				* What were you doing when it happened?
				* Did you do anything unusual?
				* Is this your file or somebody else's?
				* What have you tried to get around it
				%% need some good qa advice here%%
		* get accurate repro steps, ideally from the person who reported the bug
			* You want to train your users to learn your debugging methods, - over time you;ll make each other more efficient
			* look for patterns, try to recognize common cases
				* It's usually bad data; a typo, an extra suffix, a bad character or something similar...
					* Games are like programming languages: finicky and "syntax" obsessed
				* After that, it's likely to be a bug in a TA tool.
				* Then in in-house tools
				* then the engine / dcc / etc.
					* Sure, the big boys have bugs too: but they are rarer than in-house ones.  That's how they make their living
		* Make sure you build good debugging tools
			* Real time bug notices. Know what's breaking, with enough context to diagnose and fix it
				*  "context" may be pretty complex:
				* not just what line of code or what error.  What about:
					* User? Machine? OS? DCC version? these may all be useful diagnostic tools
					* Can you get a copy of the bad file? User may have messed with something in a wierd way
						* making people more productive is the core of the TA ethic
					* are you sure user has the right tool version?
				* ++ this might be a good place for giveaway code++
			* Good mechanisms for submitting non-crash bugs and suggestions.  
				* “Report me” button should go into a public queue
			* Automatic stats collection
				* ++ good place for a guest plug from Jeff Hanna / Adam++
				* Error Stats. 
					* \It's nice to know which tools/ modules/ functions are the most reliable
					* Lots of bugs concentrated in a single module is a warning flag about design flaws
				* Usage stats - over the long haul it's good to know which tools do and don't get used
					* of course, stats can be a diversion from the real job too
			* Coordinate with programming team on high-quality, user-friendly error messages
				* Users that you (or other programmers) understand may not mean much to end users
				* Make sure to provide as much built in translation as you can.
					* Often providing a ‘translator’ is a very valuable tool
					* ++ example: crytek engine error warnings \> human readable warnings++