### Workshop 1
Remote Desktop Connection - Advanced - Settings - (Kommer i E-post).
https://view.uio.no
https://svar.in2120.uiocloud.no/

___
### Workshop 3
Teorioppgave 2
- *Hva menes med begrepet «tillitsanker» i systemsikkerhet?*
	- Et eksempel på et tillitsanker er å trykke på knappen til å starte et system, så lastes det inn Kernel, og drivere, til slutt lastes det inn selve opperativsystemet. Dette vises på skjermen med ikoner osv. BIOS er et tillitsanker - UEFI.
- *Hva er forskjellen mellom et generelt «system» og et «virtuelt system»?*
	- En virtuell mikroprosessor som imiterer en fysisk mikroprosessor.
- *Hva er en virtuell maskin når man snakker om datamaskiner?*
	- Programvare som later som det er en fysisk datamaskin med et virtuelt mikroprosessor, som kjører på et allerede eksisterende OS. 
- *På hvilken måte kan virtualisering støtte sikkerhet?*
	- Teste skadelig programvare uten sjans for skade på eksisterende filer, eller hardware. Du kan begrense hvor stor tilgang den virtuelle maskinen har, i forhold til hardware eller tilgang til resten av det vanlige OS-et. 
___
## Forelesning
###### Forelesning #5
[Angrepsvektor](Angrepsvektor) og [Skadevare](Skadevare.md)

#### Forelesning #6
**Pentesting**

___
#### Forelesning #8 - IAM
![[Pasted image 20231023151907.png]]

___
#### Forelesning #9 - Nettverkssikkerhet
**Kommunikasjonssikkerhet**
Tematikk for forelesning
* [Nettverkslag](nettverkslag)
* TLS
* QUIC
* IPsec
* VPN og TOR
* Applikasjonssikkerhet og OWASP TOP 10

Sikre kommunikasjonen mellom A og B, ikke kun sikre endepunktene. 
![[Pasted image 20231017102134.png]]

OSI - Open Systems Interconnection

Sikkerhetsprotokoller:
Mange forskjellige sikkerhetsprotokoller for forskjellige formål
- Autentisering, integritet, konfidensialitet
- Nøkkelutveksling
- E-valg

Eksempler: TLS og IPSEC 
Sikkerhetsprotokoller er overraskende vanskelig å designe uten sårbarheter!
- Mange sårbarheter oppdages år senere
- Noen blir aldri oppdaget (eller kanskje bare av angriperne)

TLS i internettstakken
TLS består egentlig av et sett med protokoller for ulike trinn i økten.
TLS handshake protokollen ligger i applikasjon laget, mens TLS Record Protokollen ligger i transport laget.
![[Pasted image 20231017102904.png]]

Diffie Hellmann nøkkelutveksling 
![[Pasted image 20231017103045.png]]

TLS 1.3
- Designet for hurtighet i etableringen av øktnøkkel
- Trenger kun én meldingsrunde (frem og tilbake) for å etabler øktnøkkel
- Foroversikkerhet (forward secrecy) betyr at tidligere øktnøkler ikke blir kompromittert selv om en langsiktig kryptonøkkel blir kompromittert en gang i fremtiden.
- Foroversikkerhet oppnås ved bruk av Diffie-Hellman

QUIC
- QUIC er en protokoll på transportlaget
	- Originalt fra Google
	- Mer enn halvparten av Chrome forbindelser til Google tjenester bruker nå QUIC
- All trafikk kryptert
- Reduserer overhead fra TLS + TCP
	- Først må en TCP handshake gjennomføres
		- Deretter TLS handshake
	- QUIC kombinerer og forenkler dette 

IP Sikkerhet
- Internettprotokollsikkerhet (IPSec) er standard for sikker kommunikasjon over internettprotokollen (IP-laget)
	- Ved bruk av kryptografiske sikkerhetstjenester.
- Bruker kryptering, autentisering og protokoller for nøkkelutveksling
- Basert på en ende-til-ende sikkerhetsmodell på ip-laget
- Konfigueres på OS-nivå, ikke i applikasjoner.

Applikasjonssikkerhet
- Fokus er på sikkerhet i klient- og tjenerapplikasjoner som kommuniserer over internett
- Slike applikasjoner er mye brukt og man ser stadig nye slike tjenester
- Disse er ofte web-tjenere som
	- ofte bruker HTTP (port 80) eller HTTPS (port 443) protokollene
	- står vanligvis utenfor den indre brannmuren og er direkte eksponert mot internett
- Web-tjenere er ofte koblet til backend-tjenere (indre segment)
	- Gjennom sårbarheter i web-tjeneren kan dermed backend-tjeneren angripes
- Klienter som kommuniserer er også eksponert ved at de angripes når de kontakter sårbare tjenerapplikasjoner. 

OWASP
- Open Web Application Security Project
	- Ideell organisasjon med mål om å forbedre sikkerheten til applikasjoner og tjenester på internett
	- Gjennom råd, veiledning og verktøy
	- Involverer bedrifter, utdanningsinstutisjoner og enkeltpersoner fra hele verden
	- Flere parallelle prosjekter
OWASP top 10:
1. Brudd på tilgangskontroll
- Angripere utnytter feil i hvordan tilgangskontroll er håndhevet
* Lese eller endre andre brukeres data
2. Kryptografiske feil
- qq
3. Injeksjon
- qq
4. Usikkert design
- ..
5. Feilkonfiguert sikkerhet
- blb 
6. Sårbare og utdaterte komponenter
- qqq
7. Feil i identifisering og autentisering
- qq
8. Feil i (data og programvare) integritet
- qqq
9. Utilstrekkelig logging og overvåking
- qq
10. Server side request forgery
- q

#### Forelesning 10 - Datanettsikkerhet og cyberoperasjoner
Oversikt:
- Brannmur
- Inntrengningsdeteksjon
- Hva en SOC er
- TLS-inspeksjon
- Cyberoperasjoner - Defensive vs offensive
- Cyber kill chain
- Avanserte trusselaktører / advanced persistent threat (APT)
- MITRE ATT & CK rammeverket

Brannmurer (ser på skilt)
- En brannmur er et sjekkpunkt som beskytter de interne nettverkene mot angrep fra eksterne nettverk.
- Sjekkpunktet bestemmer hvilken trafikk som kan passere inn og ut basert på regler.
Tilstandsløse brannmurer
- Enkleste type brannmur som inspiserer pakkehoder på transport- og internett-laget og basert på dette bestemmer om pakke skal godtas eller avvises.
- bruker for eksempel IPadresse, portnummer, type transportprotokoll
- Iptables er et mye brukt pakkefilter for Linux
	- ```iptables -A FORWARD -s 131.124.123.22 -j ACCEPT```
	- ```iptables -IN -s uio.no --dport 80 -j DROP
- Alle pakker fra (kilde) ip-adresse

Tilstandsbaserte brannmurer (ser hvem som kommer inn og ut)
- Har oversikt over tilstanden i hver forbindelse / økt mellom klient og tjener
- Kan opprette midlertidige regler for spesifikt økt
- Mer fleksibilitet og høy ytelse men krever mye minne for å huske tilstand
	- iptables -A forward -m state
		- --state ESTABLISHED, RELATED -j ACCEPT
	- Aksepterer alle pakker som tilhører en etablert TCP-forbindelse eller er relatert til eksisterende UDP-kommunikasjon.

Applikasjonsbrannmur (sjekker innhold av pakkene)
- En applikasjonsbrannmur kan inspisere brukerdata i tillegg til pakkehoder
- Støtter spesifikke applikasjonsprotokoller (HTTP, FTP,)
- Kan konfiguereres for friltrering av spesifikke brukerapplikasjoner (Youtube,  facebook)
- Kan filtrere ende-til-ende-forbindelse mellom klient og tjener
	- eller i 2 deler der brannmuren spiller rollen som proxy
	- proxy tjener for klienten og proxy-klient for tjeneren
- En proxy brannmur kalles ofte en gateway og brukesi VPN som vi har sett
- Applikasjonsbrannmurer med høy ytelse kalles ofte neste generasjons brannmurer (next gen firewalls)

Inntrengningsdeteksjon
- inntrengningsdeteksjonssystemer (IDS) er systemer som forsøker å detektere mistenkelige aktivitet
- HIDS (Host-based IDS) forsøker å detektere aktivitet på vert/system den er installert
	- Overvåker prosesser, filendring
- NIDS (Network-based IDS) forsøker å detektere aktivitet på et eller flere nettverkssegment
	- Overvåker nettverkstrafikk
- Vi fokuserer på NIDS her
- To hovedkategorier: Signaturbaserte, og anomalibaserte

![[Pasted image 20231024103329.png]]


Signaturbaserte IDS:
Signaturbasert deteksjon:
- Kjente angrepssignatur (beskrivelse av kjente angrep)
- Sekvenser av systemanrop, mønstre for nettverkstrafikk, etc.
- Kan bare oppdage kjente angrep
Snort er en mye brukt signaturbasert NIDS
- Eksempel signatur:
	- alert tcp $HOME_NET any -> 10.0.0.56 22
	- (msg "SSH til IP-adresse 10.0.0.0.56")
- $HOME_NET er en variabel som (typisk) inneholder IP-adresser for eget nett (som skal beskyttes)
- Gir alarm dersom det er TCP kommunikasjon fra $HOME_NET til port 22 på IP-adresse 10.0.0.0.56

Anomalibasert IDS
- Bruker en modell for normal atferd for å oppdage avvikende atferd
- For eksempel utløses en alarm når en statistisk sjelden hendelse oppstår
- Ofte basert på ML
- Kan oppdage ukjente angrep
- ... men vil typisk gi flere falske alarmer 
- Store datamengder data
- NIDS bruker maskinlæringsmodellen
- Når systemet overvåker vil NIDS gi alarm basert på svar fra ML modellen
	- Kan for eksempel være at oppførsel observert
- Rom for alarm:
![[Pasted image 20231024104435.png]]

Sikkerhetsopperasjonssenter (SOC)
- Et team bestående av eksperter i infosec
- Organisert for å forebygge, detektere, analyse, respondere og rapportere, om cybersec.
- Flere lignende begreper som har lignende oppgaver/overlapp:
	- [CERT](CERT)(
	- In summary, CERT is a community-based program that trains volunteers in basic disaster response skills in order to provide immediate assistance during emergencies.)
	- [CIRT](CIRT)(Overall, CIRT plays a crucial role in maintaining the cybersecurity posture of an organization by promptly responding to and managing security incidents effectively.)
	- CSIRT(Computer Security Incident Response Team)

TLS-Inspeskjon
- Noen org ønsker å kunne lese kryptert HTTPS-trafikk fra ansatte
- For å bryte TLS-kryptering må gateway brannmur(proxy) utgi seg for å være ekstern tjener
- Proxy-serversertifikatet valideres automatisk av den lokale klienten, så brukeren kan tro at han/hun har TLS-tilkobling til den eksterne serveren

Hva er en cyberoperasjon?
- CyOp er et ganske vagt begrep som er angrep og forsvar (blue team, red team)
- I en militær setting snakker man ofte om offensive og defensive cyberoperasjoner
- Iffensive cyop brukes om uautorisert tilgang til informasjon og data i IKT-systemer (datainnbrudd). For eksempel statlige aktører eller kriminelle som bryter seg inn i systemer for vinningskrimintalitet eller sabotasje.
- Defensive cyop brukes om hvordan cyop brukes til å håndtere angrepene, eller trusler. 

Avanserte angrep/cyops
- CyOps brukes ofte om aktiviteter i digitale infrastrukturer utført av statlige aktører.
- Vi har sett flere tilfeller av disse mot norske mål f.eks.
	- Angrep mot Stortinget
	- Angrep mot Østre Toten kommune
	- Angrep mot 12 departementer
	- Håndterer nytt avansert cyberangrep mot Norge
- Nasjonalt digitalt risikobilde blir utgitt hvert år, hvor NSM observerer de en stor en stor økning av cyberangrep. 
- Slike angrep varer ofte over lengre tid
- Flere steg.

Cyber Kill Chain
- Utviklet av Lockheed Martin
- Beskriver trinnene i et målrettet cyberangrep
- Kill referer til at angrepet kan bli stoppet/drept i hver av disse trinnene
	- Jo tidligere desto bedre

1. Rekognisering
- Trusselaktøren velger ut det potensielle offeret
- Samler informasjon og "forsker" på det
- Forsøker å identifisere sårbarherter i nettverket som kan utnyttes
- Kan innebære skanning av infratruktur, bruk av nyheter, sosiale medier, etc.
- Eksempel:
	- Et firma velges for å uthente spesifikk informasjon for bruk i vinningskriminalitet
	- Gjennom skanning av nettverket identifiserer systemer som brukes og en gitt tjeneste har en kjent sårbarhet som kan utnyttes gjennom en makro i et PDF dokument
	- Gjennom annonser oppdages det at firmaet har en jobb ute på anbud
	- Gjennom LinkedIN oppdages en aktuell kontaktperson for anbudet som trolig har god systemtilgang

2. Bevæpning
- Trusselaktøren konstuer exploit-skadevare i et egnet format som kan leveres til offeret
- Kan f.eks. utnytte en eller flere kjente sårbarheter eller 0-days

3. Overlevering
- Skadevare som ble utviklet overleveres til målet for angrepet
- Kan f.eks være gjennom en USB, webtjener, phishing, eller andre [angrepsvektorer](angrepsvektor).

4. Utførelse av exploit
- Kjøring av exploit som utnytter sårbarhet i system til målet.

5. Installering
- Skadevare installers på systemet
- En vanlig effekt av å kjøre exploit er å få åpnet en eller annen form for tilgangspunkt (f.eks en bakdør) i form av en kommando og kontroll (K2, C2, C&C) kanal angriper kan bruke.
- Nå har angriper ekstern tilgang til det infiserte systemet.

6. Kommando og kontroll
- Angriper kan utforske nettverket rundt det infiserte systemet, forplante seg videre til andre systemer (lateral movement), skjule spor og identifisere ressurser som kan stjeles/saborteres/utnyttes.
- Kommunikasjon med angriper gjennom opprettet kanal.

7. Aksjon
- Det faktiske målet med angrepet utføres
- Dette kan være uthenting av data som betyr at data samles inn, klargjøres og sendes ut av nettverket til servere som kontrolleres av angripere.
- Det kan også være sabotasje, og i så fall blir ødeleggende aksjoner iverksatt.

APT - Advanced Persistent Threat
- Et begrep som ofte brukes i tilknytning til det illustrerte eksempelet er APT.
- En APT er en trusselaktør eller gruppering.
- Tilhører ofte, eller er ofte sponset av, nasjonalstater.
- Finnes også kriminelle APT-er uten slik tilknytning.
- En APT må sees på som en gruppering med en aktivitetsprofil.
- CyOps fra APT-er er typisk målrettede mot land og sektorer (f.eks. forsvar, finans, industri, helse, energi)
- Mye ressurser, mye etterretning, mye kompetanse, og kan utvikle exploits. Kompetanse til å utføre angrepene. Avansert.
- Vedvarende, eller persistent. De lar seg ikke stoppe til tross for at du setter kjepper i hjulene. Utholdenhet til angrep som tar lang tid, eller sakte. Skjules mest mulig, gå under radar.
- Trussel, ønsker å gjøre ting, og har kapasiteten til det.

MITRE ATT&CK
- MITRE er en amerikasnk (non-profit) organisasjon. Gjennom forsknings- og utviklingsaktiviteter støtter de mange amerikanske organisasjoner på ulike nivåer, i både offentlig og privat sektor, inkludert akademia.
- MITRE ATT&CK er en kunnskapsbase som strukturer taktikker og teknikker brukt av angripere og ulike APT-grupper.
- Inneholder mapping av ulike APT-grupper med teknikker observert av dem
	- Basert på observasjoner av faktiske hendelser
- En viktig del av rammeverket er ATT&CK-matrisen med flere tilhørende prosjekter
- ATT&CK matrisen er strukturert rundt teknikker og taktikker
- En teknikk representerer her hvordan en angriper oppnår et taktisk mål gjennom å utføre en handling.
	- Dette kan for eksempel være phshing
	- En teknikk kan deles opp i under-teknikker
- En taktikk representerer her hvorfor en teknikk utføres, med andre ord målet til en angriper.
	- For eksempel er "tilgang til et system" en taktikk.
- Hver kolonne i ATT&CK matrisen ser man taktikk med teknikker. 
- MITRE ATT&CK og APT-er:
	- Holder styr på ulike grupper/APT-er
	- Mapper grupper til observerte teknikker i ATT&CK-matrisen

