## Forth Artificial Life manual

***************************************************************************
************************** 4th Artifical Life ******************************
***************************************************************************

This package presents three programs that demonstrate some very interesting concepts: chaos in rules (Life), evolution (Animal Farm)
and learning in neural networks (ChaseNet):

1) 'LIFE', the famous AUTOMATIC BOARD GAME, that calculates
	new populations with 3 rules. Produces interesting 'swerms'.
2) 'ANIMAL FARM', a GENETIC cellular AUTOMATA algoritm, that 	demonstrates concepts like evolution and even biosystems.
	Witness evolving fauna eating too much flora and disturbing balance.
3) 'CHASENET', a small NEURAL NET that drives a very simplistic 
	'virtual robotcar'. It uses 'hill climbing' to improve chasing an object. 
>> These three programs can be EXECUTED by dropping them on 'Forth' <<

*The file Extended.4th is a small extension that is used by these files.
*The Forth programming language is explained in short in the Manual
  and all the commands are described in the Glossary (see below)

***************************************************************************
### Animal Farm

Animal farm presents a small 'world' on the display,
it is an 20*20 array, so that means a 400 places to stay
for the creatures that are going to live in that world.
Each place receives some free energy (like from the SUN)
and a creature on that place can collect that energy.

Species & Energy:
Time begins with just one member of the specie 'A'.
The specie name is calculated from it's features:
-defense force (D)
-attack force (A)
-speed  (S)
Specie name: A+4*D+10*S  ->  0-25  ->  A-Z
So the higher the ASCI-code the more 'powerful' the specie!
Of course having features costs energy (E):
each calculation step: E -> E+SUN-(A+D+2S)

Moving and Reproducing:
When a specie CAN move, it moves randomly. But every place it 
decides to take over it has take conquer the creature that's already there.
When his attack is more powerful than the defense of his opponent
he takes that place and the life and energy of his opponent (if not: v.v.)
The same thing occurs when a creature decides to divide itself (energy is 
splitted). It's offspring (which might be mutated) has to conquer a place to 
live.

Notice that after a while species occur which could not live without the
lower species: a real bio system!

[Animal Farm concept: Mervyn@xs4all.nl 1995]

***************************************************************************
Life

Life explains what is does as it is executed

[Life concept: Conway 1970]

***************************************************************************
ChaseNet

ChaseNet explains what it does as it is executed.

PS: the values that are constantly changing are the factors that the
0/1 at the inputs are multiplied with. The threshold is 10. So when an
input is high (1) and the factor is greater than 10, the next neuron is activated (just follow the lines on the screen).

[ChaseNet concept: Mervyn@xs4all.nl 1995]

***************************************************************************
************************ FORTH Manual ***********************************
***************************************************************************

Creating your own clickable Mac applications is quite easy. 
Pocket Forth (by Chris Heilman) is a powerful tool to do just that. 
*Create your source code using your favorite word processor (plain text)
*Drop the document on Pocket Forth
 Pocket Forth compiles the new word definitions and interprets direct
 commands in the document (e.g. 'run this program').
*If the program is debugged and does the job fine, drop it onto a COPY
 of Forth, and make it a 'turnkey' by saving it into the 'standard library'
 (of that copy) and tell it to always start with that program. It then is
 a clickable application! (Forth is only 18K small, so who cares!)

***************************************************************************
FORTH PROGRAMMING in just 6 small steps

<< This is NOT a manual that describes all the possibilities
    of FORTH, it's meant to get you going. I learned FORTH during the 
    last14 days, so I can't tell you all the ins and outs, but I hope this 
    will prove to you that FORTH is simple,  but powerful!                  >>

***************************************************************************
1 THE STACK

The most important item to understand when using Forth is the STACK.
The stack is a piece of memory that works like a tube with only one
open end: YOU CAN ONLY GET OUT WHAT YOU PUT IN LAST!!

The only thing you can put in are 16 bit values. Since one bit is used as
a sign bit, that leaves 15 bits too define the value: 2^15=32768
This means you can insert INTEGERS in the RANGE -32767 to 32767.
(32 bit numbers and floats are also possible, but use special commands)

The stack is used for all calculations, that's why it is 'post-fixed'.
Each value (or address) that is typed or present in a program, is
put on the stack. Standard commands or self defined 'words' always
use values that have to be ALREADY ON THE STACK. They take them off, and
instead put a result (if there is any) on the stack.

For example: 	2 3 + .		
This puts 2 on stack, 3 on stack, runs the standard word "+", which
always takes and adds the two values on the top of the stack and leaves the
result on the stack. The command "." takes the value of the top of the stack
and puts it onto the screen, so the value 5 appears on screen as a result of these instructions.
It could have been left on the stack to perform another calculation:
			2 3 + 6 - .		puts the value -1 on the screen
		or	2 3 6 + - .		puts the value -7 on the screen!

The stack is quite 'deep', but not infinite, so ALWAYS MAKE SURE THAT WHAT GOES ON THE STACK, GOES OFF AGAIN (SOON OR LATE)!
If this is not done, it will result in errors (stack overflow or underflow) and stop the program, especially when using loops!

***************************************************************************
2 VARIABLES

Of course not everything is stored 'on the stack'. But also storing values
in normal memory addresses is done via the stack.
			variable AD
This command allocates space in the memory for a value on the address AD.
AD is now the same as the address that can be used. It IS that address, a value, just like 6770 is! So just type:
			AD .
to check which address. Not that that's interesting, because that value is just the address of a piece of memory we can use!
The commands @ and ! can be used to read and write on that address:
			AD			puts the allocated address on stack 
			AD @		puts the content of address AD on stack
			AD @ .		puts the content of address AD on screen
			100 AD !		puts 100 in address AD
			AD 100 !		puts address AD in address 100: ILLEGAL!
NB: SO "@" MEANS READ AND "!" MEANS WRITE!

***************************************************************************
3 ARRAYS

Sometimes it is necessary to store or read a whole list of values.
This could be done by defining just as many variables, but it is usually done using an array.
			variable AD allot 10
This command allocates not just room for one value, but for FIVE values.
NB: ONLY EVEN ADDRESSES ARE USED e.g.:
			AD 2 + @		puts the content of address AD+2 on stack
			10 AD 10 + !	puts 10 in address AD+10
			10 10 AD + !	(idem!)


***************************************************************************
4 LOOPS

A loop can be used to fill an array with data:
			10 0 Do   200 I 2 * +   AD I + !    2 +Loop
This creates a loop between "Do" and "Loop". 
It 'loops' 5 times: 0 to 10, step 2
"I" puts the 'index' of the loop on the stack (0 2 4 6 8)
It stores (!) 200+2*I in the address AD+0 AD+2 AD+4 AD+6 and AD+8.
So afterwards:	AD @		puts 200 on stack
			AD 2 + @		puts 204 on stack		
			AD 4 + @ 		puts 208 on stack
			AD 6 + @ 		puts 212 on stack
			AD 8 + @ 		puts 216 on stack

The line:		Begin ... Again
Creates an endless loop between "Begin" and "Again".


***************************************************************************
5 CONDITIONAL LOOPS AND BRANCHING

Not all loops are defined or endless. Sometimes something has to be
done UNTIL e.g. a key is pressed. Or only IF a key is pressed, or a certain
value is reached!
Conditions can be tested and the result will set a 'FLAG' to true or false.
			2 3 =		This will set the FLAG to false
			2 3 * 6 =		This will set the FLAG to true
AFTER the FLAG is set it can be used to break or maintain a loop, or to
execute a conditional set of instructions:
			(flag) if ... then		... is executed if the flag is true
			(flag) if . else ... then	... is executed if the flag is false
			BEGIN �  (flag) WHILE � REPEAT
			BEGIN �  (flag) UNTIL

***************************************************************************
6 USING and CREATING "WORDS": PROGRAMMING

These are frequently used STANDARD COMMANDS or "WORDS":

: WORD ... ;		compile ... as new subroutine called WORD			
/ * - + 		divide, times, minus, sum
=   <   >		checks relation upper two stack values, sets flag 
.			displays top value on stack (removes value off stack)
." text"		display textstring (start with space!)
DUP			duplicates stack (to evoid destruction)
DROP		destroy top of stack
SWAP		exchange upper two stck values
VARIABLE X	claims use of memory address to be called X
4 ALLOT		claims 4 more bytes beyond X (used after variable ...)
2 X !			puts 2 in address X
2 X +!		adds 2 to the content of address X
8 X 2 + !		puts 8 in address X+2 (array)
X @			puts content of address X on stack
KEY			puts ASCII code of typed key on stack (waits)
PAGE		clears screen, cursor to upper left
@MOUSE		puts mouse coordinates on stack
?BUTTON		sets flag true if mousebutton clicked
?TERMINAL	sets flag true if key pressed
CR			carriage return
!PEN			moves cursor/drawing pen to 2 upper stack coordinates
@PEN		puts pen coordinates on stack
-TO			draws line to 2 upper stack coordinates
13 emit		display character 13 of ASCII table
BEEP			sounds default beep
QUIT		exits program, return to interpreter
S 10 EXPECT	stores 10 characters starting at address S
S 10 TYPE		displays 10 characters starting at address S
PMODE		uses stack to set drawing mode
--> Drive:Path:Name	loads and interprets Forth file (see example below)

NB (conditional) loops and branches are described in �4 and 5!
NB Check the Glossary and download the original Pocket Forth-package 
for more info on Forth, Apple Events and the toolbox.

Defined in Extended.4th:
I					puts index of loop on stack (J if nested)
-9 DABS				returns absolute value (puts 9 on stack)
RANDOMIZE			randomize using the clock
5 RANDOM			puts random integer between 0-4 on stack
create "name" , " string"	puts string on address "name" (WINDOW)
"name" WTITLE			uses "string" as window title
200 100 WSIZE			sizes window 200x100 pixels
FCOLOR				use: 	white, black, blue, green, red, cyan, 
BCOLOR				magenta, yellow  e.g. "blue FCOLOR"
					F=foreground(pen)  B=background(window)
!FONT 				( n -- )	set font
!FSIZE 				( n -- ) 	set size
!FACE 				( face -- )	set style
!FMODE 				( mode -- ) set mode
SYSFONT 				use System font
MONACO9 			use Normal font


NEW WORDS can be CREATED by using ":" and ";"
			: TEST ." test" ;
This instruction compiles a subroutine TEST, that can be called from the
interpreter, or be used in another subroutine e.g.:
			: GO Do TEST ?terminal Until ;
GO displays "test test test ....." until a key is pressed.

NB: 	-Forth is not case sensitive: DO is the same as Do or do.
	-a SPACE or TAB has to divide ALL instructions (remember that
	  also values and things like "+" or ":" and ";" are instructions!)

We will now take a look at LIFE to demonstrate how an application is made:
This is my file "Documenten:Development:Forth:Life.4th"
(Comment is found after "\ ")

\ ****** LIFE  in  FORTH  by  MERVYN@xs4all.nl *******
--> Documenten:Development:Forth:Extended.4th
\ this adds the new words in Extended.4th to the language!
\ this file can be altered to create your own customized Forth version
variable FIELD 2600 allot  variable FIELD2 2600 allot  
\ this allocates twee arrays for 1300 (remember?) integers
variable PLACE variable PL variable X variable Y  
create "TITLE" ," Life"  
\ this puts the string Life on the address "TITLE"

: COPYFIELDS  2600 0 Do  I FIELD2 + @  I FIELD + !  2 +Loop ;
\ a new word that copies the changed array FIELD2 to FIELD

: SETUP Begin  2480 80 Do  80 0 Do   
	I J + FIELD2 + @  1 = if I 5 * J 80 - 6 / !PEN ." *" then 
	\ this displays the array as a 2d field of stars (if field=1)
	\ I is the second (nested) index, J the first!
	2 +Loop  80 +Loop  key 
	dup 28 = if PLACE @ 2 - PLACE ! then
	dup 29 = if PLACE @ 2 + PLACE ! then
	dup 30 = if PLACE @ 80 - PLACE ! then
	dup 31 = if PLACE @ 80 + PLACE ! then
	dup 32 = if  1 FIELD2 PLACE @ + !  then
	\ this uses the cursor keys and space to set up a field
	       13 = Until ;

: INIT  FIELD2 2600 0 fill  COPYFIELDS 1400 PLACE !  
	BLACK bcolor WHITE fcolor 500 310 wsize  "TITLE" wtitle page 
	\ sets colors and sizes and names window, clears screen
	CR CR 
	."       LIFE by Mervyn@xs4all.nl (programmed in Forth)" CR CR
	."       LIFE calculates new board populations using these rules:" CR
	."       -3 neighbours? -> Birth " CR
	."       -Less than 2 or more than 3 neighbours? -> Death" CR CR
	."       Press any key to toggle between <Field setup> and <Life>" CR
	."       (Use space/arrow keys to create a field)  " 
	key drop page SETUP ; 

: MAINLOOP  2480 80 Do  80 0 Do  I J + FIELD + PL !	
	PL @ 2 + @ 		PL @ 2 - @	
	PL @ 78 + @		PL @ 78 - @ 
	PL @ 80 + @		PL @ 80 - @ 	
	PL @ 82 + @		PL @ 82 - @	
	+ + + + + + +  
	\ puts the amount of neighbors on the stack
	PL @ @ 
	\ puts the content of the current PLace on the stack (0=empty / 1=*) 
	0 = if 3 = if 1 I J + FIELD2 + !  I 5 * J 80 - 6 / !PEN ." *" then else
	dup 2 < if 0 I J + FIELD2 + ! I 5 * J 80 - 6 / !PEN ."  " drop else 
	       3 > if 0 I J + FIELD2 + ! I 5 * J 80 - 6 / !PEN ."  " then then then
	2 +Loop  80 +Loop ?TERMINAL if SETUP then ;
	\ applies rules on amount of neigbors

: LIFE INIT Begin  COPYFIELDS  MAINLOOP Again ; 
\ the main routine: life

READY		
\ READY puts echo back on after calling Extended.4th !!!!!!
\ SO READY MUST BE CALLED WHEN USING Extended.4th !!!!!!!
LIFE 		
\ types LIFE to run itself

This file will run itself when dropped on Pocket Forth, but it can be
made a clickable application:
-make a copy of Forth
-drop Life on the copy of Forth
-quit Life by clicking mouse (within the window)
-type: 	' life 26 +md ! save bye
-rename Forth to Life
-Life is your application!
(Follow the same procedure for your own programs. Make sure that
the word that is used is the main subroutine, and that you use a copy!)

	That's all, have fun, send all your comments to:

				Mervyn@xs4all.nl
		
References:
(1) L. Brodie	Starting Forth, Prentice Hall, Englewood Cliffs, 1981.
(2) C. Heilman	Pocket Forth glossary and Brodie Glossary.



***************************************************************************
	Pocket Forth Glossary  version 0.6.3   [by Chris Heilman]
***************************************************************************

! ( n addr -- ) say: "store"  <standard>   Store value n at the relative address, addr.

!PEN ( h v -- ) say: "store pen"   Move the graphics pen to the coordinates on the stack.

# ( dval -- dquotient ) say: "sharp"  <standard>   Convert one digit of a numeral represented by the dvalue, by dividing the value by the numeric base.  Use between "greater-than-sharp" and "sharp-less-than".

#> ( dval -- addr len ) say: "sharp-less-than"  <standard>   Leave the address and length of a string representing the formatted dvalue.  Use with #, "sharps", "sharp", "hold" and "greater-than-sharp".

#S ( dval -- 0 0 ) say: "sharps"  <standard>   Convert all of the digits of the dvalue according to the current numeric base.  Use between "greater-than-sharp" and "sharp-less-than".

' ( -- addr ) say: "tick"  <standard>   Return the relative address of the next word from the input stream.

( ( -- ) say: "parenthesis"  <standard>   Begin a comment.  A right parenthesis ends the comment.

(DO) ( limit index -- ) say: "paren-do" <standard>   This is the runtime word compiled into the dictionary by "do". "Paren-do" begins a loop.

* ( n1 n2 -- n1*n2 ) say: "star" or "times" <standard>   Multiply n1 by n2, and leave the 16 bit result on the stack.

*/ ( n1 n2 n3 -- [n1*n2]/n3 ) say: "star-slash" <standard>   Using a 32 bit intermediate, "star-slash" puts the scaled result on the stack.

+ ( n1 n2 -- n1+n2) say: "plus" <standard>   Leave the result of n1 plus n2 on the stack.

+! ( n addr -- ) say: "plus-store" <standard>   Add the value, n, to the value found at the relative address, addr.

+LOOP ( n -- ) say: "plus-loop" <standard>   Used inside of a colon definition, with "do".  Increment a loop index by n, and branch to the beginning of the loop until the index reaches the limit.  (see "loop" and "do")

+MD ( offset -- addr ) say: "plus-em-dee"   Calculate the relative address of an unnamed variable from an offset on the stack.

, ( n -- ) say: "comma" <standard>   Write and enclose the value, 'n' into the dictionary.

,s ( -- d ) say: "comma-ess"  Stack or compile a double number literal from ASCII characters which follow ,s by exactly one space.  ,S is immediate.

,$ ( -- ) say: "comma-dollar"   Compile a hex number from the input stream into the dictionary.   Used to compile traps and machine code.  ,$ is immediate.

- ( n1 n2 -- n1-n2 ) say: "minus" <standard>   Leave n1 minus n2 on the stack.

--> ( -- ) say: "load"  <almost standard>   Take a filename from the input stream, and load the file from the disk.  If no disk or path is specified, the default is used.  NOTE: Names may not contain spaces.

-TO ( h v -- ) say: "line to" Draw a line and move the pen to the coordinates on the stack.

-TRAILING ( addr count -- addr count' ) say: "dash-trailing" <standard>   Assuming string data on the stack, adjust the count to eliminate trailing blanks.

. ( n -- ) say: "dot" <standard>   Print the value on the stack according to the current number base.   (see "base")

." ( -- ) say: "dot-quote" <standard>   Used inside of a colon definition to compile a routine and string data into the dictionary.  The string data follows "dot-quote" and is delimited by another quote. The string is printed at runtime.

.OK ( -- ) say: "dot-oh-kay"   Print 'ok' on the screen, indicating that the interpreter ready for input.

/ ( n1 n2 -- quotient ) say: "slash" <standard>   Divide n1 by n2 and leave the 16 bit quotient on the stack.

/MOD ( n1 n2 -- quotient remainder ) say: "slash-mod" <standard>   Divide n1 by n2 and leave the 16 bit quotient and 16 bit remainder on the stack.

0  ( -- 0 ) say: "zero" <standard>  Leave a zero on the stack.

0< ( n -- flag ) say: "zero-less-than" <standard>   Leave a negative one on the stack if n is less than zero. Otherwise leave a zero.

0= ( n -- flag ) say: "zero-equal" <standard>   Leave a true flag on the stack if n is zero.  Otherwise leave a zero on the stack.

0> ( n -- flag ) say: "zero-more-than" or "zero-greater-than"  <standard>   Leave a true flag on the stack if n is greater than zero.  Otherwise leave a zero.

1+ ( n -- n+1 ) say: "one-plus"  <standard>   Add one to the value, n on the stack.  Leave the result on the stack.

1- ( n -- n-1 ) say: "one-minus"  <standard>   Subtract one from the value on the stack.  Leave the result on the stack.

2! ( d addr -- ) say: "two-store"  <standard>   Store the 32 bit number, d, at the relative address, addr.

2+ ( n -- n+2 ) say: "two-plus"  <standard>   Add two to the value on the stack, leaving the result on the stack.

2* ( n -- n*2 ) say: "two-star" or "two-times"  <standard>   Double the value on the stack.

2/ ( n -- n/2 ) say: "two-slash" <standard>   Halve the value on the stack, truncating to an integer.

2>R ( d -- ) ( rstack: -- d ) say: "two to are"   Put a 32 bit number on the return stack.  Use within colon definitions.

2@ ( addr -- d ) say:  "two at"  <standard>   Fetch a 32 bit number from relative address on the stack.

2CONSTANT ( compile: [ d -- ] run: [ -- d ] ) <standard>   Create a 32 bit constant.

2DROP ( d1 -- ) say: "two drop" <standard>   Drop a 32 bit number.

2DUP ( n1 n2 -- n1 n2 n1 n2 ) say: "two-dupe" <standard>   Duplicate the top two values on the stack.

2OVER ( d1 d2 -- d1 d2 d1 ) say: "two-over" <standard>   Duplicate the 32 bit second number to the top of the stack.

2R> ( -- d ) ( rstack: d -- ) say: "two-are-from"   Move a 32 bit number from the return stack to the parameter stack.

2ROT ( d1 d2 d3 -- d2 d3 d1 ) say: "two-rote" <standard>  Rotate the top three 32 bit numbers.

2SWAP ( n1 n2 n3 n4 -- n3 n4 n1 n2 ) say: "two-swap" <standard>   Reverse the order of the top two and the second two values on the stack.

2VARIABLE ( compile: [ -- ] run: [ -- addr ] )  <standard>   Create a 32 bit variable.  See change to "variable", below.

: ( -- ) say: "colon" <standard> "Colon" creates a new word, called a colon definition.  The token following "colon" is the name of the new word.  Non-immediate words following the name are compiled into the definition until a "semi-colon" is reached.

; ( -- ) say: "semi-colon" <standard>  "Semi-colon" ends a colon definition and compiles a machine language return instruction. "Semi-colon" is immediate.

;AE ( -- ) say "semi-a-e  Use "semi-a-e" to end an Apple Event definition. Pocket Forth's registers are saved and the calling registers are restored. "Semi-a-e" is an immediate word.

< ( n1 n2 -- flag ) say: "less-than" <standard>   Leave a true flag on the stack if n1 is less than n2.  Otherwise leave a zero.

<# ( -- ) say: "greater-than-sharp"  <standard>   Set up for number conversion by clearing the pad, and setting 'held' to "pad"-1.

= ( n1 n2 -- flag ) say: "equal" <standard>   Leave a true flag on the stack if n1 is the same as n2.  Otherwise leave a zero.

> ( n1 n2 -- flag ) say: "greater-than" <standard>   Leave a true flag on the stack if n1 is more than n2. Otherwise leave a zero.

>ABS ( addr16 -- daddr32 ) say: "to-abs"   Convert a relative address on the stack to a double number absolute address.   (see ">rel")

>LINK ( addr -- link.addr ) say: "to-link"  <standard>   Return the relative address of the link field of the word whose address is on the stack.

>NAME ( addr -- name.addr ) say: "to-name"  <standard>   Leave the relative address of the name field of the word whose address is on the stack.

>R ( n -- ) return stack: ( -- n ) say: "to-are" <standard>   Remove a value from the parameter stack and place it on the return stack.   (see "are-from")

>REL ( daddr32 -- addr16 ) say: "to-rel"   Convert a double number absolute address on the stack to a relative address.

?BUTTON ( -- flag ) say: "question-button"   The flag is true if the mouse button is down, false if up.

?DUP ( n -- n n OR n [if n=0] ) say: "question-dupe" <standard>   Duplicate the value on the stack only if it is not zero.

?GESTALT ( d.selector -- d.response -1  or  0 ) say: "question-gestalt"  Run the system trap _Gestalt on the stacked double number.  If _Gestalt does not exist or if it exits with an error, a false flag (that is, a zero) is left on the stack.  If the call is successful, a true flag (-1) is left on the stack on top of the double number result.  Use "question-gestalt" to test computer in use.

?STACK ( ? -- ) say: "question-stack"   Print a warning, '*?', if stack underflow has occurred.

?TERMINAL ( -- flag ) say: "question-terminal" <standard> Leave a true flag if a key has been pressed.  In the application, events are handled by "?terminal".

@ ( addr -- n ) say: "at" (some people say: "fetch") <standard>   Leave the value found at the relative address on the stack.  The address must be even.

@MOUSE  ( -- h v ) say: "at-mouse"   Get the coordinates of the mouse pointer.

@PEN ( -- h v ) say: "at-pen"   Get the coordinates of the graphics pen pen.

A>R ( addr -- : -- dabs.addr ) say: "a-to-are"   Convert an address to absolute, and put it on the return stack. This word is used for system trap setup.  Use only within a colon definition.

ABORT ( -- )  <standard>   Stop execution, print a warning, '?' and return to the interpreter loop.

AE: ( d.type d.class -- ) say: "a-e-colon"  "Ae:" begins the definition of an Apple Event handler. D.type and d.class are the type and class signatures of the event to be handled. Follow the definition with ";ae".

AGAIN  while compiling: ( addr -- )  while executing: ( -- )  <standard>   Used to compile an unconditional branch to a relative address left by "begin".  (see "begin" and "back")  "Again" is an immediate word.

ALLOT ( n -- )  <standard>   Allocate and enclose n bytes in the dictionary.  If n is odd, n+1 bytes will be allocated.  The value of the bytes is undefined at compile time.

AND ( n1 n2 -- n1ANDn2 )  <standard>   Leave the result of n1 AND n2 on the stack.  The value is computed bitwise.

BACK while compiling: ( addr -- )  no execution behavior  <standard>   Compiles the difference between the current compilation address and the address on the stack.  "Back" is used by "again", "repeat" and "until". (also see "begin" and "while")

BASE ( -- addr )  <standard>   "Base" leaves the address of a variable containing the current number base.

BEEP ( -- )   Causes the speaker to beep at the current volume.

BEGIN ( -- )  <standard>   "Begin" starts a conditional or unconditional loop in the following manner:
          BEGIN � ( -- flag ) WHILE � REPEAT,
          BEGIN � ( -- flag ) UNTIL and
             BEGIN � AGAIN
        "Begin" is an immediate word and is used within a colon definition.  (see "while", "again", "repeat" and "until")

BYE ( -- )  "Bye" sets a variable (194 +md) that causes Pocket Forth to quit on the next trip through the event loop.

C! ( c addr -- ) say: "sea-store"  <standard>   Store the 8 bit value at the relative address (even or odd).

C@ ( addr -- c ) say: "sea-at"  <standard>   Retrieve the 8 bit value found at the address (even or odd) to the stack.

CBLK ( -- addr ) say: "sea-bee-el-kay"   Returns a relative address which contains a byte value.  If the value is 128, then the interpreter looks for input from the keyboard.  A zero value causes text to be interpreted from the file stack.

CMOVE ( addr1 addr2 n -- ) say: "sea-move" <standard>   Moves n bytes from addr1 to addr2.

COMPILE ( addr -- )   "Compile" writes a subroutine call to the relative address on the stack into the dictionary. This is not identical to Forth's standard COMPILE which takes its argument from the input stream.

CONSTANT while compiling: ( n -- )  while executing: ( -- n )  <standard>   Creates a word from the next token in the input stream, which, when executed, returns the value, n.

COUNT ( addr -- addr+1 length )  <standard>   Assuming that the relative address on the stack is the start of string data, and the byte found at addr is the strings length, the address of the start of the string characters and the string length are left on the stack.

CR ( -- ) say: "sea-are"  <standard>   "Cr" advances the cursor to the next line.  Do not confuse this word with "{cr}".

CREATE while compiling: ( -- ) while executing: ( -- addr )  <standard>   Create builds a word from the next token in the input stream.  When the new word is executed, it returns the relative address of the cell following the words entry.

CSTATE ( -- addr ) say: "sea-state"   Returns the relative address of a byte which is zero if the interpreter is not in 'compiling' mode and 128 if it is.

D+ ( n1 n2  n3 n4 -- n1+n3 n2+n4 ) say: "dee-plus"  <standard>   Adds the top two double numbers and leaves the double number sum on the stack.

D. ( d -- ) say: "dee-dot"  <standard>   Print the dvalue on the stack according to the current number base.

D>F ( d -- f ) <floating> say: "dee-to-eff" Convert a double number on the stack to a floating point number.

DABS ( dval -- |dval| ) say: "dabs"  <standard>   Return the absolute value of the dvalue on the top of the stack.

DECIMAL ( -- )  <standard>   Sets the current number base to ten.

DEPTH ( -- n )  <standard> Return the number of 16 bit entries on the stack.

DL! ( n1 n2 daddr32 -- ) say: "dee-el-store"   Store a 32 bit value at an absolute 32 bit address.

DL@ ( daddr32 -- n1 n2 ) say: "dee-el-at"   Get the 32 bit value from the 32 bit absolute address on the stack.

DLITERAL  compiling: ( d -- )  executing: ( -- d )  <standard>   "Dliteral" compiles a double number from the stack. When a word containing a dliteral is executed, the number is pushed to the stack.

DNEGATE ( d -- -d ) say: "dee-negate"  <standard>  Negate the 32 bit value on the stack.

DO ( -- )  <standard>   Compile the word "paren-do" to begin an indexed loop.  The 16 bit index is kept on the return stack, and can be accessed with r.  Use with "loop" or "+loop". "Do" is an immediate word to be used within a colon definition.  (see "paren-do", "loop" and "+loop")

DOES>  while compiling: ( -- ) while executing: ( addr -- ) say: "does"  <standard>  "Does>" is used in the definition of a defining word, following "create" to define the run-time behavior of the defined word.

DROP ( n1 n2 -- n1 )  <standard>   Remove the value on the top of the stack.

DUP ( n -- n n ) say: "dupe"  <standard>   Duplicate the value on the top of the stack.

ELSE while compiling: ( addr -- addr )  while executing: ( -- )  <standard>   Used optionally between "if" and "then" in a conditional forward branch.  "Else" is an immediate word and is used within a colon definition.

EMIT ( c -- )  <standard>   Print the ASCII character represented by the value of a number on the stack.

EXECUTE ( addr -- )  <standard>   "Execute" causes the routine whose relative address is on the stack to happen.

EXIT ( -- )  <standard>   "Exit" drops an absolute address from the return stack and executes a machine language return instruction, terminating the current routine.

EXPECT ( addr count -- )  <standard>   Waits for 'count' number of characters to be typed, storing the characters, in order, at the relative address, addr.  If more characters are typed, they are echoed to the screen, but not saved. A blank character and a zero byte are appended to the characters.  Events are handled normally during "expect".

F! ( f addr -- ) <floating> say: "eff-store" Store the floating point number, f, at address, addr.

F* ( f1 f2 -- f1*f2 ) <floating> say: "eff-times" Multiply f1 by f2 returning the product to the stack.

F+ ( f1 f2 -- f1+f2 ) <floating> say: "eff-plus" Add f1 to f2 returning the sum.

F, ( f -- ) <floating> say: "eff-comma" Enclose a floating point number from the stack to the dictionary.

F- ( f1 f2 -- f1-f2 ) <floating> say: "eff-minus" Subtract f2 from f1.

F. ( f -- ) <floating> say: "eff-dot" Output a floating point number from the stack. Infinities and NAN codes are supported. See "sci" and "fix".

F/ ( f1 f2 -- f1/f2 ) <floating> say: "eff-slash' divide f1 by f2.

F>D ( f -- d ) <floating> say: "eff-to-dee" Convert a floating point number on the stack to a double number.

F@ ( addr -- f ) <floating> say: "eff-at" Fetch the floating point number from an address in memory.

FATN ( f -- atn[f] ) <floating> say: "eff-ay-tee-en" Return the arctangent, in radians, of a floating point number. (1 radian = 57.2957795131 degrees)

FCOMPARE ( f1 f2 -- f1 f2 flag ) <floating> say: "eff-compare" A non-destructive comparison, returns a flag that depends on the relative values of f1 and f2.  If f1>f2 the flag is +1, if f1<f2 the flag is -1.  If f1=f2 exactly, the flag is zero.  Notice that f1 and f2 are unchanged, and left on the stack.

FCOS ( f -- cos[f] ) <floating> say: "eff-cos" Return the cosine of a floating point angle expressed in radians. (1 radian = 57.2957795131 degrees)

FDROP ( f -- ) <floating> say: "eff-drop" Remove the top floating point value from the top of the stack.

FDUP ( f -- f  f ) <floating> say: "eff-dup" Duplicate the floating point value on the top of the stack.

FEXP ( f -- e^f ) <floating> say: "eff-eksp" Return the value of Euler's number raised to the power of a floating point number. (e = 2.71828182846 )

FILL ( addr count char -- )  <standard>   Places 'count' characters of 'char' at the relative address, 'addr'.

FINT ( f -- int[f] ) <floating> say "eff-int" Return the whole number part of a floating point number.

FIX ( n -- ) <floating> Set floating point output to decimal fractions with n digits to the right of the decimal point. See "sci" and "f.".

FLITERAL ( comp: f -- | exec: -- f ) <floating> say: "eff-literal" Compile the code to push the value of a floating point number at runtime. Floating point literals are twenty (20) bytes in length. If a number is used more than once it is more efficient to use a constant; see "fconstant".

FLN ( f1 -- ln[f1] ) <floating> say: "eff-ell-en" Return the natural logarithm of a floating point number. (base = e = 2.71828182846 )

FNUMBER ( dabs.addr -- f ) <floating> say: "eff-number" Convert a character string located at the absolute address on the stack to a floating point number. Infinities and NAN codes are supported.

FORGET ( -- )  <standard>   Searches the dictionary for the next token from the input stream.  If found, that word and all subsequent words are removed from the dictionary.

FPACK ( fn..f1 fnew m -- fn..f1 :: fm = fnew ) <floating> say: "eff-pack" Place the floating point number, fnew, into the 'm-th' position on the stack. The floating point value, fnew, and the index, m, are removed from the stack.

FPICK ( fn..f1 m|n�m�1 -- fn..f1 fm ) <floating> say: "eff-pick" Duplicate the 'm-th' floating point value to the top of the stack.

FREM ( f1 f2 -- rem[f1/f2] ) <floating> say: "eff-rem" Return the remainder of f1 divided by f2.

FROLL ( fn..f1 m -- fn..fm+1 fm-1..f1 fm ) <floating> say: "froll" Roll the 'm-th' floating point number to the top of the stack, shifting the numbers between position 1 and position m ten bytes up.

FSIN ( f -- sin[f] ) <floating> say: "eff-sign" Return the sine of a floating point angle expressed in radians. (1 radian = 57.2957795131 degrees)

FSQRT ( f -- sqrt[f] ) <floating> say: "eff-squirt" Return the square root of a floating point number.

FSWAP ( f1 f2 -- f2 f1 ) <floating> say: "eff-swap" Exchange the position of the two top most floating point values on the stack.

FTAN ( f -- tan[f] ) <floating> say: "eff-tan" Return the tangent of a floating point angle expressed in radians. (1 radian = 57.2957795131 degrees)

FVARIABLE ( compile: -- ) ( run: -- addr ) <floating> say: "eff-variable" Create a ten byte variable for storing floating point numbers.

F^ ( f1 f2 -- f1^f2 ) <floating> say: "eff-to-the" Return the value of f1 raised to the power of f2.

GROW ( n -- ) <DA only> Adjust the dictionary allocation by n (modulo 32K) bytes. If n is negative, the allocation is diminished.

HEADER ( -- )   "Header" builds a name and link field for a new word at "here".

HERE ( -- addr )  <standard>   "Here" is the relative address of the start of free memory.

HEX ( -- )  <standard>   "Hex" sets the current number base to sixteen.

HOLD ( c -- )  <standard>  Insert the character on the stack into the number being converted to a string.  Use between "greater-than-sharp" and "sharp-less-than".

IF ( flag -- )  <standard>   Used with "else" and "then" to branch conditionally.  A true flag causes the words following "if" and before "then" (or "else") to be executed.  "If" is an immediate word and is used within a colon definition.

ID. ( addr -- ) say: "eye-dee-dot"  <standard>   Print the name of the word whose address is on the stack. Undefined characters are represented by an ellipsis.

IMMEDIATE ( -- )  <standard>   "Immediate" is used after a definition, to flag the word as 'immediate' so that is it will execute within a colon definition, rather than being compiled into the definition.  "Immediate" sets bit seven of the name length byte of the last word defined.

INTERPRET ( -- ) <standard>   Begin interpreting the contents of the input buffer.

KEY ( -- n )  <standard>   Waits for a character to be typed, echoes the character to the screen, advances the cursor and returns the ASCII code on the stack.  Events are handled during the wait.

L! ( n daddr32 -- ) say: "el-store"   Store the value of n at the absolute address on the stack.

L@ ( daddr32 -- n ) say: "lat" or "el-at"   Retrieve the value found at the absolute address on the stack.

LATEST ( -- name.addr )  <standard>   Return the name address of the last word defined.  Latest is used by "search" to find the end of the dictionary.

LEAVE ( -- )  <standard>   Causes a premature exit from a "do", "loop" (or "+loop") construct by setting the loop index equal to the loop limit.  Use only within a definite loop structure.

LITERAL compiling: ( n -- )  executing: ( -- n )  <standard>   "Literal" compiles a number from the stack to the dictionary.  When a word containing a literal is executed, "literal" pushes the number onto the stack.

LOOP compiling: ( addr -- )  executing: ( -- ) <standard>   "Loop" is an immediate word used to terminate a "do" � "loop" construction, in a colon definition.  Branch to the beginning of the loop if the index is less than the limit.  (see "+loop" and "do")

M/MOD ( numer32 denom16 -- rem16 quot32 ) say: "em-slash-mod"  <standard>   Divide a double number by a single number leaving a single remainder and a double quotient.

MACRO ( -- ) A word is flagged as a macro definition by following the word's definition with the word "macro".  Macro definitions compile their code field inline rather than compiling a subroutine call.  "Macro" sets bit six of the name length byte of the last word defined.  (see "mcompile" and "immediate" )

MAX ( n1 n2 -- n )  <standard>   Returns the larger of the two top numbers on the stack.

MCOMPILE ( addr -- ) "Mcompile" writes the code field found at the address on the stack.  An RTS instruction signals the end of the routine and compilation stops.  "Mcompile" compiles any word's code field.

MIN ( n1 n2 -- n )  <standard>   Returns the smaller of the top two numbers on the stack.

MOD ( n1 n2 -- remainder ) say: "mod"  <standard>   Returns the remainder (but not the quotient) of 'n1' divided by 'n2'.

MON ( -- )   Causes a monitor such as TMON or MacsBug to activate via the  _Debugger trap. Execution will continue upon exit from the monitor.

NEGATE ( n -- -n )  <standard>   Leave the result of zero minus n on the stack.

NULL ( -- )   This is a no operation word.

NUMBER ( addr -- n t  OR  f )  <standard>   "Number" attempts to convert the string at addr to a value according to the current number base.  If the conversion is successful (that is, if all characters are numerals) the value and a true flag are left on the stack.  Failure leaves only a false flag on the stack.  Unlike FORTH's NUMBER, "number" does not convert double length numbers.

OPEN ( -- ) "Open" displays the standard file dialog that allows you to select a file to be interpreted.  Unlike "-->", this does not require the path to be specified.  (see "load next file")

OR ( n1 n2 -- n1ORn2 )  <standard>   Leave the result of n1 OR n1 on the stack.  The value is computed bitwise.

OVER ( n1 n2 -- n1 n2 n1 )  <standard>   "Over" duplicates the second number on the stack to the top of the stack.

PAD ( -- addr )  <standard>   Leave the address of a scratch pad for numeric conversion.  The pad is used downward in memory.  The address of "pad" is 40 bytes beyond "here".

PAGE ( -- )  <standard>   "Page" is from the days of mechanical Teletype terminals but is still used.  It clears the window and moves the cursor to the upper left hand corner.

PMODE ( mode -- ) say: "pea-mode"   Set the drawing transfer mode of the pen.

QUIT ( -- )  <standard>   "Quit" stops executing and returns to the input loop with no message. (see "abort")

R ( -- n ) say: "are"  <standard>   "Are" puts the top 16 bit number of the return stack onto the (parameter) stack. The return stack is unaffected.  During the execution of a definite loop ("do" � "loop") the index is kept on the top of the return stack.  "Are" is used to retrieve the value of the index within these loops. (see "to-are", "are-from", "do", "loop" and "plus-loop")

R0@ ( -- dabs.addr ) say: "are-naught-at"   Return the absolute address of the bottom of the return stack.

R> ( -- n )  return stack: ( n -- ) say: "are-from"  <standard>   "Are-from" gets a number off the return stack and puts it on the parameter stack.  (see "to-are" and "are")

REPEAT while compiling: ( addr1 addr2 -- )  while executing: ( -- )  <standard>   "Repeat" is an immediate word, used within a colon definition to terminate a "begin" �"while", � "repeat" indefinite loop.  At runtime "repeat" branches unconditionally to the word following "begin" (at addr1).  (see "begin" and "while")

ROOM ( -- bytes ) "Room" leaves the bytes of headroom above "here" on the stack.  Addresses beyond the headroom should not be written to, even if they are addressable, because they may be used by the system.

ROT ( n1 n2 n3 -- n2 n3 n1 ) say: "rote"  <standard>   "Rot" brings the third stack item to the top of the stack.

RP@ ( -- dabs.addr ) say: "are-pea-at"  Return the absolute address of the top of the return stack.

S0@ ( -- dabs.addr ) say: "ess-naught-at"  Return the absolute address of the bottom of the parameter stack.

S>D ( n -- d ) say: "ess-to-dee"   Make a single number on the stack into a double number using sign extension.

SAVE ( -- )   "Save" writes the dictionary to the disk.  All pertinent data, such as headroom size, the values of variables, etc. are also saved.

SCI ( n -- ) <floating> say: "sigh" Set floating point output to scientific notation with n significant digits. See 'fix' and 'f.'.

SEARCH ( addr -- addr t OR f )   "Search" looks for the next token from the input stream in the dictionary, starting with the word whose name address is on the stack.  If found, its address and a true flag (minus one) are returned. If the search fails, a false flag (zero) is left on the stack.

SIGN ( n d -- d )  <standard>   If the single number is negative, place a negative sign into the conversion "pad".  Use between "greater-than-sharp" and "sharp-less-than".

SP@ ( -- dabs.addr ) say: "ess-pea-at" <standard>  Return the absolute address of the top of the parameter stack before the address is put on it.

SPACE ( -- ) <standard>   "Space" prints a space character.

SWAP ( n1 n2 -- n2 n1 )  <standard>   "Swap" exchanges the top two numbers on the stack.

TASK ( -- )   "Task" is a no operation word which marks the end of the dictionary.  The added part of the dictionary can be removed by executing:  FORGET TASK    : TASK ;

THEN while compiling: ( addr -- )  while executing: ( -- )  <standard>   "Then" is an immediate word which terminates an "if", ("else"), "then" construction within a colon definition. (see "if" and "then")

TIB ( -- addr ) say: "tib" (rhymes with rib)  <standard>   "Tib" returns the relative address of the terminal input buffer. The buffer is an 82 byte data area below the dictionary.  The input stream usually points to a byte within "tib".

TOKEN ( -- )   "Token" moves the next word from the input stream to "here", the end of the dictionary.

TYPE ( addr n -- ) <standard>   "Type" prints n number of characters from memory starting at the relative address, addr.  For best results addr should contain at least n ASCII characters.

U. ( n -- ) say: "you-dot"  <standard>   Print the value of n in the current numeric base as an unsigned number.

U* ( n1 n2 -- d[n1*n2] ) say: "you-star"  <standard>   "You-star" multiplies two unsigned 16 bit numbers from the stack and leaves a double number product on the stack.

UNTIL ( flag -- )  <standard>   "Unitl" is an immediate word used with in a colon definition after "begin" to conditionally terminate an indefinite loop.  If flag is true execution passes to the next word.  If false it branches back to the word following "begin".   (see "begin" and "back")

UPPER ( addr -- ) Given a string's address on the stack, "upper" converts lower case to upper case.  The first byte must contain the length of the string.

VARIABLE compiling: ( -- ) executing: ( -- addr )  <standard>   "Variable" creates a word from the next word in the input stream, and reserves one cell (two bytes) of data.  When the new word is executed, it leaves the relative address of the data cell on the stack.   Words created with "variable" are four byte macros.

WARM ( -- ) <standard> "Warm" restarts the Pocket Forth application as if it had been rebooted, except changes to the dictionary are kept.

WHAZAT ( -- ) say: "what-is-that"   "Whazat" prints the current token from the input stream, and executes "abort", if the current token was not found in the dictionary.

WHILE ( flag -- )  <standard>   "While" is an immediate word used within a colon definition, between "begin" and "repeat" to control an indefinite loop with an exit in the middle.  If the flag is true, the words after "while" and before "repeat" are executed, if the flag is false, execution jumps to the word following "repeat". (see "begin" and "repeat".)

WORD ( c -- )  <standard>   "Word" moves the next token, delimited by the character on the stack, from the input stream  to "here", the end of the dictionary.

WORDS ( -- )  <standard>   "Words" prints all of the words in the dictionary.

XOR ( n1 n2 -- ) <standard> say: "zor" or "eks-or"   Leave the result of a bitwise exclusive or of n1 and n2 on the stack.

[ ( -- ) say: "left-bracket"  <standard>   "Left-bracket" sets the interpreter into immediate mode.  Words following "left-bracket" are executed rather than compiled.  "Left-bracket" is an immediate word.

[COMPILE] ( -- ) say: "bracket-compile"  <standard>   "Bracket-compile" is an immediate word used within a colon definition to compile the following immediate word from the input stream into the current definition.

\ ( -- ) say "back slash"  <standard>   "Back slash" causes the rest of the line to be ignored. Used for commenting. "Back slash" is an immediate word.

] ( -- ) say: "right-bracket"  <standard>   "Right-bracket" puts the interpreter into compile mode so that subsequent non-immediate words will be compiled to the dictionary.  "Right-bracket" is an immediate word.

"{cr}" ( -- ) say: ""   When the token consisting of an ascii 13 is executed, the return stack is reset, and the input sequence is restarted.  This is an immediate word.  Do not confuse this word with "cr".

"{null}" ( -- ) say: "" <standard>   This is an alias for "{cr}" to assure that "expect"ed text, which is terminated by a null (zero byte), and pasted text are treated the same.  This is an immediate word.