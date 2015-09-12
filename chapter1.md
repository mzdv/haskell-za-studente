Šta je Haskell i kako može da mi pomogne?
-----------------------------------------
Haskell. Ime koje se često izgovara u programerskim krugovima ili kao predmet razonode
ili kao predmet obožavanja. Haskell je funkcionalni programski jezik, bez ikakvih 
primesa ostalih paradigmi (poput objektno orijentisane ili imperativne paradigme), čime
u startu ljudi postaju odbijeni od njega, a posebno kada im se kaže da Haskell ne sadrži
promenljive niti petlje. Sve u Haskell-u su funkcije. Svaka funkcija u Haskellu je "čista" funkcija
iliti funkcija koja uvek vraća rezultat koji je određen ulaznim parametrima, bez bočnih efekata.
Bočni efekti predstavljaju skup promena gde se menja neko stanje iz "spoljnog sveta" (poput globalne promenljive;
u ovom slučaju, "unutrašnji svet" predstavlja doseg funkcije).

Naravno, ima još koncepata koji čine funkcionalni jezik, poput funkcija višeg reda,
currying-a, monada, rekurzije (koja se koristi svuda gde bi se koristila petlja; naravno
ne koristi se klasična rekurzija koja se uči, nego njena optimizovana varijanta, tzv. rekurzija repa
(tail recursion) i matematičkog aparata koji se zove teorija kategorija (koji pak povlači svoje pojmove
poput funktora, morfizama, kategorija i sličnoga). Ovo ne treba da vas brine (za sada) jer ćemo proći
svaki od ovih pojmova u sledećim poglavljima.

A da li ste znali da je Haskell više nego reč u etru?
Haskell koriste razne velike firme, kao što je [Facebook](https://code.facebook.com/posts/745068642270222/fighting-spam-with-haskell/)
koji ga koristi za borbu protiv spam-a, ili [Microsoft](https://news.ycombinator.com/item?id=1719456) koji zapošljava
osobe koje se zapravo bave razvitkom novih verzija Haskell-a i unapređivanjem postojećih.

Ovo nisu jedine kompanije koje ga koriste (ili koje se bave njegovim razvitkom). Koriste ga i banke, poput
[Barclays](https://www.haskell.org/communities/12-2007/html/report.html#sect7.1.2), kao i svima poznate IT
firme Google i Intel.

Sad kada smo Vas, čitaoca, ubedili da se Haskell zapravo koristi, a i zaplašili, vreme je da vidimo kako
Haskell može da pomogne u svakodnevnim programerskim aktivnostima. Koristeći Haskell, Vi, kao programer,
ne govorite računaru **šta on treba da uradi da bi došao do rezultata**, nego **kako rezultat treba da izgleda**. Samim time, Haskell
je *deklarativni* programski jezik (poput SQL-a). 

Primer: želite da iz niza elemenata [1,2,3,4,5] izvadite sve elementi koji su deljivi sa dva i da ih
ispišete na ekran.

U imperativnom programskom jeziku, poput C#-a (zanemarujući OOP komponente), algoritam bi izgledao ovako:

int niz[] = [1,2,3,4,5];
for(int i = 0; i < niz.Length; i++) {
	if(niz[i] % 2 == 0)
		Console.WriteLine(niz[i] + '\n');	
}

Rezultat bi bio: 

2

4

Obratite pažnju da smo mi računari rekli *svaki korak* koji on treba da uradi da bi ispisao vrednosti (za svaki
element niza, počevši od nulte pozicije, pa do maksimalne pozicije, ne uključujući nju, sa korakom od jedne pozicije,
proveri da li je trenutni element na koraku iz niza deljiv bez ostatka sa dva; ako jeste, ispiši ga na konzolu).

U Haskell-u, ovo bi se moglo uraditi na sledeći način:
