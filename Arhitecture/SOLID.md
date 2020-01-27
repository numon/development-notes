# S.O.L.I.D. STANDS FOR:
S — Single responsibility principle 

O — Open closed principle

L — Liskov substitution principle

I — Interface segregation principle

D — Dependency Inversion principle


## Single responsibility principle
A class should have one and only one reason to change, meaning that a class should only have one job.
Every function you write should do exactly one thing. It should have one clearly defined goal.
Can use function factory

Let’s say for every user that logs in you always need to fetch their favorite music, favorite TV shows and favorite music.  
We now know that you’ll want to divide them up to getShows(), getMovies() and getMusic() functions.
But what if those functions are almost always called together. 
We don’t want to create a getShowsAndMoviesAndMusic() function. But we also don’t want call all 3 different functions every time either.
In order to not repeat ourselves, it’s ok to create one wrapping function which encapsulates all 3. 
I would call it getUserMedia(). This isn’t cheating as long as getUserMedia() is comprised out of 3 independent pure functions

## Open-closed Principle
Objects or entities should be open for extension, but closed for modification.
Open-Closed Principle means our JavaScript modules should be open to extension, but closed to modification.
In simpler words, means that a class or factory function in our case, 
should be easily extendable without modifying the class or function itself
Can use function composition

## Liskov substitution principle
