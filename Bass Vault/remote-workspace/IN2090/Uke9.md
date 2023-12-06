Avansert SQL:
1. Hvilke verdier forekommer i attributtet filmtype i relasjonen filmitem? Lag en oversikt over filmtypene og hvor mange filmer innen hver type (7).
```sql
SELECT DISTINCT filmtype, COUNT(filmtype)  
FROM filmitem 
GROUP BY filmtype;
```
2. Skriv ut serietittel, produksjonsår og antall episoder for de 15 eldste TV-seriene i filmdatabasen (sortert stigende etter produksjonsår).
```sql
-- Ikke riktig, viser bare de som har null 
SELECT maintitle, firstprodyear
FROM series
ORDER BY firstprodyear DESC
LIMIT 15;
```
3. Mange titler har vært brukt i flere filmer. Skriv ut en oversikt over titler som har vært brukt i mer enn 30 filmer. Bak hver tittel skriv antall ganger den er brukt. Ordne linjene med hyppigst forekommende tittel først. (12 eller 26)
```sql

```
4. Finn de “Pirates of the Caribbean”-filmene som er med i flere enn 3 genre (4)

5. Hvilke verdier (fornavn) forekommer hyppigst i firstname-attributtet i tabellen Person? Finn alle fornavn, og sorter fallende etter antall forekomster. Ikke tell med forekomster der fornavn-verdien er tom. Begrens gjerne antall rader. (176029 rader, 16108 for flest fornavn)

6. Finn filmene som er med i flest genrer: Skriv ut filmid, tittel og antall genre, og sorter fallende etter antall genre. Du kan begrense resultatet til 25 rader.

7. Lag en oversikt over regissører som har regissert mer enn 5 norske filmer. (60)

8. Skriv ut serieid, serietittel og produksjonsår for TV-serier, sortert fallende etter produksjonsår. Begrens resultatet til 50 filmer. Tips: Ikke ta med serier der produksjonsåret er null.

9. Hva er gjennomsnittlig score (rank) for filmer med over 100 000 stemmer (votes)?

10. Hvilke filmer (tittel og score) med over 100 000 stemmer har en høyere score enn snittet blant filmer med over 100 000 stemmer (subspørring!) (20).

11. Hvilke 100 verdier (fornavn) forekomer hyppigst i firstname-attributtet i tabellen Person?

12. Hvilke to fornavn forekommer mer enn 6000 ganger og akkurat like mange ganger? (Paul og Peter, vanskelig!)

13. Hvor mange filmer har Tancred Ibsen regissert?

14. Lag en oversikt (filmtittel) over norske filmer med mer enn én regissør (135).

15. Finn regissører som har regissert alene mer enn 5 norske filmer (utfordring!) (49)

16. Finn tittel, produksjonsår og filmtype for alle kinofilmer som ble produsert i året 1893 (4)

17. Finn navn på alle skuespillere (cast) i filmen Baile Perfumado (14).

18. Finn tittel og produksjonsår for alle filmene som Ingmar Bergman har vært regissør (director) for. Sorter tuplene kronologisk etter produksjonsår (62).

19. Finn produksjonsår for første og siste film Ingmar Bergman regisserte

20. Finn tittel og produksjonsår for de filmene hvor mer enn 300 personer har deltatt, uansett hvilken funksjon de har hatt (11).


