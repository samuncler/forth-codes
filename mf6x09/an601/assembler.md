S = Forth data stack pointer U = Forth return stack pointer  

D = TOS
Y = IP
X = free

CODE <name>  ...  NEXT END-CODE    

: NEXT ( -- ) Y )++ \[\] JMP ;

 

**Motorola**     **MaisForth an601**

push & pull

PULS D,X      REG D,X PULS
PULU ...      ALLREG  PULU (all registers)

indexed

     )
    #)

LDD  0,Y      Y ) LDD
LDB   ,U      U ) LDB
LDA   33,X    X  33 #) LDA
LDY   -2,S    S  -2 #) LDY
LDX  400,Y    Y 400 #) LDX

    D)
    A)
    B)

LDX  D,Y      Y D)  LDX
LEAX A,X      X A)  LEAX
LDA  B,Y      Y B)  LDA

     )+
     )++
    -)
   --)

LDA  ,X+      X )+  LDA       
STD  ,Y++     Y )++ STD
LDB  ,-Y      Y  -) LDB
LDX  ,--S     S --) LDX

indexed indirect

LDA \[$10,X\]   X 10 #) \[\] LDA

extended indirect

LDA \[$1234\]   1234    \[\] LDA

inherent

ASLA          ASLA
CLRB          CLRB

immediate

LDA    #7        7 # LDA
LDD #1234     1234 # LDD

extended/absolute

LDA >$0100     100 LDA
JMP >$1234    1234 JMP

relative

BRA 1234      1234 BRA

PC relative (not used)

LDA $1234,PC  1234 PC) LDA

DP relative (not used, DP=0)

LDA   $34,DP    34 DP) LDA

assembler conditionals

IF AHEAD ELSE THEN
BEGIN WHILE AGAIN UNTIL REPEAT

conditions
  
preceding
  
 IF UNTIL WHILE

CS?  <?  U<?  =?
VS?  >?  U>?  0<?
NO ( opposite condition )
=? IF  |  CS? NO UNTIL  |  U<? NO WHILE