# Challenge 13 - Group users based on their rentals using k-means clustering

## Overview

The purpose of this challenge is to group users based on their rental patterns. The users will be grouped using k-means clustering. The groups are,

1. **Bronze users** - users who have the lowest expenditure on rentals and the shortest rental duration.
2. **Silver users** - users who have average expenditure on rentals and average rental duration.
3. **Gold users** - users who have the highest expenditure on rentals and the longest rental duration.

## Instructions

1. Create the `getUserRentSummary()` function in `controller/rentalController.js` to retrieve user rental data from the database, and make data object for each user. The data object should contain the following information:
   - User ID
   - Data points for k-means clustering:
     - Total rental expenditure
     - Total rental duration(in days)

`Note: The total rental expenditure is the sum of the rental cost for each rental and the total rental duration is the sum of the days rented for each rental.`

**example data object:**

```js
{
    userId: 'c784dd78-b26e-4cc0-9c8a-b84bdb4330b9',
    point: [ 1425, 13 ]
}
```

2. Perform k-means clustering on the data objects to group users into three clusters: Bronze, Silver, and Gold.

   - **Bronze users:** cluster with the lowest centroid value
   - **Silver users:** cluster with the middle centroid value
   - **Gold users:** cluster with the highest centroid value

   The algorithm can be broken down into the following steps:

   1. Choosing the number of clusters (In this case, 3 clusters)

   2. Initialize the centroids.
      In this scenario we use k-means++ algorithm for cluster centroid initialization. The algorithm is as follows:

      - Usually in k-means++ the first cluster centroid is randomly selected from the data points. However, here we will select the first cluster centroid as the data point with the minimum total rental expenditure.
      - For each data object, calculate the distance from the nearest cluster centroid.
      - The next cluster centroid is selected from the data objects with a probability directly proportional to the squared distance from the nearest, previously chosen cluster centroid. (i.e. the point having maximum squared distance from the nearest centroid will be selected next as a centroid)
      - Repeat the above steps until the required number of cluster centroids are selected.

   3. Assign each data object to the nearest cluster.

   4. Update the cluster centroids by calculating the mean of the data objects in each cluster.

   5. Repeat steps 3 and 4 until the cluster centroids do not change or if the maximum number of iterations(100) is reached.

3. Finally the response should contain the following information:
   - The centroids of the three clusters
   - The assignment of each user to a cluster

You should implement this in the `getUserGroups()` function in the `controller/userController.js` file. So when you run the server and make a GET request to the **`GET /api/user/groups`** endpoint, the server should return the response with the centroids and the user assignments.

### Expected response

```json

    "data": {
        "centroids": [
            [
                131.25,
                1.25
            ],
            [
                691.6666666666666,
                5.666666666666667
            ],
            [
                1333.3333333333333,
                11.333333333333334
            ]
        ],
        "assignment": [
            {
                "user": "c784dd78-b26e-4cc0-9c8a-b84bdb4330b9",
                "group": "Gold Renters "
            },
            {
                "user": "da9347a6-2a7f-4573-be27-15f05569fb0d",
                "group": "Gold Renters "
            },
            {
                "user": "fce17e94-3415-4c08-b2c9-beddba191b4d",
                "group": "Silver Renters"
            },
            {
                "user": "4fd09491-2299-4684-a4fb-d7ca0bb074eb",
                "group": "Gold Renters "
            },
            {
                "user": "999da33d-74c3-4176-bb26-98c53215a71c",
                "group": "Silver Renters"
            },
            {
                "user": "4a90e4f3-d695-4c54-a698-099cdb39e4ad",
                "group": "Bronze Renters"
            },
            {
                "user": "1ebd273d-9b35-4f9f-a96e-6e0c09194d1f",
                "group": "Bronze Renters"
            },
            {
                "user": "52ef9366-6e86-4498-be32-a33087d03670",
                "group": "Bronze Renters"
            },
            {
                "user": "7dfcf073-99b9-4ed0-9458-600484a2e265",
                "group": "Bronze Renters"
            },
            {
                "user": "fe1f120c-85a1-4d83-9ebd-ef993951c51c",
                "group": "Silver Renters"
            }
        ]
    }
;
```
