#Naš model i priključenija
--------------------------

Uvod
----
Da bismo na što bolji način razumeli Haskell kao programski jezik, a ne kao skup simbola
i funkcija, ostatak knjige će se baviti primenom Haskell-a kroz konkretnu implementaciju:
implementaciju aerodromskog hangara gde se servisiraju avioni, čuvaju do sledećeg letenja,
kao i unapređuju. Pored toga, sistem će se moći koristiti za praćenje ovih karakteristika
i na kraju za kreiranje izveštaja i statistike kojom se može oceniti učinak rada hangara.
Pošto je cilj učenje korišćenja jezika, nećemo se baviti problemima perzistentnosti
podataka, pošto bi to zahtevali pisanje knjige samo za tu namenu.

Hangar
------
Potrebno je da hangar može da:
* Održava spisak aviona koji su trenutno u njemu
* Omogući dolazak aviona u hangar
* Omogući izlazak aviona iz hangara
* Izvrši unapređenje aviona ako postoji neophodna količina novca od strane naručioca

Avion
-----
Avion predstavlja glavni entitet ovog modela. On se sastoji od sledećih elemenata:
* Naziv aviona
* Ime avio kompanije kojoj pripada; 
	* Ako ne pripada nijednoj, polje je prazno
* Model aviona
* Registracija
* Unapređenja
	* Sastoje se od mape gde je ključ redni broj, a vrednost `True` ili `False`
	  u zavisnosti od toga da li je unapređenje odrađeno ili ne
* Vrednost
* Vrednost unapređenja

Potrebno je omogućiti i kreiranje izveštaja gde će se prikazati podaci o avionu.

Unapređenja
-----------
Sva unapređenja, nezavisno od tipa aviona, imaju istu cenu definisanu putem mape, gde je
ključ redni broj unapređenja, a vrednost cena unapređenja.

Naručilac
---------
Korisnik sistema. Sadrži novac koji se troši radi unapređenja aviona u hangaru.

Izveštaji i statistika
----------------------

Potrebno je omogućiti kreiranje sledećih izveštaja i statistika:
* Ukupan broj aviona, zajedno sa unapređenim i neunapređenim
* Ukupan broj remontovanih i ne remontovanih aviona
* Ukupna cena potrošenog novca u hangaru radi unapređenja svih aviona
* Ukupna cena potrošenog novca u hangaru radi unapređenja određene avio kompanije

Zaključak
---------