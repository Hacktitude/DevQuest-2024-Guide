# Challenge 14 - Delete a movie

In this task you need to use the following API endpoint
```http
DELETE /api/movie/:id
```
Movie deletion is carried as a soft delete. Following conditions need to be considered before deleting a movie.

1. Whether there are any rentals available for the current month 
2. Does the income generated by all the rentals for the movie is higher than the average income generated by a movie in the system.

If above conditions fails, the movie won't be deleted.

You need to implement `deleteMovie()` function in both `movieController` and `movieRepository` to fulfill this task. When delete movie operation carried out, `is_deleted` attribute of the movie record in the movie table should be updated as `true` or `false` accordingly since it is a boolean attribute.

If one or more above conditions fails, you need to send the response with the `400` status code.

Otherwise, `is_deleted` attribute should be updated.

After this challenge, anywhere that movie data are retrieved **DELETED MOVIES SHOULDN'T BE RETRIEVED.**