#### Innlevering 2:
#2090innlevering2
Oppgave 1: 
SSH inn på ifi maskin:
```bash
ssh -YC sebassha@login.ifi.uio.no
```

Logge inn på databasen:
```bash
psql -h dbpg-ifi-kurs03 -U sebassha -d sebassha
```

___
Oppgave 2: 
a) Navn på alle planeter som går i bane rundt stjernen Proxima Centauri
```sql
SELECT * FROM planet WHERE stjerne = 'Proxima Centauri';
```
Output:
			navn        | masse | oppdaget |     stjerne
-------------------+---+------------+-------------
Proxima Centauri b |       |     2016        | Proxima Centauri
Proxima Centauri d |       |     2020       | Proxima Centauri

b) Hvilke årstall (uten duplikater) det ble oppdaget planeter i bane rundt stjernene med navn TRAPPIST-1 og Kepler-154

```sql
SELECT DISTINCT oppdaget FROM planet where stjerne = 'Kepler-154' or stjerne = 'TRAPPIST-1' ;
```
----------
     2014
     2016
     2017
     2019
 (4 rows)

c) Antall planeter det er som ikke har oppgitt en masse (altså hvor masse
er NULL).
```sql
SELECT * FROM planet WHERE masse IS NULL  ;
```
*For lang output, irrelevant å vise hele tabellen* 

d) Navn og masse på alle planeter oppdaget i 2020 med masse høyere enn
gjennomsnittet av massen til alle planeter
```sql
SELECT AVG(masse) FROM planet;
```
**AVG** (Output)
___
6.482840891253784
(1 row)

```sql
SELECT * FROM planet WHERE masse > (SELECT AVG(masse) FROM planet ) AND masse = '2020' ;
```
 navn | masse | oppdaget | stjerne
------+-------+----------+---------
(0 rows)

e) Antall år mellom første og siste oppdagede planet i planet-tabellen.
1
```sql
ALTER TABLE planet ADD COLUMN differanse INT DEFAULT NULL;
```
2
```sql
UPDATE planet SET differanse = (SELECT MAX(oppdaget) - MIN(oppdaget) FROM planet);
```
3
```sql
SELECT DISTINCT differanse from planet;
```
Output
 differanse
-----------
34
(1 row)
___
##### Oppgave 3


