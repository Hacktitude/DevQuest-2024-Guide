# Challenge 2 - Authentication & Authorization

## Part a

Here you need to check if the user is authenticated for accessing any API endpoint.

For any request, if the `token` is **not provided** it should return the following meassage in the response.

```text
Access denied! No token provided
```
For any request, if an **invalid token** is provided it should return the following message in the response.

```text
Invalid token
```
## Part b

In this part, if a non-admin user try to access any admin user API endpoint it should return the following response:

```text
Access denied!
```
