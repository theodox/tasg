@service
## Survival Skill 3: Service skills
* One of the hardest jobs a TA has is knowing what not to do.
* Tech work is often very seductive… its easy to get sucked in to perfecting an bit of code or rebuilding a system to make it bulletproof at the expense of things the team really needs
* Everything is about relationships…
	* TBD: include some of the stuff from the GDC talk 
	* All other aspects of the job depend on the relationships you create here
* What makes good service?
	* _Responsiveness_
		* The stereotype about technically inclined people is that they are anti-social and overly analytical
		* That might work for somebody who is buried deep in network code or writing a super high end shader compiler but it’s death for a TA
		* You need to be a reliable source of help and advice to your customers
		* _key tips_
			* Fast response time
				* Nothing helps a relationship like instant debugging information
				* Whenever your tools go bad, you should get an email or a text message or something
				* You should be at the user’s desk, unprompted, before they have time to write you an email
				* This goes hand in hand with good exception handling design ++xref++
			* Prioritize unblocking people
				* Idle users are unhappy users. Get them working - somehow - before you move on to ‘more important’ things
				* This might mean 
					* fixing it yourself
					* providing a temporary workaround
					* bandaid scripts
				* If need be, you should sacrifice your schedule for theirs (especially when lots of people involved)
				* Obviously, this is a fail case. This is why ++xref++ defensive design is so important.
			* After unblocking, bug fixes:
				* Bug fixes are important for two reasons
					* Most importantly, they help prove you care
					* Secondly, they increase overall reliability
						* At least, they should
						* If your code is well designed, most bug fixes should be small, localized improvements which increase the overall stability of the system - not sweeping changes!
				* new features and fancy new tech the lowest priority
					* It’s the riskiest and hardest to do right
					* But if you have a solid, functional foundation it’s far easier to do new tech correctly
					* 
		* _Reliability makes for good friends_
			* Release tools that are tested, tested and re-tested
				* Unit tests and human tests
					* ++xref to defensive design++
				* Schedule major releases in advance
					* make sure they don’t come close to deadlines!
					* Allow a couple of days for the dust to settle
					* Don’t surprise people!
			* 
	* What is success? 
		* Your first metric for success is how well people can use what you provide
			* The annals of tools programming are littered with systems that are theoretically brilliant but hated by their users.
			* A good tool is one which makes users happy
			* Sometimes, your job is helping your users see what they really want 
				* __Anecdote: The zipper ‘polygon reversal tool++
			* But of often it is giving them what they want even if it it’s not what you want.
			* You need to negotiated between the needs of the projects, the tastes of the users, and your own preferences.
				* The first two matter. The third does not !
				* ++ Anecdote: the bungie light map system.  Allowing people to think they have hand control when they don’t isn’t service: it’s pandering!++
		* Your second metric is building a good relationship with your users
			* Nothing gets tossed over the wall and forgotten
				* Keep tabs on who is happy
				* Keep tabs on what’s being used
				* Keep looking for ways to improve the user experience 
					* ++ x-ref  to defensive design: Well built tools are (fairly) easy to take apart and put back together in new ways as the project evolves++
	* _Communications_:
		* Your team has lots of needs
		* Some of them are very important to the project
		* Some matter a lot to only one person
			* And some times that persons is you
		* This means that you spend a lot of time prioritizing ( see the discussion of backlogs in the next chapter)
		* Make sure to communicate to your users the things that are shaping your current priorities so you can be clear with them about what you can - and can’t — do for them
		* Enhancing transparency
			* Write up your tasks when you get them
				* If a user makes a request, get it into written form and make sure they see your writeup
					* make the description as clear and concise as you can, but don’t burden it with details that can only interest you.
					* Send your written write up back to the users to make sure it’s really what they ask for
				* Don’t turn this into a bureaucratic hurdle - use it it as a tool for making your promises concrete
			* Make your backlog public
				* Putting your task list or backlog in a public place is a good way to for people to see how your work fits into the big picture
				* It lets users have a realistic sense of when their requests or bugs are really going to be looked at
				* It also helps them see what the competition for your time and energy is
				* If they’re not happy you can point them to the other stakeholders to help them negotiate a better priority list
		* _Standing up for your users_ 
			* Part of your job as a TA is to stand in for users who may not be able to stand up for themselves
			* You need to use the ++xref to project analysis++ skills you’ve got to help head off potential problems and keep the team from committing to grind work
			* Surprisingly, you may have a hard time selling this idea
				* Plenty of artists accept undue burdens without complaint:
					* “Oh I just have to do X… and Y… then Z… then make sure I didn[t forget Q… then try P and if that does’t work then R…” 
						]()* Familiarity often makes grunt work seem “simple”
					* But it’s not:
						* ++ get some cog sci research about cognitive load and finite decision queues++
						* Grunt work wastes brain power
			* Help educate the artists so they can stand up for themselves
			* Help educate the programmers so they don’t want to accept human-brain-wasting solutions 
			* Provide tools that bridge the gap
				* ++ Anecdote: Valve QC exporter.  Perfectly adequate for a programmer but very hard for artists.. it’s not conceptually difficult, it’s just a lot of things to remember and easy ways to shoot yourself in the foot.  TA provides a tool to make it routine.  Way better than just writing QC files for everybody else on the team!++
			*  1

