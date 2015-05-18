@ Error handling
%% if we to do deep dives in code

* Importance of error management
	* Errors are inevitable. All code has bugs.
	* You'll spend more time debugging than you will creating
	* So, make your life easier with good tools
* Background: exception handling
	* Most of us look at errors and wish we had a way to make them just disappear.
	* However, that's not a great idea in the end.
		* You find flaws in the code by seeing bugs
		* The goal of good error handling is not to keep things from breaking.
			* How many times have you gotten a dialog that said something useless like "An error occurred".  Were you grateful? 
		* instead:
			* Save as much creative work as possible
			* Make sure you have the information you need to fix the bugs!
			* Keep your users from freaking out
			* Involve them in the QA process
	* What's an exception?
		* A situation where the computer can't do what you're asking:
			* as fundamental as divide by 0
			* as situational as looking for a missing file
			* as confusing as badly formed data
		* At that point the code goes boom
		* But TA languages don't just crash.
		* The irs metaphor:
			* I'm filling out taxes
				* putting data into places
					* doing worksheets and sub worksheets
					* When things go bad....
				* I work my way backwards through the whole stack, looking for help
			* If I don't find it, I give up and call the accountant.
		* In other words, code 'nests' different scopes as it goes along.
		* When an error happens, the code works back through the stack hopng somebody knows what to do
		* This is intimately related to goodn code scope:
			* limited, well scoped code does not want to decide how to recover from all problems - that's the job of high level strategic code
		* Try/Catch is how languages implement this paradigm
			* Try sets up a situation
			* Catch is the 'does this if something goes wrong' part
			* Always be specific in what you catch:
				* You can fix specific problems, but you can'd fix the set of all problems.
		* "Throw low, catch high"
			* allow exceptions in granular code with narrow scopes
			* Handle exceptions close to the user
			* EG: * * your XML library does not decided what to do when it encounters a locked file
				* You 'save-my-rig-to-xml' tool does decide - or more likely, it defers the ultimate authority: the user
* Global exception handling
	* Know you know all that, you know that the global handle doesn't fix things
		* there are too many possible problems to catch intelligently at that point
	* Instead, you want to use this opportunity to extract all the juicy debugging information that's caught in the stack
	* You want to save it out in a format you can study
	* you want to send it somewhere you can get at it
	* Ideally you want to ask the user to provide extra context
	* And then let things go on
* Python
	* sys.excepthook
	* Maya: guiexcepthook
	* YAML is a great way to serialize the data
		* it preserves object references
		* dumb serializer
	* JSON, XML are OK too
	* inspect module is great for inspecting the stack
	* 
* C\#
	* tbd
* Max
	* refer back to the talk
	* 
