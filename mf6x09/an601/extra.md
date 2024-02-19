an601extra-gb body{font:10pt verdana;margin:10%;color:#300} pre {font:11pt "letter gothic mt",monospace;color:#000} tt {font:11pt "letter gothic mt",monospace;color:#000} a {font:11pt "letter gothic mt",monospace;color:#f00;text-decoration:none} h2 {font:13pt "letter gothic mt",monospace;font-weight:100;color:#00f;margin-left:3em;margin-top:2em;margin-bottom:0.2em} .kop{font-size:14pt;color:#300;text-align:center} td {font-size:10pt;color:#300;vertical-align:top} span{font:10pt verdana;color:#300} .rood{font-size:8pt;color:#300;background-color:#f00;font-weight:600;text-align:center} .klein{font-size:8pt;color:#300}

20apr2006

  MaisForth an60x  

Albert Nijhof  
12jul2005

EXTRA and ONLY words (non-standard)

**EXTRA**

[!USART](#bau)
[!VECTOR](#!ve)

["](#wor)

['FIRQ](#!ve)
['IRQ](#!ve)
['NMI](#!ve)
['SWI](#!ve)
['SWI2](#!ve)
['SWI3](#!ve)

[+TO](#str)

[.MSG](#msg)
[.VOC](#voc)

[1+!](#xxx)
  

[\>NAME](#bod)
[\>OK](#ok)

[?BASE](#pai)
[?COMP](#pai)
[?EXIT](#})
[?DNEGATE](#neg)
[?NEGATE](#neg)
[?PAIR](#pai)
[?RE](#})  
[?STACK](#pai)
[@+](#xxx)

[ALLWORDS](#wid)
[ANEW](#ane)

[BACKSPACE](#pag)
[BINARY](#him)
[BYTESWAP](#xxx)
[BODY>](#bod)

[C+!](#xxx)
[CELL](#xxx)
[CELL-](#xxx)
[COLD](#him)
[CTRL](#wor)

[D.STRING](#du.)
[DIGIT>](#dot)
[DISABLE](#!ve)
[DNUMBER?](#dot)
[DOER:](#doe)
[DOERCODE](#doe)
[DOT?](#dot)
[DU\*](#DU*)
[DU/MOD](#du*) 
[DU.](#du.)
[DU.R](#du.)
[DU.STRING](#du.)
[DU2/](#xxx)

[ENABLE](#!ve)

[HIDE](#ane)
[HIMEM](#him)
[HOR](#pag)

[INCR](#str)

[MANY](#man)
[MSEE](#mse)
[MSG"](#msg)

[NAME>](#bod)

[OK](#ok)

[PARSE,](#wor)
[PLACE](#upp)

[RDROP](#xxx)
[RE](#})
[REMOVE](#ane)
[REVEAL](#ane)
[RE}](#})
[RTYPE](#du.)

[S<>](#upp)
[SCAN](#ski)
[SKIP](#ski)
[STOP?](#pai)
[STRING](#str)

[TIMES](#man)

[U.S](#him)
[UMAX](#xxx)
[UMIN](#xxx)
[UPPER](#upp)

[VARIABLES](#var)
[VER](#pag)
[VOCABULARY](#voc)

[WORD>](#wor)
[WORD,](#wor)

[}](#}) 

**ONLY**

[BN](#hx)
[DM](#hx)
[HX](#hx)
[FRESH](#wid)
[EXTRA](#wid)
[INSIDE](#wid)

MSEE ( adr -- )
---------------

Decompile starting from adr (may be any address).

: SEE ( <name> -- ) ' MSEE ;

[top  
^](#top)

VOCABULARY ( <ccc> -- )
-----------------------

Create a wordlist with the name ccc  
When ccc is executed, it replaces the top wordlist in the search order by itself.

.VOC ( wid -- )
---------------

Display the name that corresponds with wid  
If there is no name, display a question mark. Only an even number 0..126 can be a valid wid

[top  
^](#top)

EXTRA ( -- )
------------

A vocabulary (wordlist) containing non-standard words for programmers.

INSIDE ( -- )
-------------

A vocabulary with non-standard auxiliary words for Forth itself. Programmers should not need them.

FRESH ( -- )
------------

Make FORTH FORTH EXTRA ONLY the search order.  
Forth starts up with FRESH DEFINITIONS

ALLWORDS ( -- )
---------------

Display all words in all wordlists.

ONLY ( -- )
-----------

A special vocabulary that, when executed, sets the search order to ONLY ONLY  
It contains the following words:

 \[AHEAD\]  \[IF\]  \[ELSE\]  \[THEN\]  BN  DM  HX  WORDS  FRESH  ORDER 
 SET-CURRENT  GET-CURRENT  DEFINITIONS  PREVIOUS  ALSO  ASSEMBLER 
 EXTRA  INSIDE  FORTH

[top  
^](#top)

HX ( <ccc> -- )
---------------

Handle the next number or word in the input stream.  
During this process BASE is temporarily set to 16.

DM ( <ccc> -- )
---------------

BASE is temporarily 10.

BN ( <ccc> -- )
---------------

BASE is temporarily 2.

Examples:

*   Before numbers
    
    DECIMAL \[rtn\] OK
    HX 10 . \[rtn\] 16  OK
    BN 10 . \[rtn\] 2  OK
    : TEN HX A . ; TEN \[rtn\] 10  OK
    
    This works both executing and compiling.
    
*   Before Forth words
    
    HX DM and BN are also useful before words that display numbers.
    
    DECIMAL 10 20 \[rtn\] OK
    .S \[rtn\] ( 10 20 )  OK
    HX .S \[rtn\] ( A 14 )  OK
    BN .S \[rtn\] ( 1010 10100 )  OK
    HX . BN . \[rtn\] 14 1010  ok
    
    This works only executing.  
    HX DM en BN have no effects before words that are compiled.

[top  
^](#top)

ANEW ( <ccc> -- )
-----------------

Create a marker with the name ccc  
If ccc already exists, execute it and then create the new marker ccc

REMOVE ( -- )
-------------

Erase the newest definition if "unfindable" and display its name.  
Nothing happens when the newest definition can be found.

REVEAL ( -- )
-------------

Make the newest definition "findable".

HIDE ( -- )
-----------

Make the newest definition "unfindable".

[top  
^](#top)

MSG" ( msg# <ccc"> -- )
-----------------------

Define a THROW message.

.MSG ( msg# -- )
----------------

Display the message corresponding with msg#

Ex.:

\-100 MSG" tsssss" \[rtn\] OK
-100 .MSG \[rtn\] tsssss (Message # -100)  OK
-100 THROW \[rtn\]
THROW  tsssss (Message # -100) 

[top  
^](#top)

: ?COMP ( -- ) STATE @ ?EXIT -14 THROW ;  
: ?PAIR ( x y -- ) = ?EXIT -22 THROW ;
---------------------------------------------------------------------------------

?STACK ( -- )
-------------

Test for Data Stack Overflow and Underflow.

?BASE ( -- )
------------

Execute DECIMAL when BASE is not in \[2..72\].

STOP? ( -- flag )
-----------------

Test for pressed key:

**key**             **effect**           **flag**

no key          -                 false

\[space\]         wait 
    and then
\[space\]         continue          false

\[esc\]           -28 THROW         -
anything else   continue          true

[top  
^](#top)

?EXIT
-----

Short for IF EXIT THEN

}
-

Short for EXIT THEN

RE
--

RE compiles a jump back to the beginning of the current definition. Compile time it does not interfere with controle structures. From within a do-loop of course an UNLOOP is needed.

?RE
---

Short for IF RE THEN

RE}
---

Short for RE THEN

RE ?RE and RE} can be used only within colon definitions (not in :NONAME definitions or in Does-code).

RE is nice in loops with multiple conditions, whether nested or not, when you want to be able  
1) to repeat the loop or  
2) to leave the word.  
Using RE and EXIT in such cases, you get rid of the paired conditionals gymnastics needed for nested constructions with UNTILs, WHILEs and REPEATs. Just as LEAVE the words EXIT en RE do not interfere with compile time control structures.

[top  
^](#top)

'NMI 'SWI 'IRQ 'FIRQ 'SWI2 'SWI3 ( -- adr )
-------------------------------------------

6809 interrupt vectors

DISABLE ( 'vector -- )
----------------------

Ex.: 'SWI3 DISABLE

!VECTOR ( adr 'vector -- )
--------------------------

Vb: 47AE 'SWI3 !VECTOR

ENABLE ( 'vector -- )
---------------------

Vb: 'SWI3 ENABLE

[top  
^](#top)

!USART ( baudfactor -- )
------------------------

Using the "baudfactor", set the Baud Rate for communication.  
 

**baudfactor  Baud rate
HX/DM**

7F/127      19200 (default)  
7E/126       9600  
7D/125       7200  
7C/124       4800  
7B/123       3600  
7A/122       2400  
79/121       2000  
78/120       1800  

**baudfactor  Baud rate 
HX/DM**

77/119       1200  
76/118        600  
75/117        300  
74/116        150  
73/115        134.5  
72/114        110  
71/113         75  
70/112         50  

[top  
^](#top)

DOER: ( <ccc> -- )
------------------

DOER: ccc ... ;  
is short for  
: ccc DOES> ... ;

DOERCODE ( <ccc> -- )
---------------------

DOERCODE ccc ... END-CODE  
is short for  
: ccc ;CODE ... END-CODE

Ex.:

DOER: DOKON  @ ;
: KONSTANT   CREATE , DOKON ;
or
: KONSTANT   CREATE DOKON , ;

[top  
^](#top)

HOR ( -- q )
------------

q is the horizontal output position (column#).

VER ( -- q )
------------

q is the vertical output position (row#).

BACKSPACE ( -- )
----------------

Do a backspace when HOR is not zero.

HOR and VER are zero after PAGE  
CR makes HOR zero and adds 1 to VER

[top  
^](#top)

VALUE ( x <ccc> -- )  
TO ( x <ccc> -- )  
+TO ( y <ccc> -- )  
INCR ( <ccc> -- )
---------------------------------------------------------------------------------

STRING ( maxlen <ccc> -- )  
TO ( a1 n <name> -- )  
+TO ( a2 n <ccc> -- )  
INCR ( char <ccc> -- )
---------------------------------------------------------------------------------------------------

Ex.:

10 VALUE N N . \[rtn\] 10  OK
7     TO N N . \[rtn\] 7  OK
8    +TO N N . \[rtn\] 15  OK
    INCR N N . \[rtn\] 16  OK
N    +TO N N . \[rtn\] 32  OK
N 2/  TO N N . \[rtn\] 16  OK

Ex.:

12   STRING NN NN TYPE \[rtn\] OK
S" Mad"  TO NN NN TYPE \[rtn\] Mad OK
S" rid" +TO NN NN TYPE \[rtn\] Madrid OK
CHAR - INCR NN NN TYPE \[rtn\] Madrid- OK
NN      +TO NN NN TYPE \[rtn\] Madrid-Madri OK
NN 2/    TO NN NN TYPE \[rtn\] Madrid OK

[top  
^](#top)

" ( <ccc"> -- adr len | -- )
----------------------------

The same as S"  
Compiling: compile the string.  
Executing: put the string (adr,len) on the stack.

PARSE, ( ch <ccc> -- )
----------------------

Parse a string with delimiter ch and put the result in the dictionary as a counted string.

WORD, ( ch <ccc> -- )
---------------------

Execute ch WORD and put the result in the dictionary as a counted string.

WORD> ( ch <ccc> -- adr )
-------------------------

Execute ch WORD  
Do a REFILL when the result is the nullstring, and try again.  
\-16 THROW is executed when REFILL does not succeed.

CTRL ( <ccc> -- q | -- )
------------------------

AND the first character of ccc with HX 1F and  
(executing:) put the result on the stack;  
(compiling:) compile the result as a literal.

[top  
^](#top)

DIGIT> ( char -- x true | char false )
--------------------------------------

Convert a digit (character) into its value if possible. A false flag means: result not valid. BASE is implicitly used.

DNUMBER? ( adr len -- xlo xhi true | ? ? false )
------------------------------------------------

Convert the string adr len into a double number using BASE  
A false flag means: result not valid. A minus sign is accepted only as the first character of the string. One dot is accepted in any position, see DOT?

DOT? ( -- q )
-------------

After execution of DNUMBER? the position of a dot is in the value DOT?

Ex.:

**string**    **DOT?**

1234      0        (no dot)
1234.     1
123.4     2
.1234     5

[top  
^](#top)

OK ( -- q )
-----------

q contains the prompt properties.

\>OK ( q -- )
-------------

Set OK to q

For q=0 there is only a CR  
When bit n in q is set:  
 

bit 0:

Display OK (executing) or ok (compiling), followed by a CR

bit 1:

Execute .S after CR

bit 2:

If bit 1 is not set: execute U.S after CR

bit 3:

Display BASE (if not ten)

bit 4..7:  

not used

[top  
^](#top)

: ?NEGATE ( x y -- x2 ) 0< IF NEGATE THEN ;
-------------------------------------------

: ?DNEGATE ( dx y -- dx2 ) 0< IF DNEGATE THEN ;
-----------------------------------------------

[top  
^](#top)

VARIABLES ( n -- )
------------------

: VARIABLES
  CREATE CELLS ALLOT
  DOES> ( index -- adr ) SWAP CELLS + ;

Ex.:
3 VARIABLES Z ( index -- adr )
111 0 Z !
555 2 Z !              \\ Index must be <3
0 Z @ . \[rtn\] 111  OK

[top  
^](#top)

DU\* ( ud1 u2 -- ud3 )
----------------------

32bit \* 16bit >> prod=32bit

DU/MOD ( ud1 u2 -- u3 ud4 )
---------------------------

32bit / 16bit >> rem=16bit, quot=32bit

[top  
^](#top)

: BODY> ( body -- xt ) 3 - ;
----------------------------

\>NAME ( xt -- nfa )  
NAME> ( nfa -- xt )
------------------------------------------

In MaisForth xt = cfa

[top  
^](#top)

SCAN ( adr len ch -- adr2 len2 )
--------------------------------

Ex.:

S" AAABC" CHAR B SCAN TYPE \[rtn\] BC OK
S" AAABC" CHAR F SCAN TYPE \[rtn\] OK

SKIP ( adr len ch -- adr2 len2 )
--------------------------------

Ex.:

S" AAABC" CHAR A SKIP TYPE \[rtn\] BC OK
S" AAABC" CHAR B SKIP TYPE \[rtn\] AAABC OK

[top  
^](#top)

MANY ( -- )
-----------

Interpret the text before MANY (on this line) again and again. Continue after MANY when a key is pressed.

Ex.:

0 \[rtn\] OK
1+ DUP . MANY 0 . \[rtn\] 1 2 3 4 5 6 ...

TIMES ( q -- )
--------------

Interpret q times the text before TIMES (on this line) and then continue after TIMES

Ex.:

0 \[rtn\] OK
1+ DUP . 5 TIMES 0 . \[rtn\] 1 2 3 4 5 0  OK

[top  
^](#top)

DU. ( xlo xhi -- )  
DU.R ( xlo xhi r -- )
------------------------------------------

D.STRING ( xlo xhi -- adr len )
-------------------------------

Convert the signed double number xlo xhi into a string.

DU.STRING ( xlo xhi -- adr len )
--------------------------------

Convert the unsigned double number xlo xhi into a string.

Lifetime of the result of D.STRING or DU.STRING is short, it wil be overwritten in the next conversion.

RTYPE ( adr len r -- )
----------------------

Display the string (adr,len) right aligned in a field of r positions.

: D.   ( d -- )    D.STRING  TYPE SPACE ;
: .R   ( n r -- )  >R S>D D.STRING  R> RTYPE ;

[top  
^](#top)

UPPER ( adr len -- )
--------------------

Convert lowercast characters of the string into uppercast.

PLACE ( adr len dest -- )
-------------------------

Put the string (adr,len) as a counted string in dest

S<> ( adr1 adr2 len -- q )
--------------------------

Compare string1 (adr1,len) to string2 (adr2,len)

string1 = string2:    q =  0
string1 < string2:    q = -1
string2 < string1:    q =  1

[top  
^](#top)

RDROP ( -- )
------------

Short for R> DROP

2RDROP ( -- )
-------------

Short for RDROP RDROP

UMAX ( u1 u2 -- u )  
UMIN ( u1 u2 -- u )
-----------------------------------------

CELL ( -- 2 )  
CELL- ( x -- x-2 )
----------------------------------

: 1+! ( a -- ) 1 SWAP +! ;  
: C+! ( x a -- ) TUCK C@ + SWAP C! ;
-----------------------------------------------------------------

@+ ( adr -- adr+cell x )
------------------------

The 16 bit variant of COUNT

: DU2/ ( du1 -- du2 ) D2/ HX 7FFF AND ;
---------------------------------------

Double number logical shift right.

BYTESWAP ( xy -- yx )
---------------------

Swap low and high byte of a 16 bit pattern.

Ex.:

HEX 1234 BYTESWAP . \[rtn\] 3412  OK

[top  
^](#top)

HIMEM ( -- q )
--------------

q is the amount of RAM, or: the lowest non existing RAM address.

COLD ( ? -- )
-------------

Do a cold start.

U.S ( -- )
----------

A .S variant that displays unsigned numbers.

: BINARY ( -- ) 2 BASE ! ;
--------------------------

[top  
^](#top)