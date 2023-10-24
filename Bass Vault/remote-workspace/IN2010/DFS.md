DFS starter fra en gitt startnode og går så dypt som mulig langs hver gren før den kommer tilbake og utforsker andre grenene. Den bruker en stack for å holde styr på hvilke noder som skal utforskes neste gang. DFS finner ikke nødvendigvis den korteste veien mellom to noder, men kan brukes til å finne ulike strukturer i grafen, for eksempel topologisk sortering eller sykler.

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

