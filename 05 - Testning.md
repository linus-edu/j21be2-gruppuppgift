Testning
========

Uppgiften går ut på att säkerställa att komponenterna vi har satt ihop fungerar som de ska. Det kan göras med testning på olika nivåer.

### Enhetstestning
* Enhetstester ska vara små och snabba att köra
* Typiskt testas en enskild metod eller klass
* Gränsen mellan enhetstest och integrationstest är aningen flytande i spring, men det är koden i funktionen som ska testas, inte interaktionen mellan koden och spring
* En bra sak att enhetstesta är någon del av JWT-koden
* För att kunna testa koden vi är intresserade av kan den behövas brytas ut på något lämpligt sätt

##### Uppgift A
Ha minst ett rent enhetstest som inte är direkt beroende av spring

### Integrationstest

En viktig sak att testa är att autentiseringen fungerar. För att försäkra oss om det så vill
vi testa integreringen mellan delarna som ingår i autentiseringen: Autentiseringskonfigureringen 
i spring, JWT-filter, controllern som anropas osv.

##### Uppgift B
Skriv integrationstest som bekräftar att:
* Det **inte går** att komma åt `GET /customers` **utan** en giltig jwt-token, och att felkoden är `403`
* Att det **går** att komma åt `GET /customers` **med** en giltig jwt-token
* Att det **går** att komma åt `GET /items` **utan** en jwt-token

Exempel på att hämta en token i ett test:  
https://github.com/linus-edu/j21be2-trava/blob/main/api/src/test/java/se/mbi/be2/trava/api/MockMvcIntTest.java

### End-to-end test

Ett end-to-end test interagerar med systemet så som en användare skulle göra. Genom att ha ett enkelt e2e-test 
som gör några typiska anrop så kan vi få en bra indikation på att tjänsten fungerar som den ska, eller åtminstonde inte är helt trasig.

##### Uppgift C
Skriv ett enkelt automatiskt end-to-end-test som kan köras mot en fullt uppsatt stack (frontend + API + DB + RabbitMQ + receipt-service)
* Den här sortens tester hör inte till en specifik service, utan passar bättre i ett eget projekt, men för enkelhets skull kan det läggas i API-projektet
* Det här testet kan vara disablat (@Disable). När vi vill köra det mot en uppsatt miljö så kan vi enabla det tillfälligt och köra det från IDEA
* När testet körs så:
	* Gör det requests mot API:et
		* Skapar det en användare
		* Hämtar ut en JWT-token
		* Lägger till några items med JWT-token
		* Testar att göra ett köp
	* Testar att frontend ger tillbaks HTML med de items som lagts till
		* Behöver inte parsa HTMLen, vi kan bara t.ex. kolla om namnen på de items som lades till finns med i svaret
* TestRestTemplate kan användas för att göra API-anrop i testet
* Vi hoppar över att testa recepipt-service. För att testa den också så hade testet behövt bekräfta att en kvitto-PDF skapats
