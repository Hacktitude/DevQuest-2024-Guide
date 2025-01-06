# Challenge 6 - Suggest Movies to User

In this challenge, movies will be suggested for the user based on their current rentals. The following API endpoint will be used for this challenge.

```http
GET /api/movie/get/suggestions
```
To accomplish this task, you should implement the `getMovieSuggestions()` function in both the `movieController` and `movieRepository`.

Here's a breakdown of the steps to follow:

1. Retrieve the `rental` data of the user. user ID should be taken from the jwt token
2. Extract the `genres` of the rented movies.
3. For each genre, fetch the movies belonging to that genre.
4. Compile a list of all movies from the selected genres.
5. Remove the movies that have been already rented by the user.
6. Sort the resulting movie list based on the rating. The rating should be a combination of `50%` from the `imdb rating` and `50%` from the `average user rating`.

The response format should be as follows:

````json
[
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
    "isDeleted": 0
  },
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
    "isDeleted": 0
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
    "isDeleted": 0
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
    "isDeleted": 0
  }
]
````