Dockerize
---------

#### Förbered projektstrukturen

Se till att API:t ligger i en separat katalog, eftersom det annars blir svårt att lägga till andra java-services

Förslag på projektstruktur: https://github.com/linus-edu/j21be2-trava
Dvs. varje java-komponent ligger i separata kataloger, i dessa finns också varje komponents Dockerfile
I rootkatalogen finns docker-compose.yml för att köra igång allt

#### Skriva en Dockerfile för APIt

* Lägg till en Dockerfile som packeterar API-projektet som en docker image
* Projektet ska gå att bygga från ett nytt utcheckat git-projekt, utan att manuellt ha kört maven först:

docker build -t webshop-api .

* Så att det går att köra med:

docker run -d --rm -p 8080:8080 --name api webshop-api


#### Lägg till en docker-compose.yml

Lägg till att starta ert api och databasen (PostgreSQL eller MySQL).
Att köra igång allt med compose återkommer som en senare uppgift, men det är smidigt att använda, så lika bra att lägga till på en gång.
