# Challenge 11 - Recommend Similar Movies

## Overview

The objective of this challenge is to develop a function that takes a movie ID as input and returns a list of movies that are similar to the input movie. The returned list should be sorted in descending order of similarity.

**This challenge consists of two parts:**

a. Get similar movies for a given movie using Jaccard similarity index
b. Get similar movies for a given movie using Cosine similarity index

## Instructions

For both parts, you will need to implement the following API endpoint:

```http
GET /api/movie/get/similarMovies/:option/:movieId
```

i. The `option` parameter specifies the method to be used to calculate the similarity index. It can have one of the following values:

- `jaccard`: Use the Jaccard similarity index to calculate the similarity between movies.
- `cosine`: Use the Cosine similarity index to calculate the similarity between movies.

ii. The `movieId` parameter specifies the ID of the movie for which you want to find similar movies.

This API calls the `getSimilarMovies()` function in the `src/controller/movieController.js` file. You need to implement the function according to the option parameter, where the function should implment the logic to get similar movies for the given movie using Jaccard or Cosine similarity index. Finally, the function should return a list of similar movies sorted in descending order of similarity. (i.e. From most similar to least similar)

#### Note

- When similarity index is same for two movies, the order should be based on the movie's title in ascending order.
- When similarity index is high for a movie A and low for a movie B, movie A should come before movie B in the list.

## a. Get similar movies using Jaccard similarity index

The Jaccard similarity index is a statistic used for comparing the similarity and diversity of sample sets. The Jaccard coefficient measures similarity between finite sample sets and is defined as the `size of the intersection` divided by the `size of the union` of the sample sets.

```text
Jaccard Similarity = (Intersection of A and B) / (Union of A and B)
```

In this segment of the challenge, you'll employ the Jaccard similarity index to generate recommendations for movies that bear resemblance to a specified movie.

To accomplish this, you'll need to create a set for each movie that includes its `genres`, `actors`, and `directors`.

#### example

Consider the following movie:

```json
{
      "id": "b5f37e47-40a7-4688-b6aa-420356eabcf8",
      "title": "The shawshank redemption",
      "year": 1994,
      "dailyRentalRate": 100,
      "discountRate": 0,
      "genres": [
          "Romance",
          "Adventure",
          "Drama"
      ],
      "userRating": 4,
      "imdbRating": 9.3,
      "posterUrl": "https://posters.movieposterdb.com/05_02/1994/0111161/l_7266_0111161_d2436dce.jpg",
      "bannerUrl": "https://m.media-amazon.com/images/I/71MpMh9upxL._AC_UF894,1000_QL80_.jpg",
      "plot": "\"The Shawshank Redemption\" tells the story of Andy Dufresne, a banker who is wrongfully convicted of murder and sentenced to life in Shawshank State Penitentiary, where he forms a friendship with fellow inmate Red and ultimately engineers a daring escape over the course of two decades, all while maintaining his innocence. Through perseverance, hope, and resilience, Andy triumphs over adversity and finds redemption on the outside.",
      "runtime": "2h 22m",
      "directedBy": "Frank Darabont",
      "starring": "Tim Robbins,Morgan Freeman",
      "releaseAt": "2022-04-14T00:00:00.000Z",
      "isDeleted": 0
  }
```

The set of this movie should be like follow,

```text
[Romance, Adventure, Drama, Frank Darabont, Tim Robbins, Morgan Freeman]
```

Subsequently, you can compute the similarity index between the reference movie and all other movies by comparing their respective sets and put it as an attribute to all other movies.
Finally, you can arrange the movies in descending order based on their similarity index to the reference movie, thereby producing a list of recommended movies.

**The response from the `GET /api/movie/get/similarMovies/jaccard/ad41b6f6-d79f-4e58-89d6-9bb53498ccd9` API should be as follow.**

```json
[
      {
        "id": "b349436c-a26a-4959-99af-7a1d9c4088fc",
        "title": "The Dark Knight",
        "year": 2008,
        "dailyRentalRate": 125,
        "discountRate": 0,
        "genres": [
          "Crime",
          "Adventure",
          "Action"
        ],
        "userRating": 3.7,
        "imdbRating": 9,
        "posterUrl": "https://posters.movieposterdb.com/08_05/2008/468569/l_468569_f0e2cd63.jpg",
        "bannerUrl": "https://eskipaper.com/images/the-dark-knight-4.jpg",
        "plot": "\"The Dark Knight\" follows the story of Batman as he faces off against the Joker, a sadistic criminal mastermind who seeks to undermine Gotham City's sense of justice and morality. As the Joker's reign of terror threatens to destroy the city, Batman must confront his own inner demons and make sacrifices to protect the people he loves. With its complex characters, intense action, and thought-provoking themes, \"The Dark Knight\" is a gripping exploration of heroism, villainy, and the blurred lines between them.",
        "runtime": "2h 32m",
        "directedBy": "Christopher Nolan",
        "starring": "Christian Bale,Heath Ledger,Aaron Eckhart",
        "releaseAt": "2023-04-29T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.5555555555555556
      },
      {
        "id": "e3d0cd0e-4150-4118-a227-329dfae69d9f",
        "title": "Dune part 2",
        "year": 2024,
        "dailyRentalRate": 127.5,
        "discountRate": 0.15,
        "genres": [
          "Adventure",
          "Action"
        ],
        "userRating": 0,
        "imdbRating": 8.2,
        "posterUrl": "https://image.tmdb.org/t/p/original/czembW0Rk1Ke7lCJGahbOhdCuhV.jpg",
        "bannerUrl": "https://assets-prd.ignimgs.com/2023/12/03/dune-1701627712924.jpg",
        "plot": "Dune: Part Two\" continues the epic saga of Paul Atreides as he navigates the treacherous politics and power struggles of the desert planet Arrakis. As Paul embraces his destiny as the messiah of the Fremen people, he must confront the forces of the Empire and the malevolent Baron Harkonnen in a battle for control of the most valuable substance in the universe: the spice melange. With its stunning visuals, intricate world-building, and compelling characters, \"Dune: Part Two\" is a mesmerizing and thought-provoking exploration of power, destiny, and the human spirit.",
        "runtime": "2h 35m",
        "directedBy": "Denis Villeneuve",
        "starring": "Timothée Chalamet,Rebecca Ferguson,Jason Momoa",
        "releaseAt": "2025-09-20T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.18181818181818182
      },
      {
        "id": "91ff065e-e390-4721-8b0e-1b3da38f5945",
        "title": "American Sniper",
        "year": 2014,
        "dailyRentalRate": 150,
        "discountRate": 0,
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
        "isDeleted": 0,
        "similarityIndex": 0.16666666666666666
      },
      {
        "id": "a742a595-e707-458a-9240-66742251dabf",
        "title": "Spider Man 1",
        "year": 2002,
        "dailyRentalRate": 100,
        "discountRate": 0,
        "genres": [
          "Romance",
          "Adventure",
          "Action"
        ],
        "userRating": 4,
        "imdbRating": 7.3,
        "posterUrl": "https://posters.movieposterdb.com/08_10/2002/145487/l_145487_821ea90e.jpg",
        "bannerUrl": "https://i.pinimg.com/originals/74/6d/79/746d79553f55de04e8f9560cb35d2e41.jpg",
        "plot": "Peter Parker, a shy high school student, is often bullied by his classmates. However, his life changes when he is bitten by a genetically altered spider and gains superpowers. He must now use his newfound abilities to fight the evil Green Goblin and save the city.",
        "runtime": "2h 1m",
        "directedBy": "Sam Raimi",
        "starring": "Tobey Maguire,Kirsten Dunst,Willem Dafoe",
        "releaseAt": "2023-08-25:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.16666666666666666
      },
      {
        "id": "284db811-12a5-4cc9-b51b-fd5a0468ce6e",
        "title": "Spider Man 2",
        "year": 2004,
        "dailyRentalRate": 100,
        "discountRate": 0,
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
        "isDeleted": 0,
        "similarityIndex": 0.16666666666666666
      },
      {
        "id": "b5f37e47-40a7-4688-b6aa-420356eabcf8",
        "title": "The shawshank redemption",
        "year": 1994,
        "dailyRentalRate": 100,
        "discountRate": 0,
        "genres": [
          "Romance",
          "Adventure",
          "Drama"
        ],
        "userRating": 4,
        "imdbRating": 9.3,
        "posterUrl": "https://posters.movieposterdb.com/05_02/1994/0111161/l_7266_0111161_d2436dce.jpg",
        "bannerUrl": "https://m.media-amazon.com/images/I/71MpMh9upxL._AC_UF894,1000_QL80_.jpg",
        "plot": "\"The Shawshank Redemption\" tells the story of Andy Dufresne, a banker who is wrongfully convicted of murder and sentenced to life in Shawshank State Penitentiary, where he forms a friendship with fellow inmate Red and ultimately engineers a daring escape over the course of two decades, all while maintaining his innocence. Through perseverance, hope, and resilience, Andy triumphs over adversity and finds redemption on the outside.",
        "runtime": "2h 22m",
        "directedBy": "Frank Darabont",
        "starring": "Tim Robbins,Morgan Freeman",
        "releaseAt": "2022-04-14T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.08333333333333333
      },
      {
        "id": "47ef0a76-fbed-4d6f-bdd5-55ffc6506c03",
        "title": "Happy Gilmore",
        "year": 1996,
        "dailyRentalRate": 100,
        "discountRate": 0,
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
        "isDeleted": 0,
        "similarityIndex": 0.07692307692307693
      },
      {
        "id": "f800a874-d19f-40e4-80af-778188705a44",
        "title": "Harry Potter and the Chamber of Secrets",
        "year": 2002,
        "dailyRentalRate": 100,
        "discountRate": 0,
        "genres": [
          "Adventure",
          "Mystery",
          "Fantasy"
        ],
        "userRating": 4,
        "imdbRating": 7.4,
        "posterUrl": "https://posters.movieposterdb.com/11_08/2002/295297/l_295297_6be2c5d1.jpg",
        "bannerUrl": "https://picfiles.alphacoders.com/620/62025.jpg",
        "plot": "Harry ignores warnings not to return to Hogwarts, only to find the school plagued by a series of mysterious attacks and a strange voice haunting him.",
        "runtime": "2h 41m",
        "directedBy": "Chris Columbus",
        "starring": "Daniel Radcliffe,Rupert Grint,Emma Watson",
        "releaseAt": "2023-11-12T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.07692307692307693
      },
      {
        "id": "2d3e6418-34eb-4753-aae4-b45eb78acbed",
        "title": "Harry Potter and the Sorcerer's Stone",
        "year": 2001,
        "dailyRentalRate": 100,
        "discountRate": 0,
        "genres": [
          "Adventure",
          "Mystery",
          "Fantasy"
        ],
        "userRating": 4.3,
        "imdbRating": 7.6,
        "posterUrl": "https://posters.movieposterdb.com/13_02/2001/241527/l_241527_da927a3d.jpg",
        "bannerUrl": "https://picfiles.alphacoders.com/622/62263.jpg",
        "plot": "Harry Potter, an orphaned child, discovers that he is a wizard and is invited to study at Hogwarts. Even as he escapes a dreary life and enters a world of magic, he finds trouble awaiting him.",
        "runtime": "2h 32m",
        "directedBy": "Chris Columbus",
        "starring": "Daniel Radcliffe,Rupert Grint,Emma Watson",
        "releaseAt": "2023-11-08T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.07692307692307693
      },
      {
        "id": "6ba1472e-563c-4dbd-ad31-d78aec32f5af",
        "title": "The Godfather",
        "year": 1972,
        "dailyRentalRate": 150,
        "discountRate": 0,
        "genres": [
          "Thriller",
          "Action",
          "Drama"
        ],
        "userRating": 3,
        "imdbRating": 9.2,
        "posterUrl": "https://posters.movieposterdb.com/22_07/1972/68646/l_68646_8c811dec.jpg",
        "bannerUrl": "https://c4.wallpaperflare.com/wallpaper/874/376/908/the-godfather-movies-vito-corleone-wallpaper-preview.jpg",
        "plot": "\"The Godfather\" follows the story of the powerful Italian-American crime family, the Corleones, led by Don Vito Corleone. When the aging Don is nearly assassinated, his reluctant son, Michael, is drawn into the world of organized crime and eventually rises to power, navigating betrayal, loyalty, and vengeance in a ruthless quest to protect his family's legacy.",
        "runtime": "2h 55m",
        "directedBy": "Francis Ford Coppola",
        "starring": "AI Pacino,Marion Brando,James Caan",
        "releaseAt": "2022-05-14T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.07692307692307693
      },
      {
        "id": "e09ab8f1-bbd9-4066-a287-f31a54c2aef5",
        "title": "The Godfather: Part II",
        "year": 1974,
        "dailyRentalRate": 150,
        "discountRate": 0,
        "genres": [
          "Thriller",
          "Action",
          "Drama"
        ],
        "userRating": 4,
        "imdbRating": 9,
        "posterUrl": "https://posters.movieposterdb.com/22_07/1974/71562/l_71562_28dbaac1.jpg",
        "bannerUrl": "https://wallpapercave.com/wp/wp4119161.jpg",
        "plot": "The Godfather: Part II\" continues the saga of the Corleone family, exploring the rise of a young Vito Corleone as he builds his criminal empire and the reign of his son, Michael, as he seeks to expand the family's influence and protect their legacy. As the story unfolds, the film delves into themes of power, corruption, and the consequences of violence, offering a compelling and complex portrait of the American dream and the cost of pursuing it.",
        "runtime": "3h 22m",
        "directedBy": "Francis Ford Coppola",
        "starring": "AI Pacino,Robert De Niro,Robert Duvall",
        "releaseAt": "2023-03-29T00:00:00.000Z",
        "isDeleted": 0,
        "similarityIndex": 0.07692307692307693
      },
      {
        "id": "e6f46ab0-67a4-4126-9b30-b8647a5e2856",
        "title": "The Matrix",
        "year": 1999,
        "dailyRentalRate": 125,
        "discountRate": 0,
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
        "isDeleted": 0,
        "similarityIndex": 0
      }
    ]
```