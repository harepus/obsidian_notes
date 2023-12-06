# Innleveringer:
| Oppgave                           | Publiseres   | Frist        |
| --------------------------------- | ------------ | ------------ |
| **1. [Modellering](Modellering)** | **14.09.23** | **28.09.23** |
| 2. [Enkel SQL](Enkel_Sql)         | 28.09.23     | 12.10.23     |
| 3. Normalformer                   | 12.10.23     | 26.10.23     |
| 4. Avansert SQL                   | 26.10.23     | 09.11.23     |
| 5. Programmering med SQL          | 02.11.23     | 16.11.23     |
|                                   |              |              |
**Innlevering 1 er obligatorisk**, resten er ikke obligatorisk. 

``psql -h dbpg-ifi-kurs03 -U sebassha -d northwind``

___
# [Ukesoppgaver](ukesoppgaver.md)
___
## [EKSAMENSPLAN](Eksamensplan_2090)
___
# Forelesning

### Uke 4
___
**Modellering og realisering:**
Entity Relationship (**ER**) diagram er et flytskjema som viser til hvordan forholdet mellom personer, objekter, og konsepter relateres til i et system.
Tertiær ER-diagram, med eksempel til ukesoppgaver:
- Relasjoner mellom butikk, selger, og kunde
- Relasjoner mellom tillatelse, person og autoritet 

### Uke 5
___
**Eksempeloppgaver: SQL**

```sql
SELECT product_name, unit_orice, units_in_stock, unit_price * units_in_stock AS verdi FROM products WHERE unit_price * units_in_stock > 1000;
```

```sql
/* comment :) */
SELECT (SELECT count (*) FROM forum.log_entry)
AS logged_in_now, 
(SELECT count(*))
AS logged_in_today FROM forum.log_entry WHERE log_out is NULL or current_date::timestamp <= log_out;
```



### Uke 7
___
#### Databasedesign og normalformer
```
personnr -> født, fødselsnr
født, fødselsnr -> personnr
postnr -> poststed
født -> alder
```


**GITT FØLGENDE RELASJON:**
	Person(personnr,navn,initialer,fødselsdato,alder)
personnr -> navn, fødselsdato
navn -> initialer
fødselsdato -> alder

Tillukningene til:
	1.1 navn
		navn+ = navn, initialer
	1.2 personnr
		personnr+ = personnr, navn, fødselsdato, initialer, alder
	2. Finn alle kandidatnøklene til Person
		Aldri på høyresider: personnr
		Bare på høyresider: initialer, alder
		Forsøk å utvide med: navn, fødselsdato
		Ser over at personnr er en kandidatnøkkel, og bestemmer de andre, så dermed den eneste.
___

```sql
CREATE TABLE person(personnr text, navn text, initialer text, fødselsdato text, alder text);
INSERT into person values('01019012345', 'Ole', 'O', '010190', '33');
SELECT * from person;
```

Finn kandidatnøklene til relasjonen:
	Produkt(produktID, navn, kategori, pris, butikkID, butikknavn, butikktype, adresse, postnr, poststed)
Med FDene:
	- produktID -> navn, kategori, pris
	- navn, kategori -> produktID
	- butikkID -> butikknavn, butikktype, adresse, postnr
	- postnr -> poststed
Finn alle kandidatnøklene til Produkt.

Aldri på høyresider: butikkID
Bare på høyresider: pris, butikknavn, butikktype, adresse, postested
Forsøk å utvide med: navn, kategori, postnr, produktID

{butikkID, produktID}+ = butikkID, produktID, navn, kategori, pris, butikknavn, butikktype, adresse, postnr, poststed

Kandidatnøkler: {butikkID, produktID}, {butikkID, navn, kategori}

Gitt relasjonen R(A, B, C, D, E, F, G) med FDene AB -> DE, C -> E, AE -> BF, finn alle nøkler.

Hvilke forekommer ikke i noen høyreside : C G
Bare forekommer i høyresider: F
Begynn med C G og utvid med A, B, D, E.
	1. X = CG . CG+ = CGA. CG er ikke en kandidatnøkkel.
	2. Prøv å utvide X med B, D, E. (A allerede er i CG+, ikke noe poeng å utvide med A.)
		2.1 X = BCG. BCG+ = BCGADEF. BCG er en kandidatnøkkel.
		2.2 X = CDG. CDG+ = CDGA. CDG er ikke en kandidatnøkkel.
		2.3 X = CEG. CEG+ = CEGABDF. CEG er en kandidatnøkkel.
		2.4 Fortsett med X = CDG. Prøv å utvide med B, E.
			2.4.1 X = BCDG. BCDG+ = BCDGAEF. Men BCG er en kandidatnøkkel, så BCDG er ikke minimal, og ikke kandidatnøkkel.



### Repetisjon forelesning - Modellering:
Prøveeksamen H20(?)
3. Relasjonsmodellen og dekomponering
3.1 Nøkler 
```
R(A,B,C,D,E)
med FDene
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
___
```sql
CREATE TABLE barn(
	bid int PRIMARY KEY,
	navn text NOT NULL,
	nyttig boolean NOT NULL
);
CREATE TABLE gave(
	
);

SELECT b.navn, count(g.gid)
FROM barn AS b 
	LEFT JOIN ønskeliste as ø ON (b.bid = ø.barn)
	LEFT JOIN (SELECT * FROM gave WHERE nyttig) AS g ON (ø.gave = g.gid)
GROUP BY b.bid, b.navn;
```


```SQL
--Nyttige gaver
SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster

--Unyttige gaver
SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE NOT g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster

--Kombinere disse to spørringene med UNION / UNION ALL. Hvor UNION behandler alt som mengder, og fjerner duplikater. UNION ALL er mer effektiv.

SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE NOT g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster
UNION ALL
SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE NOT g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster
```

```sql

```
___


___
# SQL Intro Uke 5:
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

## SQL Datamanipulering (Uke 6):
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
# Aggregering og Sortering (Uke 9)











___
# Ytre joins og mengdeoperatorer (Uke 10)








### Repetisjonsforelesning: SQL

```sql
CREATE TABLE barn(
	bid int PRIMARY KEY,
	navn text NOT NULL,
	nyttig boolean NOT NULL
);
CREATE TABLE gave(
	
);

SELECT b.navn, count(g.gid)
FROM barn AS b 
	LEFT JOIN ønskeliste as ø ON (b.bid = ø.barn)
	LEFT JOIN (SELECT * FROM gave WHERE nyttig) AS g ON (ø.gave = g.gid)
GROUP BY b.bid, b.navn;
```

```SQL
--Nyttige gaver
SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster

--Unyttige gaver
SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE NOT g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster

--Kombinere disse to spørringene med UNION / UNION ALL. Hvor UNION behandler alt som mengder, og fjerner duplikater. UNION ALL er mer effektiv.

SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE NOT g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster
UNION ALL
SELECT g.navn, nyttig, count(*) AS ant
FROM gave AS g JOIN ønskeliste AS ø ON(g.gid = ø.gave)
WHERE NOT g.nyttig
GROUP BY g.gid, g.navn
ORDER BY ant DESC LIMIT 3 --for å kun finne de tre forekomster
```

```sql
--Snille barn får alle gavene de vil ha, usnille med ønsker får alle nyttige, usnille uten ønsker får genser.
WITH
	snille_barn AS (
	SELECT b.navn, g.navn AS gave
	FROM barn AS b 
		JOIN ønskeliste AS ø ON (b.bid = ø.barn)
		JOIN gave AS g ON (ø.gave = g.gid)
		WHERE b.snill
	),
	usnille_med_ønsker AS(
	SELECT b.bid, b.navn, g.navn AS gave
	FROM barn AS b 
		JOIN ønskeliste AS ø ON (b.bid = ø.barn)
		JOIN gave AS g On (ø.gave = g.gid)
		WHERE NOT b.snill AND g.nyttig
	),
	--NOT IN / se boritfra det som er inne i parantesen
	usnille_uten_ønsker AS(
		SELECT b.navn, 'Genser' AS gave
		FROM barn AS b
		WHERE NOT b.snill AND b.bid NOT IN(
		SELECT bid
		FROM usnille_med_ønsker
		)
	),
SELECT * FROM snille_barn
UNION ALL
SELECT navn, gave FROM usnille_med_ønsker
UNION ALL
SELECT * FROM usnille_uten_ønsker;
```

