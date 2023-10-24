# Innleveringer
| Oppgave                                     | Publiseres   | Frist        |
| ------------------------------------------- | ------------ | ------------ |
| **1. [Obligatorisk innlevering 1](oblig1)** | **28.08.23** | **28.09.23** |
| 2. Innlevering 2                            | 28.09.23     | 05.10.23     |
| 3. Innlevering 3                            | 05.10.23     | 19.10.23     |
| 4. Innlevering 4                            | 19.10.23     | 02.11.23     |

___
# Ukesoppgaver
#### "Oppvarming"
*Hva er en algoritme?*
- En algoritme er en rekke instruksjoner som gjennomføres for å løse et spesifikt problem eller utføre en oppgave. Algoritmen fungerer som en oppskrift, hvor du må følge hvert trinn i en bestemt rekkefølge for å oppnå det bestemte resultatet du ønsker å oppnå. Ofte brukes algoritmer i henhold til effektive ((datastrukturer)). 

*Hva er en datastruktur?*
- En datastruktur er en tegning som gir oversikt over data, og måten dataene håndteres og lagres. Vanlige typer datastrukturer er lister, trær, hauger, "hash-tabeller". En god datastruktur er essensielt for at algoritmen er effektiv. 
___
# Forelesning Chad
### Uke 1: Introduksjon og grunnleggende konsepter

- **Introduksjon**: Kurs i algoritmer og datastrukturer ved Universitetet i Oslo, høsten 2023. Foreleser er Lars Tveito (Page 1).
    
- **Om Algoritmer**: En algoritme er en presis beskrivelse for å løse et problem. Den må terminere etter et endelig antall steg, hvert steg må være presist definert, og den må ta null eller flere input og produsere et output (Page 3).
    
- **Om Datastrukturer**: En samling av verdier som følger en fast struktur. Algoritmer er avhengige av gode datastrukturer for å være effektive (Page 4).
    
- **Fokus i kurset**: Forstå, analysere, anvende og lage algoritmer. Det vil være viktig å studere eksempler og implementere dem (Page 5).
    
- **Studietips**: Vær en god medstudent, delta i gruppetimer, og prøv å kode litt hver dag. Det anbefales også å løse oppgaver fra ulike kilder som Kattis, LeetCode, Project Euler, etc. (Page 6).
    
- **Undervisning og Innleveringer**: Det vil være fire innleveringer, hvorav den første er obligatorisk. Innleveringene er designet for å hjelpe deg med å jobbe jevnt og få tilbakemelding (Pages 7-9).
    
- **Abstrakte Datatyper (ADT)**: Fokus på å finne effektive implementasjoner for sentrale ADT som Stack, Set, og Map (Pages 12-16).
    
- **Pseudokode og Notasjon**: Pseudokode brukes for å formidle algoritmer. Det vil også være en introduksjon til forskjellige notasjoner som brukes i algoritmer (Pages 17-19).
    
- **Søkealgoritmer**: Introduksjon til enkel søking og binærsøk. Binærsøk krever at arrayet er sortert (Pages 20-24).
___
### Uke 2: Sortering: Bubble, Selection, Insert, Merge

- **Oversikt**: Denne uken fokuserer på sortering. Det vil bli dekket Bubble sort, Selection sort, Insertion sort og Merge sort. Senere i kurset vil også Heapsort, Quicksort, Bucket sort og Radix sort bli studert (Page 3).
    
- **O-notasjon**: Introduksjon til O-notasjon, som handler om å estimere hvor lang tid en algoritme bruker. O-notasjon lar oss ignorere konstantfaktorer og fokusere på det største leddet (Pages 6-9).
    
- **Sortering**: Fokuset er på å sortere elementer i en datastruktur, spesielt arrayer. Sortering har ulike applikasjoner som å samle ting som hører sammen, matche elementer i sekvensielle strukturer, og søk i sorterte arrayer er raskere (Pages 10-13).
    
- **Bubble Sort**: En enkel sorteringsteknikk som går ut på å bytte om elementer som er i feil rekkefølge. Kjøretidskompleksiteten er O(n^2) (Pages 15-18).
    
- **Selection Sort**: Denne algoritmen finner det minste elementet i resten av arrayet og plasserer det først. Kjøretidskompleksiteten er også O(n^2), men den er generelt raskere enn Bubble sort fordi den gjør færre bytter (Pages 19-22).
    
- **Insertion Sort**: Denne sorteringsteknikken plasserer hvert element der det hører hjemme i den sorterte delen av arrayet. Kjøretidskompleksiteten er lik de andre, O(n^2) (Pages 23-26).
___
### Uke 3: Trær, Binære Søketrær og AVL-trær

- **Oversikt**: Fokus denne uken er på binære søketrær og AVL-trær, som er selvbalanserende varianter av binære søketrær. Det vil også bli nevnt rød-svarte trær som et alternativ til AVL-trær (Page 3).
    
- **Anvendelser av Trær**: Trær har to hovedkategorier av anvendelser: de representerer iboende hierarkiske strukturer og gir effektive implementasjoner for datasamlinger som mengder og ordbøker (Page 5).
    
- **Eksempler på Trær**: Syntaks i programmeringsspråk, HTML, filsystemer, og alle mulige sjakkpartier kan representeres som trær (Page 6).
    
- **Definisjon av Trær**: Et tre er enten tomt eller består av en node med en peker til et element, 0 eller flere pekere til barnenoder, og nøyaktig én foreldernode med mindre noden er roten (Page 7).
    
- **Terminologi**: Introduksjon til grunnleggende terminologi som roten, barn, foreldre, løvnoder, interne noder, subtrær, forfedre, etterkommere, sti, dybde og høyde av trær (Pages 8-20).
    
- **Traversering**: To hovedmåter for å traversere et tre: preorder og postorder. Disse har ulike bruksområder, for eksempel for å kopiere eller slette et tre (Pages 21-22).
    
- **Binære Trær**: Dette er trær hvor hver node har maksimalt to barn. I binære trær refereres det til venstre og høyre barn (Page 24).
    
- **Binære Søketrær**: Dette er binære trær som oppfyller visse egenskaper, som at elementet i en node er større enn alle elementer i venstre subtre og mindre enn alle elementer i høyre subtre (Page 25).
    
- **Algoritmer for Binære Søketrær**: Det blir introdusert algoritmer for innsetting, oppslag og sletting i binære søketrær. Disse har kompleksitet O(h), hvor h er høyden på treet (Pages 27-32).
___
### Uke 4: Binære Heaps og Prioritetskøer

- **Oversikt**: Denne uken fokuserer på prioritetskøer og binære heaps. Det vil også bli introdusert en anvendelse av prioritetskøer, nemlig Huffman-koding (Page 3).
    
- **Prioritetskøer**: En prioritetskø er en samling elementer som støtter operasjonene `insert(e)` og `removeMin()`. Det er flere måter å implementere en prioritetskø på, inkludert usorterte og sorterte lenkede lister, balanserte binære søketrær og heaps (Page 5).
    
- **Totale Ordninger**: Det blir forklart hva en total ordning er, og hvordan den kan implementeres i programmeringsspråk som Java og Python (Pages 6-7).
    
- **Binære Heaps**: En binær heap er et komplett binært tre der hver node som ikke er rotnoden, er større enn sin foreldrenode. Dette er en effektiv måte å implementere en prioritetskø på (Page 9).
    
- **Forskjell fra Balanserte Søketrær**: Binære heaps har samme kompleksitet som balanserte søketrær for innsetting og sletting av minste element, men de støtter færre operasjoner og har en svakere invariant. De er også enklere å implementere (Page 10).
    
- **Implementasjon**: Binære heaps er vanligvis implementert med arrayer fordi de alltid er komplette og dermed enkle å indeksere. Det blir også forklart hvordan innsetting og sletting fungerer i en binær heap (Pages 12-23).
___
### Uke 5: Grafer, Traversering og Topologisk Sortering

- **Oversikt**: Denne uken fokuserer på grafer, deres representasjon, traversering og ordning. Det vil også bli dekket temaer som korteste stier i en graf og minimale spenntrær i fremtidige forelesninger (Page 3).
    
- **Eksempler på Grafer**: Grafer kan representere kart, bekjentskapsnettverk, tilstander og trær (Page 5).
    
- **Grafer og Terminologi**: En graf er definert som to mengder �=(�,�)G=(V,E), der �V er en mengde av noder og �E er en mengde av kanter mellom noder fra �V (Page 6). Det blir også introdusert terminologi som parallelle kanter, løkker, rettede/urettede grafer, vektede/uvektede grafer, etc. (Page 7).
    
- **Stier og Veier**: En sti er en sekvens av noder i grafen, forbundet av kanter, der ingen noder gjentas. En vei er en sekvens av noder i grafen, forbundet av kanter, der ingen kanter gjentas (Page 9).
    
- **Sammenhengende Grafer og Komponenter**: En graf er sammenhengende hvis det finnes en sti mellom alle par av noder. En graf som ikke er sammenhengende kan deles inn i komponenter (Page 10).
    
- **Sykler og Asykliske Grafer**: En sti i med minst tre noder som forbinder første og siste node kalles en sykel. En graf som ikke inneholder en sykel kalles asyklisk (Page 11).
    
- **Representasjon av Grafer**: Grafer kan representert ved nabomatrise eller naboliste. Nabomatriser egner seg for tette grafer, mens nabolister egner seg for tynne grafer (Pages 15-17).
    
- **Graftraversering**: To hovedmetoder for graftraversering er dybde-først søk (DFS) og bredde-først søk (BFS). DFS kan implementeres rekursivt eller iterativt (Pages 19-23).
___
### Uke 6: Vektede Grafer, Korteste Stier og Minimale Spenntrær

- **Oversikt**: Denne uken fokuserer på vektede grafer, og hvordan man kan finne den billigste veien fra én node til andre noder. Det blir også diskutert hvordan man kan finne den billigste måten å koble alle noder i en graf (Page 3).
    
- **Korteste Stier**: Det blir forklart hvordan man kan finne den korteste stien i en graf fra en gitt node til alle andre. For uvektede grafer kan bredde-først søk brukes (Page 5).
    
- **Vektede Grafer**: Bredde-først søk fungerer ikke på vektede grafer. Det blir introdusert to algoritmer for å finne korteste stier i vektede grafer: Dijkstra og Bellman-Ford (Page 6).
    
- **Dijkstras Algoritme**: Dette er en modifikasjon av bredde-først søk som tar hensyn til kantenes vekt. Algoritmen bruker en prioritetskø for å ordne noder etter avstand fra startnoden (Pages 7-8).
    
- **Bellman-Ford**: Denne algoritmen kan håndtere grafer med negative vekter og oppdager negative sykler. Den går gjennom alle kanter ∣�∣∣V∣ ganger, noe som gir en kompleksitet på �(∣�∣⋅∣�∣)O(∣V∣⋅∣E∣) (Pages 12-14).
    
- **Korteste Stier i DAGs**: For rettede asykliske grafer (DAGs), kan man finne korteste stier i �(∣�∣+∣�∣)O(∣V∣+∣E∣) ved å besøke nodene i topologisk sortert rekkefølge (Page 15).
    
- **Minimale Spenntrær**: Det blir introdusert begrepet om minimale spenntrær og hvordan man kan finne dem ved hjelp av Prims algoritme (Pages 16-20).
___
## Uke 10 : Hashing
- Fokuset for denne uken er på hashing, som er den underliggende teknikken for hash maps og hash sets. Hashing kan deles inn i tre hovedproblemer:
    1. Konvertere en vilkårlig verdi til et tall som brukes som en indeks.
    2. Håndtere situasjoner der to verdier får samme indeks.
    3. Opprettholde en ideell størrelse på arrayet.
- Målet er å oppnå effektiv innsetting, oppslag, og sletting (Side 3).

#### Hash Maps og Hash Funksjoner

- Hash maps er en måte å implementere den abstrakte datatypen map. De bruker et enkelt array og en hashfunksjon for å konvertere nøkler til tall (Side 6).
- En god hashfunksjon må være konsistent og gi få kollisjoner. Den må også være godt distribuert, slik at ulike input hasjer til ulike output så ofte som mulig (Side 8).

#### Dårlige og Gode Hashfunksjoner

- Eksempler på dårlige hashfunksjoner inkluderer inkonsistente og dårlig distribuerte funksjoner (Side 9).
- For strenger, er en god hashfunksjon en som tar hensyn til rekkefølgen av bokstavene, i tillegg til deres numeriske verdi (Side 11).

#### Kollisjonshåndtering

- To hovedmetoder for å håndtere kollisjoner er "Separate Chaining" og "Linear Probing" (Side 19).
    - Separate Chaining: Hver plass i arrayet peker til en "bøtte", som kan være en lenket liste eller et binært søketre (Side 15).
    - Linear Probing: Ved kollisjoner ser man etter neste ledige plass i arrayet (Side 17).

#### Effektivitet

- Load factor er forholdet mellom antall elementer i hashmappen og størrelsen på arrayet. En ideell load factor bør avgjøres eksperimentelt og ligger antageligvis mellom 1/2 og 3/4 (Side 19).
- Rehashing utføres når arrayet blir for fullt eller for tomt. Dette innebærer å lage et større array og sette inn alle elementene fra det forrige arrayet (Side 20).
___
# Forelesning
#### 28. aug - **Sortering** (Uke 2)
___
![[Pasted image 20230912190132.png]]


#### 4. sep - **Trær, Binære og Balanserte Søketrær** (Uke 3)
___



##### Uke 7 - 2-sammenhengende grafer og sterkt sammenhengende komponenter:
___
Hva vil det si at en graf er [2-sammenhengende](2-sammenhengende-graf)?
Vit at vi har effektive algoritmer som gjør dette. Å lære disse algoritmene kan være litt tunge, bruk tid på det.

En [graf](graf) kalles sammenhengende hvis det finnes en sti mellom alle par av noder.
Dersom en graf ikke er sammenhengende deles den inn i komponenter.
Vi kan sjekke om en [urettet graf](urettetgraf) er en sammenhengende med et dybe først søk([DFS-search](DFS-search))
	- Grafen er sammenhengende hvis DFSVisit besøker alle noder i grafen
	- Dette er i O(|E|)
En graf G = (V , E) er 2-sammenhengende hvis G forblir sammenhengende selv hvis en hvilken som helst node v ∈ V fjernes fra G.
	- Sagt annerledes, det finnes to distinkte stier mellom hver par av noder
	- To stier mellom u og v er distinkte dersom de ikke deler noen kanter eller noder utenom u og v.
Mer generelt sier vi at en graf er k-sammenhengende dersom grafen forblir sammenhengende hvis man fjerner færre enn k noder.
Dette er et nyttig begrep i anvendelser der det er et ønske om redundans.
	- I et nettverk betyr det at en hvilken som helst maskin kan gå ned, og pakker vil fremdeles nå frem.
	- Hos Ruter kan det bety at det kan være full stans rundt en holdeplass, men at det finnes en alternativ rute for alle reisende
En [separasjonsnode](separasjonsnode.md) er en node som holder grafen sammenhengende
[Sterkt sammenhengende komponenter](sterk-sammenhengende-komponent) er en rettet graf, dersom det finnes en sti mellom alle par av noder
Den reverserte grafen til G er den grafen hvor alle kanter er snudd
	- Hvis G = (V, E) sier vi at Gr = (V, Er) er den reverste grafen
	- Hvis (u, v) ∈ E så er (v, u) ∈ Er
Grafen G og dens reverserte. graf Gr har alltid de samme sterkt sammenhengende komponentene!
Vi kan finne den sterkt sammenhengende komponenten til en node v ved å 
	- Finne alle noder som kan nås fra v i G
	- Finne alle noder som kan nås fra v i Gr
	- Nodene som kunne nås i både G og Gr utgjør den sterkt sammenhengende komponenten til v
Dette er en algoritme i O(|V| · (|V| + |E|)) 
	- Vi er en liten innsikt unna å få dette ned til O(|V| + |E|)
Ved å anse hver sterkt sammenhengende komponent som en enkelt node, så får vi det vi kaller for komponentgrafen.
Komponentgrafen er garantert å ikke inneholde noen sykel (er asyklisk)
Observerer at noder i den topologisk siste komponenten kan ikke nå noen andre komponenter
# Gruppetime
____
### Uke 4:
#### Prioritetskøer  
- En kø/samling med elementer som er sortert etter prioritet
- Eks: Størrelse, alder, høyde, osv.
- En prioritets kø må støtte følgende operasjoner:
- Insert(e)/push(e) - legger til et nytt element e
- removeMin()/pop() - Fjerner elementet med høyest prioritet
#### Binære Heaps  
- Hver node v er mindre enn barne-nodene
- Treet må være komplett
- Det betyr at treet fylles opp fra venstre til høyre
- ==Max vs min heap (?)==
- Min heap er hvor minste elementet er på toppen i treet (som illustrert under), max heap største elementet på toppen.
![Image preview](https://images.mentimeter.com/images/72cc6c8e-5db0-4422-922d-1f22d5142fe5.png?auto=compress%2Cformat&fm=png&w=2160&expires=1697327999&s=4e880ff1f0946924804686c290a5e209)

#### Array Representasjon:
![Image preview](https://images.mentimeter.com/images/2ff2fbab-5ac0-4a59-a9a2-811578457252.png?auto=compress%2Cformat&fm=png&w=2160&expires=1697327999&s=fa414fb593978ff2811b66364a1acf3e)

#### Huffman-koding  
- Formål: Komprimere data
- Huffman-koding representerer frekvenser av symboler
- Med frekvensene så kan vi representere setninger med bitstrenger
- Start ved roten, gå mot venstre i en sti = 0, høyre = 1. Så 0010 tilsier venstre, venstre, høyre, venstre.
- [https://cmps-people.ok.ubc.ca/ylucet/DS/Huffman.html](https://cmps-people.ok.ubc.ca/ylucet/DS/Huffman.html)
![Image preview](https://images.mentimeter.com/images/23f29995-83e5-4f87-a8a9-66067352e849.png?auto=compress%2Cformat&fm=png&w=2160&expires=1697327999&s=fbf207d12860f9309380c1cf498e4f7a)
____
#### Uke 7
[DFS](DFS) - Dybde Først Søk
![[Pasted image 20231005122839.png]]
Naiv metode:
- Går gjennom alle nodene i grafen
- For hver node v så fjerner vi den noden og sine kanter
- Deretter gjør vi et Dybde først søk på den resterende grafen G'
- Hvis DFS ikke besøker alle nodene i G', så er v en separasjonsnode
Rask metode (DFS):
- Gjør DFS(for å lage et spenntre)
- Vi indekserer nodene i rekkefølgen vi oppdager de
- Når vi oppdager noder lager vi en discovery edge(rettet)
- Om en node har 2 eller flere barn, så er det en seperasjonsnode.

Rask metode (Depth Low)
![[Pasted image 20231005123557.png]]

- Depth: Rekkefølgen noden ble oppdaget
- Low: Laveste depth en node kan nå ved å følge treet
- Man kan følge veien i treet, og ta med maksimalt ÉN back-edge
- En node v er en separasjonsnode dersom det finnes en node u(med kant til v) som har en low som er mindre eller lik v

Sterk sammenhengende graf : Gjelder for rettede grafer
___
##### Uke 8 - Repetisjon
O-Notasjon (==**SE NÆRMERE PÅ DETTE SENERE**==)
- Hvor vanskelig er et problem/algoritme å løse
- AKA: hvor mange steg trenger man for å løse problemet
- Eksempel: Hvor mange steg må man gjøre for å finne en vilkårlig løsning?
Hvordan finner man kjøretids kompleksiteten?
- Identifiser iterative steg (løkker, og rekursive kall)
- Finne avhengigheter (er det prosesser som skjer i løkker og rekursive kall)
- Blir andre funksjoner kalt på? Hva er kjøretiden til de
Lifehack Regler:
- Når de ter ledd mellom plusstegn, så kan man ta hensyn til det leddet som vokser raskest
	- Eksempel: O(N^3+n^2+n) = O(n^3) fordi n^3 vokser raskest når n øker.
- Konstanter og koffesienter kan man se bort ifra, eller redusere ned til 1.
	- Eksempel 1: O(50n) = O(1n) = O(n)
	- Eksempel 2: O(1000) = O(1)
- Variabler kan ganges sammen for å gjøre det enklere å se hva som vokser raskest
	- Eksempel: O((n+15)(n+20)) = O(n^2 + 20n + 15n +1520) = O(n^2) ettersom at n^2 vokser raskest

[BFS](BFS.md) og [DFS](DFS):
BFS (Bredde-Først Søk) og DFS (Dybde-Først Søk) er to algoritmer som brukes til å traversere eller søke gjennom en graf. 

Begge algoritmene kan brukes til å løse forskjellige problemer avhengig av hva man ønsker å oppnå med grafen. BFD er generelt sett mer effektiv enn DFS når man ønsker å finne den korteste veien mellom to noder, men DFS er ofte mer praktisk når man ønsker å utforske ulike strukturer i grafen.

![[Pasted image 20231012124420.png]]

![[Pasted image 20231012124433.png]]

