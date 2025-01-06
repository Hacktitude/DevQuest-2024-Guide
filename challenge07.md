# Challenge 7 - Search movies

For this task, pagination and search functionality need to be implemented.

## Part a

The following API endpoint needs to be implemented.

```http
GET /api/movie/get/pagination?pageSize=4&page=3
```

To achieve this, you should implement the `getMoviesWithPagination()` function in both the `movieController` and `movieRepository`. This function should handle pagination for the movies, where a fixed number of movies are returned per page, based on the `pageSize` and `page` parameters.

Here's the desired response format for `page = 1` with `pageSize = 4`:

````json
"data": [
        {
            "id": "ad41b6f6-d79f-4e58-89d6-9bb53498ccd9",
            "title": "The Dark Knight Rises",
            "year": 2012,
            "dailyRentalRate": 125,
            "genres": [
                "Crime",
                "Adventure",
                "Action"
            ],
            "userRating": 3.7,
            "imdbRating": 8.4,
            "posterUrl": "https://posters.movieposterdb.com/21_06/2012/1345836/l_1345836_429edb63.jpg",
            "bannerUrl": "https://c4.wallpaperflare.com/wallpaper/727/965/131/batman-movies-film-batman-the-dark-knight-rises-cities-entertainment-movies-hd-art-wallpaper-preview.jpg",
            "plot": "Eight years after the Joker's reign of anarchy, Batman, with the help of the enigmatic Catwoman, is forced from his exile to save Gotham City from the brutal\n      guerr",
            "runtime": "2h 44m",
            "directedBy": "Christopher Nolan",
            "starring": "Christian Bale,Tom Hardy,Anne Hathaway"
        },
        {
            "id": "b349436c-a26a-4959-99af-7a1d9c4088fc",
            "title": "The Dark Knight",
            "year": 2008,
            "dailyRentalRate": 125,
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
            "starring": "Christian Bale,Heath Ledger,Aaron Eckhart"
        },
        {
            "id": "284db811-12a5-4cc9-b51b-fd5a0468ce6e",
            "title": "Spider Man 2",
            "year": 2004,
            "dailyRentalRate": 100,
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
            "starring": "Tobey Maguire,Kirsten Dunst,Alfred Molina"
        },
        {
            "id": "a742a595-e707-458a-9240-66742251dabf",
            "title": "Spider Man 1",
            "year": 2002,
            "dailyRentalRate": 100,
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
            "starring": "Tobey Maguire,Kirsten Dunst,Willem Dafoe"
        }
    ]
````
## Part b

The following API endpoint is needed to be implemented for this part.

```http
GET /api/movie/search/movies?keyword=dark&pageSize=3&page=1
```

For this part, you need to implement search functionality for movies. Movies can be searched by their `Title`, `Year`, `Genres`, `Director`, and `Starring`. Additionally, when retrieving the data, pagination should be applied as in **Part a**.

The response format for the search term "dark" should be as follows:

````json
"data": [
        {
            "id": "b349436c-a26a-4959-99af-7a1d9c4088fc",
            "title": "The Dark Knight",
            "year": 2008,
            "dailyRentalRate": 125,
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
            "starring": "Christian Bale,Heath Ledger,Aaron Eckhart"
        },
        {
            "id": "ad41b6f6-d79f-4e58-89d6-9bb53498ccd9",
            "title": "The Dark Knight Rises",
            "year": 2012,
            "dailyRentalRate": 125,
            "genres": [
                "Crime",
                "Adventure",
                "Action"
            ],
            "userRating": 3.7,
            "imdbRating": 8.4,
            "posterUrl": "https://posters.movieposterdb.com/21_06/2012/1345836/l_1345836_429edb63.jpg",
            "bannerUrl": "https://c4.wallpaperflare.com/wallpaper/727/965/131/batman-movies-film-batman-the-dark-knight-rises-cities-entertainment-movies-hd-art-wallpaper-preview.jpg",
            "plot": "Eight years after the Joker's reign of anarchy, Batman, with the help of the enigmatic Catwoman, is forced from his exile to save Gotham City from the brutal\n      guerr",
            "runtime": "2h 44m",
            "directedBy": "Christopher Nolan",
            "starring": "Christian Bale,Tom Hardy,Anne Hathaway"
        }
    ]
````