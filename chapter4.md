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
let avion = ("Antonov","Antonov Airlines","An-225","AN-AAA",(1, 1000),15000,1000)
let hangarB = avion:hangarA -- operator : vrši konkatenaciju na početak liste
```

Rezultat:
```
[("Antonov","Antonov Airlines","An-225","AN-AAA",(1,1000),15000,1000)]
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


Naručilac
---------

Izveštaji i statistika
----------------------

Zaključak
---------