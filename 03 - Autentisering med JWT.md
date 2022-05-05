# Autentisering med JWT

Målet med den här uppgiften är att lägga till JWT-autentisering på API:t

Läs på om jwt: https://jwt.io/introduction


Få lite översikt över hur spring security fungerar:
https://spring.io/guides/topicals/spring-security-architecture


Den här guiden går specifikt igenom att lägga till JWT-autentisering i spring, den bör innehålla vad som behövs om uppgiften:
https://www.toptal.com/spring/spring-security-tutorial

Det som ska göras behöver inte göras i exakt ordningen som delarna är listade, det kan finnas andra ordningar som är lättare.

Det här kan vara en ganska svår uppgift, så fastna inte för mycket
Se till att projektet är i fungerande skick, så kan vi kan återkomma till det senare. Det kan vara bra att arbeta på en separat feature-branch.


### Lägg till lösenord

Lägg till en ny kolumn för att spara (hashade) lösenord för användare.
Lagra lösenorden hashade med en lämplig algoritm som bcrypt.


### Endpoint för att registrera ny användare

Lägg till en ny endpoint `POST "/sign_up"`

Som tar en JSON-body

    {
	    username: '...',
	    password: '...'
    }

och skapar en ny användare.  
Om anropet gick bra returneras HTTP-koden: `201 Created`


### Endpoint för att logga in

Lägg till en endpoint: `POST "/login"`

Den här tar en likadan request body som `"/sign_up"`, men returnerar en JWT-token om användaren finns och lösenordet är rätt.


### Slå på autentisering

Konfigurera projektet så att alla endpoints kräver en giltig JWT-token utom:
 * `/sign_up` - Annars går det inte att skapa en användare
 * `/login` - Annars går det inte att logga in
 * `/items` - För att frontend ska komma åt dem
