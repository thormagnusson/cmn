# CMN: (Code Music Notation)

**Code Music Notation for Human Interpreters**

Quick Instructions of the Code Music Notation language for human interpreters. The below instructions hopefully clarify the syntax, but also introduce the computational thinking that code notation makes possible. 

The CMN is a notational language for human interpreters and thus different from traditional live coding CUI's (Code User Interfaces) written for machine interpreters. CMU is an object oriented programming language with a C-family syntax and dot notation, also supporting functional approaches, such as first class functions and recursion.

The syntax is inspired by SuperCollider and Lua, using the latter language's syntax for comments and various other things. When performing, choose Lua syntax colouring in your favourite code editor.


**1) Variables**

A variable contains a value of some sort. It could be a note, a player, an instrument, etc. but it's the name of that value. This value is 'assigned' to the variable with a '=' sign.

example:

	note = C

Here the variable 'note' contains the value C. We can then do:

	note + fifth

and you'd play a G


**2) Methods**

CMU is object oriented so objects can have methods. The methods are like verbs (play, sleep, etc.)

example:
	
	note.play

Here you would play the note C

	(note+fifth).play

Here you play the note G.

Methods are applied to objects - or objects can have methods. Just like a bird can fly (bird = object; fly = method) - ojbects are nouns, whereas methods are verbs. 

Methods can have adverbs, where the verb is given furhter instructions:

	note.play(loudly)

They can also be overloaded, such that they are given a subject

	note.play(lefthand)
	
and of course:

	note.play(lefthand, loudly)

The possible methods infinite: any word from the vocabulary can be used. The CMN is about the relationship between the coder and the interpreter.

**3) Arrays**

Arrays are collections of values. Like a bag full of stuff. The items in the bag are separated with a comma.

example:

	scale = [C, C#, F, G, G#] // ambasel

Here you have five notes in an Ethopian scale called Ambasel. the '//' signifies a comment, so don't 'execute' that.

the scale can be played like this:

	scale.play // play the whole scale as it's written

or

	scale.choose.play // where ONE note from the scale is chosen and played

Arrays can also have methods applied to them so we can write:

	scale.scramble.play // scramble the array and THEN play it. 
	scale.reverse.play // reverse the scale and THEN play it.

**4) Loops**

The CMN has two types of looping structures a) do-loops and b) while-loops

a) do-loop

example:

	10 do
		scale.choose.play // here you play a random note from the scale 10 times
		1.wait; // wait for a second
	end

or 

	inf do
		scale.scramble.play // scramble the scale and play it; scramble and play infinetely
		1.wait // wait for a second
	end

b) while-loops

	while(something is true) do 
		code
	end

example:

	while(bored == false) do 
		note.play // play until the CONDITION is false
		1.wait
	end

here YOU decide whether you're bored or not - obviously.


**5) Conditionals**

A condition is a statement of that is either true or false. For example, "it's raining" is a conditional that's either true or false.

The syntax for checking condition is '==' (as opposed to assigning '=' a value to a variable (see 1) above))

example:

	if(raining == true) {
		umbrella.open
	}

or, here introducing the ELSE block (which is evaluated if it is not raining)

	if(raining == true) {
		umbrella.open
	} else {
		umbrella.close
	}

**6) Comments**

Comments are secondary notations in CMN. Like in all programming languages, comments are human readable, but in CMN they can be explanations or further instructions, perhaps like Eric Satie's instructions in his Gnossienne scores.

example:
	
	if(lefthand.busy == true) {
		righthand.copy(lefthand.note+7) -- the right hand is angry!
	} else {
		4 do
			scale.play(righthand) -- slowly but concentrated
		end
	}

**7) Functions**

Functions are very helpful if blocks of code have to be repeated (or "called") from another location in the code. They are a black-box, or an encapsulation of a musical pattern of some sort.

Functions are notated with the use of curly brackets "{}" and are typically stored in a variable:

	myFunc = {
		if(silence == true){
			chord = [C, Eb, G, A, Bb].choose(3) -- choose three notes out of the array
		}
	}

The function then needs to be "called" or evaluated:

	myFunc.value
	
or 

	10 do
		myFunc.value
		10.rand.wait
	end


**8) Classes**

CMN is is an object-oriented language and classes can be created in real-time. This is a feature that might not be used in a live-coding context, since it is quite laborous, but this is supported:

	class agent(scale, tempo)
		this.scale = scale
		this.tempo = tempo
	end
	
and the class is instantiated (an object is created from the class) as such:

	a = agent(minor, 120)
	b = agent(major, 90)

properties and methods can then be added to the class (just as in JavaScript's prototypes)

	agent.play = {arg tempo; 
		inf do
			this.scale.choose.play
			(tempo/60).wait
		end
	}

which now means that we can run:

	a.play
	b.play(220) -- overriding the default tempo
	
	


NOTE: when performing, it can be useful to signal when a new section of the code has been evaluated by the coder. This can happen by any means, such as light, movement, or sound. At the performance at the International Conference on Live Coding, a sound signal is emitted every time code is evaluated:

	{SinOsc.ar(3999*Line.ar(1, 0, 0.01, doneAction:2)!2)}.play
