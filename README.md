# CMN (Code Music Notation)

**Instructions for the Code Music Notation for Human Interpreters**

This language enables composers to write notation for human instrumentalists, for example in a live coding context. Textual instructions are powerful and commonly used in musical notation, but with CMN, a language for algorithmic or computational notation is added to the technique of text-based scores. The below instructions hopefully clarify the CMN syntax, but also introduce the type computational thinking that code notation makes possible. 

The CMN is a notational language for human interpreters and thus different from traditional live coding CUI's (Code User Interfaces) designed for machine interpreters. CMU is an object oriented programming language with a C-family syntax and dot notation, also supporting functional approaches, such as first class functions and recursion.

The syntax is inspired by [SuperCollider](http://supercollider.github.io) and [Lua](http://www.lua.org), using the latter language's syntax for comments, syntax colouring, and various other things. When performing, choose Lua syntax colouring in your favourite code editor.

A key feature of this language is that it's written for humans, who incidentally have much stronger capability and flexibility of interpreting language syntax and semantics than machines. Any word in any human language can therefore be used; the reason CMN exists is to provide a general syntax, a protocol, between the composer and the performer.


**1) Variables**

A variable contains a value of some sort. It could be a note, a player, an instrument, etc. but it's the name of that value. This value is 'assigned' to the variable with a '=' sign.

example:

	note = C

Here the variable 'note' contains the value C. We can then do:

	note + fifth

and the performer would play a G. Another syntax for that would be:

	note + 7

where a whole number represents a semitone.


**2) Methods**

CMU is object oriented so objects can have methods. The methods are like verbs (play, sleep, etc.)

example:
	
	note.play

If the variable note has been declared, as above, here you would play the note C.

	(note+fifth).play

And by bracketing, a scope can be created and this would result in playing the note G.

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

	scale = [C, C#, F, G, G#] -- ambasel

Here you have five notes in an Ethopian scale called Ambasel. the '//' signifies a comment, so don't 'execute' that.

the scale can be played like this:

	scale.play -- play the whole scale as it's written

or

	scale.choose.play -- where ONE note from the scale is chosen and played

Arrays can also have methods applied to them so we can write:

	scale.scramble.play -- scramble the array and THEN play it. 
	scale.reverse.play -- reverse the scale and THEN play it.

**4) Loops**

The CMN has two types of looping structures a) do-loops and b) while-loops

a) do-loop

example:

	10 do
		scale.choose.play -- here you play a random note from the scale 10 times
		1.wait; -- wait for a second
	end

or 

	inf do
		scale.scramble.play -- scramble the scale and play it; scramble and play infinetely
		1.wait -- wait for a second
	end

b) while-loops

	while(something is true) do 
		code
	end

example:

	while(bored == false) do 
		note.play -- play until the CONDITION is false
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

Diverse terms might be useful to include either as comments or as methods or arguments in the language itself, such as:

texture:  soft, sustain, sharp, brittle, hard, edgy, resonant, deadnote, etc.
technique: edge, rattan, roll, percussive, etc.
body movements: alternate hands, pedals, etc.

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
	

**9) Rhythmic scores**
	
In some cases graphical elements can be helpful, for example for percussive scoring. In live coding languages we have good precedence of such scores for example:

	perc = |q   c   q c q   |
	
or
	
	perc = |q...c...q.c.q...|

the above is percussive notation in [ixi lang](http://www.ixi-audio.net), where alphabetic characters map to samples (of percussive nature). Another type of notation would be:

	drummer.playHard("o-x-o-xxo-x-") 

which is a [Gibber](http://gibber.mat.ucsb.edu) style notation, similar to ixi lang, where letters signify sounds and "-" silences.

Finally, we find an interesting syntax in [Tidal](http://yaxu.org/tidal/), where sub-arrays can be introduced, thus less visually isomorphic than ixi lang or Gibber, but with a potantial for more complexity:

	drummer "[bd sn [bd sn] sn bd [sn [bd sn]]]"

Check ixi lang, Gibber and Tidal for further explorations of how these scores work.

**10) CMN Assembly**

Like [Extempore](http://extempore.moso.com.au), CMN has a lower level realtime compiled language, called assembly. This low-level feature of the language goes below the semantic level of functions, methods, and semantic commands of actions, to a more descriptive body movement notation. In short, down from the level of gesture and action, to the fundamental level of movement and motion. 

The assembly language is also OOP, with dot-syntax, but the focus is on the human body:

	body.arm.left.degree(30)
	body.arm.left.movetoDegree(100, seconds:2)
	body.arm.right.follow(body.arm.left, delay: 4)
	body.head.nod(updown, seconds:2)
	body.foot.left.lift(seconds:2)
	body.foot.right.lift(seconds:2) -- yes, you're not so tall anymore



NOTE: when performing, it can be useful to signal when a new section of the code has been evaluated by the coder. This can happen by any means, such as light, movement, or sound. At the performance at the International Conference on Live Coding, a sound signal is emitted every time code is evaluated:

	{SinOsc.ar(3999*Line.ar(1, 0, 0.01, doneAction:2)!2)}.play
