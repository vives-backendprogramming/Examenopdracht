## 🏆 Evaluatie

Alle ingediende code wordt volledig **geëvalueerd** en moet door de student zelf zijn geschreven.  
De focus ligt op het leveren van een **volledig werkende, foutloze backendapplicatie** die voldoet aan alle functionele en niet-functionele vereisten.

### 1️⃣ Functionele werking
- De backendapplicatie moet **volledig operationeel** zijn:
    - de applicatie start probleemloos op in de ontwikkelomgeving;
    - alle endpoints functioneren correct, inclusief CRUD-operaties, filtering en security;
    - er mogen **geen 5xx-fouten** optreden tijdens gebruik.
- Functionaliteit die **onvolledig** is of waarbij 5xx-fouten optreden, levert maximaal **50% van de punten** voor die specifieke feature op.

### 2️⃣ Testen
- **Unit tests** zijn verplicht voor alle controllers en repository-methodes.
- Een endpoint dat niet volledig getest is, wordt als **half afgewerkt** beschouwd; dit betekent maximaal **50% van de punten** voor dat endpoint.
- Tests moeten zowel **happy flows** als **error/edge cases** afdekken.
- Beveiligde endpoints (authenticatie en autorisatie) moeten getest zijn op correcte toegang voor verschillende rollen.

### 3️⃣ REST API en documentatie
- De REST API moet **conform de best practices** van HTTP en REST zijn:
    - correcte HTTP-methodes (`GET`, `POST`, `PUT`, `DELETE`);
    - juiste statuscodes (`200`, `201`, `400`, `401`, `403`, `404`, …);
    - duidelijke en consistente endpoint-structuur.
- **Swagger/OpenAPI-documentatie** moet volledig zijn en toegankelijk in de applicatie:
    - alle endpoints gedocumenteerd;
    - welke endpoints beveiligd zijn en voor welke rollen toegankelijk;

### 4️⃣ Security
- De applicatie moet beveiligd zijn en beschikt over **minstens twee rollen**.
- Security wordt geëvalueerd op:
    - correcte implementatie van authenticatie en autorisatie;
    - correcte rolgebaseerde toegang tot endpoints;
    - aanwezigheid van **standaardgebruikers** voor beide rollen.

### 5️⃣ Profielen
- Correct gebruik van **minstens twee Spring-profielen** (`dev` en `prod`) met **afzonderlijke databases**.
- De profielen moeten correct geconfigureerd zijn zodat de applicatie probleemloos in verschillende omgevingen kan draaien.

### 6️⃣ Clean code
- Leesbaarheid, consistentie en structuur van de code worden beoordeeld:
    - duidelijke package-structuur;
    - betekenisvolle namen voor classes, methoden en variabelen;
    - correcte scheiding van lagen (controller, service, repository, model);
    - naleving van best practices in Java en Spring Boot.

### 7️⃣ Build
- De applicatie moet probleemloos **gebuild** kunnen worden (`BUILD SUCCESS`) en starten in een ontwikkelomgeving.

### 8️⃣ Mondelinge verdediging
Tijdens het mondeling examen wordt geëvalueerd in welke mate je jouw applicatie kunt toelichten en verdedigen. 

Je moet kunnen uitleggen hoe de verschillende onderdelen van je applicatie werken, welke technische keuzes je hebt gemaakt, hoe de code is opgebouwd en hoe de belangrijkste functionaliteiten werden geïmplementeerd. Je kan je ontwerpkeuzes in domeinmodel, architectuur, security, integratie, ... toelichten en verdedigen. 
 
Het is hierbij niet voldoende dat de applicatie correct functioneert. Je moet ook kunnen aantonen dat je de ingediende code begrijpt en zelfstandig kunt verklaren. Dit geldt eveneens voor code die met behulp van AI-tools, online bronnen of andere hulpmiddelen tot stand is gekomen. Wanneer je niet in staat bent om essentiële onderdelen van je eigen project toe te lichten of vragen over de implementatie te beantwoorden, kan dit erop wijzen dat je de gebruikte oplossing niet zelf begrijpt of zelfstandig hebt uitgewerkt.
In dat geval kun je, ongeacht de kwaliteit van de ingediende applicatie en code, geen voldoende behalen voor deze opdracht. 

Een werkende applicatie alleen is immers onvoldoende bewijs van de vereiste competenties; je moet ook kunnen aantonen dat je de gebruikte technieken begrijpt en zelfstandig kunt toepassen.

> Een perfect uitgewerkte Java Spring Boot backend is nog maar je ingangsticket tot de mondelinge verdediging
