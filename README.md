## forth-codes

A library of Forth applications to build knowledge of it

## Baseline code

* Using [gforth](https://gforth.org/) as the base currently

## What this is about

To start the design process for an intuitive program that I have been contemplating for some years that exists in several guises.

### table of contents

* [hello](/first-design/README.md) world application
* [m6809](/mf6x09/an601/README.md) project for [M6x09-II-SBC](https://github.com/cartheur/M6x09-II-SBC)

### here are the words in here

```
thread-key prep-key keypollfds UDefer udefer-to kill event-block sleep halt wake restart (restart) 
thread-deadline pause event-loop stop-dns stop-ns stop ?events event? send-event (stop) execute-task 
stacksize4 stacksize >pagealign-stack c-section critical-section unlock lock cond sema semaphore 
initiate pass (pass) activate (activate) task newtask newtask4 thread-init 's user' wake# epipew 
epiper pthread-id compsem: intsem: set-compsem to-errno errno-table fork+exec fpid fork() getpid 
fd>file int-errno-exec saved-errno ?ior ?errno-throw errno-throw fds[]! fds!+ LC_IDENTIFICATION 
LC_MEASUREMENT LC_TELEPHONE LC_ADDRESS LC_NAME LC_PAPER LC_ALL LC_MESSAGES LC_MONETARY LC_COLLATE 
LC_TIME LC_NUMERIC LC_CTYPE POLLHUP POLLOUT POLLPRI POLLIN revents events fd pollfd pagesize environ 
unsetenv setenv getrandom getentropy strlen getcwd mkstemp mknod rmdir readlink link symlink exit() 
execvp (fork) (getpid) setlocale close write read open ioctl2 ioctl fcntl freopen fdopen posix_spawnp 
epoll_wait epoll_ctl epoll_create ppoll poll fileno getpagesize ->errno FIONBIO FIONREAD errno 
pthread-conds pthread-mutexes pthreads pthread-cond+ pthread-mutex+ pthread+ pthread_cond_t 
pthread_mutex_t pthread_t pthread_self stick-to-core wait_read check_read create_pipe 
pthread_cond_timedwait pthread_cond_wait pthread_cond_broadcast pthread_cond_signal 
pthread_cond_destroy pthread_cond_init pthread_detach_attr sched_yield pthread_mutex_unlock 
pthread_mutex_lock pthread_mutex_destroy pthread_mutex_init pthread_cancel pthread_kill pthread_exit 
pthread_create gforth_create_thread thread_start disasm disline disassembler rec-meta 
scope-search-prefix ?search-prefix in-wordlist in rec-scope scope-split nosplit? rec-env rectype-env 
translate-env env$, rec-complex translate-complex zliteral z.s z. fc. zacot zatan zacos zasin pi/2 
zacoth zatanh zacosh zasinh Im Re Imag Real ztan zcos zsin ztanh zcosh zsinh zfib phi z** zsqrt z0= 
zln pln zexp polar> >polar z2* z2/ zabs |z| z/ 1/z zsqabs z/i z*i zconj znegate zscale z* x- x+ zr- 
z- z+ ZVarue za-to ZValue z-to ZVariable some-zalocal some-zlocal compile-z@local compile-pushlocal-z 
to-za: to-z: z!a-table z!-table z+! z! z@ z-rot zrot zdepth zpick zswap zr> z>r zover zdrop zdup fl> 
complex+ complex' &of addr default-w: default-wa: to-fa: to-ca: to-da: to-xta: to-wa: fvarue 
dummy-fvarue fvarue-to 2varue dummy-2varue 2varue-to Varue dummy-varue varue-to f!a-table c!a-table 
2!a-table defera-table !a-table marker marker! marker, sections-marker! sections-marker, 
included-files-mark .unresolved auto-resolve is-forward? forward unfixed-forward 
unresolved-forward-error forward-needs-: unresolved-forward fancy-after-l whereg delete-whereg 
whereg-filename s` sh-get sh$ plain-output plain-out plain-form help help-section help-word open-doc 
set-help-view count-lfs doc-file# unused-words unused-wordlist unused@ unmark-used unused-all -unused 
+unused .wids unused-mask usage# browse (browse) browse-results bw nw ww where-</> where-index-- 
where-index++ (ww) where prepend-where expand-where short-where where-reset where-setup (where) 
forwheres .whereview1 .whereline .wheretype1 width-type type-notabs unbounds bt nt tt bt-</> 
backtrace-- backtrace++ backtrace# bt-location gg g-once ll l-once next-l|g l|g edit g extern-g b n 
view locate .rec'-stack locate-name name-set-located-view l l1 no-</> index-- index++ after-l 
append-locate-lines prepend-locate-lines display-locate-lines located-erase l2 print-locate-header 
view>filename current-location? current-location?1 located-buffer locate-print-line locate-type 
located-diff locate-lines+ locate-lines# type-prefix locate-next-line locate-line set-bn-view 
view>buffer included-buffer included-file-buffers backtrace-index where-index where-results -status 
+status .status-line status-xts .order .stacks .base wide? replace-char .unstatus-line redraw-status 
status-attr status-offset mwords wordlist-mwords .mwords[] wid>words[] mword-filename-match 
mword-search-match mword-match words[] le-uxd@ le-ux@ le-ul@ le-uw@ be-uxd@ be-ux@ be-ul@ be-uw@ 
le-xd! le-x! le-l! le-w! be-xd! be-x! be-l! be-w! sxd@ sx@ sl@ sw@ uxd@ ux@ ul@ uw@ find sfind word 
sword +place place (word) .strings name parse-word comp: definer! [(')] lastxt longstring, header, 
obsoletes scroll-down scroll-up cursor-previous-line cursor-next-line erase-display insert-lines 
cursor-down cursor-up control-sequence: restore-cursor-position save-cursor-position 
(control-sequence) auto-color magenta-input dark-mode light-mode uncolored-mode default-bg rgb-split 
term-bg? term-fg? term-color? term-rgb@ is-xterm? is-color-terminal? is-terminal? term-rgb$ <<<m m>>> 
mark-attr BlackSpace (theme-color!) white? theme-color@ theme: current-theme (Attr!) Attr A> <A FG> 
BG> >FG >BG Dim Invisible Italic Strikethrough Invers Blink Underline Bold defaultcolor White Cyan 
Magenta Blue Yellow Green Red Black load-rc0 load-rc load-rc? disasm-gdb 0x. ppid 
append-extend-string >string-execute >string-out >string-form >string-cr >string-emit >string-type 
>string-len >string-buffer >string-initial-buflen end-c-library c++-library c-library reopen-libs 
.libs map-libs prefetch-lib c-lib host? get-host? clear-libs add-lib c-function \c !!0.7-style!! 
basename dirname scan-back break" break: break:, dbg dbg-ip see-code xt-see-code see-code-range 
simple-see xt-simple-see simple-see-range .backtrace-view .sourceview-width .bt print-backtrace 
print-bt-entry .backtrace-pos >bt-entry backtrace-return-stack extra-backtrace# see name-see 
(.compile-only) (.immediate) (xt-see-xt) xt-see discode see-voc end-code ;abi-code !;abi-code ;code 
(;code) code-address! abi-code code init-asm assembler subst>filename $unescape unescape substitute 
$substitute .substitute .% replacer: warn-hardcoded replaces macro: $Value $value-to $!-table 
macros-wordlist rec-body rec-dtick rec-tick ?rec-nt rec-to rectype-to translate-to post-to, 
rec-string rectype-string translate-string slit, vt100-page vt100-at-deltaxy vt100-at-xy #esc[ #n; #n 
.\" s\" \"-parse \-escape, \-escape-table parse-num parse-num-x char/ history-cold get-history 
xchar-history xins xchar-edit-ctrl std-ekeys xchar-ctrlkeys xdelw xchar-altkey altbindkey 
xchar-altkeys xreformat setsel setcur xchars>chars xback-chars setsel# setcur# xtranspose xpaste 
xpaste@ xtab-expand (xtab-expand) xkill-expand xeof' (xenter) xins-string xclear-first xclear-rest 
xpaste! xend-pos xfirst-pos xeof <xdel> ?xdel xdel (xdel) xforw xback (xins) xgrow-tib xhide 
xedit-update .rest .all-rest .all .resizeline get-width+all get-width+ hw>width get-hw xedit-startpos 
setstring-color kill-prefix tib-full? simple-search-prefix search-prefix prefix-string prefix-off 
search-voc word-lex alphabetic-tab prefix-found extract-word (enter) write-history lastline<> 
thisline# lastline# prev-line find-prev-line next-line get-line hist-setpos hist-pos xretype 
clear-line edit-curpos-off history-file force-open -scan vt100-modifier end^ backward^ forward^ 
history ctrl ctrl-i ebindkey bindkey >edit-rest edit-terminal-c edit-terminal paste$ setstring$ 
screenw edit-curpos ekeys edit-error grow-tib paste@ paste! mkdir-parents file-exist# EEXIST uclass 
uvar umethod uval-o user-o class-o ekey? ekey>fkey ekey>xchar ekey>char ekey xkey? get-xkey read-xkey 
esc-sequence esc-prefix clear-ekey-buffer esc-mask ekey-buffer esc-sequences buf-key? inskeys inskey 
unkeys unkey buf-key inskey@ char-append-buffer key-buffer s-k12 s-k11 s-k10 s-k9 s-k8 s-k7 s-k6 s-k5 
s-k4 s-k3 s-k2 s-k1 k12 k11 k10 k9 k8 k7 k6 k5 k4 k3 k2 k1 k-eof k-sel k-tab k-backspace k-voldown 
k-volup k-mute k-pause k-winch k-f12 k-f11 k-f10 k-f9 k-f8 k-f7 k-f6 k-f5 k-f4 k-f3 k-f2 k-f1 k-enter 
k-delete k-insert k-next k-prior k-end k-home k-down k-up k-right k-left fkey. simple-fkey-string 
k-ctrl-mask k-alt-mask k-shift-mask mask-shift# keycode keycode-table keycode-limit keycode-start 
voctable cs-vocabulary cs-wordlist table cs-wordlist-search-map tablesearch-map table-rec table-find 
savesystem dump-fi preamble-start prepare-for-dump 'clean-maintask update-maintask 
update-image-included-files repl-included-files del-included-files block-included --> +thru +load 
thru load block-input list updated? scr buffer block get-buffer flush empty-buffers save-buffers 
empty-buffer save-buffer update block-position get-block-fid use open-blocks flush-blocks block-cold 
offset block-offset block-fid block-limit buffers last-block block-buffers buffer-struct next-buffer 
block-buffer buffer-dirty buffer-fid buffer-block ... wrap-xt smart.s. smart<> .s.smart .s.string 
.s.cs .s.skip .string. .string.( smart. .cs. .var. .addr. cs? string? .var? addr? smart.s-skip 
.elapsed timer-reset .!time !@time .time (.time) @time !time .times init-timer map-timer timer: 
timer-list +t last-tick timer-tick profile( +debug set-debug +-? debug-eval ~db -db +db )else( debug: 
debug-doer assert( assert3( assert2( assert1( assert0( ) assertn assert-canary assert) (end-assert) 
assert-level level-check .hm .name? color-prompt prompt-text prompt-ok #loc edit-file-cmd editor-cmd 
vi-l:c emacs-l:c kate-l:c view' (view') rec'@ rec'[] type-prefix esc'type -ltrace +ltrace line-tracer 
~~Value ~~value-to ~~>body ~~Variable watch-opt: watch-does> replace-word >prim-code >colon-body 
?warn-dp warning-recs shadow-num-warning shadow-warning !!FIXME!! FIXME# WTF?? dbg-shell ??? ???-loop 
~~1bt ~~bt once ]nocov nocov[ cov-stack coverage? ~~ .debugline-directed (.debugline) .debugline 
printdebugdata #line save-source-filename# .sourcepos compile-sourcepos .sourceview .sourcepos3 
view>char decode-view decode-pos loadfilename#>str prepend~~ expand~~ short~~ plain~~ source-pos# 
source-line# prepend-file expand-file shorten-file lastfile filename>display *terminal*# utf-8-cold 
set-encoding-utf-8 utf-8 x-maxlines x-maxlines+rest x-lines x-lines+rest +x-lines+rest xc-hw+ u8width 
xc-width+ xc-width -u8trailing-garbage u8addrlen u8!+? u8@ u8\string- +u8/string u8emit u8key 
check-xy u8<< u8>> u8!+ u8@+ u8len max-single-byte UTF-8-err WordInfo InfoTable Com-color Str-color 
Ali-color Use-color Col-color Def-color Doe-color Val-color Var-color Con-color Pri-color prim? 
xtprim? colon? defered? does? user? value? con? var? .recognizers .recognizer-sequence prim>name 
>head @threaded>name threaded>name >name look PrimStart @threaded>xt threaded>xt xt= [f:h [d:h [n:h 
[f:d [d:d [n:d [f:l [d:l [n:l [f: [d: [n: [*:: :d :h :l (;]xt) alloc-by-xt, (;]l) (;]*) ;> <{: [{: 
end-dclosure closure> free-closure closure-:-hook (closure-;]) wrap-closure dummy-local, pop-locals 
push-locals extra-locals lp> >lp allocd alloch >addr 1t-closure? endref, end-d locals-lists 
locals-sizes opt-u/mod opt-/modf opt-umod opt-modf opt-u/ opt-/f lit/, /f-stage1m u/-stage1m 
staged/-size staged/-divisor staged/-inverse-hi staged/-shift staged/-inverse dffield: sffield: 
ffield: 2field: field: xfield: lfield: wfield: cfield: end-structure begin-structure extend-structure 
standard:field +field sizeof [sizeof] (sizeof) standard+field .sections opt@ opt-array>mem opt* opt+- 
(+loop)-optimizer replace-(+loop) fold4-4 fold4-2 fold4-1 fold3-3 fold3-2 fold3-1 fold2-3 fold2-2 
fold2-1 fold2-0 fold1-2 fold1-1 fold1-0 folds optimizes fold-constants >4lits 4lits> >3lits 3lits> 
>2lits 2lits> [WHILE] [AGAIN] [REPEAT] [UNTIL] [BEGIN] [I] comp-[i] INT-[I] [NEXT] [FOR] [LOOP] 
[+LOOP] [?DO] [DO] input< input-drop >input loop-indices input-stack (i) $[]free $[]. $[]map 
$[]slurp-file $[]slurp $slurp-line $slurp-file $+slurp-file $slurp $+slurp $tmp $. $exec $-out $form 
$cr $emit $type $execstr-ptr tmp$ tmps# tmp$# tmp$[] $+[]! $[]@ $[]# $[]+! $[]! $off $over rpick 
open-warp time&date (xparse) string-parse [char] char append s+ traverse-matched-dir traverse-dir 
try-read-dir adjust-buffer init-buffer buffer% buffer-maxlength buffer-address buffer-length 
buffer-descriptor rectype-word translate-word basic-help 2Value dummy-2value 2value-to 
2value-compile, name>comp name>int nr> n>r \\\ th dump hex.r hex. h. dec. base-execute 
derived-output: derived-input: execute-theme-color theme-color infile-execute outfile-execute 
xaligned xalign laligned lalign waligned walign *align *aligned xd, x, l, w, xd>s x>s xdle xle lle 
wle xdbe xbe lbe wbe noop0 /x /l /w typewhite what's action-of preserve f.s f.s-precision f.rdp 
f>str-rdp f>buf-rdp f>buf-rdp-try push-right mem+do mem-do u-[do -[do general-mem+loop const-mem+loop 
array>mem mem*do-noconstant ]] rec-[[ rectype-[[ translate-[[ try-recognize try-free +after -stack 
set-recognizers get-recognizers forth-recognizer set-recognizer-sequence get-recognizer-sequence 
>rec-stack defers@ rectype-dnum rectype-num rectype-nt rectype-null rectype: rectype rectype>post 
rectype>comp rectype>int file>fpath file>path slurp-fid slurp-file const-does> (const-does>) 
in-colon-def? compile-fliterals compile-literals in-return-stack? ]L sh system $? ctz pow2? dmax dmin 
?CSP !CSP CSP needs save-mem-dict translate-state >compile >interpret translate-method: 
translate-method-to >translate-method translator-overflow translator-max-offset# translator-offset 
locals| >definer noname-w: (local) (exit-like) (until-like) (again-like) (begin-like) (then-like) 
locals-;-hook locals-:-hook {: { new-locals new-locals-rec some-waddr some-xtlocal some-wlocal 
some-flocal some-dlocal some-clocal locals-types val-part-off to-f: to-c: to-d: to-xt: to-w: laddr, 
c!-table 2!-table 2+! c+! laddr#, lp-offset create-local locals-where, locals-headers create-local1 
locals-name-size+ check-begin set-locals-size-list locals-list! list-size sub-list? common-list /list 
list-length compile-pushlocal-[ compile-pushlocal-c compile-pushlocal-d 2>l compile-pushlocal-f 
compile-pushlocal-w locals, val-part maxalign-lp alignlp-f alignlp-w deactivate-locals 
activate-locals rec-locals locals-rec translate-locals locals-post, no-post locals adjust-locals-size 
compile-lp+! compile-f@local compile-@local locals-size next-case endcase closecase contof endof of 
?of case case-depth expect span capssearch capsstring-prefix? search blank convert [compile] C" m*/ 
d>s .( frem ftrunc fmod fcopysign fsign-offset f~ f~rel f~abs NaN -inf -infinity inf infinity 1/f f2/ 
f2* pi fvariable rec-float rectype-float translate-float >postponer fp. prefix-number zero-exp 
si-prefixes sfnumber fs. fe. f. f$ -zeros zeros scratch set-precision precision fclearstack fdepth 
fvalue dummy-fvalue fvalue-to f!-table f+! fconstant opt-fcon opt-fval FLiteral flit, f, dfloat+ 
sfloat+ dfalign sfalign dump-sections extra-section >extra-sections #>section section# lits<> 
new-section create-section which-section? sections-execute section-execute set-section 
extra-section-error first-section-error image-offset section-defaultsize #extra-sections sections 
.words hash-cold make-hash hash-wordlist hashdouble (rehash) rehashall clearhash addall inithash 
tablevoc-to hashvoc-to tablevoc-table hashvoc-table table-reveal hash-reveal (reveal lastlink! 
hash-rec hash-find bucket NewFix DelFix hash-alloc hashsearch-map HashTable HashPop HashIndex 
HashPointer revealed insRule hash erase Hashlen hashbits reserve-mem to: interpret/compile: 
>to+addr-table: to-table: to-method: never-happens warning-error broken-pipe-error exceptions 
exception next-exception errstring linked minos? glx? gles? getrandom? getentropy? 
include-ffi.h-string libffi-present ffcall-present libtool-flags libtool-cxx libtool-cc 
libtool-command machine lib-suffix has? $has? e? environment? environment-wordlist environment 
version-string>internal (0s) process-voc-option options image-options vocs map-vocs order .voc .name 
.id id. seal set-order get-order Only Root Forth previous also >order >voc >wordlist Vocabulary 
wordlist mappedwordlist wordlist-class set-wordlist wl, slowvoc definitions set-current back> >back 
search-order %alloc %allocate %allot %align %size %alignment double% sfloat% dfloat% float% char% 
cell% struct end-struct field create-field field, nalign naligned default-recognize 
recognizer-sequence: recognize trace-recognizer set-current-view set-located-view view>line 
view>filename# after-locate before-locate located-slurped located-bottom located-top bn-view 
located-len located-view kill-task catch-frame endtry-iferror endtry restore iferror try nothrow 
stored-backtrace store-backtrace resize free allocate current-memory-words heap-words do;abicode, 
doabicode, dodoes: dofield, dodefer, douser, dovar, docol, dovalue, docon, do;abicode: 
(;abi-code-dummy) doabicode: (abi-code-dummy) dodoes: (does-dummy) dofield: dodefer: douser: dovar: 
docol: dovalue: docon: vlist words wordlist-words .word word-colorize traverse-wordlist map-wordlist 
cols rows ? dump .line .chars .4 /dump .s maxdepth-.s .s. [ENDIF] [THEN] [ELSE] [IFUNDEF] [IFDEF] 
[IF] scanif [undefined] defined [defined] scanning? ?if scanif-r [struct]-voc [struct]-search 
scan-rec dummy endif? countif ." s" warning" abort" SLiteral CLiteral previous-section next-section 
;inline inline: ;] [: comp-[: int-[: (;]) (int-;]) wrap! wrap@ wrap!-kernel wrap@-kernel endscope 
adjust-locals-list scope execute-exit ?EXIT EXIT exit-like NEXT S+LOOP -LOOP +LOOP LOOP loop-like FOR 
U-DO -DO U+DO +DO ?DO ?do-like DO ?LEAVE LEAVE DONE leave> >leave leave-empty? clear-leave-stack 
leave-stack CONTINUE REPEAT WHILE UNTIL until-like AGAIN again-like BEGIN begin-like ELSE ENDIF THEN 
cs>addr then-like ?DUP-0=-IF ?DUP-IF IF AHEAD NOPE YET BUT <resolve >resolve >mark? >mark ?colon-sys 
?struc if-like other-control-flow cs-push-orig cs-push-part CS-DROP CS-ROLL CS-PICK cs-item-size 
cs-item? non-orig? scope? do-dest? dest? orig? scopestart do-dest dest dead-orig live-orig 
pop-stack-state pop-stack-state1 push-stack-state push-stack-state1 after-cs-pop before-cs-push 
cs-depth1-- cs-depth1++ update-backedge-locals-default ASSUME-LIVE UNREACHABLE ;-hook21 :-hook1 
cs-floor cs-depth1 backedge-locals-default backedge-locals dead-code locals-list .included require 
include required included >include-auto-extension include-auto-extension-filename >include >included 
included1 add-included-file included? str>loadfilename# sourceline# included-filename[] 
sourcefilename included-files open-fpath-file open-path-file execute-path-file open-ofile reworkdir 
compact-filename skip-..-prefixes preserve-root del-./s del-string expandtopic remove~+ extractpath 
need/ pathsep? absolute-file? .fpath .path next-path path>string fpath= path= substc fpath+ path+ 
only-path clear-path also-path os-cold clear-paths tfile ofile fpath 'image save-strings boot-strings 
$[]Variable $Variable $[]saved $saved boot[][] boot$[] $[]save $[]boot $save $boot $bit@ $-bit $+bit 
$bit $[] $room $iter $split $init $del $ins c$+! $+! $+!len $@ $! $!len $@len $make $!buf $free 
$padding insert delete ( write-line +fmode bin r/o r/w w/o os-boot (process-args) process-option 
(process-option) args-evaluate args-required args-required1 os-execute-parsing next-arg shift-args 
clear-args script? argc argv pathdirs pathstring #! arg cstring>sstring set-encoding-fixed-width 
set-encoding fixed-width ca-size c-size c@+? invalid-char c!+? c!+ string- +string char- xc, xhold 
x@+/string xc@+? -trailing-garbage x-width x-size xc-size xc@+ xc!+? xc!+ xc@ x\string- +x/string 
xchar- xchar+ xkey xemit xc-vector authors license include-file execute-parsing-file 
execute-parsing-named-file ?set-current-view get-input-colored get-input read-loop read-loop1 
line-end-hook query clear-tibstack evaluate execute-parsing execute-parsing-wrapper create-input 
restore-input save-input pop-file push-file expand-tib new-tib file-input read-line evaluate-input 
terminal-input .unstatus .scanning input-start-line input-lexeme! accept edit-line edit-key decode 
>control kernel-editor (edit-everyline) (edit-update) std-ctrlkeys (edit-control) (ret) (bs) 
(ins-string) (ins) edit-linew altkeys ctrlkeys edit-update everyline everychar edit-control 
insert-string insert-char edit-out recursive voc-to voc-table reveal (reveal) (nocheck-reveal) 
i/c>comp does> int-does> int-does>; comp-does> comp-does>; concat ; :noname dummy-noname : :start 
colon-sys defstart colon-sys-xt-offset 0-adjust-locals-size ;-hook2 ;-hook :-hook +TO [+TO] <+TO> IS 
[IS] <IS> TO defer-is value-to reveal-method reveal! defer! to-opt: ?fold-to (to), opt!-compile, opt: 
int-opt; set-name>link set-name>string set->comp set->int set-to set-does> does-code! set-execute 
set-optimizer general-compile, !namehm ?hm make-latest hm, (hm,) hm= hmrestore hmsave hmcopy, hmcopy 
hm-activate hmtemplate does>-like Defers Defer defer-default (Field) to-table-size# AValue Value 
AConstant Constant (Value) (Constant) AUser User uallot 2Variable AVariable Variable buffer: Create 
synonym? Synonym synonym-mask alias? Alias synonym, s-compile, s-to s>comp s>int a>comp a>int 
obsolete compile-only restrict immediate imm>comp lastflags or! ," postpone ] [ set-forth-recognize 
forth-recognize minimal-recognize stack# stack> >stack stack do-stack: stack: set-stack get-stack 
rec-num nt>rec translate-nt? translate-dnum translate-num translate-nt name-compsem >postpone 
translate: do-rec 2lit, lit, postpone, [COMP'] COMP' ['] default-i/c default-name>comp flush-code 
peephole-compile, prim-check name>view addr>view xt-location1 xt-location bt-pos-width lump-compile 
basic-block-end cfa, clear-litstack lits, lits# lits> >lits litstack ?parse-name ALiteral 2Literal 
Literal latest latestxt latestnt noname noname-header nextname nextname-header nextname$ input-stream 
input-stream-header noname-from create-from header header-extra header-name, record-name noname, 
?noname-hm named-hm noname-hm namehm, 0name, name, lastnt recurse check-shadow current-view 
current-sourceview replace-sourceview encode-view current-sourcepos3 encode-pos get-current string, 
mem, const A, cfalign maxalign falign align >align 2, c, small-allot allot hm-list is-umethod (uv) 
uvar, umethod, does, ;abi-code, abi-code, field+, defer, user, variable, :, constant, value, 
does-check call-check kernel-bye bye boot xt, cold 'cold process-args bootmessage gforth (c) do-find 
do-execute quit (DoError) rec-level reset-dpp .error-frame (.error-level) .error-level .error-line 
part-type mark-end mark-start .error-string dobacktrace DOERROR -trailing dec.r input-error-data 
>error error> error-stack /error (quit) (quit1) (prompt) prompt .status 'quit extend-mem free-mem-var 
save-mem interpret2 bt-rp0-wrapper bt-rp0-catch interpret int-execute before-line before-word 
parse-name ' (') '-error any-code! only-code-address! >does-code xt>name >code-address body> >body 
>head-noprim xt? hm? ??? (name>intn) noname>link noname>string named>link named>string name?int 
?obsolete obsolete? ?compile-only compile-only? immediate? , compile, >extra initwl defer@ hmsize 
name>link name>string name>compile name>interpret (to) opt-compile, >namehm >cfa >link >f+c >hm>link 
>hm>string >hm>comp >hm>int >hmextra >hmto >hmcompile, >hmlink ((name>)) (x>int) compile-only-error 
ticking-compile-only-error flag-sign lcount-mask obsolete-mask restrict-mask find-name rec-nt 
search-wordlist find-name-in notfound no.extensions (where,) where, where-struct where-loc where-nt 
wheres context voclink current f83search forth-wordlist rec-f83 wordlist-struct wordlist-extend 
wordlist-link wordlist-id wordlist-map wordlist-exec wordlist-start \G \ ( number (number?) snumber? 
s>number s>number? s>unumber? ?warn# s'>unumber? ?dnegate sign? getbase bases name-too-long? 
name-too-short? (name) parse (parse) version-string .error error$ errlink>string do-debug >stderr 
>exec c(warning") .warning ErrRanges ErrLink u. . ud. d. u.r .r ud.r d.r holds #s # sign #>> <<# #> 
<# hold +hold pad ms ns kernel-deadline deadline backspaces spaces spaces-loop status-color 
error-hl-inv error-hl-ul input-color success-color info-color warning-color error-color default-color 
theme-color: theme-color# theme-to theme-table theme@ theme! space bell #lf #ff #cr #del #esc #tab 
#bs #bell #eof output: input: default-in debug-vector debug-out default-out key (cr) key? key-ior 
ip-vector theme-color! control-sequence attr! at-deltaxy at-xy page form cr emit type op-vector 
(key?) (key) key-file EBADF EINTR EOK (err-emit) (err-type) (emit) (type) out debug-fid outfile-id 
infile-id hex decimal "lit clearstacks clearstack depth ?stack abort ?warning (abort") c(abort") 
throw catch ud/mod s>d >number_ >number accumulate digit? stick roll dabs off on ->here here dpp 
in-dictionary1? in-dictionary? unused usable-dictionary-end usable-dictionary-end1 dictionary-end 
section-desc codestart targets primbits locs[] section-name section-dp section-size section-start 
current-section A! chars cfaligned maxaligned NIL str< string-suffix? string-prefix? str= no-to >comp 
tib+ tib loadfilename# #fill-bytes blk loadfile loadline old-input max#tib #tib new-where 
input-lexeme >in (restore-input) (save-input) source-id refill source current-input warnings Last dp 
state >num-state dpl base holdend holdptr holdbuf-end holdbuf holdbufptr "error errorhandler 
backtrace-rp0 wraphandler first-throw handler throw-entry lp0 fp0 rp0 sp0 save-task prev-task 
next-task udp main-task def#tib pad-minsize word-pno-size chars/block l/s c/l /line bl float false 
true 2Constant 2constant, UValue (UValue) u-compile, uvalue-to to:, to:exec >uvalue defer-table 
!-table warn! oam-warning [noop] n/a cell */ */mod /mod mod / r@ forthstart image-header up@ o u#+ 
u#exec x#exec o#exec o> >o lit-execute ;abi-code-exec abi-call compile-prims finish-code| tag-offsets 
@decompile-prim decompile-prim3 forget-dyncode3 finish-code compile-prim1 barrier ?!@ +!@ !@ u8@+? 
log2 >pow2 l>s w>s c>s xd>< x>< l>< w>< xd@ xd! x@ x! close-lib2 close-lib lib-error l! l@ w! w@ 
wcall lib-sym2 lib-sym open-lib2 open-lib ffourth fthird fpick f>l >l lp! lp+2 lp+ lp- lp+! lp@ 
f@localn @local3 @local2 @local1 @local0 @localn flit1 flit0 flit f-rot sfloat/ dfloat/ float/ 
>float1 faxpy v* dfaligned sfaligned dfloats sfloats fatanh facosh fasinh ftanh fcosh fsinh ftan 
fsqrt fsincos fsin falog flog flnp1 fln fexpm1 fexp fcos fatan2 fatan fasin facos fabs >float 
represent fmin fmax fround floor floats float+ ftuck fnip frot fover fswap fdup fdrop fnegate f**2 
fm*/ fm/ fm* f** f/ f* f- f+ sf! sf@ df! df@ f@ f! f>s f>d d>f s>f f0>= f0<= f0> f0< f0<> f0= f>= f<= 
f> f< f<> f= (ns) ntime cputime utime newline =mkdir get-dir set-dir filename-match close-dir 
read-dir open-dir file-eof? file-status flush-file emit-file write-file (read-line) read-file 
resize-file file-size reposition-file file-position rename-file delete-file create-file open-file 
close-file winch? gforth-pointers call-c@ call-c# call-c strsignal strerror heap-resize heap-free 
heap-allocate (ms) >time&date&tz close-pipe open-pipe getenv (system) (bye) flush-icache wcwidth isfg 
isatty (form) term-prep? stderr stdout stdin key?-file (key-file) debugging-method threading-method 
faligned aligned skip scan (parse-white) hashkey2 (hashkey2) (hashkey1) (tablelfind) (hashlfind) 
(listlfind) inc# cell- cell/ count char+ cells cell+ 2@ 2! c! c@ +! ! lit@ @ sps@ 2tuck 2nip 2rot 
2swap 2over 2dup 2drop fourth third pick ?dup tuck nip -rot rot dup swap drop over 2rdrop 2r@ 2r> 2>r 
rdrop r> >r fp! fp@ rp! rp@ sp! sp@ up! within du>= du<= du> du< du<> du= d0>= d0<= d0> d0< d0<> d0= 
d>= d<= d> d< d<> d= u>= u<= u> u< u<> u= >= <= > < <> = 0>= 0<= 0> 0< 0<> 0= darshift arshift u*/ 
u*/mod u/mod umod u/ du/mod dror drol lror lrol wror wrol ror rol drshift dlshift select mux umin 
umax lshift rshift invert xor or and d2/ d2* dnegate d- d+ m+ /modf-stage2m modf-stage2m /f-stage2m 
u/mod-stage2m umod-stage2m u/-stage2m um/mod um* m* sm/rem fm/mod 2/ 2* */s */mods /mods mods /s */f 
*/modf /modf modf /f * abs min max 1- 1+ negate - under+ lit+ + lit safe/string /string capscompare 
toupper compare fill cmove> cmove move rpick# r'@ delta-i bounds k j i' i fast-throw uncatch (try) 
(u-[do) (-[do) (u-do) (-do) (u+do) (+do) (?do) (do) (for) (s+loop)-lp+!# (s+loop) (/loop)#-lp+!# 
(/loop)# (-loop)-lp+!# (-loop) (+loop)-lp+!# (+loop) (loop)-lp+!# (loop) (next)-lp+!# (next) 
?dup-0=-?branch ?dup-?branch ?branch-lp+!# ?branch branch branch-lp+!# does-xt lit-perform unloop 
execute-;s ;s perform execute call noop23 noop22 noop21 noop20 noop19 noop18 noop17 noop16 noop15 
noop14 noop13 noop12 noop11 noop10 noop9 noop8 noop7 noop6 noop5 noop4 noop3 noop2 noop
```