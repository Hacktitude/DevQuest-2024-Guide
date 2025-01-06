# Challenge 5

## Overview

The purpose of this challenge is to implement a function that use to rent movies. The logic should be implemented in the `addRental()` function in the `/controller/rentalController.js` file and database queries should be implemented in the  `addRental()` function in the `/repositories/rentalController.js` file.

The function should take the following parameters:

- `movieId`: The ID of the movie to be rented.
- `daysRented`: The number of days the movie will be rented for.

userId should be retrieve from the token.

## Instructions

The function should perform the following steps:

1. First get movie details by calling `getMovieById()` function in `repositories/movieRepository` and user details by calling `getUserById()` function in `repositories/userRepository`.

2. Check if the movie is available for rent. That means check whether,

    - The movie is available in the database. If the movie is not available in the database, return a response with a status code of 404 and error message as an json object.

    ```text
         status: 404
         message: "Movie not found"
    ```

    - The movie is not already rented by the user. If the movie is already rented by the user, return a response with a status code of 500 and error message as an json object. Use `getLastRentalStatusService()` function to check the rental status of the movie.

    ```text
         status: 500
         message: "There is an active rental for this movie"
    ```

3. Calculate the rental fee by multiplying the number of days rented by the movie's daily rental rate. Since `getMovieById()` function returns the daily rate after calculating the discount, you can directly use the daily rate directly to calculate the rental fee.

4. Check if the user has enough balance to rent the movie. If the user does not have enough balance, return a response with a status code of 500 and error message as an json object.

    ```text
         status: 500
         message: "Insufficient balance"
    ```

5. Deduct the rental fee from the user's balance.

6. If the movie release date is in the future, set rentedAt to the movie's release date. Otherwise, set rentedAt to the current date and time.

**Request `"POST /rentals"`** with the following JSON object:

```json
{
  "movieId": "b5f37e47-40a7-4688-b6aa-420356eabcf8",
  "daysRented": 2
}
```

**The response should be as follows:**

```json
{
    "data": {
        "id": "3f0131a5-4ed8-4a34-a081-783f3d50283f",
        "userId": "da9347a6-2a7f-4573-be27-15f05569fb0d",
        "movieId": "b5f37e47-40a7-4688-b6aa-420356eabcf8",
        "rentalFee": 200,
        "daysRented": 2,
        "rentedAt": "2024-04-25T10:53:51.769Z"
    }
}
```