#Alkalmazások fejlesztése beadandó
##Course
Készítette: Katona Bence (D7JO4Q)

###Követelményanalízis
	####Feladat és célkitűzés
		A program a hirhedt Neptun rendszer egy leegyszerűsített, de határozottan nem rosszabb, megvalósítása. A fő feladat a tantárgyfelvétel, regisztráció és felhasználói adatmódosítás. A rendszer neve Course, az angol kurzus szóból származva.
	####Funkcionális követelmények:
		Adminisztrátorként:
			Főoldalon bejelentkezés
			Jelszó módosítása
			Új hallgató felvétele (név, ckód, jelszó)
			Új oktató felvétele (név, ckód, jelszó)
			Új tárgy felvétele (név, tematika)
			Tárgy oktatóhoz való hozzárendelése
			Törlések
			Kijelentkezés
		Hallgatóként:
			Főoldalon bejelentkezés (ckód, jelszó)
			Jelszó módosítása
			Tárgyakra lebontva a kurzusok között szabadon böngészni
			Oktatók között szabadon böngészni, hogy milyen tárgyakat oktatnak és melyik kurzust
			Felvenni egy tárgyat, tehát jelentkezni egy kurzusra
			Felvett tárgyak megtekintése
			Leadni egy kurzust, bármikor mivel nagyon jófej ez az egyetem
			Kijelentkezés
		Oktatóként:
			Főoldalon bejelentkezni (ckód, jelszó)
			Jelszó módosítása
			Új kurzust (oktatott kurzusok közül) meghirdetni tetszőleges számú hallgatónak
			Oktatott kurzusok megtekintése
			Kurzusra jelentkezettek megtekintése
			Kurzus létszámának növelése / csökkentése
			Kurzus törlése
			Kijelentkezés
			
	####Nem funkcionális követelmények:
		Ergonomikus elrendezés, felhasználóbarát felület
		Könnyen megérthető és elsajátítható működés
		Gyors működés
		Biztonságos, jelszóval védett adatok
		Egyértelmű hibajelzések
		Könnyen karbantartható és bővíthető

	####Szakterületi fogalomjegyzék:
		Tárgy - Tudományterület, amelyről tanulunk az egyetemen.
		Kurzus - A kurzus az a keret, amelyben a hallgatók meghatározott rend (előadás, gyakorlat, házi feladat, stb.) szerint gyarapítják tudásukat, és arról számot is adnak.
		Hallgató - Egy felsőoktatási intézményben tanuló személy.
		Oktató - Egy felsőoktatási intézményben tanító személy.
		
	####Használatieset-modell, szerepkörök
		Vendég: Csak a publikus a oldalt éri el, ami egy bejelentkezési felület
		Adminisztrátor: Felhasználók felvétele, új tárgy felvétele, oktatók tárgyainak rendezése, törlési műveletek
		Hallgató: Kurzusok keresése, oktatók keresése, kurzus felvétele / leadása, felvett kurzusok megtekintése
		Oktató: Új kurzus meghirdetése, oktatott kurzusok megtekintése, jelentkezett hallgatók megtekintése, létszám növelése / csökkentése, kurzus törlése
		Közös tulajdonságok: Bejelentkezés, jelszó módosítása, kijelentkezés
		
	nomnoml:
		#direction: right
		[<actor>Adminisztrátor] --> [<actor>Vendég]
		[<actor>Oktató] --> [<actor>Vendég]
		[<actor>Hallgató] --> [<actor>Vendég]

		[<usecase>Bejelentkezés] - [<actor>Oktató]
		[<usecase>Bejelentkezés] - [<actor>Adminisztrátor]
		[<usecase>Bejelentkezés] - [<actor>Hallgató]
		[<usecase>Kijelentkezés] - [<actor>Oktató]
		[<usecase>Kijelentkezés] - [<actor>Adminisztrátor]
		[<usecase>Kijelentkezés] - [<actor>Hallgató]
		[<usecase>Jelszó módosítása] - [<actor>Oktató]
		[<usecase>Jelszó módosítása] - [<actor>Adminisztrátor]
		[<usecase>Jelszó módosítása] - [<actor>Hallgató]

		[<actor>Oktató] - [<usecase>Új kurzus;meghirdetése]
		[<actor>Oktató] - [<usecase>Kurzusra jelentkezett;hallgatók megtekintése]
		[<actor>Oktató] - [<usecase>Kurzus létszámának;növelése / csökkentése]
		[<actor>Oktató] - [<usecase>Kurzus törlése]
		[<actor>Oktató] - [<usecase>Oktatott kurzusok;megtekintése]

		[<actor>Hallgató] - [<usecase>Kurzusok keresése]
		[<actor>Hallgató] - [<usecase>Oktatók keresése]
		[<actor>Hallgató] - [<usecase>Kurzus felvétele]
		[<actor>Hallgató] - [<usecase>Kurzus leadása]
		[<actor>Hallgató] - [<usecase>Felvett kurzusok;megtekintése]

		[<actor>Adminisztrátor] - [<usecase>Új hallgató felvétele]
		[<actor>Adminisztrátor] - [<usecase>Új oktató felvétele]
		[<actor>Adminisztrátor] - [<usecase>Új tárgy]
		[<actor>Adminisztrátor] - [<usecase>Oktató által tanítható;tárgyak beállítása]
		[<actor>Adminisztrátor] - [<usecase>Hallgató törlése]
		[<actor>Adminisztrátor] - [<usecase>Oktató törlése]
		[<actor>Adminisztrátor] - [<usecase>Tárgy törlése]
		
	####Példa egy folyamatra:
		Hallgatóként egy kurzusra jelentkezés
			1. A felhasználó a főoldalra érkezve bejelentkezik halgatóként
			2. Megkeresi a felvenni kívánt kurzust
			3. Ha tudja elveszi, ha nem új kurzust keres
			4. Vagy végez a tárgyfelvétellel vagy felveszi a többi tárgyát is
			5. Kijelentkezik
			#direction: right
			[<start>Start]-> [<state> Főoldal]
			[<state> Főoldal] -> [<state> Bejelentkezés]
			[<state> Bejelentkezés] -> [<choice> Sikeres?]
			[<choice> Sikeres?] Nem -> [<state> Bejelentkezés]
			[<choice> Sikeres?] Igen -> [<state> Kurzus;keresése]
			[<state> Kurzus;keresése] -> [<state> Felvesz]
			[<state> Felvesz] -> [<choice> Felvétel;sikeres?]
			[<choice> Felvétel;sikeres?] Nem -> [<state> Kurzus;keresése]
			[<choice> Felvétel;sikeres?] Igen -> [<choice> Új kurzus felvétele]
			[<choice> Új kurzus felvétele] Nem -> [<state> Kijelentkezés]
			[<state> Kijelentkezés] -> [<end>End]
			[<choice> Új kurzus felvétele] Igen -> [<state> Kurzus;keresése]
			
###Tervezés
	####Oldaltérkép
		Publikus:
			Belépés
		Bejelentkezett:
			Főoldal
				Adminisztrátor, oktató:
					Hallgatók
					Oktatók
					Tárgyak
				Hallgató:
					Felvett tárgyak
			Adatok módosítása
			Hallgatók
				Adminisztrátor:
					Új hallgató felvétele
					Törlés
			Oktatók
				Adminisztrátor:
					Új oktató felvétele
					Törlés
			Tárgyak
				Adminisztrátor:
					Új tárgy felvétele
			Kurzusok
				Adminisztrátor, oktató:
					Új kurzus felvétele
					Módosítás
					Törlés
				Hallgató:
					Felvesz
	####Végpontok
		GET/login: bejelentkező oldal
		POST/login: bejelentkező adatok felküldése
		GET/logout: kijelentkező oldal
		GET/: főoldal
		
		GET/hallgatok/list: hallgatók kilistázása
		GET/hallgatok/new: új hallgató felvétele
		POST/hallgatok/new: új hallgató felvételéhez szükséges adatok felküldése
		GET/hallgatok/edit=id: hallgató módosítása
		POST/hallgatok/edit=id: hallgató módosítása, adatok felküldése
		
		GET/oktatok/list: oktatók kilistázása
		GET/oktatok/new: új oktató felvétele
		POST/oktatok/new: új oktató felvételéhez szükséges adatok felküldése
		GET/hallgatok/edit=id: oktató módosítása
		POST/hallgatok/edit=id: oktató módosítása, adatok felküldése
		
		GET/targyak/list: tárgyak kilistázása
		GET/targyak/new: új tárgy 
		POST/targyak/new: új tárgy felvételéhez szükséges adatok felküldése
		GET/hallgatok/edit=id: tárgy módosítása
		POST/hallgatok/edit=id: tárgy módosítása, adatok felküldése
		
		GET/kurzusok/list: kurzusok kilistázása
		GET/kurzusok/new: új kurzus felvétele
		POST/kurzusok/new: új kurzus felvételéhez szükséges adatok felküldése
		GET/hallgatok/edit=id: kurzus módosítása
		POST/hallgatok/edit=id: kurzus módosítása, adatok felküldése
		
		GET/profil: felhasználói adatok
		POST/profil: felhasználói adatok felküldése

	####Oldalvázlatok
		KÉÉÉPEK
		KÉÉÉPEK
		KÉÉÉPEK
		KÉÉÉPEK
	
	####Osztálymodell
		[User | 
		name: String
		cCode: Int
		password: String]

		[Subject |
		name: String]

		[Course |
		id: Int
		capacity: Int]

		[Student] -:> [User]
		[Administrator] -:> [User]
		[Teacher] -:> [User]
		[Subject] +-> 1..* [Course]
		[Course] +-> 1 [Teacher]
		[Course] +-> 0..* [Student]
		[Student] +-> 0..* [Subject]
