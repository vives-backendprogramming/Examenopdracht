# 🎓 Examenopdracht: Spring Boot Backend

## 🧾 Opdrachtomschrijving
Ontwikkel een **backendapplicatie** met behulp van **Spring Boot 4** en **Java 25** die een **REST API** voorziet voor een mobiele app.  
De ontwikkelde REST API zal dienen als **backend** voor de mobiele applicatie die je (eventueel) ontwikkelt binnen het vak **Cross-Platform Development**.

De opdracht bouwt verder op de technieken uit de cursus [spring-boot-backend-course](https://github.com/vives-backendprogramming/spring-boot-backend-course).

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
- De controller die de entiteit aan de **één-kant** van de één-op-veel-relatie (de parent) beheert, bevat een **volledige CRUD-functionaliteit**:

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

### 🌍 Externe API
De backend roept **minstens één externe REST API** aan, en gebruikt die gegevens op een zinvolle manier in het eigen domein (bijv. gegevens opzoeken, aanvullen of importeren).
- De externe API wordt aangeroepen via een HTTP-client van Spring, bij voorkeur een **declaratieve client** (`@HttpExchange`) of `RestClient`.
- De configuratie (base URL, eventuele API-key, …) staat in de configuratie, niet hardcoded in de code. Een API-key of ander geheim komt **niet** in de GitHub-repository terecht.
- Er zijn **timeouts** ingesteld (connect en read).
- Fouten van de externe API worden netjes afgehandeld en vertaald naar eigen exceptions en correcte HTTP-statuscodes, bijvoorbeeld:
    - `422 Unprocessable Content` wanneer de externe API onbruikbare of onvolledige gegevens teruggeeft;
    - `502 Bad Gateway` wanneer de externe API niet bereikbaar is of zelf een fout teruggeeft.

## 🔒 Security

Beveiliging vormt een essentieel onderdeel van de backendapplicatie.  

### 🔐 Authenticatie met JWT
De authenticatie en autorisatie gebeuren met **JWT** (JSON Web Token). Er wordt **geen externe identity provider** (OAuth2/OIDC) gebruikt.

- De applicatie beheert zelf de gebruikers: gebruikersnamen en wachtwoorden worden in de database bewaard, de wachtwoorden **versleuteld met BCrypt** (nooit in plain text).
- De applicatie voorziet eigen authenticatie-endpoints voor **registratie** en **login**.
- Na een geslaagde login ontvangt de gebruiker een JWT, dat bij elke request wordt meegestuurd in de header `Authorization: Bearer <token>`.
- De applicatie valideert het token (handtekening en vervaldatum) en geeft enkel toegang aan geauthenticeerde gebruikers met de juiste rol.
- De geheime sleutel en de geldigheidsduur van het token staan in de configuratie, niet hardcoded in de code.

### 👥 Rollen en autorisatie
In de applicatie zijn **minstens twee gebruikersrollen** voorzien.
Deze rollen worden opgenomen in het JWT dat aan de backend wordt doorgestuurd.  
Op basis van deze rollen worden endpoints afgeschermd in de applicatie.

Sommige endpoints zijn enkel toegankelijk voor gebruikers met een specifieke rol.  
Andere endpoints zijn afgeschermd en enkel beschikbaar voor een andere rol.

Voor beide rollen moet er een **standaardgebruiker** met wachtwoord voorzien zijn, die bij het opstarten van de applicatie in de database aanwezig is.
Deze standaardgebruikers en hun bijhorende inloggegevens moeten **beschreven worden in de README** van je project, zodat tijdens evaluatie eenvoudig kan ingelogd worden.

### 🔑 Beveiligde endpoints
De beveiliging van de endpoints wordt gerealiseerd via **Spring Security**.  
Er wordt gecontroleerd of een gebruiker geauthenticeerd is en of die gebruiker over de juiste rol beschikt om een bepaalde actie uit te voeren.  
De applicatie geeft correcte HTTP-statuscodes terug:
- `401 Unauthorized` bij een ontbrekend, ongeldig of verlopen token, en bij een mislukte login;
- `403 Forbidden` wanneer een geauthenticeerde gebruiker niet over de vereiste rol beschikt.

Alle endpoints moeten correct omgaan met toegangsrechten, tokens en foutscenario’s, zodat de applicatie veilig en betrouwbaar blijft.

## 🧪 Technische vereisten

Naast de functionele vereisten moet je backend ook aan volgende **technische criteria** voldoen.

### 🧩 Testen
- De **controller-laag** (REST API-functionaliteit) wordt **uitvoerig getest**, bijvoorbeeld met `@WebMvcTest`.  
  Hierbij test je zowel:
    - het **verwachte gedrag** (happy flow);
    - als **mogelijke foutscenario’s** (error handling, edge cases, …).
- Alle **niet-standaard databasequeries** in de **repository-laag** (eigen query methods, `@Query`, …) worden eveneens uitgebreid getest, bijvoorbeeld met `@DataJpaTest`.
- De **client voor de externe API** wordt getest zonder de echte externe API aan te roepen, bijvoorbeeld met `@RestClientTest`, zowel voor een geslaagde call als voor de foutscenario's.
- De **beveiligde endpoints** worden getest om na te gaan of:
    - enkel geauthenticeerde gebruikers toegang krijgen;
    - enkel gebruikers met de juiste rol bepaalde acties kunnen uitvoeren;
    - foutieve of ontbrekende tokens correct leiden tot `401 Unauthorized` of `403 Forbidden` responses.
- Elke test maakt via een duidelijke naam (of `@DisplayName`) duidelijk welk gedrag getest wordt, en controleert dat gedrag met assertions.

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

De volledige applicatie kan worden uitgevoerd in **Docker-containers**, inclusief de backend en de database.  
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
- Alle tests moeten foutloos runnen.

### 5. Deadline
- Je vindt de deadline terug op Toledo.
- Het project moet vóór de opgegeven deadline **volledig** op je GitHub repository staan.
- Controleer dat alle vereiste bestanden aanwezig zijn en dat de README up-to-date is.

## 🏆 Evaluatie

[EVALUATIE.md](EVALUATIE.md)
