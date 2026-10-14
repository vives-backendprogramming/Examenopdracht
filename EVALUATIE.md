## 🏆 Evaluatie

Alle ingediende code wordt volledig **geëvalueerd**. Je bent verantwoordelijk voor alle ingediende code en moet ze volledig kunnen verklaren.  
De focus ligt op het leveren van een **volledig werkende, foutloze backendapplicatie** die voldoet aan alle functionele en niet-functionele vereisten.

### 1️⃣ Functionele werking
- De backendapplicatie moet **volledig operationeel** zijn:
    - de applicatie start probleemloos op in de ontwikkelomgeving;
    - alle endpoints functioneren correct, inclusief CRUD-operaties, filtering, security en de integratie met de externe API;
    - er mogen **geen 5xx-fouten** optreden tijdens gebruik. Enige uitzondering is een `502 Bad Gateway` wanneer de externe API effectief onbereikbaar is of een fout teruggeeft.
- Functionaliteit die **onvolledig** is of waarbij 5xx-fouten optreden, wordt als **onvoldoende afgewerkt** beschouwd.

### 2️⃣ Testen
- **Tests** zijn verplicht voor alle controllers, voor alle niet-standaard repository-queries en voor de client van de externe API.
- Een endpoint dat niet volledig getest is, wordt als **onvoldoende afgewerkt** beschouwd.
- Tests moeten zowel **happy flows** als **error/edge cases** afdekken.
- Tests draaien zonder extra setup, los van de productiedatabase en de echte externe API.
- Beveiligde endpoints (authenticatie en autorisatie) moeten getest zijn op correcte toegang voor verschillende rollen, inclusief `401`- en `403`-responses.

### 3️⃣ REST API en documentatie
- De REST API moet **conform de best practices** van HTTP en REST zijn:
    - correcte HTTP-methodes (`GET`, `POST`, `PUT`, `DELETE`);
    - juiste statuscodes (`200`, `201`, `400`, `401`, `403`, `404`, …);
    - duidelijke en consistente endpoint-structuur;
    - server-side validatie van alle input en een consistente foutafhandeling.
- **Swagger/OpenAPI-documentatie** moet volledig zijn en toegankelijk in de applicatie:
    - alle endpoints gedocumenteerd;
    - welke endpoints beveiligd zijn en voor welke rollen toegankelijk.

### 4️⃣ Security
- De applicatie moet beveiligd zijn en beschikt over **minstens twee rollen**.
- Security wordt geëvalueerd op:
    - correcte implementatie van authenticatie en autorisatie met JWT;
    - veilige opslag van wachtwoorden (BCrypt);
    - een gebruiker kan zichzelf bij registratie geen hogere rol toekennen;
    - correcte rolgebaseerde toegang tot endpoints;
    - aanwezigheid van **standaardgebruikers** voor beide rollen.

### 5️⃣ Profielen
- Correct gebruik van **minstens twee Spring-profielen** (`dev` en `prod`) met **afzonderlijke databases**.
- De profielen moeten correct geconfigureerd zijn zodat de applicatie probleemloos in verschillende omgevingen kan draaien.

### 6️⃣ Clean code
- Leesbaarheid, consistentie en structuur van de code worden beoordeeld:
    - duidelijke package-structuur;
    - betekenisvolle namen voor classes, methoden en variabelen;
    - correcte scheiding van lagen (controller, service, repository, model) en gebruik van DTO's;
    - naleving van best practices in Java en Spring Boot.

### 7️⃣ Build
- De applicatie moet probleemloos **gebuild** kunnen worden **inclusief alle tests** (`mvn clean verify` geeft `BUILD SUCCESS`, zonder tests over te slaan).
- De applicatie start probleemloos op onder **elk profiel** (`dev` en `prod`).

### 8️⃣ Mondelinge verdediging
Tijdens het mondeling examen wordt geëvalueerd in welke mate je jouw applicatie kunt toelichten en verdedigen. 

Je moet kunnen uitleggen hoe de verschillende onderdelen van je applicatie werken, welke technische keuzes je hebt gemaakt, hoe de code is opgebouwd en hoe de belangrijkste functionaliteiten werden geïmplementeerd. Je kan je ontwerpkeuzes in domeinmodel, architectuur, security, integratie, ... toelichten en verdedigen. 
 
Het is hierbij niet voldoende dat de applicatie correct functioneert. Je moet ook kunnen aantonen dat je de ingediende code begrijpt en zelfstandig kunt verklaren. Dit geldt eveneens voor code die met behulp van AI-tools, online bronnen of andere hulpmiddelen tot stand is gekomen. Wanneer je niet in staat bent om essentiële onderdelen van je eigen project toe te lichten of vragen over de implementatie te beantwoorden, kan dit erop wijzen dat je de gebruikte oplossing niet zelf begrijpt of zelfstandig hebt uitgewerkt.
In dat geval kun je, ongeacht de kwaliteit van de ingediende applicatie en code, geen voldoende behalen voor deze opdracht. 

Een werkende applicatie alleen is immers onvoldoende bewijs van de vereiste competenties; je moet ook kunnen aantonen dat je de gebruikte technieken begrijpt en zelfstandig kunt toepassen.

> Een perfect uitgewerkte Java Spring Boot backend is nog maar je ingangsticket tot de mondelinge verdediging.
