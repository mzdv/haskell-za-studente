#Model podataka
--------------------------

Uvod
----
Da bismo na što bolji način razumeli Haskell kao programski jezik, a ne kao skup simbola i funkcija, 
ostatak knjige će se baviti primenom Haskell-a kroz konkretnu implementaciju: implementaciju aerodromskog 
hangara gde se servisiraju avioni i čuvaju do sledećeg letenja. Pored toga, sistem će se moći koristiti za 
praćenje ovih karakteristika i na kraju za kreiranje izveštaja i statistike kojom se može oceniti učinak 
rada hangara. Pošto je cilj učenje korišćenja jezika, nećemo se baviti problemima perzistentnosti 
podataka, pošto bi to zahtevalo pisanje knjige samo za tu namenu.

Avion
-----
Avion predstavlja glavni entitet ovog modela. On se sastoji od sledećih elemenata:
* Naziv aviona
* Ime avio kompanije kojoj pripada; 
	* Ako ne pripada nijednoj, polje je prazno
* Model aviona
* Registracija
* Unapređenja
	* U zavisnosti od toga da li je unapređenje odrađeno ili ne
* Vrednost
* Vrednost unapređenja

Potrebno je omogućiti i kreiranje izveštaja gde će se prikazati podaci o avionu.

Hangar
------
Potrebno je da hangar može da:
* Održava spisak aviona koji su trenutno u njemu
* Omogući dolazak aviona u hangar
* Omogući izlazak aviona iz hangara

Unapređenja
-----------
Sva unapređenja, nezavisno od tipa aviona, imaju istu cenu definisanu putem mape, gde je
ključ redni broj unapređenja, a vrednost cena unapređenja.

Izveštaji i statistika
----------------------

Potrebno je omogućiti kreiranje sledećih izveštaja i statistika:
* Ukupan broj aviona, zajedno sa unapređenim i neunapređenim
* Ukupan broj aviona, unapređeni
* Ukupna cena potrošenog novca u hangaru radi unapređenja svih aviona
* Ukupna cena potrošenog novca u hangaru radi unapređenja određene avio kompanije

Zaključak
---------
Gore navedeni dokument predstavlja specifikaciju na osnovu koje ćemo da vršimo programiranje u 
Haskell-u. Podložno je izmeni, ali na retroaktivan način: kada se implementuje nešto novo kao izmena,
vraća se nazad na ovaj dokument i vrši se njegova izmena.