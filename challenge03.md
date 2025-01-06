# Challenge 3
## Part a - add a movie

Using `addMovie()` function in both `movieController` and `movieRepository`, you need to implement this functionality.

Following API endpoint will be used in this task
```http
POST /api/movie/
```
The request body should be as the following example.

````json
{
      "title": "Batman Begins",
      "year": 2005,
      "dailyRentalRate": 2.5,
      "genres": ["Action", "Adventure"],
      "imdbRating": 8.2,
      "posterUrl":
        "https://www.imdb.com/title/tt0372784/mediaviewer/rm4261716480/",
      "bannerUrl":
        "https://www.imdb.com/title/tt0372784/mediaviewer/rm4261716480/",
      "plot": "After training with his mentor, Batman begins his fight to free crime-ridden Gotham City from corruption.",
      "runtime": "2hr 20min",
      "directedBy": "Christopher Nolan",
      "starring": "Christian Bale, Michael Caine, Ken Watanabe",
      "releaseAt": "2024-10-20T00:00:00.000Z",
    }
````
The system cannot have two movies with same `title` and `year`. Currently this condition is not evaluated in the backend. Therefore, you need to implement `getMovieByNameAndYear()` function in the `movieRepository` to return a boolean value checking for an existing movie with same title and year.

If there is an existing movie with same title and year it should return the following response with `400` http status.
````json
{
    "message":"Movie already exists."
}
````
If not new movie should be inserted and `201` status should be returned.

## Part b - Update daily rental rate of a movie

For this task you need to implement the `updateDailyRentalRateMovie()` function in both `movieController` and `movieRepository`

Following endpoint is needed to be implemented for this task

```http
 PATCH /api/movie/:id
```
In the body of the request daily rental rate should be provided as in following example.

````json
{
  "dailyRentalRate":150
}
````
First you need to check if ther is a movie with given movie id. If not, it should return a message named `Movie not found`. If there is a movie, it should return `200` status in the response.

## Part c - Add new genre

In the current application user can add the same genre multiple times. You need to implement a check for this scenario in the `addGenre()` functions of `genreController`.
If the genre already exists in the database it should return `Genre already exists` 