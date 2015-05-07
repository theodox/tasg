@picking 3rd party modules
## picking 3d party modules
* ++ probably forms a boxout or mini-chapter++
* Good ‘shopping’ for 3d party libraries and code - particularly, but not exclusively in Python - is a huge force multiplier for TA’s
	* Concentrate on your own problems, not generic ones that have been solved before
		* For example, you can write an XML file formatter or parser in a few hours with elementTree or LXML that would take weeks to do on your own — at lower quality
	* Particularly for python, lots of high quality code is available for free
* Picking external libraries
	* Start with the std lib
		* ++Seth Gibson: If you’re not using the stansardlib, you’re doing it wrong++
		* Lots of great stuff available for free
			* and no extra stuff to distribute
		* Often, a std lib solution is best even if it’s not technically optimal
			* it’s well understood,  and well documented
			* Usually - though not always - encourages idiomatic coding style
	* Open source projects
		* Always ‘try before you buy’. Every library has builtin an assumptions and limitations that may not be obvious at a glance
		* Many projects have enthusiastic supporters - or enthusiastic haters. Do some research to make sure you know what you’re getting:
	* Look for:
		* Dependencies: does the module depend on others? Do you have to include thousands of lines to use hundreds?
			* Examples:
				* Requests is a great help for dealing with web requests
				* But it depends on XXXX
		* Requirement: does the module impose limitations you can’t accept - like a binary plugin or a live net connections
			* Examples:
				* ++example needed here++
		* Licenses: is your company ok with the license? Are you ready to distribute your own source code to comply with the GPL? 
			* Many companies are automatically anti GPL
			* Always check with a lawyer
				* ++anecdote: Xnormal / crazybump and microsoft++
		* Project status: If the project is open source, is it still active? Are you comfortable with the project’s direction? Can you maintain if yourself
			* Example: 
				* ++PyJS++