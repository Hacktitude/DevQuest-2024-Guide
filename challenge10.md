# Challenge 10
#### Provide discount for Least rented movies.

## Overview

Some movies may not be rented as much times than other movies. In order to promote those movies and gain more revenue from them special discount was introduced for those movies.

In this challenge you need to implement this feature in `movieRepository` and `movieController` as `getLeastRentedMovies()` function.

Use following endpoint to reach to this function.
```http
GET /api/movie/least-rented
```

Following conditions need to be satisfied for a movie to be selected as least rented movie.

1. Movie should be released before a month from the time this function is called.
2. Calculate rented count for each movie and take the least 4 only.

The response from the implemented function should be as follows.

```json
[
  {
      "id": "47ef0a76-fbed-4d6f-bdd5-55ffc6506c03",
      "title": "Happy Gilmore",
      "year": 1996,
      "dailyRentalRate": 85,
      "discountRate": 0.15,
      "genres": [
          "Comedy",
          "Romance",
          "Adventure"
      ],
      "userRating": 0,
      "imdbRating": 7,
      "posterUrl": "https://posters.movieposterdb.com/07_10/1996/116483/l_116483_181afe60.jpg",
      "bannerUrl": "https://picfiles.alphacoders.com/963/96345.jpg",
      "plot": "A rejected hockey player puts his skills to the golf course to save his grandmother's house.",
      "runtime": "1h 32m",
      "directedBy": "Dennis Dugan",
      "starring": "Adam Sandler,Christopher McDonald,Julie Bowen",
      "releaseAt": "2023-12-30T00:00:00.000Z",
      "isDeleted": 0
  },
  {
      "id": "91ff065e-e390-4721-8b0e-1b3da38f5945",
      "title": "American Sniper",
      "year": 2014,
      "dailyRentalRate": 127.5,
      "discountRate": 0.15,
      "genres": [
          "Adventure",
          "Thriller",
          "Action"
      ],
      "userRating": 0,
      "imdbRating": 7.3,
      "posterUrl": "https://posters.movieposterdb.com/22_05/2014/2179136/l_2179136_e67933e8.jpg",
      "bannerUrl": "https://static.thcdn.com/images/large/original//productimg/1600/1600/15278576-5465127341444934.jpg",
      "plot": "American Sniper\" follows the story of Chris Kyle, a Navy SEAL sniper with the most confirmed kills in U.S. military history. As Kyle becomes a legend on the battlefield, he struggles to reconcile his military service with his family life, facing the challenges of war, trauma, and the toll of his actions on his mental and emotional well-being.",
      "runtime": "2h 13m",
      "directedBy": "Clint Eastwood",
      "starring": "Bradley Cooper,Sienna Miller,Kyle Gallner",
      "releaseAt": "2024-01-20T00:00:00.000Z",
      "isDeleted": 0
  },
  {
      "id": "e6f46ab0-67a4-4126-9b30-b8647a5e2856",
      "title": "The Matrix",
      "year": 1999,
      "dailyRentalRate": 106.25,
      "discountRate": 0.15,
      "genres": [
          "Thriller",
          "Mystery",
          "Fantasy"
      ],
      "userRating": 0,
      "imdbRating": 8.7,
      "posterUrl": "https://posters.movieposterdb.com/06_01/1999/0133093/l_77607_0133093_ab8bc972.jpg",
      "bannerUrl": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSRnW2auKIUMHvoiX-eTeVWTjXmHUb47Hi1lSRPCGDHlB6oMbkj3VpF1dhqQ6gtK-fqbzs&usqp=CAU",
      "plot": "Thomas Anderson, a computer programmer, is led to fight an underground war against powerful computers who have constructed his entire reality with a system called the Matrix.",
      "runtime": "2h 16m",
      "directedBy": "Lana Wachowski,Lilly Wachowski",
      "starring": "Keanu Reeves,Laurence Fishburne,Carrie-Anne Moss",
      "releaseAt": "2023-12-15T00:00:00.000Z",
      "isDeleted": 0
  },
  {
      "id": "284db811-12a5-4cc9-b51b-fd5a0468ce6e",
      "title": "Spider Man 2",
      "year": 2004,
      "dailyRentalRate": 85,
      "discountRate": 0.15,
      "genres": [
          "Romance",
          "Adventure",
          "Action"
      ],
      "userRating": 3.5,
      "imdbRating": 7.3,
      "posterUrl": "https://posters.movieposterdb.com/13_04/2004/316654/l_316654_ec1564ae.jpg",
      "bannerUrl": "https://m.media-amazon.com/images/S/pv-target-images/1b5a47977489320f63ec82e39dc7377922f37de680cb9e4f76ed272aa5c9b533.jpg",
      "plot": "Peter Parker, a.k.a. Spider man faces a new challenge as he battles Doctor Octopus, a scientist who has been transformed into a dangerous villain following a failed experiment.",
      "runtime": "2h 7m",
      "directedBy": "Sam Raimi",
      "starring": "Tobey Maguire,Kirsten Dunst,Alfred Molina",
      "releaseAt": "2023-10-30T00:00:00.000Z",
      "isDeleted": 0
  }
]
```