Hardware

MaisForth an601 is een 6809 Forth voor het "maiskastje". De woorden die de hardware aanspreken zijn:

   KEY? ( -- vlag )
   KEY ( -- char )
   EMIT? ( -- vlag )
   EMIT ( char -- )
   !USART ( baudfactor -- )

*   MaisForth an601
    
    Raadpleeg file an601extra-nl.html voor de niet-standaard Forth woorden in deze tekst.
    
    MaisForth an601 **start op met:**
    
    *   7F !USART d.w.z. met Baud Rate 19200 (zie !USART). Tijdens het zenden van een file moet de terminal aan het eind van iedere regel **ca. 10 MS wachten** om te voorkomen dat MaisForth het begin van de volgende regel misschien zal missen.
    *   DECIMAL
    *   FRESH (zie FRESH)
    *   5 >OK (zie >OK)
    *   HERE = HX 300
    
    Het interne werkgebied van Forth (0000-02FF):
    
    000-07F Dictionary draden, Users, Find Stack  
    080-0FF Terminal Input Buffer  
    100-17F Data Stack, dalend  
    180-1FF Return Stack, dalend  
    200-27F Circulaire Buffer voor tijdelijke opslag, o.a. strings  
    280-2FF Compiler Stack, dalend
    
    Bij de koude start wordt de beschikbare hoeveelheid RAM vastgesteld (zie HIMEM) en op de terminal gemeld.
    
*   Standaard/niet-standaard woorden (ANS)
    
    Vocabularies in MaisForth: FORTH ONLY EXTRA INSIDE ASSEMBLER
    
    De **standaard woorden** in FORTH en ONLY worden bekend verondersteld.
    
    De ruim 80 **niet-standaard woorden** in EXTRA en ONLY staan beschreven in file an601extra-nl.html
    
    De **interne hulpwoordjes** in INSIDE zullen voor de gemiddelde programmeur niet van belang zijn. Wie er meer over wil weten, kan de target code in file targ601.f bestuderen.
    
*   Hoe maak je een nieuwe ROM image, bijvoorbeeld na veranderingen in de targetcode?
    
    De metacompiler zou moeten werken op iedere standaard 32-bits Forth. (Ik heb o.a. Win32forth gebruikt.)
    
    *   Zet deze drie files in een directory:   meta601.f   cras601.f   targ601.f
    *   Maak een file aan met de naam an601.bin
    *   Voer -META uit (wis eventuele resten van de metacompiler).
    *   Laad file meta601.f
    *   Voer het woord ROMIMAGE uit.
    
    De MaisForth image voor HX C000-FFFF is nu opgeslagen in file an601.bin
    
*   Decompileren met SEE
    
    De decompiler wandelt door het geheugen en kijkt bij ieder adres of er een (16 bit) Forthwoord gecompileerd staat. Zo ja, dan drukt hij de naam af.
    
    Als bijvoorbeeld op D08E en op D08F beide een gecompileerd woord lijkt te staan, laat SEE beide zien, hoewel minstens een van beide een toevalstreffer moet zijn. In zo'n geval worden de namen niet recht onder elkaar afgedrukt. De lezer moet zelf de juiste lezing kiezen.
    
       see accept 
       D089: BD   C0   BDC0.   --  ACCEPT  --  doer DO:  --  FORTH Word
       D08A: C0   FF   C0FF  
       D08B: FF   C8   FFC8. 
       D08C: C8    8   C808      SWAP
       D08E: C5   D4   C5D4      FALSE
       D08F: D4   D0   D4D0.         COMPILE,
       D090: D0   23 # D023      ACCEPTING
       D092: C0   7E ~ C07E      EXIT
    
    De manier om snel de decompiler te leren lezen is: maak zelf een paar kleine woordjes en laat er SEE op los.
    
    
    Woorden met een naam eindigend op () , (C) of (S) hebben een **inline argument**:
    
    naam
    
    inline    
    
    voorbeelden
    
    ..()
    
    cel
    
    IF() GOTO() COMPILE() ()    
    
    ..(C)
    
    byte
    
    (C)
    
    ..(S)  
    
    counted string  
    
    ."(S) "(S) ABORT"(S)
    
    Het is handig dit te weten, want SEE laat zien **wat** er in het geheugen staat en niet **hoe** het daar gekomen is.
    
    Voorbeelden:  
    Het getal 1000 wordt gecompileerd als () gevolgd door een cel met 1000 erin.  
    Het getal 1 wordt gecompileerd als (C) gevolgd door een byte met 1 erin.  
    ." Hallo!" compileert ."(S) met de counted string "Hallo!" erachter.  
    AHEAD compileert GOTO() met daarachter het 16 bits doeladres.  
    enz.
    
    
    Na TO() , +TO() en INCR() volgt het data-adres van een **Value**. Dat kan een gewone Value zijn of een indirecte ROM Value.
    
    Voorbeeld:
    
       see allot 
       CCE2: BD   C0   BDC0    --  ALLOT  --  doer DO:  --  FORTH Word
       CCE3: C0   FF   C0FF. 
       CCE4: FF   C2   FFC2  
       CCE5: C2   E4   C2E4.         +TO()
       CCE7:  0   49 I   49. 
       CCE8: 49 I C0   49C0  
       CCE9: C0   7E ~ C07E.         EXIT
    
    0049 is het data adres (RAM) van HERE
    
    De RAM adressen van alle indirecte ROM values:
    
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
    
    Deze ROM values gedragen zich voor de programmeur als constanten. Het systeem kan hun waarde wijzigen, de programmeur kan dat alleen indirect.
    
*   De metacompiler
    
    Als het metacompileren begint is de metacompiler af, daar komt dus niets meer bij. Daarom kan de target image er gewoon achter komen te staan. De HERE tijdens het metacompileren is de gewone HERE van de host Forth. Voor de overzichtelijkheid laat ik de target image beginnen op het eerst beschikbare adres dat in hex op 000 eindigt.
    
    De metacompiler meta601.f is nog wat rommelig en niet al te uitvoerig gedocumenteerd. Hier volgt een ori�nterende rondleiding met enige hints:
    
    Tekst tussen <---- en ----> wordt door Forth overgeslagen.
    
    
    De metacompiler wordt gestart met :::MAIS::: en heeft zijn eigen QUERY-INTERPRET lus.  
    Hij wordt verlaten met ;;;MAIS;;; of als er een fout optreedt.
    
    **Bestudeer allereerst het woord METACOMPILING** dat de kern van :::MAIS::: is.
    
    
    De Target code
    
    Door TRACE en NOTRACE om een stuk programmatekst in de target code te zetten, is tot in detail te volgen wat daar bij het metacompileren gebeurt. (spatiebalk: wacht/doorgaan)
    
    
    Zie file an601color.html voor de Target code in kleur.
    
    **Rode** woorden in de target code staan in het META vocabulary. Zij zijn **actief** tijdens het metacompileren. Zie META-WORDS: gevolgd door de woordenlijst, bijna aan het eind van file meta601.f
    
    **Blauwe** woorden worden tijdens het metacompileren **gecompileerd**. Ze worden ter plekke opgezocht in de target-image voorzover die tot dan toe opgebouwd is. Er volgt een foutmelding als ze niet kunnen worden gevonden.
    
    
    De metacompiler kent geen voorwaartse referenties, de target code moet dus in de natuurlijke Forth volgorde staan.  
    Dit lijkt misschien een probleem, maar zie hoe dat opgelost is:
    
    Het DOES-deel van een defini�rend woord wordt los van het CREATE-deel gedefinieerd (bijv. DOCREATE DOVAR DO: DOCON enz.).
    
       DOER: ccc1      <high level Forth code>  ;
       DOERCODE ccc2   <assembler code>         NEXT END-CODE
    
    zijn functioneel gelijk aan
    
       : ccc1 DOES>    <high level Forth code>  ;
       : ccc2 ;CODE    <assembler code>         NEXT END-CODE
    
    *   Voorbeeld met MET-DOER in CREATE
        
        In xCREATE wordt "DOCREATE" **als string** gecompileerd.
        
           \\ in metacompiler:
           : xCREATE   ( -- )   xHEADER MET-DOER DOCREATE ;
        
           \\ in target:
           DOERCODE DOCREATE REG X PULS  REG D PSHS  X D TFR NEXT END-CODE
        
        Pas tijdens het metacompileren, als xCREATE wordt uitgevoerd, wordt het adres van "DOCREATE" opgezocht en in het cfa bij de zojuiste gebouwde header gezet.
        
    *   Zo ook KOMPILE
        
        In xAHEAD wordt "GOTO()" als string gecompileerd.
        
           : xAHEAD ( -- AHEADa 11 ) KOMPILE GOTO() HERE 0 x, HX 11 ;
        
        Tijdens het metacompileren, als xAHEAD wordt uitgevoerd, wordt het adres van GOTO() opgezocht en gecompileerd.
    
    Met deze late bindingen zijn we in principe van de voorwaartse referenties af.
    
    <>
    
    **x-woorden**
    
    Woorden in de metacompiler beginnen vaak met een x (x: x; xIF enz.) Zij worden later en masse zonder die x in het META vocabulary herdefinieerd. Deze wat omslachtige werkwijze maakt het voor de lezer veel gemakkelijker om de metacompiler te doorgronden.  
    Zo kennen de immediate woorden vier varianten, bijv. de punt-komma:
    
    *   de ; van de host Forth.
    *   de x; in de metacompiler (voorlopige vorm, die geen verwarring zaait).
    *   de ; als herdefinitie van x; in het META vocabulary. Dit is de ; die bij het metacompileren in actie komt om een nieuw target woord af te sluiten. (rood)
    *   de ; zoals die in de target gedefinieerd wordt, maar die tijdens het metacompileren nooit in actie kan komen! (groen)
    
    (an)