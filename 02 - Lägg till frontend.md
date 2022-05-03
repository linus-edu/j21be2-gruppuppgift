Skapa web-front service
-----------------------

Skapa ett nytt spring-boot-projekt med namnet frontend

Servicen frontend har en enkel uppgift. Den ska visa en enkel websida som innehåller alla items från API:t

frontend gör detta genom att varje gång man går in på /products så
* Hämtar den listan med alla items från API:t
* Renderar en enkel HTML-sida med alla items

#### Instruktioner för att göra GET-anrop från spring

https://attacomsian.com/blog/http-requests-resttemplate-spring-boot

#### Rendera sidan

Detta gör lämpligtvis med Thymeleaf som ni lärde er i Backend 1

#### Förbered för docker

Om både api och frontend är startade i docker, med namnen (--name) api och frontend, så kan frontend använda http://api:8080 för att göra anrop.

För att köra frontend i intellij under utveckling så får http://localhost:8080 användas för att nå APIt istället.

#### Gör API-URLen konfigurerbar

För att inte behöva ändra URLen till vårt API i koden hela tiden, använd en milövariabel. Detta görs lätt i spring med:

	@Value("${api_base_url:http://localhost:8080/}")
	private String apiBaseUrl;

Sedan kan variabeln sättas till "http://api:8080/" i docker-compose.yml (eller anges till docker run)

Gör en Dockerfile
-----------------
Lägg till en Dockerfile för att bygga en image även för den här. Om Dockerfile från api-komponenten fungerar bra så är det inte mycket som behöver ändras.
