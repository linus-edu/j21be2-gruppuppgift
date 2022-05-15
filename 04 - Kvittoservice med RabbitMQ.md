Kvittoservice med RabbitMQ
==========================

Målet med den här uppgiften är att lägga till en ny micro-service och koppla ihop den med API-servicen över AMQP (RabbitMQ)

Bakgrund
--------

Varje gång ett köp görs i webshoppen så ska ett kvitto mailas till köparen som ett PDF-dokument.

Eftersom det tar lite tid att generera PDF och skicka mailet så ska det göras i en separat micro-service, istället för direkt i API:t

Den här sortens asynkrona jobb passar perfekt att utföra genom att posta dem till en message-broker.
Det är då väldigt lätt att sätta upp flera lastbalanserade services vid behov och API:et behöver inte hålla koll på hur många som körs.

Vad som ska göras
-----------------

#### 1. Starta RabbitMQ med docker compose

Det kan göras genom att i `docker-compose.yml` lägga till

    rabbitmq:
	  image: "rabbitmq:3-management"
	  ports:
	    - 5672:5672
	    - 127.0.0.1:15672:15672

5672 är AMQP-porten, på 15672 kan man komma åt admin-gränssnittet.

#### 2. Skapa en ny service

Skapa en ny service (nytt java-projekt i repot): **receipt-service**

Vid uppstart kopplar receipt-service upp sig mot RabbitMQ och börjar prenumerera på en lämplig kö.

För att receipt-service ska hitta RabbitMQ både i docker och från intellij idea kan `application.properties` användas 
på samma sätt som för att konfigurera vart databasen körs:

	 spring.rabbitmq.host=${rabbitmq_host:localhost}

När ett jobb-meddelande dyker upp på kön så genererar receipt-service en PDF baserat på meddelandet. 
Det finns inga krav på hur PDFen ser ut: https://www.baeldung.com/java-pdf-creation

ReceiptService ska inte skicka mail på riktigt, den viktiga delen i uppgiften är att koppla in en ny service över AMQP

#### 3. Skicka meddelande från API:et

Varje gång någon gör ett köp genom att posta till `/items/buy` så ska API-komponenten publicera ett 
meddelande med all info som behövs för att generera och skicka kvittot i en JSON-sträng över
AMQP

API-servicen behöver inte lyssna på RabbitMQ utan bara skicka till den, men behöver konfigureras 
så att den kan koppla upp sig på samma sätt som receipt-service

#### Felsökning

Det går både att publicera och läsa meddelanden i RabbitMQs admin-sida (user,pass=guest,guest)

RabbitMQ sätter upp en default-exchange som kan användas istället för att göra egna (utifall att det krånglar)

Det finns exempelkod att titta på i https://github.com/linus-edu/j21be2-trava
