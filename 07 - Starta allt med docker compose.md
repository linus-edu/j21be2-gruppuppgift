Starta allt med docker compose
==============================

Målet med uppgiften
-------------------

Det ska gå att hämta ut repot för gruppuppgiften och köra igång alla komponenter med docker compose, utan att 
behöva göra några extra steg eller ha någnting annat än docker-compose (och docker) installerat.

Vad som ska göras
-----------------

Den här uppgiften påbörjades redan i deluppgift 1, så om ni har fortsatt att använda docker och docker 
compose för att göra resten av uppgifterna så är det troligtvis inte mycket att göra. 

### 1. Bygg allt med Docker

De egenbyggda komponenterna api, frontend och receipt-service ska ha varsin Dockerfile för att bygga respektive projekt.

- Eftersom samtliga är spring-projekt så är Dockerfilerna troligtvis nästan likadana.

Se till att komponenterna går att bygga med docker direkt efter att ha hämtat ut projektet.

- Det är lätt hänt att docker-bygget beror på någnting som har gjorts lokalt, som att bygga det 
  med maven eller IntelliJ IDEA utanför docker.

### 2 Bygg och starta allt med docker compose

De komponenter som ska köras igång i docker-compose.yaml är:
* frontend
* api
* receipt-service
* RabbitMQ
* Databas (MySQL eller PostgreSQL)

De egenbyggda komponenterna: frontend, api och receipt-service ska byggas när compose-filen körs, 
dvs. det ska stå `build: ...` istället för `image: ...` på dem i docker-compose.yaml

Ett bra sista test att är att checka ut en färsk kopia av repositoryt, köra docker compose up, och kontrollera att allt verkar fungera
