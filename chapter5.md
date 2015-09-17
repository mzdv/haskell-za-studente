#Kompilacija i još par koncepata
--------------------------------

Uvod
----

Pre par poglavlja sam rekao da ćemo se baviti kompilacijom Haskell programa. Pokazao sam čak
i primer kako se izvršava kompilacija. Da li možemo svaki Haskell program koji interpretiramo
da kompajliramo? **Ne.**

Pre toga moramo da napravimo nekoliko sitnih izmena.

Uzmimo sledeći kod kao primer:
```
Prelude Data.Map> let listaBrojeva = [1,2,3,4,5]
Prelude Data.Map> listaBrojeva
[1,2,3,4,5]
Prelude Data.Map> zip [5,6,7,8,9] listaBrojeva
[(5,1),(6,2),(7,3),(8,4),(9,5)]
```

Ovaj kod koristi funkciju `zip` koja pravi uređene parove između dve liste. I ovaj kod se
interpretira. Ali sad, ako bismo ga kompajlirali, kompajler bi prijavio grešku. Zašto? Zato
što ne postoji ulazna tačka programa - `main` monada.

Main monada
-------------

`main` monada je tipa `IO()` koji je polimorfni tip. Ovo je već rečeno pre. `IO()` tip se tako
zove iz razloga što on omogućava I/O (ulazne / izlazne) operacije za Haskell programe.

Jedna obična `main` monada bi izgledala ovako:
```
main :: IO()
main = putStrLn "Pozdrav svete!"
```

Njenom kompilacijom i izvršavanjem bismo dobili sledeći rezultat:
```
Pozdrav svete!
```

Prosto da ne može prostije. Ali šta ako bismo hteli da imamo više ulaznih ili izlaznih 
funkcija? Koristimo ključnu reč `do` koja spaja sve funkcije unutar njenog bloka u jednu
funkciju (koja je tipa `IO()` što se poklapa sa `main` monadom).

Primer:
```
main :: IO()
main = do
	putStrLn "Pozdrav svete!"
	putStrLn "Pozdrav ponovo!"
	ime <- getLine
	putStrLn ("Zdravo " ++ ime ++ "!")
```

Rezultat:
```
Pozdrav svete!
Pozdrav ponovo!
Zdravo Milos!
```

Sada kada imamo osnove funkcionisanja `main` monade, hajde da naš gornji primer predstavimo
u obliku programa koji se kompajlira.
```
main :: IO()
main = do
	let listaBrojeva = [1,2,3,4,5]
	noviBrojevi <- getLine
	let brojeviInt = map (\x -> read [x]::Int) noviBrojevi
	putStrLn (show(zip brojeviInt listaBrojeva))
```

Izlaz (za ulaz `11111`):
```
[(1,1),(1,2),(1,3),(1,4),(1,5)]
```

Ovde se susrećemo sa novim elementima sintakse. Jedan od njih jeste lambda funkcija, označena
znakom `\`. Ona nam omogućava da na licu mesta definišemo funkciju koja će postojati samo
dok postoji doseg funkcije u kojoj je definisana. U ovom slučaju, ona za svaki element stringa
`noviBrojevi` (pošto je unos u Haskell-u uvek string) vrši kastovanje putem funkcije `read` u
tip podataka `Int`, a potom ga stavlja u novu listu.

Kasnije, putem funkcije `show` pretvaramo rezultat naše funkcije u string kako bi on mogao
da se ispiše na ekran korisnika.

Na ovaj način moguće je prilagodjavati programe po potrebi koji su radili u interpreteru
da bi se kompajlirali radi veće brzine izvršavanja, kao i radi omogućavanja unosa od strane
korisnika.

Monade
------
Šta je zapravo monada? Definicije su razne, ali je najjednostavnija za razumevanje sledeća:

Monada je način da se struktuiraju računanja po pitanju vrednosti i njihovog redosleda.

Iz ovoga se može shvatiti da su monade zapravo grupisanja funkcija koje se mogu koristiti
u daljim računanjima. Pored toga, monade imaju još jednu karakteristiku: funkciju povezivanja
ili `>>=`. Funkcija povezivanja kombinuje monadu tipa a sa računom koji generiše monadu tipa
b na bi se napravila monada tipa b. Može se smatrati kao mixin klasa kada je u pitanju 
objektno-orijentisana paradigma.

Pored toga, monade imaju i `return` funkciju koja vraća vrednost računa unutar monade, tako 
da, u kombinaciji sa funkcijom povezivanja, možemo monade da koristimo u potpunosti.

Postoje različiti tipovi monada. Jedna od njih je `main` monada, koja je zapravo oblik
`IO()` monade. Još jedan primer monade jeste `Maybe` monada koja ili vraća `Nothing` ako
vrednost ne postoji ili vraća `Just vrednost` ako vrednost postoji. `Just vrednost` koristi
jednu od osobina monada, tačnije funkciju identiteta monade: svaka monada mora da implementuje
funkciju kojom se vraća vrednost koju ona generiše.

Ako bismo tretirali monade kao nekakav vid objekata iz objektno orijentisanog programiranja,
mogli bismo da shvatimo da, koristeći monade, mi pretvaramo ulazne podatke, kroz niz funkcija
koje karakterišu jednu monadu, u drugi tip funkcija koje karakterišu drugu monadu sve dok ne
dobijemo izlaz koji generišu željene funkcije. Pored toga, monade imaju svoje posebne osobine
koje nam mogu dodatno pomoći u računu, kao i najrazličitiji tipovi monada koje Haskell pruža.
