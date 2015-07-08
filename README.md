# cmn


**CMN: (Code Music Notation)**

**Code Music Notation for Human Interpreters**

Quick Instructions of the Code Music Notation language for human interpreters. The below instructions hopefully clarify the syntax, but also include the computational thinking that code notation makes possible. 

The CMN is a notational language for human interpreters and thus different from traditional live coding CUI's (Code User Interfaces) written for machine interpreters. CMU is an object oriented programming language with a C-family syntax and dot notation, also supporting functional approaches, such as first class functions and recursion.


**1) Variables**

A variable contains value of some sort. This value is 'assigned' to the variable with a '=' sign.

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

Here you play the note G


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

inf do
	scale.scramble.play // here you would scramble the scale and play it, then scramble it again and play it - infinitively 
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

A condition is a statement of that is either true or false. "It is raining" is a conditional that's either true or false.

The syntax for checking condition is '==' (as opposed to assigning '=' a value to a variable (see above))

example:

if(raining == true) {
	umbrella.open
}

or, here introducing the ELSE statement

if(raining == true) {
	umbrella.open
} else
	umbrella.close
}




**Example**


note = C // play as if someone isn't listening
note.play // you play C

10 do
note.play
1.wait;
end

scale = [C, C#, F, G, G#] // ambasel

while (notbored == true) do
scale.choose.play(lefthand)
[0.5, 1].choose.wait;
end

while (lefthand.playing == true) do
(scale+12).choose.play(righthand)
[0.5, 1].choose.wait;
end

inf do
if(audience.clapping == true) {
tempo = tempo + 1; // this might get people clapping and you would speed up (they too)
}
1.wait;
end

player.stopAll // I will stop the madness

while(notesleft) do 
scale = scale + 1;
scale.play // arpeggio - here you play the scale a whole note higher every time you play it
end



//

if(tired) {
	mallet.rotate;
	while(tired){
		glissando.updown;
	}
}

