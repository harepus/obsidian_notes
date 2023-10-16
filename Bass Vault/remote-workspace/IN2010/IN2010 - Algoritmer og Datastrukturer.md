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
# Forelesning
#### 28. aug - **Sortering** (#2)
___
![[Pasted image 20230912190132.png]]


#### 4. sep - **Trær, Binære og Balanserte Søketrær** (#3)
___



##### Uke 7 - 2-sammenhengende grafer og sterkt sammenhengende komponenter:
___
Hva vil det si at en graf er [2-sammenhengende](2-sammenhengende-graf)?
Vit at vi har effektive algoritmer som gjør dette. Å lære disse algoritmene kan være litt tunge, bruk tid på det.

En [graf](graf) kalles sammenhengende hvis det finnes en sti mellom alle par av noder.
Dersom en graf ikke er sammenhengende deles den inn i komponenter.
Vi kan sjekke om en [urettet graf](urettetgraf) er en sammenhengende med et dybe først søk
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

#### Uke 7
DFS = Dybde Først Søk
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
Hvordan finner man kjøretidskompleksiteten?
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

BFD og DFS:
![[Pasted image 20231012124420.png]]

![[Pasted image 20231012124433.png]]

