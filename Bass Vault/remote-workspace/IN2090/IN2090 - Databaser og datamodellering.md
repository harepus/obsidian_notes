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
