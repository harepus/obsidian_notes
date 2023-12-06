Plan for mandag 4. desember:
#### Juridica kl 8:
**Gjøremål:**
# [x] Relasjonsmodellen 
# [x] Relasjonsalgebra
# [x] ER-modellering
# [x] Ternære relasjoner 
# [x] Repetisjonsforelesning: Modellering og normalformer
# [x] Realisering

___
Plan for tirsdag 5. desember:
#### Juridica kl 8:
**Gjøremål:**
# [x] Normalformer
# [x] Repetisjonforelesning: SQL
# [x] Aggregering 
# [x] Sortering
# [x] Ytre joins 
# [x] Mengdeoperasjoner
# [x] Indekser og spørreprossering
# [x] Programmering med SQL
# [x] Sikkerhet og SQL-Injection-angrep

___
## Ytterligere gjøremål før eksamen:


___
# ALT AV SQL:
### Grunnleggende SQL (slides):
```SQL
SELECT henter informasjon
SELECT <kolonner> from <KOLONNE>

CREATE lager noe (f.eks ny tabell)
INSERT setter inn rader i en tabell
UPDATE oppdaterer data i en tabell
DELETE sletter rader fra en tabell
DROP sletter en hel ting

```
```sql
LIKE % som wildcard

Name LIKE 'TV%'
TV 50 inch, og TVSHOW

Name LIKE '%TV'
50 inch TV, MTV

Name LIKE '%TV%inch'
TV 50 inch

LIKE eller SIMILAR TO eller ~

SELECT Name
FROM Products
WHERE NOT Description LIKE '%simple%'

Hvordan sjekke om en verdi er NULL.
IS NULL
SELECT StdName
FROM Students
WHERE StdBirthdate is NULL
--HVIS DU ANVENDER NULL SOM 'UKJENT' BLIR DET MER INTUITIVT
UKJENT AND TRUE resulterer i UKJENT (NULL)
10 + UKJENT resulterer i UKJENT

```
```sql
--Uttrykk i SELECT
SELECT contact_title || ' ' || contact_name AS contact_person
FROM customers
eksempel ('hel' || 'lo' = 'hello')

--Hvordan ungår man duplikater?
bruk DISTINCT-nøkkelordet
SELECT DISTINCT ...

sum(<column>)i SELECT klausulen

tilsvarende har man:
avg - gjennomsnitt
max - maksimum
min - minimum
count - antall rader

--for å finne **antall**(count) produkter som koster mer enn 20 dollar:
SELECT count(*) as nr_expensive_products
from products
where unit_price > 20

```

```sql
SELECT ProductName, Customer
FROM products, orders
WHERE ProductID = OrderedProduct

SELECT p.product_name, o.unit_price
FROM products AS p, order_details AS o
WHERE p.product_id = o.product_id

--kan også droppe å bruke 'AS p', istedenfor bare bruke
FROM products p, order_details o

--Istedenfor å skrive (implisitt join):
SELECT product_name
FROM products AS p, orders AS o
WHERE p.product_id = o.product_id AND 
o.unit_price > 7000

--kan man skrive (eksplisitt join)
SELECT p.product_name
FROM products AS p INNER JOIN order_details as o
	ON (p.product_id = o.product_id)
WHERE o.unit_price > 7000

--self-join
SELECT P2.Name, P2.Price
FROM Product AS P1, Product AS P2
WHERE P1.Name = 'Laptop 2.5GHz' AND P1.Price < P2.Price

--naturlig join MERK: må være sikker på at vi ønsker å joune på ALLE kolonnene med likt navn!
SELECT product_name
FROM categories NATURAL JOIN products
WHERE category_name = 'Beverages';
```
```sql
SELECT product_name, unit_price
FROM products
WHERE unit_price = (SELECT min(unit_price) from products)

--Hva er den største differansen mellom prisen på laptop
SELECT max(l1.Price - l2.Price) AS diff
FROM (SELECT Price FROM products WHERE Name LIKE '%Laptop%') AS l1,
     (SELECT Price FROM products WHERE Name LIKE '%Laptop%') AS l2

--Denne vil være ekvivalent med
WITH
	laptop AS (SELECT Price FROM products WHERE Name LIKE '%Laptop%')
SELECT max(l1.Price - l2.Price) as diff
FROM laptops AS l1, laptops AS l2
```
___
### Grunnleggende SQL (oppgaver):
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
___
### SQL Datamanipulering(slides):
#### Datamanipulering
```sql
--lage tabeller, brukere, skjemaer osv.
CREATE
CREATE SCHEMA northwind;
CREATE TABLE <tabellnavn> ( <kolonner> )

--Hvordan tilføye verdier i <kolonner>
CREATE TABLE Students (
SID int,
StdName text,
StdBirthdate date
);
--NOT NULL
CREATE TABLE Students (
SID int,
StdName text NOT NULL,
StdBirthdate date
);

--UNIQUE - unike verdier
CREATE TABLE Students (
SID int UNIQUE NOT NULL,
StdName text NOT NULL,
StdBirthdate date
);
--men istedenfor å skrive UNIQUE NOT NULL (for studentid kan ikke være null) man kan kun ha én primary key:
CREATE TABLE Students (
SID int PRIMARY KEY,
StdName text NOT NULL,
StdBirthdate date
);

--Kan skrive skranke til slutt
CREATE TABLE Students (
SID int,
StdName text NOT NULL,
StdBirthdate date,
CONSTRAINT sid_pk PRIMARY KEY (SID)
);

--Referanse / REFERENCES:
CREATE TABLE TakesCourse (
SID int REFERENCES Students (SID),
CID int REFERENCES Course (CID),
Semester text
);

--Sett data inn med INSERT:
INSERT INTO <tabell>
VALUES (<rad>), (<rad>), (<rad>);

-- Eksempelvis for å sette inn dette til Students:
/*
(0, 'Anna Consuma', '2000-01-01')
(1, 'Deez Nuts', '2010-10-10')
*/
INSERT INTO Students
VALUES  (0, 'Anna Consuma', '2000-01-01'),
		(1, 'Deez Nuts', '2010-10-10');

-- Annen måte å sette inn data
CREATE TABLE Students2018 (
SID int PRIMARY KEY,
StdName text NOT NULL
)
INSERT INTO Students2018
SELECT S.SID, S.StdName
FROM Students AS S 
		INNER JOIN TakesCourse AS T ON (S.SID = T.SID)
WHERE T.Semester LIKE '%18';
-- Kan gjøres direkte, da mister vi PRIMARY KEY, og NOT NULL.
CREATE TABLE Students2018 AS SELECT S.SID, S.StdName 
FROM Students AS S 
		INNER JOIN TakesCourse AS T ON (S.SID = T.SID)
WHERE T.Semester LIKE '%18';

--Default verdi
CREATE TABLE personer (
pid int PRIMARY KEY,
navn text NOT NULL,
nationalitet text DEFAULT 'norge'
);

--Serial, automatisk genererer unike heltall, må være sikker på at radene faktisk representerer noe unikt. 
CREATE TABLE Students (
SID SERIAL PRIMARY KEY,
StdName text NOT NULL,
StdBirthdate date
);
-PostgreSQL CSV
COPY filnavn
FROM 'path/to/filnavn.csv' DELIMITER ',' NULL AS '';
--Kan også lese fra stdin med Bash
--\copy i psql

--Slette tabell
DROP TABLE Students
--Dropp skjema
DROP SCHEMA northwind;

--For å slette ting og alt som avhenger av den tingen:
DROP TABLE Students CASCADE;

--For å slette rader fra en tabell:
DELETE
FROM Students
WHERE StdBirthdate > '1990-01-01';

--Oppdatering / ALTER / UPDATE ; Alt i skjemaet kan endres med ALTER
ALTER TABLE Students
RENAME TO UiOStudents;

ALTER TABLE Courses
ADD COLUMN Teacher text;

--Legge til skranker i ettertid:
ALTER TABLE courses
ADD CONSTRAINT cid_pk PRIMARY KEY (cid);

--Oppdatere data
UPDATE Students
SET StdBirthdate = '1987-10-03'
WHERE StdName = 'Sam Penny'

UPDATE products
SET unit_price = unit_price * 1.1
WHERE quantity_per_unit LIKE '%bottles%';
```
___
#### Typer og skranker
Typer:
- Numeriske
- Streng
- Dato- og tid
- Boolean
- Array
Kan også lage egne (utenfor pensum)

Ønsker å pakke bestilte varer i kubeformede bokser for hvert produkt, så vil finne 3. roten av antall bestilte varer for de som er bestilt. Samt ca. pris avrundet til nærmeste heltall.
```sql
SELECT product_name,
	ceil(power(units_on_order, 1.0/3)) AS box_size,
	round(unit_price * units_on_order) AS ca_price
FROM products
WHERE units_on_order > 0;
```
Kan bruke + og - mellom tidstyper:
```sql
date '2001-09-28' + interval '1 hour' = timestamp '2001-09-28:01:00:00'
date '2001-09-28' - interval '1 hour' = timestamp '2001-09-28:23:00:00'
date '2001-09-28' + 7 = date '2001-10-05'

now() -- gir et timestamp med nåværende tidspunkt
current_date -- konstant, inneholder dagens dato
make_date(year int, month int, day int)
OVERLAPS --i tilfelle tidstyper overlapper, hvis de overlapper resultat: True / else: False
```
"Text" er goat, men bruk "varchar(n)" eller "char(n)" som skranker (begrensning).
```sql
position(sub in str) --finner posisjonen til sub i str

substring(str from s for e) --finner substrengen i str som starter på indeks s og har lengde e

--I postgres

strpos(str, sub) --samme som position-uttrykket over
substr(str, s, e) --samme som substring-uttrykket over
```
CHECK lar oss bruke et generelt uttrykk for å avgjøre om verdier kan settes inn i kolonnen eller ikke:
```sql
CREAT TABLE students (
sid int PRIMARY KEY,
name text NOT NULL,
birthdate date CHECK (birthdate < date '2010-01-01')
);
```
___
#### Views
Lage VIEW for å slippe å lage samme spørring som skjer jevnlig.
Et view er bare en navngitt spørring:
```sql
CREATE VIEW StudentTakesCourse (StdName text, CourseName text)
AS
	SELECT S.StdName, C.CourseName
	FROM Students AS S,
	Courses AS C,
	TakesCourse AS T
	WHERE S.SID = T.SID AND C.CID = T.CID
```
Et view kan så brukes som det er en vanlig tabell, men blir beregnet på nytt hver gang den tas i bruk.
Views brukes også for å bygge lag med abstraksjoner:
![[Pasted image 20231203114710.png]]
Kan introdusere utledbare attributter uten å måtte lagre, oppdatere eller lignende:
```SQL
CREATE VIEW person_alder AS
SELECT navn,
fødselsdato,
EXTRACT(year FROM age(current_date,fødselsdato)) AS alder
FROM person
```
Materialiserte views lagres som en vanlig tabell på disk, som gjør de like effektive som en vanlig tabell
```sql
CREATE MATERIALIZED VIEW person_alder AS 
SELECT navn ,
fødselsdato ,
EXTRACT(year FROM age(current_date ,fødselsdato )) AS alder 
FROM person
```
Den kan enkelt oppdateres, men den må bruke
```sql
REFRESH MATERIALIZED VIEW person_alder;
```
___
#### SQL Scripts og Transaksjoner
Sjekk slides.
```sql
--SQL Scripts trygge kommandoer:
IF EXISTS AND IF NOT EXISTS

--Transaksjoner
UPDATE balances
SET balance = balance - 100
WHERE id = 1;
UPDATE balances
SET balance = balance + 100
WHERE id = 2;

--Transaksjoner omsluttes av BEGIN og COMMIT slik:
BEGIN;
UPDATE balances
SET balance = balance - 100
WHERE id = 1;
UPDATE balances
SET balance = balance + 100
WHERE id = 2;
COMMIT;
```
___
### SQL Datamanipulering (oppgaver):
1. CREATE TABLE: Skriv SQL-setninger som oppretter tabellene i skjemaet. Finn passende datatyper for attributtene. I tillegg ønsker vi at attributtet status i relasjonen Prosjekt kun skal kunne inneholde verdiene 'planlagt', 'aktiv', eller 'ferdig'.
```sql
CREATE TABLE Kunde (
kundenummer int PRIMARY KEY,
kundenavn text NOT NULL,
kundeadr text,
postnr text,
poststed text
);

CREATE TABLE Ansatt (
ansattnr int PRIMARY KEY,
navn text NOT NULL,
fodselsdato date,
ansattDato date
);

CREATE TABLE Prosjekt (
prosjektnummer int PRIMARY KEY,
prosjektleder int REFERENCES ansatt(ansattnr),
prosjektnavn text NOT NULL,
kundenummer int REFERENCES Kunde(kundenummer),
status text CHECK (status = 'planlagt' OR status = 'aktiv' OR status = 'ferdig')
);

CREATE TABLE AnsattDeltarIProsjekt(
ansattnr int REFERENCES Ansatt(ansattnr),
prosjektnr int REFERENCES Prosjekt(prosjektnummer)
CONSTRAINT deltar_pk PRIMARY KEY (ansattnr, prosjektnummer)
);
```
___
## Aggregering og Sortering (slides)
#### Sortering:
Å sortere radene i resultatet fra en SELECT spørring, bruke ORDER BY og kommer alltid ETTER WHERE klausulen:
```sql
SELECT product_name, unit_price
FROM products
ORDER BY unit_price;
```
Sorteres i henhold til type. Tall - verdi, text - alfabetisk, tidspunkt - kronologisk
Standard er fra minst til størst, for å reversere dette trenger man bare legge til DESC:
```sql
SELECT product_name, unit_price, units_in_stock
FROM products
ORDER BY unit_price DESC,
		units_in_stock DESC;
```
For å begrense antall rader bruker man LIMIT (kommer alltid sist), velg ut de 5 dyreste produktene:
```sql
SELECT product_name, unit_price
FROM products
ORDER BY unit_price DESC
LIMIT 5;
```
Finn navn og pris på produktet med lavest pris
```sql
-- Ved min-aggreggering og tabell-delspørring
SELECT p.product_name , p.unit_price 
FROM products AS p INNER JOIN (
		SELECT min(unit_price) AS minprice FROM products) AS h 
		ON p.unit_price = h.minprice;

-- Ved min-aggreggering og verdi-delspørring
SELECT product_name , unit_price 
FROM products 
WHERE unit_price = (SELECT min(unit_price) FROM products );

-- Ved ORDER BY og LIMIT 1
SELECT product_name , unit_price 
FROM products 
ORDER BY unit_price 
LIMIT 1;
```
Hvis du ønsker å hoppe over en rad bruk OFFSET, f.eks vise 10 og 10 produkter av gangen:
```sql
SELECT product_name , unit_price 
FROM products 
ORDER BY unit_price DESC 
LIMIT 10 OFFSET ; -- Først 0, så 10, så 20, osv.
```
___
#### Aggregering:
GROUP BY tar en liste med kolonner, og grupperer dem i henhold til likhet på verdiene i kolonnene.
```SQL
-- Antall produkter per bestilling
SELECT order_id, sum(quantity) AS nr_products
FROM order_details
GROUP BY order_id;

--Finn gjennomsnittspris for hver kategori
SELECT c.category_name , avg(p. unit_price ) AS Averageprice 
FROM categories AS c INNER JOIN products AS p 
		ON (c. category_id = p. category_id ) 
GROUP BY c. category_name ;
```
Ved gruppering på flere kolonner vil hver gruppe bestå av de radene med like verdier på alle kolonnene vi grupperer på:
```sql
-- Finn antall produkter for hver kombinasjon av kategori og hvorvidt produktet fortsatt selges
SELECT c.category_name , p.discontinued , count(*) AS nr_products
FROM categories AS c INNER JOIN products AS p
		ON (c. category_id = p. category_id )
GROUP BY c.category_name , p. discontinued ;

--Finn navn på ansatte og antall bestillinger den ansatte har håndtert, sortert etter antall bestillinger fra høyest til lavest
SELECT format('%s %s', e.first_name , e.last_name) AS emp_name ,
	count(*) AS num_orders
FROM orders AS o INNER JOIN employees AS e
		ON (o.employee_id = e.employee_id)
GROUP BY e.first_name , e.last_name
ORDER BY num_orders DESC;
```
Vil man ha kategorinavn og antall produkter på kategoriene som har flere enn 10 produkter kan det se sånn ut:
```sql
SELECT category_name , nr_products
FROM (
SELECT c.category_name , count(*) AS nr_products
FROM categories AS c
INNER JOIN products AS p ON (c.category_id = p.category_id)
GROUP BY c.category_name) AS t
WHERE nr_products > 10;

--Men vi kan heller anvende HAVING som fungerer litt som en WHERE for grupper.
SELECT c.category_name , count(*) AS nr_products
FROM categories AS c
		INNER JOIN products AS p ON (c.category_id = p.category_id)
GROUP BY c.category_name
HAVING count(*) > 10;
```
```sql
WITH <navngitte -spørringer >
SELECT <kolonner >
FROM <tabeller >
WHERE <uttrykk >
GROUP BY <kolonner >
HAVING <uttrykk >
ORDER BY <kolonner > [DESC]
LIMIT <N>
OFFSET <M>
```
___
#### Ytre Joins
Aggregering med sum, min, max, og avg ignorerer NULL-verdier.
Count teller med NULL-verdier, med mindre du counter en gitt kolonne : count(product_name).
```sql
SELECT min(Age) FROM Person; --> 2
SELECT avg(Age) FROM Person; --> 3
SELECT count(Age) FROM Person; --> 2
SELECT count(*) FROM Person; --> 3
SELECT sum(Age) FROM Person
WHERE Name = 'Mari'; --> NULL
SELECT count(Age) FROM Person
WHERE Name = 'Mari'; --> 0
```
Flere varianter: 
left outer join
right outer join
full outer join
Brukes ved å bytte ut INNER JOIN med f.eks LEFT OUTER JOIN
Hovedideen er å bevare alle rader fra en eller begge tabellene i joinen, så fylle inn med NULL hvor vi ikke har en match.

LEFT OUTER JOIN
Alle rader i den venstre tabellen blir med i svaret
```sql

LEFT OUTER JOIN b ON (a.c1 = b.c2)
--Blir det samme som 
INNER JOIN b ON (a.c1 = b.c2) --men hvor alle rader fra a som ikke matcher noen i b, blir lagt til resultat, med NULL for alle bs kolonner.
--Left outer join mellom products og orders (bevarer alle radene i products for products er den venstre tabellen)
SELECT *
FROM products AS p LEFT OUTER JOIN orders AS o 
	ON p.ProductID = o.ProductID;

--Hvor mange har kjøpt hvert produkt?
SELECT p.ProductName, count(o.Customer) AS num
FROM products AS p LEFT OUTER JOIN orders AS o
	ON p.ProductID = o.ProductID
GROUP BY p.ProductName

--Oversikt over navn, tlf nummer, og epost
SELECT p.Name, n.Phone, e-Email
FROM Persons AS p
	LEFT OUTER JOIN Numbers AS n
		ON(p.ID = n.ID)
	LEFT OUTER JOIN Emails AS e
		ON(p.ID = e.ID);
```
RIGHT OUTER JOIN
Samme som left outer join bare at den ikke bevarer alle radene fra venstre tabell, men heller bevarer alle radene fra høyre tabell.

FULL OUTER JOIN
Er en kombinasjon av de to, alle radene fra begge tabellene vil være med i svaret.
```sql
SELECT p.Name, n.Phone
FROM Persons AS p
	FULL OUTER JOIN Numbers AS n
		ON (p.ID = n.ID);
```
Eksempler:
```sql
--Finn navn på alle kunder som har gjort 2 eller færre bestillinger
SELECT c.company_name , count(o.order_id ) AS num_orders
FROM customers AS c
		LEFT OUTER JOIN orders AS o USING ( customer_id )
GROUP BY c. company_name
HAVING count(o.order_id ) <= 2;

--Finn ut hvor mange produkter i hver kategori firmaet Leka Trading supplier 
WITH
supplies AS (
SELECT category_id
FROM suppliers INNER JOIN products USING ( supplier_id )
WHERE company_name = 'Leka Trading '
)
SELECT c.category_name , count(s. category_id ) AS nr_products
FROM categories AS c
		LEFT OUTER JOIN supplies AS s USING ( category_id )
GROUP BY c. category_name ;
```

### Mengdeoperatorer
Eksempel Union:
```sql
-- Finn navn og by på alle leverandør og kundefirmaer fra Tyskland
(SELECT company_name , city
FROM customers
WHERE country = 'Germany ')
UNION
(SELECT company_name , city
FROM suppliers
WHERE country = 'Germany ');
```
EXISTS kan brukes før en delspørring i WHERE klausulen. EXISTS q er sann om q har minst ett svar. 
Kan bruke NOT EXISTS q for å finne ut om q ikke har no svar.
```sql
SELECT p.Name
FROM persons AS p
WHERE NOT EXISTS (
SELECT * -- Kan bruke hva som helst her
FROM companies AS c
WHERE c.country = p.country
);
```
![[Screenshot 2023-12-05 at 13.37.59.png]]
___
#### Sikkerhet
Lage bruker med SQL:
```Sql
CREATE USER leifhka WITH PASSWORD 'hemmelig '
	ROLE kundeadmin , produktansvarlig ;

--lage rolle
CREATE ROLE produktansvarlig ;

--Gi og fjerne rettigheter med GRANT
GRANT <privileges> ON <object> TO <role>;
--<privileges>
SELECT , UPDATE , INSERT , DELETE , CREATE , CONNECT , USAGE , ALL
--<object> er en database, tabell, skjema.. fjerner rettigheter med REVOKE
--For å gi rollen kundeadmin rettighetene til å oprette og oppdatere ws.users-tabellen kan vi kjøre følgende kommando:
GRANT INSERT , UPDATE ON TABLE ws.users TO kundeadmin ;

--For å gi rollen webshopadmin alle rettigheter innenfor skjemaet ws:
GRANT ALL ON SCHEMA ws TO webshopadmin ;

--Kan også gi en bruker en ny rolle med GRANT:
GRANT kundeadmin TO leifhka;

--Kan til og med gi tillatelser på kolonnenivå:
GRANT UPDATE (price) ON ws.products TO prisansvarlig ;

--For å fjerne kunde-rollens tilgang til categories kan vi kjøre
REVOKE USAGE ON ws. categories FROM kunde;
```

Programmering med SQL:
```python
def sett_inn_barn(conn, navn): 
	cur = conn.cursor() 
	cur.execute( "INSERT INTO barn VALUES (%, 1+(SELECT max(bid) FROM barn), true);", 
	(navn,)) 
	conn.commit()

#eller
def sett_inn_barn(conn, navn):
cur = conn.cursor()
cur.execute("SELECT max(bid) FROM barn;")
bid = cur.fetchone()[0]+1
cur.execute("INSERT INTO barn VALUES (%, %, true)", (navn, bid))
conn.commit()
```
Sikkerhet:
*for å finne alle barn i databasen med sql injection*
gave = "' AND false UNION SELECT * FROM barn;--"


Stenge tilkobling i Python
Connection og Cursor har close() metode.

___
# ALT ANNET (MODELLERING ++) 

## Relasjonsmodellen
*Relasjon*: en signatur og en mengde tupler 
*Relasjonsdatabase*: mengde med relasjoner med unikt navn.

![[Pasted image 20231204084029.png]]
Relasjonssignatur består av mengde med attributter/kolonner:
- Customers(CustomerID (int), Name (text), Birthdate (date), NrProducts (int))
- Customers(CustomerID, Name, Birthdate, NrProducts)
- Customers: {CustomerID: int, Name: text, Birthdate: date, NrProducts: int}
*Attributt*: en kolonne, består av et navn og type (Birthdate kolonnen f.eks).
Tuppel: en rad, mengde med par av attributtnavn og verdier:
- {CustomerID: '2', Name: 'Carla Smith', Birthdate: '1986-06-14', NrProducts: '8'}

**Databasedesign** || ' ' || **Tommelfingerregel**: 
- Én relasjon per entitet (kurs, student, osv.) 
- Én relasjon per forhold (karakter, foreleser for, gift med, osv.)  
- Aldri repeter data

**Supernøkkel**: "Mengde med attributter som alltid har unike verdier i en relasjon"
- Kan bruke en supernøkkel for å unikt identifisere en rad (altså en ting)
- En relasjon kan ha mange supernøkler
- Hvis vi har en supernøkkel, vil alle utvidelser også være en supernøkkel
- Viktig: En supernøkkel sier hva som alltid er unikt
- Beskriver altså virkeligheten (ikke bare dataene) ![[Pasted image 20231204085531.png]]
Kandidatnøkkel: en minimal supernøkkel, hvor du ikke kan fjerne flere attributter mens det fremdeles er en supernøkkel.
Fremmednøkkel: når en primærnøkkel referer fra en relasjon/tabell til en annen.
![[Pasted image 20231204085813.png]]
___
## Relasjonsalgebra
**Projeksjon**(π) = tar ett argument, mengde med attributter som subskrift.
Returnerer ny relasjon med bare attributtene listet. 
![[Pasted image 20231204090506.png]]
**StudentNavn:= πBrnavn,Etternavn(Student)**

**Seleksjon**(σ) = tar ett argument, uttrykk med attributt-navnene som varible som subskrift. 
Returnerer ny relasjon med kun de tuplene som tilfredsstiller uttrykket.
![[Pasted image 20231204090943.png]]

**Omdøping**(ρ) = tar ett argument, mengde med attributt-pil-attributt som subskrift. A -> B, sier at A omdøpes til B.
Returnerer ny relasjon med nye attributt-navn ihht. omdøpingene.
![[Pasted image 20231204091149.png]]

**Kartetisk produkt**(×) = tar to argumenter
Returnerer ny relasjon med:
- Alle attributtene til begge relasjonene
- Alle kombinasjoner av tupler fra de to relasjonene
![[Pasted image 20231204091254.png]]

**Join**() = tar to argumenter, mengde med attributt-=-attributt som subskrift. A = B sier at A skal være lik B i resultatet.
Returnerer ny relasjon med alle kombinasjoner av tupler fra de to relasjonene som tilfredsstiller uttrykket. 
![[Screenshot 2023-12-04 at 09.15.47.png]]
**Naturlig join**(stjerne) = tar to argumenter, utfører en join på alle attributter med likt navn.
**Snitt, union, og differanse** = tar to argumenter, utfører snitt, union, og differanse. 
![[Pasted image 20231204091747.png]]![[Pasted image 20231204091847.png]]

![[Pasted image 20231204091924.png]]

___
## ER-modellering
![[Pasted image 20231204093826.png]]

**Entity** (entitet) = representerer et objekt eller en ting som er signifikant for domenet du modellerer. Eksempler på entiteter kan være "Person", "Bil", "Bestilling".
**Weak Entity** (svak entitet) = en entitet som har en nøkkel som avhenger av en annen entitets nøkkel. Stiplet nøkkel-markering (attributtet) og dobbel boks på entiteten. 

**Attribute** (attributt) = representerer egenskaper, eller beskrivelser av entitet. "Person" kan ha "Navn", "Alder", "Adresse" som attributt.
**Multi-valued attribute** (flerverdi-attributt) = representerer egenskaper som kan ha flere verdier, vises ved dobbel-oval. F.eks telefonnummer, e-postadresse.
**Derived-attribute** (utledbar attributt) = oval med stiplet linjer
*Alder*: 
Du har en "Person"-entitet med attributtet "Fødselsdato". Da kan "Alder" være et utledbar attributt. Alderen kan beregnes fra dagens dato og personens fødselsdato.
*Arbeidserfaring*: 
I en "Ansatt"-entitet, hvis du har "Ansettelsesdato", kan "Arbeidserfaring" utledes ved å beregne forskjellen mellom dagens dato og ansettelsesdatoen.
**Composite Attribute** (Sammensatt attributt) = attributt + attributt = sammensatt. 
Fagkode + Emnenummer = Emnekode.
Navn: kan deles i fornavn, mellomnavn, etternavn = navn.
Adresse: kan deles i gatenavn, by, postnummer, land.

**Relationship** (relasjon) = beskriver hvordan to entiteter er relatert til hverandre. En "Person" kan "Eie" en "Bil". 
Tallet/bokstaven lengst vekk fra en entitet sier hvor mange den entiteten
høyst kan være relatert til.
**Identifying relationship** (identifiserende relasjon) = brukes ofte når en tilknyttet svak entitet er avhengig av en annen entitet (sterk) for sin identifikasjon. I en identifiserende relasjon bidrar den sterke entitetens primærnøkkel til den svake entitetens primærnøkkel. Gjøres med dobbel diamant. 

**Nedre skranke** = det minimum antall forekomster en entitet må ha i en relasjon.
* Vi skiller da kun på om det er minst én eller minst null
* Minst null representeres med enkel linje, kalles partsiell deltakelse
* Minst én representeres med dobbel linje, kalles total deltakelse
* Streken nærmest en entitet sier antall den entiteten minst må være relatert til “Nøyaktig én” representeres med total deltakelse og 1
**Øvre skranke** = det maksimale antall forekomster en en entitet må ha i en relasjon.
- èn eller mange (en = 1, mange = n / m)
### How to ER-modellere:
1. Identifiser **entiteter**:
- Finn de viktigste objektene/konseptene i systemet ditt
2. Identifiser **attributter**:
- Finn viktige egenskaper av hver entitet
- Nøkkelattributter (primærnøkler), som unikt identifiserer hver forekomst av en entitet, markeres ofte med understreking.
3. Identifiser **relasjoner**:
- Bestem hvordan entitetene relaterer til hverandre
4. Definer **kardinalitet**:
- **En-til-En (1:1)**: Hver forekomst i en entitet relaterer til nøyaktig én forekomst i en annen entitet. Tegn det som en linje med en enkel linje på hver ende, nærmest entitetene. **Eksempel:** Hvis vi har entitetene "Person" og "Pass", og hver person har nøyaktig ett pass, og hvert pass tilhører nøyaktig én person, vil dette være en 1:1-relasjon.
- **En-til-Mange (1:N)**: En forekomst i en entitet kan relateres til mange forekomster i en annen entitet. Tegn dette med en enkel stolpe på siden av "en" og en pil (eller kråkefot) på "mange"-siden. **Eksempel:** Hvis en "Forelder" kan ha flere "Barn", men hvert "Barn" har nøyaktig én "Forelder", vil dette være en 1:N-relasjon.
- **Mange-til-Mange (M:N)**: Mange forekomster i en entitet kan relateres til mange forekomster i en annen entitet. Dette representeres vanligvis med en pil (eller kråkefot) på begge sider av relasjonen. **Eksempel:** Hvis "Studenter" kan delta i flere "Kurs", og hvert "Kurs" kan ha flere "Studenter", er dette en M:N-relasjon.
5. Legg til **kardinalitetsrestriksjoner**:
- Spesifiser antall forekomster som kan delta i en relasjon. 
- For eksempel, i en 1:N-relasjon, kan du spesifisere at en "Person" kan "Eie" 0 til mange "Biler".
___
## Ternære relasjoner
* Må alltid relatere 3 entiteter
* Kombinasjonen av de relaterte elementene er ulike
* Kan ha attributter på relasjonen
Øvre skranker:
Gitt en PERSON, og en STILLING hvor mange FIRMA kan man ha?
- Gitt én PERSON, og ett FIRMA, så kan vi ha én STILLING
- Gitt én PERSON, og én STILLING, så kan vi ha mange FIRMAer
- Gitt én STILLING, og ett FIRMA, så kan vi ha mange PERSONer
![[Pasted image 20231204103851.png]]
Nedre skranker:
hvor mange entiteter vi må ha av én entitetstype i relasjonen
Må alle personer være ansatt (med en stilling i et firma)?
Antar:
PERSONer må ikke være ansatt (i noen firma i en stilling)
FIRMAer må derimot ha minst én ansatt i en stilling
En STILLING trenger derimot ikke ha noen ansatte (i noe firma)
**EKSEMPEL**
![[Pasted image 20231204104300.png]]

![[Pasted image 20231204104410.png]]
___
## Realisering
Skriv beskrivelser "Starter med å realisere vanlige entiteter"
1. Realiser de vanlige entitetene, som blir til en relasjon. Så får relasjonen sine attributter fra entiteten, og tar alltid bare løvnodene. Marker tydelig hva som er kandidatnøkkel(KN), samt primærnøkkel(PN). I tilfeller hvor det kun er en KN vil denne da være KN/PN. I tilfeller hvor KN er flere attributter må da gjøre et valg og vise til dette "Velger Navn som PN". Eksempel på hvordan det kan se ut: 
```txt
Brikke(Symbol, Verdi)
-KN/PN: {Symbol}
```

Skriv beskrivelser "Realiserer så svake:"
2. Realiser de svake entitene. Ved sammensatte attributter vil vi alltid ta i bruk løvnodene. Ta i bruk fremmednøkkel(FN) hvor navnet på FN er irrelevant, men at den -> på den vanlige entitetens KN. Så må også KN, og PN anvendes for resterende attributter. For eksempel:
```
Trekk(FraRute, TilRute, Brikke)
-KN/PN: {FraRute, TilRute, Brikke}
-FN: (Brikke) -> Brikke(Symbol)
```
Skriv beskrivelser "Realiserer **M-N** / M-1 / 1-1"
3. Realiser relasjonene. Start med 1-til-1 relasjonene. Videre 1-til-mange. Til slutt mange-til-mange (denne kan kun løses ved å lage en ny relasjon). Når du skal realisere relasjoner kan du velge mellom å tilføye relasjonen til en vanlig entitet som hører til relasjonen (ofte en entitet med en minst en (dobbel strek), samt mange (N)). Eller å lage relasjonen som vanlig som gir mening. OBS: relasjoner kan bli realisert tidligere hvis en svak entitet er koblet opp med denne. Attributter knyttet til en relasjon blir ikke en del av PN/KN.
4. Realiser flerverdi attributter, disse realiseres alltid med en egen relasjon.
5. "Altså blir det endelige skjemaet: "
*List opp alle relasjonene* så får man en fin oversikt.
[Powerpoint om realisering](https://www.uio.no/studier/emner/matnat/ifi/IN2090/h23/undervisningsmateriale/04-02.pdf)
___
### Normalformer
For å sjekke hvilken normalform et skjema oppfyller, kan vi sjekke alle tabeller opp mot alle FDer (funksjonelle avhengigheter).
Så sjekke om FDene bryter med BCNF, 3NF, 2NF.
For å sjekke om X er en **supernøkkel**, sjekk om alt er avhengig av X.
**Kandidatnøkkel**: minimal supernøkkel.
**BCNF** = 3NF + forsterket krav for avhengigheter
- *Forsterket krav for avhengigheter*: For enhver funksjonell avhengighet (A → B) i en tabell, skal A være en super-nøkkel.
**3NF** = 2NF+ ingen transitive avhengigheter
- *Ingen transitive avhengigheter*: Ingen ikke-nøkkel attributter er avhengige av andre ikke-nøkkel attributter.
**2NF** = 1NF + ingen delvis avhengighet
- *Ingen delvis avhengighet*: Ingen av de ikke-nøkkel attributtene er avhengige av bare en del av en sammensatt primærnøkkel.
**1NF** = Oppfyller atomiske krav, og unikhet:
- Hver rad er unik, og alle dataelementer er atomisk, altså ingen grupperte eller repeterende data. Hver kolonne skal inneholde udelelige verdier. 
**Eksempel for 1NF:**  
En tabell "StudenterKurs" med følgende struktur kan være i 1NF:

|StudentID|StudentNavn|KursID|
|---|---|---|
|1|Alice|101|
|1|Alice|102|
|2|Bob|103|

**Step by step guide for å sjekke normalform:**
1. Omskriving av FDer:
	- FDene må skrives på formen X -> A (splitt høyresiden)
		- Istedenfor ProduktID->Navn,Pris så: ProduktID->Navn \n ProduktID->Pris
2. Fjerne redundans:
	- Hvis X -> B, så er X ∪ Y -> B for alle Y.
	- ProduktID -> Navn ikke å bruke ProduktID,Pris -> Navn
	- Dette må gjøres når man bestemmer FDer
Algoritme for å sjekke NF:
1. Finn alle kandidatnøkler
	- øø
2. For hver tabell og hver FD X -> A 
	- **Er X en supernøkkel?**
		- Ja: Gå til neste FD, bryter ikke med BCNF.
		- Nei: brudd på BCNF. Gå til 3.
	- **Er A et nøkkelattributt?**
		- Ja: Bryter ikke med 3NF, gå til neste FD.
		- Nei: brudd på 3NF. Gå til 4.
	- Er X del av en kandidatnøkkel?
		- Nei: 2NF så langt, gå til neste FD.
		- Ja: brudd på 2NF og skjema er på 1NF, stopp. 
*Har jeg en tabell og en FD som bryter med 2NF, er skjemaet på 1NF*

___
### Tapsfri dekomponering
Tapsfri dekomponering til BCNF.
En dekomponering av R(X,Y,Z) 
Til S1(X,Y), S2(X,Z) er tapsfri hvis og bare hvis X -> Y

Steg for steg:
Tapsfri dekomponering av R(X) med FDer F:
	1. Beregn nøklene til R (fra F)
	2. Split alle FDer i F slik at det kun er ett attributt på høyresiden av hver FD (f.eks A,B -> C,D blir A,B -> og A,B -> D)
	3. Sjekk om R bryter med BCNF
		1. Hvis R ikke bryter med BCNF, stopp og returner R.
		2. Hvis R bryter med BCNF:
				1. Finn én FD Y -> A ∈ F som bryter med BCNF 
				2. Beregn Y+ med hensyn på FDene i F
				3. Dekomponer R til S1(Y+) og S2(Y,X/Y+)
				4. Fortsett rekursivt over S1 (med FDene som kun inneholder attributter fra S1(Y+))
				5. Fortsett rekursivt over S2 (med FDene som kun inneholder attributter fra S2(Y,X/Y+))


![[Screenshot 2023-12-05 at 09.41.02.png]]

### Gjennomgang av oppgave 3 fra repetisjonforelesning (Relasjonsmodellen og dekomponering)
3.1 Nøkler 
```
Gitt følgende relasjon
R(A,B,C,D,E)
med kandidatnøkler: AB og CD
med FDene:
A -> B
BC -> D
DE -> A
```
Attributter som ALDRI forekommer på noen høyreside: CE
Attributter som BARE forekommer på høyresider: Ingen
Starter med å sjekke om CE er KN, hvis ikke forsøker vi å utvide med de andre attributtene (ABD).

CE+ = CE, altså er CE ikke en KN.
CEA+ = CEA, siden vi har A kan vi legge til B og så D
CEA+ = CEABD = ABCDE = KN
CEB+ = CEBDA = ABCDE = KN
CED+ = CEDAB = ABCDE = KN
R har følgende kandidatnøkler: CEA,CEB,CED
___
3.2 Tapsfri dekomponering (funksjonelle avhengigheter)
Dekomponer relasjonen tapsfritt til BCNF. Vis hvordan du kommer frem til svaret. For hver relasjon du får underveis i dekomponeringen list opp FDer som holder, og hvilke kandidatnøkler relasjonen har.
Følgende relasjon
R(A,B,C,D,E,F)

KN: AB, CD

FDer: 
1. AB -> C : Venstresiden utgjør en supernøkkel, som betyr at den ikke bryter med BCNF.
2. AB -> D : Venstresiden utgjør en supernøkkel, som betyr at den ikke bryter med BCNF.
3. CD -> A : Venstresiden utgjør en supernøkkel, som betyr at den ikke bryter med BCNF.
4. CD -> B : Venstresiden utgjør en supernøkkel (KN på venstreside), som betyr at den ikke bryter med BCNF.
5. A -> E : 
6. C -> F : 

For FD 5 er ikke venstresiden (A) en supernøkkel, og den bryter derfor BCNF. Dekomponerer derfor denne:

A+ = AE

Dekomponerer derfor R til
S1(A, E) `minuser S1 med R i S2`
S2(A, (ABCDEF)-(AE)) = 
S2(A, B, C, D, F)

--- S1 ---
S1(A, E)
(Vi fjerner FDer som ikke har en venstreside som passer)
FDer: 
~~1. AB -> C ~~
~~2. AB -> D~~
~~3. CD -> A~~
~~4. CD -> B~~
5. A -> E 
~~6. C -> F~~

KN= A+ = AE
KN: A

Den eneste FDen A -> E bryter ikke med BCNF, altså er S1 på BCNF.

--- S2 ---

S2(A, B, C, D, F)

FDer:

1. AB -> C 
2. AB -> D
3. CD -> A
4. CD -> B
~~5. A -> E ~~
6. C -> F

KN: AB+=ABCDF, CD+=CDABF
KN: AB, CD

FD 6 bryter med BCNF, så vi må dekomponere videre.

C+ =  CF

S21(C, F)
S22(C (ABCDF)-(CF)) = S22(A, B, C, D)

--- S21 ---
S21(C, F)

FDer:
~~1. AB -> C~~
~~2. AB -> D~~
~~3. CD -> A~~
~~4. CD -> B~~ (fjernet)
6. C -> F

KN= C+= CF

KN: C

FD 6 bryter ikke med BCNF, altså er S21 på BCNF.
--- S22 ---
S22(A, B, C, D)

FDer:
1. AB -> C 
2. AB -> D
3. CD -> A
4. CD -> B
~~6. C -> F~~ (fjernet)

KN: AB, CD
Ingen FDer bryter med BCNF, altså er S22 på BCNF.

--- Endelig dekomponering ---
S1(A, E), S21(C,F), S22(A, B, C, D)
Altså kan R dekomponeres tapsfritt til BCNF som følgende relasjoner: S1(A, E), S21(C, F), S22(A, B, C, D). Med FDer og KN vist ovenfor.