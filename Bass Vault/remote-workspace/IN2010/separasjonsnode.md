En separasjonsnode er en node som holder grafen sammenhengende
Fjernes en seperasjonsnode fjernes, får grafen flere komponenter
Dersom alle stier mellom to noder går gjennom den samme noden v ∈ V, så er v en seperasjonsnoden. 
Dybde-først søk med oppgav til et spenntre T:
- Dersom vi gikk fra u til v i søket lager vi en kant fra u til v i treet kalles dette en discovery-edge.
- I tillegg holder vi styr på hvilke noder som kan nås som allerede er oppdaget kaller vi dette for back-edge.
- En node u er en separasjonsnode hvis u er rot i T og har mer enn ett barn, eller u ikke er roten, og har et barn v, slik at ingen etterkommere av v (inkludert v selv) har en back-edge til en forgjenger av u.