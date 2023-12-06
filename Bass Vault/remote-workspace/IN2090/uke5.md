# Grunnleggende SQL
[Lenke](https://www.uio.no/studier/emner/matnat/ifi/IN2090/h23/ukesoppgaver/uke05.html) til oppgavene. 
Løsningsforslag:
##### Oppgave 1
Skriv en spørring som finner:
1. Alle sjangere i tabellen Genre (28)
```sql
SELECT DISTINCT genre 
FROM filmgenre as sjanger;
```
2. Filmid og tittel for alle filmer utgitt i 1892 (12)
```sql
SELECT filmid, title 
FROM film WHERE prodyear = 1892;
```
3. Filmid og tittel for alle filmer der filmid er mellom 2000 og 2030 (14)
```sql
SELECT title 
FROM film WHERE filmid > 1999  AND filmid < 2031;
```
4. Filmid og tittel på alle filmer med Star Wars i navnet (129)
```sql
SELECT title, prodyear 
FROM film WHERE title LIKE '%Star Wars%';
```
5. Fornavn og etternavn til personid 465221 (1)
```sql
SELECT firstname || ' ' || lastname as full_name  
FROM person WHERE personid = 465221;
```
6. Alle unike rolletyper (parttype) i tabellen Filmparticipation (7)
```SQL
SELECT DISTINCT parttype FROM filmparticipation;
```
7. Tittel og produksjonsår for alle filmer som inneholder ordene "Rush Hour" (15)
```sql
SELECT title, prodyear 
FROM film WHERE title LIKE  '%Rush Hour%';
```
8. Vis filmid, navn og produksjonsår for filmer som inneholder ordet "Norge" (27)
```sql
SELECT title, filmid,  prodyear FROM film WHERE title LIKE  '%Norge%';
```
9. Vis filmid for kinofilmer som har filmtittelen Love (kinofilmer har filmtype "C") (42)
```sql

SELECT DISTINCT f.filmid, f.title, fi.filmtype 
FROM film AS f INNER JOIN filmitem as fi ON f.filmid = fi.filmid  WHERE f.title ='Love' AND fi.filmtype = 'C';

```
10. Hvor mange filmer i filmdatabasen er norske?
```sql
SELECT DISTINCT count(*) FROM filmcountry WHERE country = 'Norway';
---2245
```
#### Oppgave 2
Skriv en spørring som bruker nestede-spørringer for å finne:
1. Filmid og filmtype (fra Filmitem) for alle filmer som ble produsert i 1894(82)
```sql
--Uten delspøring
SELECT fi.filmid, fi.filmtype 
FROM film AS f INNER JOIN filmitem as fi ON f.filmid = fi.filmid
WHERE f.prodyear = '1894';

--Delspørringer
SELECT fi.filmid, fi.filmtype 
FROM filmitem AS fi 
WHERE fi.filmid IN ( SELECT f.filmid 
					FROM film AS f 
					WHERE f.prodyear = '1894' );
```
2. Navn på alle kvinnelige skuespillere (cast) i filmen med filmid 357076 (11)
```sql
-- riktig
SELECT p.firstname, p.lastname
FROM person AS p
WHERE p.gender = 'F' AND p.personid IN (	
				SELECT f.personid
                FROM filmparticipation AS f
                WHERE f.filmid = '357076'
                AND f.parttype = 'cast');

-- denne fungerer også, men den over er foretrukket.
SELECT p.firstname, p.lastname 
FROM person AS p 
INNER JOIN filmparticipation as fp 
ON p.personid = fp.personid 
WHERE fp.filmid = '357076' AND fp.parttype = 'cast' 
AND p.gender = 'F';
```

#### Oppgave 3
Skriv en spørring som finner..
1. Alle sjangere (genres) til filmen 'Pirates of the Caribbean: The Legend of Jack Sparrow' (5)
```sql
SELECT genre 
FROM filmgenre AS fg 
INNER JOIN film as f ON fg.filmid = f.filmid  
WHERE f.title = 'Pirates of the Caribbean: The Legend of Jack Sparrow'
;
--OUTPUT
-----------
 /*
 Action
 Adventure
 Comedy
 Drama
 Thriller
(5 rows)
*/
```
2. Alle sjangere for filmen med filmid 985057 (9)
```sql
SELECT genre FROM filmgenre WHERE filmid = '985057';

--OUTPUT:
/*
   genre
-----------
 Action
 Adventure
 Comedy
 Crime
 Drama
 Family
 Fantasy
 Mystery
 Thriller
(9 rows)
*/
```
3. Tittel, produksjonsår og filmtype for alle filmer som ble produsert i 1894 (82)
```sql
-- funka ikke lol
SELECT f.title, f.filmid, filmtype 
FROM film AS f 
WHERE f.prodyear = '1894' AND f.filmid IN(SELECT fi.filmid 
										  FROM filmitem AS fi 
										  WHERE fi.filmid = f.filmid);


--
SELECT f.title, fi.filmid, fi.filmtype
FROM film as F 
		INNER JOIN filmitem as fi ON f.filmid = fi.filmid
WHERE f.prodyear = '1894' ;
```

4. Alle kvinnelige skuespillere (cast) i filmen med filmid 357076. Skriv ut navn og på skuespillerne og filmid (11) - bonus: hva er tittelen? Legg til en ekstra kolonne med tittelen.
```sql
SELECT f.title, p.firstname, p.lastname, fp.filmid
FROM person AS p 
		INNER JOIN filmparticipation as fp ON p.personid = fp.personid
		INNER JOIN film as f ON fp.filmid = f.filmid
WHERE fp.filmid = '357076' 
	AND fp.parttype = 'cast' 
	AND p.gender = 'F';
```

5. Finn fornavn og etternavn på alle personer som har deltatt i TV_serien South Park. Bruk tabellene Person, Filmparticipation og Series, og løs det med:
i: INNER JOIN (21)
```sql
SELECT DISTINCT p.personid, p.firstname, p.lastname s.maintitle
FROM person AS p
		INNER JOIN filmparticipation as fp ON p.personid = fp.personid
		INNER JOIN series as s ON s.seriesid = fp.filmid
WHERE s.maintitle = 'South Park';
```
ii: Implisitt join (21)
```sql
SELECT DISTINCT p.personid, p.firstname, p.lastname, s.maintitle
FROM person AS p, filmparticipation AS fp, series AS s
WHERE p.personid = fp.personid 
	AND s.seriesid = fp.filmid 
	AND s.maintitle = 'South Park';
```
iii: NATURAL JOIN
```sql
SELECT DISTINCT p.personid, p.firstname, p.lastname, s.maintitle
FROM person as p
		NATURAL JOIN filmparticipation AS fp 
		NATURAL JOIN series AS s
WHERE s.maintitle LIKE 'South Park';
```
iv: Hvorfor gir NATURAL JOIN ulikt resultat fra INNER JOIN og implisitt join?

Natural join fungerer slik at den joiner alle attributter med samme navn. Hvilket betyr at i dette tilfellet hvor vi har serieid, filmid, personid, så vil ikke de falle i samme tabell. Så da må man bruke andre metoder.

6. Alle skuespillere (cast) i filmen, rollen deres (parttype) + tittel "Harry Potter and the Goblet of Fire" 
```sql
SELECT DISTINCT  p.firstname, p.lastname, fc.filmcharacter, f.title
FROM filmparticipation AS fp
        INNER JOIN filmcharacter AS fc ON fp.partid = fc.partid
        INNER JOIN person AS p ON fp.personid = p.personid
        INNER JOIN film AS f ON fp.filmid = f.filmid
WHERE f.title LIKE 'Harry Potter and the Goblet of Fire' 
AND fp.parttype = 'cast';

/*
						HJELPETABELL
filmcharacter(fc): filmcharacter, **partid**, billingpos
filmparticipation(fp): **partid**, **personid**, **filmid**, parttype(cast)
person(p): **personid**, firstname, lastname, gender
film(f): **filmid**, title, prodyear
*/
```

7. Finn navn på alle skuespillere (cast) i filmen Baile Perfumado (14)
```sql
SELECT DISTINCT p.firstname || ' ' || p.lastname AS name
FROM filmparticipation AS fp
		INNER JOIN person AS p ON fp.personid = p.personid
		INNER JOIN film AS f ON fp.filmid = f.filmid
WHERE f.title LIKE 'Baile Perfumado' AND fp.parttype = 'cast';

/*
						HJELPETABELL
filmparticipation(fp): **partid**, **personid**, **filmid**, parttype(cast)
person(p): **personid**, firstname, lastname, gender
film(f): **filmid**, title, prodyear 
/*
```
8. Skriv ut tittel og regissør for norske filmer produsert før 1960 (269)
```sql
SELECT f.title, fp.parttype, p.firstname || ' ' || p.lastname AS name 
FROM filmparticipation AS fp 
		INNER JOIN person AS p ON fp.personid = p.personid
		INNER JOIN film AS f ON fp.filmid = f.filmid
		INNER JOIN filmcountry AS fc ON fp.filmid = fc.filmid
WHERE fp.parttype = 'director' 
	AND fc.country = 'Norway' 
	AND f.prodyear < 1960;

---Alternativ løsning med USING. MERK filmparticpation binder alt sammen, derfor er det viktig at den kommer før person f.eks, hvis ikke funker det ikke å aksessere tabellen med personid
SELECT film.title, person.firstname || ' ' || person.lastname AS name
FROM filmcountry
		INNER JOIN filmparticipation USING (filmid)
		INNER JOIN film USING (filmid)
		INNER JOIN person USING (personid)
WHERE parttype = 'director'
	AND filmcountry.country = 'Norway'
	AND prodyear < 1960;

/*
						HJELPETABELL
filmparticipation(fp): partid, **personid**, **filmid**, parttype(director)
filmcountry(fc): **filmid**, country
person(p): **personid**, firstname, lastname, gender
film(f): **filmid**, title, prodyear
*/
```



