API-dokumentation
=================

Uppgiften går ut på att dokumentera API:t på ett standardiserat sätt (OpenAPI/Swagger)

### Vad som ska dokumenteras

**För varje endpoint som hanteras av APIt**

* GET /items
* POST /items
* GET /items/:id
* POST /items/buy
* GET /customers
* POST /customers
* GET /customers/:id
* GET /orders
* GET /orders/customerId
* POST /login

(era kanske inte ser ut exakt såhär)

**Så dokumentera**

* HTTP-metoden (GET eller POST)
* Pathen
* En kort kommentar om vad endpointen gör (summary)
* Path-parametrar som (T.ex. customerId)
* Request- och response-body
* Svarskoder när requesten går bra

### Antingen: Skriv för hand

OpenAPI/Swagger går bra att skriva för hand. För att lättare se till att det blir 
rätt kan det göras i online-editorn: https://editor.swagger.io/

Dokumentationen ska göras som en swagger-specifikation skriven i yaml.

Lägg den färdiga dokumentationsfilen högst upp i repositoryt: `api-swagger.yaml`

### Eller: Autogenerera

Ett alternativ till att skriva för hand är att lägga till ett spring-dependency som genererar 
dokumentation baserat på koden och annoteringar.

* Fördel - Det går mycket snabbare att generera dokumentationen, när det väl är uppsatt
* Fördel - Dokumentationen kommer stämma med koden
* Nackdel - Koden måste göras innan specifikationen, så vi kan inte använda det till att skissa på ett API
* Nackdel - Det blir väldigt mycket annoteringar i koden
* Nackdel - Är bara för spring-projekt

Information om att autogenerera https://springdoc.org/
