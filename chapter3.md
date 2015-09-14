#Interpreter i kompajler
------------------------

Uvod
----

Haskell, kao viši programski jezik, ima jednu zanimljivu stavku kad je u pitanju način na koji
se programi napisani u njemu izvršavaju. Naime, Haskell omogućava i kompajliranje i
interpretaciju programa, tako da se može koristiti istovremeno i kao skripting jezik, kao i
jezik opštije namene. Pored toga, u zavisnosti od implementacije kompajlera koja se koristi,
moguće je i kreiranje Haskell *bytecode*-a.

Implementacija kompajlera
-------------------------

Postoji nekoliko implementacija Haskell-a. Jedna od najpopularnijih je 
[GHC](https://www.haskell.org/ghc/) ili *Glasgow Haskell Compiler*. Glavna prednost GHC-a
je u tome što se putem njega aktivno razvija jezik, kao i mogućnost dodatne optimizacije koja
se postiže njegovim korišćenjem. Jedan od kompajlera koji je takođe popularan, ali pruža i
mogućnost kompilacije u *bytecode* jeste [UHC](https://wiki.haskell.org/UHC) ili *Utrecht
Haskell Compiler*. Još jedan od zanimljivijih primera jeste i 
[LHC](https://github.com/Lemmih/lhc), ili *LLVM Haskell Compiler*, koji koristi mogućnosti
koje pruža [LLVM](http://llvm.org/) platforma. Samim time što određene varijante BSD
operativnih sistema koriste *clang* C kompajler, koji je deo *LLVM* platforme (ona izvršava
*bytecode* generisan od strane *LLVM* kompajlera), moguće je (teoretski) koristiti Haskell
za svrhu sistemskog programiranja na sistemima koji koriste *LLVM* kao platformu za
kompilaciju.

U ostatku knjige se bavimo samo sa *GHC* kompajlerom i njegovom REPL (*read, evaluate, print, 
loop* - skup koraka koji se koriste prilikom interaktivnih interpretatora jezika) 
implementacijom za interpretiranje jezika: `ghci` (skraćeno od *Glasgow Haskell Compiler 
Interactive*).


Interpreter
------------

Kompajler
---------

Zaključak
---------