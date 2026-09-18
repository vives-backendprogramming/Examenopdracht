# 🎓 Examenopdracht: Spring Boot Backend

## 🧾 Opdrachtomschrijving
Ontwikkel een **backendapplicatie** met behulp van **Spring Boot 4** en **Java 25** die een **REST API** voorziet voor een mobiele app.  
De ontwikkelde REST API zal dienen als **backend** voor de mobiele applicatie die je (eventueel) ontwikkelt binnen het vak **Cross-Platform Development**.

Je krijgt **veel vrijheid** bij het uitwerken van deze opdracht.  
Zo bepaal je zelf:
- hoe het **domeinmodel** van je backend (en bij uitbreiding je mobiele app) eruitziet;
- welke **gegevens** je applicatie aanbiedt;
- en hoe de verschillende **entiteiten** en **relaties** vorm krijgen.

> 💡 Denk na over een domein dat je interesseert of aansluit bij je mobiele app-idee. Een goed gekozen domein maakt het makkelijker om gemotiveerd te blijven en een sterk eindresultaat neer te zetten.

## ⚙️ Vereisten

Hoewel je veel vrijheid krijgt in de keuze van het domein en de uitwerking van je backend, moet je applicatie wél voldoen aan onderstaande **specificaties**.

### 🔗 REST API
Alle endpoints moeten voldoen aan de standaardprincipes van een **REST API**:
- Gebruik van de correcte **HTTP-methodes** (`GET`, `POST`, `PUT`, `DELETE`, …)
- Duidelijke en consistente **naamgeving** van de endpoints
- Correct gebruik van **HTTP-statuscodes**
- Correct gebruik van **headers**, **queryparameters** en **request-objecten**

### 🧩 Domeinmodel
- Het domeinmodel bevat **minstens 3 entiteiten**.
- Tussen minstens 2 entiteiten bestaat een **één-op-veel**-relatie.
- Je mag uiteraard meer dan 3 entiteiten uitwerken indien dat nuttig is voor je domein.

### 💾 Persistentie
- De entiteiten worden **gepersisteerd** 
- Je kiest zelf het type database (**relationeel** of **non-relationeel**) en de gebruikte persistentietechnologie (bijv. JPA, JDBC, MongoDB, ...).
- Op je productie-omgeving gebeurt je persistentie **on disk**, voor de ontwikkelomgeving mag dit **in-memory** zijn (hoeft niet)

### 🧱 Architectuur
- De applicatie wordt opgedeeld in **verschillende lagen** (bijv. controller, service, repository, model, …).

### 🚀 Controllers
- Je applicatie bevat **minstens 2 controllers**, elk verantwoordelijk voor een specifieke entiteit.
- De controller die de **één-op-veel**-entiteit beheert, bevat een **volledige CRUD-functionaliteit**:

| Actie | Beschrijving |
|-------|---------------|
| **C** | Nieuwe resource aanmaken |
| **R** | Volledige lijst teruggeven <br> Filteren/zoeken in lijst <br> Eén resource ophalen |
| **U** | Aanpassen van een bestaande resource |
| **D** | Verwijderen van een bestaande resource (rekening houdend met child records) |

- De tweede controller mag beperkter zijn en hoeft niet de volledige CRUD te implementeren.
- Indien nuttig mag je uiteraard **extra controllers** voorzien.

### ✅ Validatie
Alle **data** die naar de REST API wordt doorgestuurd, moet **server-side gevalideerd** worden.

## 🔒 Security

Beveiliging vormt een essentieel onderdeel van de backendapplicatie.  

De authenticatie en autorisatie gebeuren
- of met behulp van **JWT** 
- of via **OAuth2** met **OpenID Connect (OIDC)**, waarbij gebruik wordt gemaakt van **Dex** als identity provider.

### 🔐 Indien authenticatie met JWT
De backendapplicatie maakt gebruik van **JWT** voor authenticatie en autorisatie.
De applicatie beheert zelf de gebruikersnamen en versleutelde wachtwoorden, en voorziet eigen authenticatie-endpoints voor login en registratie.
Gebruikers loggen in en ontvangen een JWT-token, dat bij elke request wordt meegestuurd.
De applicatie valideert het token en geeft enkel toegang aan geauthenticeerde gebruikers met de juiste rol.

### 🔐 Indien authenticatie met Dex
De backendapplicatie maakt gebruik van **Dex** als OIDC-provider.  
Dex wordt uitgevoerd in een **Docker-container** en beheert de gebruikers, tokens en sessies.  
De applicatie vertrouwt op Dex om geldige JWT-tokens uit te geven en te verifiëren.  
De configuratie van Dex bevat de clients, gebruikers en instellingen die nodig zijn om de verbinding met de Spring Boot-applicatie mogelijk te maken.

### 👥 Rollen en autorisatie
In de applicatie zijn **minstens twee gebruikersrollen** voorzien.
Deze rollen worden opgenomen in het JWT-token dat aan de backend wordt doorgestuurd.  
Op basis van deze rollen worden endpoints afgeschermd in de applicatie.

Sommige endpoints zijn enkel toegankelijk voor gebruikers met een specifieke rol.  
Andere endpoints zijn afgeschermd en enkel beschikbaar voor een andere rol.

Voor beide rollen moet er een **standaardgebruiker** voorzien zijn met wachtwoord. 
Deze standaardgebruikers en hun bijhorende inloggegevens moeten **beschreven worden in de README** van je project, zodat tijdens evaluatie eenvoudig kan ingelogd worden.

### 🔑 Beveiligde endpoints
De beveiliging van de endpoints wordt gerealiseerd via **Spring Security**.  
Er wordt gecontroleerd of een gebruiker geauthenticeerd is en of hij over de juiste rol beschikt om een bepaalde actie uit te voeren.  
De applicatie geeft correcte HTTP-statuscodes terug bij niet-geautoriseerde of niet-geauthenticeerde requests.

Alle endpoints moeten correct omgaan met toegangsrechten, tokens en foutscenario’s, zodat de applicatie veilig en betrouwbaar blijft.

## 🧪 Technische vereisten

Naast de functionele vereisten moet je backend ook aan volgende **technische criteria** voldoen.

### 🧩 Testen
- De **controller-laag** (REST API-functionaliteit) wordt **uitvoerig getest** met **unittests**.  
  Hierbij test je zowel:
    - het **verwachte gedrag** (happy flow);
    - als **mogelijke foutscenario’s** (error handling, edge cases, …).
- Alle **niet-standaard databasequeries** in de **repository-laag** worden eveneens uitgebreid getest via unittests.
- De **beveiligde endpoints** worden getest om na te gaan of:
    - enkel geauthenticeerde gebruikers toegang krijgen;
    - enkel gebruikers met de juiste rol bepaalde acties kunnen uitvoeren;
    - foutieve of ontbrekende tokens correct leiden tot `401 Unauthorized` of `403 Forbidden` responses.
- Voor elke testbare component wordt het verwachte gedrag gedocumenteerd en gevalideerd.

### 📘 API-documentatie
- De volledige REST API wordt **gedocumenteerd met Swagger** (OpenAPI).  
  Dit maakt het mogelijk om alle endpoints eenvoudig te verkennen en te testen.
- In de Swagger-documentatie moet duidelijk aangegeven zijn:
    - welke endpoints authenticatie vereisen;
    - welke rollen toegang hebben tot elk endpoint;
- De Swagger-UI moet ook bruikbaar zijn in combinatie met de securityconfiguratie, zodat geauthenticeerde requests kunnen worden uitgevoerd met een geldig token.

### ⚙️ Profielen
De applicatie maakt gebruik van **minstens twee Spring-profielen**, bijvoorbeeld `dev` en `prod`.  
Elk profiel vertegenwoordigt een **afzonderlijke runtime-omgeving**.

- Voor elk profiel is een **eigen database** voorzien.  
  De `dev`-omgeving gebruikt een afzonderlijke ontwikkelingsdatabase die veilig mag worden overschreven of herstart.  Dit mag in-memory zijn, maar hoeft niet.
  De `prod`-omgeving gebruikt een **aparte productiedatabase** met eigen connectieparameters en gegevens. Deze database is on-disk.
- De databanken mogen zowel lokaal als in de cloud worden gehost, zolang ze **duidelijk gescheiden** zijn.
- Het gekozen actieve profiel bepaalt automatisch welke databankverbinding en instellingen worden gebruikt bij het opstarten van de applicatie.
- De applicatie wordt publiek beschikbaar gesteld voor de mobiele app onder het productie profiel.

> 💡 Tip: documenteer in de README hoe de profielen worden geactiveerd en hoe de bijhorende databases geconfigureerd zijn, zodat tijdens evaluatie eenvoudig kan overgeschakeld worden tussen `dev` en `prod`.

### 🐳 Docker en containerisatie

De volledige applicatie kan worden uitgevoerd in **Docker-containers**, inclusief de backend, de database en eventueel de Dex identity provider.  
Het doel is dat de volledige stack eenvoudig kan worden gedeployed en getest, met alle componenten gescheiden maar verbonden via een Docker-netwerk.

### ☁️ Clouddeploy
- Je applicatie is tijdens de periode tussen het **indienen** en de **mondelinge verdediging publiek beschikbaar in de cloud**.
- Kies zelf de cloudomgeving (bijv. Render, Railway, Heroku, Azure, AWS, …).

## 📦 Instructies voor indienen

Bij het indienen van je examenproject moet je ervoor zorgen dat alle onderdelen volledig aanwezig zijn. Volg onderstaande richtlijnen zorgvuldig:

### 1. GitHub repository
- Het volledige project staat op de GitHub repository die je kreeg voor **Devops & Cloud Computing**

### 2. README.md
- Het project bevat een README bestand waarin het volledige project beschreven staat, instructies voor het opstarten van de applicatie en de containers, configuratie, eventuele testdata, standaardgebruikers voor beide rollen met wachtwoord, ...

Een template wordt hiervoor nog aangeleverd.

### 3. Docker en containerisatie
- Voeg een **Docker Compose-configuratie** toe waarmee de volledige stack samen kan worden opgestart.
- Controleer vooraf dat de containers correct opstarten en met elkaar kunnen communiceren.

### 4. Testen en documentatie
- Zorg dat de **Swagger-documentatie** beschikbaar is en de endpoints correct beschrijft.
- Alle unit tests moeten foutloos runnen

### 5. Deadline
- Je vindt de deadline terug op Toledo.
- Het project moet vóór de opgegeven deadline **volledig** op je GitHub repository staan.
- Controleer dat alle vereiste bestanden aanwezig zijn en dat de README up-to-date is.

## 🏆 Evaluatie

[EVALUATIE.md](EVALUATIE.md)
