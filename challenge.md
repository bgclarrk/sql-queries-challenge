# Congratulations, Secret Agent


You have been chosen to help us discover and track aliens around the universe.

Before we can go public with our UFO findings, we need all the data we can get. That is where you come in. 

---

We have a little information for you, but we need to get organized. We need YOU to collect and store data on aliens, the UFOs (or spaceship) they are using, and the planets they come from.

In your terminal, create a sqlite3 database to hold all of this information.

We need to keep track of aliens, spaceships, and planets. 

Aliens will have a name, color, age, and a dangerous attribute that is either true or false. Aliens should belong to a spaceship.

Spaceships will have a name, a speed, a description, and should belong to a planet and have many aliens aboard.

A planet should have a name and a distance from Earth in Light-Years. It should also have many spaceships (and many aliens through spaceships)


Once you have the database set up, start gathering data. Here is what we know so far:

---

**Known Aliens**

name: Dalek, color: blue, age: 200, dangerous: false, belongs to the Bebop spaceship

---

**Known Spaceships**

name: Bebop, speed: 450, description: shaped like a cowboy hat, is from the Gliese planet

---

**Known Planets**

name: Gliese, distance: 25

---

You are in charge of adding more information! Try using the Faker Gem in IRB to fake some more planets, aliens, and spaceships! Don't stress about making Alien sounding names.


Once you have gathered your data, now you need to teach us non-techies how to access your work. I need to be able to:

- return the names and colors of all the aliens that are 'blue'

SELECT aliens.name, aliens.color
FROM aliens
WHERE color = "blue";

- return the names and ages of all aliens over the age of 100

SELECT aliens.name, aliens.age
FROM aliens
WHERE age > 100;

- return the names of the dangerous aliens

SELECT aliens.name
FROM aliens
WHERE dangerous = true;

- return all of the info about the fastest spaceship

SELECT *
FROM spaceships
ORDER BY speed DESC
LIMIT 1;

- return a list of the aliens aboard the fastest spaceship

SELECT aliens.name
FROM aliens
INNER JOIN spaceships
ON aliens.spaceship_id = spaceships.id
ORDER BY speed DESC
LIMIT 1;

- return a list of all aliens and the spaceship they belong to

SELECT aliens.name AS alien_name, spaceships.name AS spaceship_name
FROM aliens
INNER JOIN spaceships
ON aliens.spaceship_id = spaceships.id;

- get a list of all aliens and the planets they belong to 

SELECT aliens.name AS alien_name, planets.name AS planet_name
FROM aliens
INNER JOIN spaceships
ON aliens.spaceship_id = spaceships.id
INNER JOIN planets
ON spaceships.planet_id = planets.id;

- get a list of all aliens aboard a the spaceship named 'Beebop'

SELECT aliens.name
FROM aliens
INNER JOIN spaceships
ON aliens.spaceship_id = spaceships.id
WHERE spaceships.name = "Beebop";

- get a list of all aliens from the planet named 'Gliese'

SELECT aliens.name
FROM aliens
INNER JOIN spaceships
ON aliens.spaceship_id = spaceships.id
INNER JOIN planets
ON spaceships.planet_id = planets.id
WHERE planets.name = "Gliese";

- return each planet's name and how many spaceships are from each planet

SELECT planets.name, COUNT(spaceships.name) AS number_of_spaceships
FROM planets
INNER JOIN spaceships
ON spaceships.planet_id = spaceships.id
GROUP BY spaceships.name;

- return each spaceships's name and how many aliens are aboard each spaceship

SELECT spaceships.name, COUNT(aliens.name) AS number_of_aliens
FROM spaceships
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
GROUP BY spaceships.name;

- return each planet's name and how many aliens are from each planet

SELECT planets.name, COUNT(aliens.name)
FROM planets
INNER JOIN spaceships
ON planets.id = spaceships.planet_id
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
GROUP BY planets.name;

- order the planets from most number of aliens to least number of aliens

SELECT planets.name, COUNT(aliens.name) AS number_of_aliens
FROM planets
INNER JOIN spaceships
ON planets.id = spaceships.planet_id
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
GROUP BY planets.name
ORDER BY number_of_aliens DESC;

- return the names of spaceships that have blue aliens aboard

SELECT spaceships.name
FROM spaceships
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
WHERE aliens.color = "blue"
GROUP BY spaceships.name;

- return a count of all spaceships from a planet and the total number of aliens from that planet

SELECT planets.name, COUNT(aliens.name) AS number_of_aliens, COUNT(spaceships.name) AS number_of_spaceships
FROM planets
INNER JOIN spaceships
ON planets.id = spaceships.planet_id
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
GROUP BY planets.name;

- order the planets based on how many aliens are from that planet

SELECT planets.name, COUNT(aliens.name) AS number_of_aliens
FROM planets
INNER JOIN spaceships
ON planets.id = spaceships.planet_id
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
GROUP BY planets.name
ORDER BY number_of_aliens DESC;

- MOST DIFFICULT: order the planets based on how many aliens over the age of 100 are from that planet

SELECT planets.name, COUNT(aliens.name) AS number_of_aliens
FROM planets
INNER JOIN spaceships
ON planets.id = spaceships.planet_id
INNER JOIN aliens
ON spaceships.id = aliens.spaceship_id
WHERE aliens.age > 100
GROUP BY planets.name
ORDER BY number_of_aliens DESC;


Deliver your report by the end of the study group!
