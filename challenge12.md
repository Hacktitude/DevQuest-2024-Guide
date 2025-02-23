# Challenge 12 - Retrieve Upcoming movies and best selling movies

## Overview
In this challenge you need to complete the features regarding upcoming movies

### Part a - Get upcoming movies
Use following API endpoint to finish this part.

```http
GET /api/movie/upcoming
```

You need to complete `getUpcomingMovies()` function in `movieController` for this part. Currently the system retrieve all the movies in the database as the response. Upcoming movie is defined by using the release date of that movie. If the release date is greater than today it will be an upcoming movie. When the API is called response should be as follows.

```json
[
  {
    "id": "e3d0cd0e-4150-4118-a227-329dfae69d9f",
    "title": "Dune part 2",
    "year": 2024,
    "dailyRentalRate": 127.5,
    "discountRate": 0.15,
    "genres": ["Adventure", "Action"],
    "userRating": 0,
    "imdbRating": 8.2,
    "posterUrl":
      "https://image.tmdb.org/t/p/original/czembW0Rk1Ke7lCJGahbOhdCuhV.jpg",
    "bannerUrl":
      "https://assets-prd.ignimgs.com/2023/12/03/dune-1701627712924.jpg",
    "plot": "\"Dune: Part Two\" continues the epic saga of Paul Atreides as he navigates the treacherous politics and power struggles of the desert planet Arrakis. As Paul embraces his destiny as the messiah of the Fremen people, he must confront the forces of the Empire and the malevolent Baron Harkonnen in a battle for control of the most valuable substance in the universe: the spice melange. With its stunning visuals, intricate world-building, and compelling characters, \"Dune: Part Two\" is a mesmerizing and thought-provoking exploration of power, destiny, and the human spirit.'",
    "runtime": "2h 35m",
    "directedBy": "Denis Villeneuve",
    "starring": "Timothée Chalamet,Rebecca Ferguson,Jason Momoa",
    "releaseAt": "2025-09-20T00:00:00.000Z",
    "isDeleted": 0,
  },
];
```
### Part b - Get best selling movies
Use following API endpoint to complete this part 

```http
GET /api/movie/bestRevenued
```
To complete this challenge you need to calculate average income generated by a movie. Then you need to calculate the income generated by each movie. Movies that generated higher income than average income will be selected as best selling movies. When the API is called response should be as follows.

```json
[
  {
  "bannerUrl": "https://picfiles.alphacoders.com/102/102644.jpg",
  "dailyRentalRate": 150,
  "directedBy": "Peter Jackson",
  "discountRate": 0,
  "genres": ["Action", "Thriller", "Fantasy"],
  "imdbRating": 8.8,
  "plot": "The Lord of the Rings: The Fellowship of the Ring follows the story of Frodo Baggins, a young hobbit who is entrusted with a powerful ring that could bring about the end of the world.",
  "posterUrl":
    "https://posters.movieposterdb.com/11_12/2001/120737/l_120737_1b4b2e7d.jpg",
  "releaseAt": "2024-06-20T00:00:00.000Z",
  "runtime": "2h 58m",
  "starring": "Elijah Wood,Ian McKellen,Orlando Bloom",
  "title": "The Lord of the Rings: The Fellowship of the Ring",
  "userRating": 0,
  "year": 2001,
}
];
```