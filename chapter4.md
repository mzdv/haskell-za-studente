#Implementacija modela
----------------------

Uvod
----
U ovom poglavlju se bavimo implementacijom modela. Ići ćemo deo po deo, kao što je definisano
pre dva poglavlja. Koristićemo interpreter WinGHCi.

Avion i hangar
--------------

Da bismo održavali spisak aviona koji se nalaze trenutno u hangaru, koristimo listu
n-torki (u ovom slučaju n-torki od sedam članova - sedmorke) aviona. Neka se lista u kojoj
one nalaze zove `hangar`. On će u početku biti prazna lista, ali će se kasnije popunjavati.

Kod za ovaj deo, gde se inicijalizuje hangar i koristi se primer aviona i dodaje u hangar
se nalazi ispod:
```
let hangarA = []
let avion = ("Antonov","Antonov Airlines","An-225","AN-AAA",[1],15000,1000)
let hangarB = avion:hangarA -- operator : vrši konkatenaciju na početak liste
```

Rezultat:
```
[("Antonov","Antonov Airlines","An-225","AN-AAA",[1],15000,1000)]
```

U rezultatu vidimo da smo uspešno dodali sedmorku u listu hangar. Pored toga, koristili smo
ključnu reč `let` i posle nje naziv funkcije koja predstavlja rekurzivnu listu deklaracija.
Ova funkcija rekurzivno generiše dodeljene vrednosti.

Gornji kod smo mogli da napišemo na drugačiji način, da ne definišemo funkciju generator
`hangarA` koja predstavlja praznu listu, a potom funkciju generator `hangarB` koja služi
da zapravo sadrži novu listu (pošto su strukture podataka u Haskell-u **nepromenljive**,
neophodno je da kreiramo novu funkciju koja generiše listu). Na ovaj način pravimo vid
zavisnih stanja među funkcijama generatorima tako da održavamo perzistentnost podataka
(u realnim sistemima, sistem uopšte ne održava stanje funkcija generatora, nego koristi
eksternu bazu podataka za taj posao).

Na ovaj način omogućavamo dolazak aviona u hangar.

Izlazak aviona iz hangara obavljamo obrnuto od ulaska aviona u hangar:
```
hangarA = drop 1 hangarB
```

Rezultat (vrednost generator funkcije `hangarA`):
```
[] -- prazna lista; hangar je prazan
```

Pored funkcije `drop` koja kao prvi parametar prima broj elemenata koji treba da se izbace
od početka liste, a drugi parametar lista iz koje se izbacuju elementi (potpis joj je
sledeći: `drop :: Int -> [a] -> [a]`), postoje i funkcije `tail` koja vraća prvi element 
i `init` koja vraća listu **bez** prvog elementa.

Unapređenja
-----------

Unapređenja definišemo koristeći strukturu podataka koja se zove **mapa**. Mapa predstavlja uređen par
ključ - vrednost. U našem slučaju, ključ će da predstavlja redni broj unapređenja (onaj isti broj koji
smo stavljali kod aviona), dok će njegova vrednost da bude cena/vrednost unapređenja.

Mape u Haskell-u se prave od listi. Najzanimljivija stvar što se mapa kao mapa **ne pravi**, nego se ona
**generiše** svaki put kada se napravi njen poziv.

Pre nego što krenemo da radimo sa mapama, potrebno je da unesemo opseg u kome se mape nalaze. Početni
opseg karakterističan za svaki GHCi program jeste "Prelude" koji predstavlja osnovne funkcije koje
pruža Haskell.

Rad sa mapama se nalazi u opsegu `Data.Map`. Njegov uvoz vršimo na sledeći način iz GHCi:
```
:m Data.Map
```
Znaćemo da je uvoz bio uspešan onog trenutka kada, pored `Prelude`, bude pisalo `Prelude Data.Map`. Sada
možemo da radimo sa mapama.

Primer rada sa mapama u kontekstu definisanja unapređenja za avione:
```
let unapredjenja = fromList [(1,1000), (2,10000), (3,5000)]
```

Ovako smo kreirali funkciju generator `unapređenja` koja generiše mapu na osnovu unete liste svaki put
kada se pozove.

Sad kada imamo mapu, šta možemo da radimo sa njom? Hajde da odredimo sve ključeve mape:
```
keys unapredjenja
```

Rezultat je:
```
[1,2,3]
```

Ali zar nismo ovo mogli da uradimo putem liste? Što smo uopšte pravili mapu? Ako bismo koristili listu
da izvadimo ključeve, kod bi izgledao ovako:
```
let unapredjenja = [(1,1000), (2,10000), (3,5000)]
map fst unapredjenja --- ako nismo uvezli Data.Map opseg; ako jesmo, map zameniti sa Prelude.map
```

Rezultat:
```
[1,2,3]
```

Iako je izvodljivo, u startu gubimo jednostavnost koda: potrebno je da izvršimo funkciju mapiranja `map`
(koja nema veze sa mapama od malopre, pošto ona vrši transformaciju jedne listu u drugu) nad prvim 
elementima (oznaka `fst` vraća prvi element iz uređenog para) iz liste `unapredjenja` (naravno, rekurzivno
na isti način kao što je opisano u prethodnim poglavljima - kreiranjem funkcije `1:2:3:[]`).

Koncept kada se više operacija može koristiti radi dolaska do istog rešenja (bile one međusobno
jednostavnije ili teže za razumevanja) se zove **sintaktički šećer** (*syntactic sugar*).

Naručilac
---------

Izveštaji i statistika
----------------------

Zaključak
---------