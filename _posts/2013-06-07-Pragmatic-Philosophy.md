---

layout: default
title: Pragmatic Philosophy

---

# Pragmatic Philosophy

This is all my notes about the [Pragmatic Programmer](http://pragprog.com/the-pragmatic-programmer), 
everyone should buy and read this book.

It's a bible for a programmer.

### Remember the big picture!

### Critical Thinker
- Think! About your work!
- Remember the big picture, always!
- Dont live with broken windows, never!
- Make quality a requirement issue
- Provide options, dont make lame excuses
- Invest regularly in your knowledge portfolio
- Care about your craft
- Listen to Nagging Doubts - Start when you're ready! (only when you're ready!)
- Critically analyze what you read and hear
- Be a catalyst for change
- An Object should do only one work, and do your work as well
- Eliminate Effects Between Unrelated Things
- There are no Final decisions
- Use Tracer Bullets to Find the target (Seek and destroy!)
- Protoype to learn
- Program Close to the Problem domain
- Estimate to avoid surprises
- Iterate the schedule with the code
- Keep knowledge in plain text
- Use the power of shell script (oh i got the power!)
- Use a single editor well
- Fix the problem, not the blame
- Dont panic! x)
- select isnt broken!
- Dont assume it - PROVE IT!
- Learn a Text Manipulation Language
- Write Code That writes code (sounds awesome)
- You cant write perfect software
- Design with Contracts
- Code defensively
- Crash Early
- If it cant happen, use assertions to ensure that it wont.
- Use Exceptions for Exceptional Problems
- Finish what you start! 
- Minimize Coupling between modules
- Configure, Dont Integrate
- Put abstractions in Code Details in Metadata
- Analyze workflow to improve concurrency
- Design using services
- Always design for concurrency
- Separate views from models (obvious)
- Use Blackboards to Coordinate Workflow
- Don't code like an idiot, understand what you're writing
- Constantly look for room for improvement and design
- Don't Program by Coincidence
- Estimate the order of your Algorithms
- Always test your estimates
- Design to test
- Test your software, or your users will (worst!)
- Dont use wizard code you dont understand
- Dont gather Requirements - Dig for them!
- Work with a user to think like a user
- Abstractions live longer than details
- Use a project glossary
- Maybe it looks imposibble. But is it really as hard as it seems?
- "Seeing further"
- Dont think outside the box - Find the box
- Some things are better done than described
- Dont be a slave to formal methods
- Expensive too do not produce better designs
- Organize around functionality, not job functions
- Dont use manual procedures
- Test early, test often, test automatically!
- Find your own bugs, dont let the others find for you!
- Coding aint done til all the tests run!
- Use saboteurs to test your testing
- Test state coverage, not code coverage
- Find bugs once
- Treat English as just another programming language
- Build documentation in, don't bolt it on
- Gently exceed your users' expectations
- Sign Your Work

<!--break-->

## Code a little, test a little

## Do unto others as you would have them do unto you

#### I wrote this, and I stand behind my work

####  People should see your name on a piece of code and expect it to be solid, well written, tested, and documented. A really professional job. Written by a real professional.

## Always try to discover the root cause of a problem, not just this particular appearance of it.

### It's a continuous process
### Take responsibility

### Comunicate
 Before you talk to anyone, by email, voice our chat, try it out before talking with your monitor or your dog, test if your arguments are right, try to imagine what they will say, what you can improve, what is the best to hit your audience.
 - Make it look good
 - Know your audience
 - Involve your audience
 - Be a Listener
 - Get back to people
 - Chose your moment

#### Know what you want to say and know how to say that

#### WISDOM acrostic (What / Is / Sophisticated / Detail / Own / Motivate)
  What do you want them to learn ?
  What is their interest in what you've got to say ?
  How sophisticated are they ?
  How much detail do they want ?
  Whom do you want to own the information ?
  How can you motivate them to listen to you ?

An investment in knowledge always pays the best interest. - Benjamin Franklin

---

# A Pragmatic Approach

## The evils of duplication

### DRY - (NEVER)Dont Repeat Yourself

- Documantation and code, document better your code
 - Write more comments, let the people know what happens when they see the file, but never duplicate
 - Know what you'll write before do it
 - Use the header files to document interface issues, and the implementation files to document the nitty-gritty details that users of your code dont need to know.

###  Don't rely on the properties of things you cant control.

### Orthogonal approach
 - Increased productivity
 - Reduced risk
 - If I dramatically change the requirements behind a particular function, how many things are affected?
 - If an object persistence scheme is transparent, then its orthogonal. If it requires you to create or access objects in a special way, then its not.

#### Toolkits and Libraries
 - Think twice about what you wanna introduce 

#### Keep your code deocupled. - Write shy code
#### Avoid global data
#### Avoid similar functions

#### Building unit tests

### Nothing is more dangerous than an idea if its the only one you have
 - How many possibles futures can your code support?
 - Which ones are more likely?
 - How hard will it be to support them when the time comes?

### Things to prototype
 - Architecture
 - New functionality in an existing system
 - Structure or contents of external data
 - Third-party tools or components
 - Performance issues
 - User interface design

When prototyping whe can ignore some details:
 - Correctness
 - Completeness
 - Robustness
 - Style

#### Prototyping Architecture
 - Are the responsibilities of the major components well defined and appropriate?
 - Are the collabrations between major compnents well defined?
 - Is coupling minimized?
 - Can you identify potential sources of duplication?
 - Are interface definitions and constraints acceptable?
 - Does every module have an access path to the data it needs during execution? Does it have that access when it needs it?

"If you feel there is a strong possibility in your environment or culture that the purpose of prototype code may be misinterpreted, you may be better off with the tracer bullet approach. You'll end up with a solid framework on which to base future development."

### The limits of language are the limits of one's world. - Ludwig Von Wittgenstein

#### Mini-Language
 - BNF

Data languages produce some form of data structure used by an application. These languages are often used to represent configuration information.

Imperative languages take this a step further. 

##### Exercises!
    
    var commands = { };
    function addCommand(name, direction) {
        commands[name] = direction;
    }
    function moveTo(command, squares) {
        if (isSelection(commands[command])) {
            return execSelect(commands[command], squares);
        }
        goTo(commands[command], squares);
    }
    function goTo(direction, squares) {

    }

    addCommand('P', 'select');
    addCommand('D', 'down');
    addCommand('W', 'west');
    addCommand('N', 'north');
    addCommand('S', 'south');
    addCommand('U', 'unselect');

    moveTo('P', 2);
    moveTo('D');

- BNF Grammar ? Backus Naur Form Pag. 76 Exercises, 5 to 8
 Back to exercises when I know exactly what is a BNF Grammar
 

### Estimating

#### How accurate is accurate enough?
 - Context
 - Calculate the answears
 - The units you use make a difference in the interpretation of the result.
 - Understand what's being asked.
 - Think about the scope before starting to guess.
 - Reexamine the original question
 - Components
 - Work out which parameters have the most impact on the result
 - Dont base your estimate in other subestimates
 - When an estimate turns out wrong, don't just shrug and walk away. 
 
##### Estimating Project Schedules
 - Check requirements
 - Analyze risk
 - Design, implement, integrate
 - Validate with the users

 "How long it will gonna take?" - "I'll back to you" - Think, and analyze carefully, dont guess.

### Keep a log of your estimates
 - Track how accurate you turned out to be. If your error was greater than 50%, try to find out where your estimate went wrong.

---
## The Basic Tools
 - Learn and adaptation
 - Always be on the lookout for better ways of doing things.

### Unix Philosophy
 - Small, sharp tools, each intended to do one thing well.

### Code, Develop Object Models, Write Documentation and Automate Buil Process

### Github FTW

Its a painful thing, to look at your own trouble and know that you youserlf and no one else has made it. - Sophocles, Ajax

### Debugging
 - Its very important to step back a pace, and actually think about what could be causing the symptoms that you believe indicate a bug.

Beware of myopia when debugging. Resist the urge to fix just the symptoms you see: it is more likely that the actual fault may be several steps removed from what you are observing, and may involve a number of other related things. Always try to discover the root cause of a problem, not just this particular apperance of it.

You must brutally test both boundary conditions and realistic end-user usage patterns. You need to do this systematically.

- Once you think you know what is going on, its time to find out what the program thinks is going on.
- The simple act of explaining, step by step, what the code is supposed to do often causes the problem to leap off the screen and announce itself.

#### Debugging checklist
 - Is the problem being reported a direct result of the underlying bug, or merely a symptom?
 - Is the bug really in that place ? Is it in the OS ? Is the User ? Or is it in your code?
 - If you explained this problem in detail to a coworker, what would you say?
 - If the suspect code passes its unit tests, are the tests complete enough? What happens if you run the unit test with this data?
 - Do the conditions that caused this bug exist anywhere else in the system?


### Code that writes code
 - Passive Code Generator are run once to produce a result. From that point forward, the result becomes freestanding - it is divorced from the code generator.

 - Active Code Generator are used each time their results are required. The result is a throw-away - it can always be reproduced by the code generator. Often, active code generators read some form of script or control file to produce their results.

### Dont trust yourself, either.

When everybody actually is out to get you, paranoia is just good thinking. - Woody Alien

### Design by contract

Nothing astonishes men so much as common sense and plain dealing. - Ralph Waldo Emerson, Essays.#

What is a correct program? One that does no more and n less than it claims to do.
 - Preconditions.
 - Postconditions.
 - Class invariants.
 - Loop invariants.
   "A loop invariant is a statement of the eventual goal of a loop, but is generalized so that it is also valid before the loop executes and on each iteration through the loop. You can think of it as a kind of miniature contract. The classic example is a routine that finds the maximum value in an array."
 - Semantic invariants.
   "It must be central to the very meaning of a thing, and not subject of the whims of policy (which is what more dynamic busniess rules are for).

"If all the routine's preconditions are met by the caller, the routine shall guarantee that all postconditions and invariants will be true when it completes."

"Subclasses must be usable through the base class interface without the need for the user to know the difference."
You want to make sure that the new subtype you have created really "is-a-kind-of" the base type.

Its much easier to find and diagnose the problem by crashing early, at the root of the problem.

Be sure not to confuse requirements that are fixed, inviolate laws with those that are merely policies that might change with a new management regime.

#### Dynamic Contracts and Agents

Points to ponder: If DBC is so powerful, why isnt it used more widely ? Is it hard to come up with the contract ? Does it make you think about issues you'd rather ignore for now? Does it force you to THINK ?? Clearly, this is a dangerous tool!


### Dead Programs Tell no Lies
 We want to know when the "impossible" has happened.
 All errors give you information. You could convice yourself that the error cant happen, and choose to ignore it. 
 Instead, Pragmatic Programmers tell themselves that if there is an error, somethinng very, very bad has happened.
 
 A dead program normally does a lot less damage than a crippled one.


### Assertive Programming
 There is a luxury in self-reproach. When we blam ourselves we feel no one else has a right to blame us. - Oscar Wilde, the Picture of Dorian Gray
 Never put code that must be executed into an assert.
 Dont use assertions in place of real error handling. Assertions check for things that should never happen.
 Your first line of defense is checking for any possible error, and your second is using assertions to try to detect those you've missed.

throws an Exception only when something that we dont expect happens.


### How to balance resources
 "I brought you into this world, " my father(if i have one) would say, " and I can take you out. It dont make no difference to me. I'll just make another one like you." - Bill Cosby, Fatherhood.

### Nest allocations
 - Deallocate resources in the opposite order to that in which you allocate them. That way you wont orphan resource if one resource contains references to another.
 - When allocating same set of resources in different places in your code, always allocate them in the same order. This will reduce the possibility of deadlock. (If proccess A claims resource1, the two proccess will wait forever.)

Allocates a resource should be responsible for deallocating it.

"Garbage collector"

In C++ Exceptions can interfere with resource deallocation.

#### Checking the Balance
 Build code that actually check that resource are indeed freed appropriately.

---

## Bend or Break

- A good way to stay flexible is to write less code.

### Decoupling and the Law of Demeter

 Good fences make good neighbors. - Robert Frost, "Mending Wall"
 - Organize your code into cells (modules/layers/..) and limit interaction between them.

 "When we ask an object for a particular service, we'd like the service to be performed on our behalf. We do not want the object to give us a third-party object that we have to deal with to get the required service."

 - Build independent "layers", a model does not need to know anything about the other.

### The Law of Demeter for functions
 
 The Law of Demeter for functions states that any method of an object should call only methods belonging to.
 The object must delegate and manage any and all subcontractors directly, without involving clients.
 
 A preprocessor that generates calls automatically will be very awesome with some languages such as C++ or even PHP, and this preprocessor should be run as part of the build/deploy.

### Metaprogramming
 No amount of genius can overcome a preoccupation with detail. - Levy's Eighth Law

 - Out with details!
 - Metadata is data about data, using the term in its broadest sense, Metadata is any data that describes the application.
 - For business logic, write rules no cut codes.
 - Dont write Dodo-Code

 Always think;
  - How much of the application might be moved out of the program itself to metadata?
  - What would the resultant "engine" look like?
  - Would you be able to reuse that engine in the context of a different application?

#### Temporal coupling
 - Its all about time.
 - Improve for concurrency

#### Architeture
 - (Always) Design for concurrency
 - Cleaner interfaces

### It's just a view

### Blackboards
A blackboard system let us decouple our objects from each other completely, providing a forum where knowledge cosumers and producers can exchange data anonymously and asynchronously.

## While you are coding
 THINK!

Do not program by Coincidence, just because a code works now it does NOT means anything, unless you know exactly what it are doing.
A code can works just for coincidence, do NOT be lazy, figure out what it really does.

- Accidents of Implementation are things that happen simple because that's the way the code is currently written
- Understand exactly what the code does and what is his purpose.

Always think:
 - It may not really be working - it might just look like it is.
 - The boundary condition you rely on may be just an accident. In different circumstances, it might behave differently.
 - Undocumented behavior may change with the next release of the library.
 - Additional calls also increase the risk of introducing new bugs of their own.

For code you write that others will call, the basic principles of good modularization and hiding implementation behind small, well-documented interfaces can all help. Awell-specified contract can help eliminate misunderstandings.

For code you call, rely only on documented behavior. If you can't, for whatever reason, then document your assumption as well.

Assumptions that aren't based on well-established facts are the bane of all projects.

### How to Program deliberately
 - Always be aware of what you are doing. Dont end like the frog.
 - Don't code blindfolded. Attempting to build an application you don't fully understand, or to use a technology you aren't familiar with, is an invitation to be misled by coincidences.
 - Proceed from a plan, whether that plan is in your head, on theback of a cocktail napkin, or on a wall-sized printout from a CASE tool.
 - Document your assumptions.
 - Don't just test your code, but test your assumptions as well. Don't guess; actually try it. Write an assertion to test your assumptions.
 - Prioritize your effort. Spend time on the important aspects.
 - Don't be a slave to history. Don't let existing code dictate future code. All code can be replaced if it is no long appropriate.

### Algorithm Speed

#### O() Notation

##### Commom Sense Estimation
 - Simple loops. If a simple loop runs from 1 to n, then the algorithm is likely to be O(n)—time increases linearly with n. Examples include exhaustive searches, finding the maximum value in an array, and generating checksums.

 - Nested loops. If you nest a loop inside another, then your algorithm becomes O(m × n), where m and n are the two loops' limits. This commonly occurs in simple sorting algorithms, such as bubble sort, where the outer loop scans each element in the array in turn, and the inner loop works out where to place that element in the sorted result. Such sorting algorithms tend to be O(n2).

 - Binary chop. If your algorithm halves the set of things it considers each time around the loop, then it is likely to be logarithmic, O(lg(n)) (see Exercise 37). A binary search of a sorted list, traversing a binary tree, and finding the first set bit in a machine word can all be O(lg(n)).

 - Divide and conquer. Algorithms that partition their input, work on the two halves independently, and then combine the result can be O(n lg(n)). The classic example is quicksort, which works by partitioning the data into two halves and recursively sorting each. Although technically O(n2), because its behavior degrades when it is fed sorted input, the average runtime of quicksort is O(n lg(n)).

 - Combinatoric. Whenever algorithms start looking at the permutations of things, their running times may get out of hand. This is because permutations involve factorials (there are 5! = 5 × 4 × 3 × 2 × 1 = 120 permutations of the digits from 1 to 5). Time a combinatoric algorithm for five elements: it will take six times longer to run it for six, and 42 times longer for seven. Examples include algorithms for many of the acknowledged hard problems—the traveling salesman problem, optimally packing things into a container, partitioning a set of numbers so that each set has the same total, and so on. Often, heuristics are used to reduce the running times of these types of algorithms in particular problem domains.

### Best isnt always best.
You also need to be pragmatic about choosing appropriate algorithms—the fastest one is not always the best for the job. 

### Code that's easy to test
 - Test against contract

 - Design the contract
 - Design the test
 - Design your code

 - Log status

#### Test harnesses
 - A standard way to specify setup and cleanup
 - A method for selecting individual tests or all available tests
 - A means of analyzing output for expected (or unexpected) results
 - A standardized form of failure reporting

 - Ad Hoc Testing - Formalize the tests on-the-fly and put it on tests

"During debugging, we may end up creating some particular tests on-the-fly. At the end of debugging session you need to formalize the adhoc test. If the code broke once, it is likely to break again. Dont just throw away the test you created; add it to the existing unit test."

A culture of testing
 - All software you write will be tested - if not by you and your team, then by the users - so you might as well plan on testing it thoroughly.


### Before the Project
 - The Requirements

#### The Requirements Pit
 Perfection is achieved, not when there is nothing left to add, but when there is nothing left to take away... - Antoine de St. Expuery, Wind, Sand, and Stars, 1939

##### Digging for requirements
 - Is this statement truly a requirement?

##### Documenting requirements
 The functions the engineers needed were sometimes hidden behind obscure names, or were achieved with nonintuitive combinations of basic facilities.
 We must be able to provide a transition to the future.

 - Successful tools adapt to the hands that use them.

##### Use case template

A. Characteristic Information
 - Goal in context
 - Scope
 - Level
 - Preconditions
 - Success end condition
 - Failed end contiion
 - Primary actor
 - Trigger
B. Main Success Scenarion
C. Extensions
D. Variations
E. Related Information
 - Priority
 - Performance target
 - Frequency
 - Superordinate use case
 - Channel to primary actor
 - Secondary actors
 - Channel to secondary actors
F. Schedule
G. Open issues


- Dont be a slave to any notation; use whatever method best communicates therequirements with your audience.

### Solving impossible puzzles

- Recognize the constraints placed on you
- Recognize the degrees of freedom you do have

When faced with an intractable problem, enumerate all the possible avenues you have before you. Don't dismiss anything, no matter how unusable or stupid it sounds. Now go through the list and explain why a certain path cannot be taken. Are you sure? Can you prove it?

#### There must be an easier way!

 - Is there an easier way ?
 - Are you trying to solve the right problem, or have you been distracted by a peripheral technicality ?
 - Why is this thing a problem ?
 - What is it that's making it so hard to solve ?
 - Does it have to be done this way ?
 - Does it have to be done at all ?

- Real constraints, the misleading constraints, and the widsom to know the difference

### Not until you're ready

When you feel a nagging doubt, or experience some reluctance when faced with a task, heed it. You may not be able to put your finger on exactly what's wrong, but give it time and your doubts will probably crystallize into something more solid, something you can address. 
Let your instincts contribute to your performance.

#### Good Judgment or Procrastination ?

How can you tell when you're simply procrastinating, rather than responsibly waiting for all the pieces to fall into place?

A technique that has worked for us in these circumstances is to start prototyping. Choose an area that you feel will be difficult and begin producing some kind of proof of concept. One of two things will typically happen. Shortly after starting, you may feel that you're wasting your time. This boredom is probably a good indication that your initial reluctance was just a desire to put off the commitment to start. Give up on the prototype, and hack into the real development.
On the other hand, as the prototype progresses you may have one of those moments of revelation when you suddenly realize that some basic premise was wrong. Not only that, but you'll see clearly how you can put it right. You'll feel comfortable abandoning the prototype and launching into the project proper. Your instincts were right, and you've just saved yourself and your team a considerable amount of wasted effort.

##### When you make the decision to prototype as a way of investigating your unease, be sure to remember why you're doing it.

### The Specification Trap
 Specification and implementation are simply different aspects of the same process - an attempt to capture abnd codify a requirement. Each should flow directly into the next, with no artificial boundaries.

It's all to easy to specify something that can't be built.

"When your entire output is seen as a set of routine calls, you'd better make sure those calls are well specified."

The longer you allow specifications to be security blankets, protecting developers from the scary world of writing code, the harder it will be to move on to hacking out code. Don't fall into this specification spiral: at some point, you need to start coding! If you find your team all wrapped up in warm, comfy specifications, break them out. Look at prototyping, or consider a tracer bullet development.

"We like to write adaptable, dynamic systems, using metadata to allow us to change the character of applications at runtime. Most current formal methods combine a static object or data model with some kind of event- or activity-charting mechanism. We haven't yet come across one that allows us to illustrate the kind of dynamism we feel systems should exhibit. In fact, most formal methods will lead you astray, encouraging you to set up static relationships between objects that really should be knitted together dynamically"

- Formal methods are just one more tool in the toolbox.

#### You should work constantly to refine and improve your processes. Never accept the rigid confines of a methodology as the limits of your world.

---

### Pragmatic Projects
#### Pragmatic teams
 - No broken windows
 - Boiled frog
  You simply need to be aware that they're happening, otherwise, it'll be you in the hot water.
 - Communicate
 - DRY
 - Orthogonality
 - Automation
 - Know when to stop adding paint

### All on automatic
 - Full build run all available tests.
"When you donbt run tests regularly, you may discover that the app broke due to a code change made three months ago. Good luck finding that one"

 git is so awesome!

Let the computer do the repetitious - it will do a better job of it than we would. We've got more important and more difficult things to do.

### Ruthless testing
 - The earlier a bug is found, the cheaper it is to remedy.
 - Code a little, test a little.
 - The time it takes to produce this test code is worth the effortr

# Just because you have finished hacking out a piece of code doesn't mean you can go tell your boss or your client that it's done. IT'S NOT! 
# First of all, code is never really done. More importantly, you can't claim that it is usable by anyone until it passes all of the available tests.

 - What to test
 - How to test
 - When to test

### What to test
 - Unit testing
 - Integration testing
 - Validation and verification
 - Resource exhaustion, errors, and recovery
 - Performance testing
 - Usability testing
 - (More, more, more, and more ... We never have too much tests)

The users told you what they wanted, but is it what they need?

When the system does fail, will it fail gracefully? Will it try, as best it can, to save its state and preven loss of work? Or will it will blows in the user's face?
We want to the tools that we create for users fit their like an extension of their hands.
Failure to meet usability criteria is just as big as bug as dividing by zero.

Test the Design/Methodology of our code
 - McCabe Cyclomatic Complexity Metric
 - Inheritance fan-in (number of base classes) and fan-out (number of derrived modules using this one as a parent)
 - Response set (Law of Demeter)
 - Class coupling ratios

- Use real test data often then synthetic data.

#### Test the tests

- Once a human testers finds a bug, it should be the last time a human tester finds that bug. Make a test for that bug, every time a bug appears, otherwise, it WILL happen again
 - Test the interface, and all the things a user can make to broken something, never let the human tester find a bug.

### It's all writing

 The palest ink is better than the best memory. - Chinese Proverb

Document everything, i mean everything, document the code, outside of code explaining to normal people what the routine does.

Apply all of our pragmatic principles to documentation as well as to code.

#### Internal Documentation

##### Comments in code
 Comments should discuss why something is done, its purpose and its goal.

Commenting source code gives you the perfect opportunity to document those elusive bits of a project that can't be documented anywhere else: engineering trade-offs, why decisions were made, what other alternatives were discarded, and so on.
We like to see a simple module-level header comment, comments for significant data and type declarations, and a brief per-class and per-method header, describing how the function is used and anything that it does that is not obvious.
Remember that you (and others after you) will be reading the code many hundreds of times, but only writing it a few times. Take the time to spell out connectionPool instead of cp.

Should not appear in source comments:
 - A list of functions exported by code in the file.
 - Revision history
 - A list of other files this file uses
 - The name of the file

With meaningful comments in place, we can use tools to extract and format them to automatically produce API-level documentation.


Documentation and code are different views of the same underlying model, but the view is all that should be different.
Don't let documentation become a second-class citizen, banished from the main project workflow. Treat documentation with the same care you treat code, and user will sing your praises.

Sometimes it is uncomfortable to document the design of source code because the design isn't clear in your mind; it's still evolving. You don't feel that you should waste effort describing what something does until it actually does it. Does this sound like programming by coincidence?

#### Great expectations

The success of a project is measured by how well it meets the expectations of its users. A project that falls below their expectations is deemed a failure, no matter how good the deliverable is in absolute terms. However, go too far and you'll be a failure, too.

- The users have a lot expectation about your work, and about what they wanna see, talk with them, try to figure out what are they expectations

#### The extra mile
 - Try to surprise your users. Not scare them, mind you, but delight them.
 - Give them that little bit more than they were expecting.

 - Balloon or ToolTip help
 - Keyboard shortcuts
 - A quick reference guide as a supplement to the user's manual
 - Colorization
 - Log file analyzers
 - Automated installation
 - Tools for checking the integrity of the system
 - The ability to run multiple versions of the system for training
 - A splash screen customized for their organization

What do your users comment on when you deliver software? Is their attention to the various areas of the application proportional to the effort you invested in each? What delights them?

### Pride and Prejudice
 
 Don't shirk from responsibility. Instead,rejoice in accepting challenges and in making our expertise well known. If we are responsible for a design, or a piece of code, we do a job we can be proud of.
