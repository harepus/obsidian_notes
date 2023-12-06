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

2. Teori
a) Hva er primærnøkkelen i relasjonen Ansatt? Hva med relasjonen AnsattDeltarIProsjekt?
Primærnøkkel for Ansatt er ansattnr, mens i AnsattDeltarIProsjekt har vi en CONSTRAINT deltar_pk som tar ansattnr og prosjektnummer. Dette er primærnøkkelen.
b) Hva er nøkkeøattributtene i relasjonen Ansatt? Hva med relasjonen AnsattDeltarIProsjekt?

c) Har relasjonen Ansatt en kandidatnøkkel? I så fall, hva er kandidatnøkkelen?

d) Hva er supernøklene i relasjonen Ansatt?

3. INSERT - Fyll tabellene med data. Skriv INSERT-setninger som gjør det mulig å teste noen av SELECT-setningene som skal skrives i neste oppgave. 
