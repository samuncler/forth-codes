(HCC Forth-gg)*   Background
    
    MaisForth started from CamelForth (Bradford J. Rodriguez, 1995), but that's hardly visible now.  
    The metacompiler is completely new and has nothing in common with the CamelForth metacompiler.  
    Assembler notation has been altered and the target code is drastically changed. In fact the only things left from CamelForth are:  
    \- the registerchoice for the Forth machine (direct threaded code);  
    \- some of the larger primitives, as MOVE UM\* UM/MOD and a few others. In the target file those words are marked with 'BJR'.
    
*   Email
    
    MaisForth an601 may still have bugs. Please contact us when you have questions or remarks about MaisForth. Click [here](http://www.forth.hccnet.nl/mail-gb.htm) and then click on "Mail us".
    
*   Files
    
    an601-readme.html
    
    This file
    
    an601-leesmij.html
    
    idem, Dutch version
    
     
    
    an601extra-nl.html  
    
    Information about non-standard words
    
    an601extra-gb.html  
    
    idem, Dutch version
    
     
    
    an601assembler.html
    
    About 6809 assembler notation
    
    an601color.html
    
    Didactically colored target code
    
    an601.bin
    
    MaisForth an601 ROM image (C000-FFFF)
    
     
    
    meta601.f
    
    Metacompiler code
    
    cras601.f
    
    Cross assembler code (part of metacompiler)
    
    targ601.f
    
    Target code
    
*   Hardware
    
    MaisForth an601 is a 6809 Forth for "maiskastje". The words that use this special hardware are:
    
       KEY? ( -- flag )
       KEY ( -- char )
       EMIT? ( -- flag )
       EMIT ( char -- )
       !USART ( baudfactor -- )
    
*   MaisForth an601
    
    See file an601extra-gb.html for information about non-standard MaisForth words in this text.
    
    MaisForth an601 **starts up with:**
    
    *   Baud rate 19200 (see !USART). While the terminal is sending a file to MaisForth, there should be a **pause of about 10 ms** at the end of each line to make sure that MaisForth is ready to receive the next line.
    *   DECIMAL
    *   FRESH (see FRESH)
    *   5 >OK (see >OK)
    *   HERE = HX 300
    
    **Internal workspace** in MaisForth (HX 000-2FF)
    
    000-07F Dictionary threads, Users, Find Stack  
    080-0FF Terminal Input Buffer  
    100-17F Data Stack, descending  
    180-1FF Return Stack, descending  
    200-27F Circular Buffer for temporary storage  
    280-2FF Compiler Stack, descending
    
    At cold start a test is done to determine the available RAM (see HIMEM). The result is displayed.
    
*   Standard / non-standard words (ANS)
    
    Vocabularies in MaisForth: FORTH ONLY EXTRA INSIDE ASSEMBLER
    
    The **standard words** in FORTH and ONLY are supposed to be known.
    
    The circa 80 **non-standard words** in the EXTRA and ONLY vocabularies are described in file an601extra-gb.html
    
    The **internal auxiliary** words in INSIDE are less important for the average programmer. You may study their definitions in the target code if you want to know what they do.
    
*   Recompiling MaisForth after you altered the target
    
    The metacompiler is supposed to work in a standard 32 bit Forth. (e.g. Win32forth).
    
    *   Put these three files in a directory:   meta601.f   cras601.f   targ601.f
    *   Create a file with the name an601.bin in that directory.
    *   Execute the word -META (erase possible remainders of a previously loaded metacompiler).
    *   Load file meta601.f
    *   Execute the word ROMIMAGE
    
    an601.bin should now contain the new MaisForth ROM image (HX C000-FFFF).
    
*   Decompiling with SEE
    
    This is what SEE does:  
    It walks through memory and looks for addresses where a (16 bit) Forth word is compiled. If found, its name is displayed.
    
    For example, if in both the addresses D08E and D08F a Forth word seems to be compiled, SEE displays both of them. Of course this is impossible and at least one of them must be a random hit. The reader has to decide which one must be ignored. A different indentation of names found at even and odd locations may be of help.
    
       see accept 
       D089: BD   C0   BDC0.   --  ACCEPT  --  doer DO:  --  FORTH Word
       D08A: C0   FF   C0FF  
       D08B: FF   C8   FFC8. 
       D08C: C8    8   C808      SWAP
       D08E: C5   D4   C5D4      FALSE
       D08F: D4   D0   D4D0.         COMPILE,
       D090: D0   23 # D023      ACCEPTING
       D092: C0   7E ~ C07E      EXIT
    
    Define a few little words and try SEE on them, that's probably the fastest way to an understanding of the SEE output.
    
    <>
    
    Words with a name ending in () , (C) or (S) need an **inline argument**:
    
     
    
    inline    
    
    examples
    
    ..()
    
    cell
    
    IF() GOTO() COMPILE() ()    
    
    ..(C)
    
    byte
    
    (C)
    
    ..(S)  
    
    counted string  
    
    ."(S) "(S) ABORT"(S)
    
    This knowledge will help you because SEE only displays **what** is found in memory, not **how** it got there.
    
    Examples:  
    The number 1000 will be compiled as () followed by a cell containing 1000  
    The number 1 will be compiled as (C) followed by a byte containing 1  
    ." Hallo!" compiles ."(S) and then the counted string "Hallo!"  
    AHEAD compiles GOTO() and then the 16 bit destination address.  
    etc.
    
    <>
    
    TO() , +TO() and INCR() are followed by the data address of a normal value or an indirect ROM value.
    
    Example:
    
       see allot 
       CCE2: BD   C0   BDC0    --  ALLOT  --  doer DO:  --  FORTH Word
       CCE3: C0   FF   C0FF. 
       CCE4: FF   C2   FFC2  
       CCE5: C2   E4   C2E4.         +TO()
       CCE7:  0   49 I   49. 
       CCE8: 49 I C0   49C0  
       CCE9: C0   7E ~ C07E.         EXIT
    
    0049 is the data location (RAM) of HERE
    
    RAM addresses of all indirect ROM values:
    
       0023 TOPVOC 
       002B HLD    
       0033 MODE   
       003B IB     
       0043 HIMEM  
    
       0025 TOPMSG  
       002D CONTEXT 
       0035 SECTION 
       003D THERE   
       0045 OK      
    
       0027 TOPPFX 
       002F CS#    
       0037 #TIMES 
       003F HOR    
       0047 DOT?   
    
       0029 TOPNFA 
       0031 MSG#-2 
       0039 #IB    
       0041 VER    
       0049 HERE   
    
    For the Forth programmer these ROM values are constants. The system may alter them, the programmer can do that only implicitly.
    
*   The metacompiler
    
    When metacompiling starts, the metacompiler **is complete**, nothing will be added to it. This is the reason why, while generating the target image, the normal HERE of the host Forth can be used. The target image starts at the first address ending in 000 (hex).
    
    The metacompiler code in file meta601.f is not (yet) very well documented. A few hints:
    
    Text between <---- and ----> is skipped by Forth.
    
    <>
    
    Metacompiling is started with the word :::MAIS:::  
    It has its own QUERY-INTERPRET loop.  
    Metacompiling ends with ;;;MAIS;;; or when an error occurs.
    
    For better understanding, study the word METACOMPILING  
    It does the real work in :::MAIS:::
    
    <>
    
    Target code
    
    Put TRACE and NOTRACE around a piece of code in filetarg601.f and you will see the details of what METACOMPILING does. Press space for wait/continue.
    
    <>
    
    See file an601color.html for colored target code.
    
    A **red** word in the target code is found in the META vocabulary. It will be **executed** during metacompilation. See META-WORDS: followed by a list of these words, in the last part of file meta601.f
    
    A **blue** word in the target code will be **compiled** during metacompilation. It will be looked up (run time) in the target image as far as it is built up at that moment. An error occurs if it is not found.
    
    <>
    
    The metacompiler does not handle forward references, so the target code must be in the natural Forth order.  
    This may seem to be a problem, but see how this problem is solved:
    
    The DOES part of a defining word is defined independently from the CREATE part (e.g. DOCREATE DOVAR DO: DOCON etc.).
    
       DOER: ccc1      <high level Forth code>  ;
       DOERCODE ccc2   <assembler code>         NEXT END-CODE
    
    are functionally equal to
    
       : ccc1 DOES>    <high level Forth code>  ;
       : ccc2 ;CODE    <assembler code>         NEXT END-CODE
    
    *   Example with MET-DOER in CREATE   (Dutch MET = English WITH)
        
        In xCREATE "DOCREATE" is compiled **as a string**.
        
           \\ in metacompiler:
           : xCREATE   ( -- )   xHEADER MET-DOER DOCREATE ;
        
           \\ in target:
           DOERCODE DOCREATE REG X PULS  REG D PSHS  X D TFR NEXT END-CODE
        
        During metacompilation, when xCREATE is executed, it searches the address of DOCREATE and puts it in the CFA.
        
    *   Similar is the action of KOMPILE  
        In xAHEAD "GOTO()" is compiled as a string.
        
           \\ in metacompiler:
           : xAHEAD ( -- AHEADa 11 ) KOMPILE GOTO() HERE 0 x, HX 11 ;
        
        During metacompilation, when xAHEAD is executed, it looks up the address of GOTO() and compiles it.
    
    With these late bindings we can easily avoid forward references.
    
    <>
    
    **x-words**
    
    Some words in the metacompiler are prefixed with an "x" (x: x; xIF etc.). Later on they are redefined in the META vocabulary without that "x". This seems to be some extra work, but definitely makes it easier for the human reader to seize the meaning of metacompiler code.  
    Thus immediate words may appear in four variants, e.g. the semicolon:
    
    *   as ; in the host Forth.
    *   as x; in de metacompiler (harmless, no conflicts while defining metacompiler words).
    *   ; as a redefinition of x; in the META vocabulary. This ; is **active during metacompilation** and closes colon definitions of target words. (red)
    *   ; as a MaisForth definition. It never will be executed during metacompilation! (green)
    
    (an)