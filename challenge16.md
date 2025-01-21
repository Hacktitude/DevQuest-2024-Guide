# Challenge 16

## Overview

In this application users can send gift vouchers to each other. The user can send a gift voucher to another user by entering the recipient's email address and the amount of the gift voucher. The recipient will receive the gift voucher in the gift voucher section of the application. The recipient can then claim the gift voucher. This challenge has 3 sub-challenges.

- Send a gift voucher
- Get gift vouchers for recipient
- Claim a gift voucher

### a. Send a gift voucher

In the application, the user should be able to send a gift voucher to another user. Use `POST /api/gift-voucher` to send a gift voucher. The request body should contain the `receiverEmail` and `amount` of the gift voucher. You can implement the `sendGiftVoucher()` function in the `/controller/giftVoucherController.js` file to send a gift voucher.

#### Instructions

- First check whether there is a user with the given email address. If the user does not exist, return an error response with status code 404 and message "No user for the email provided".
  
- Then check whether the sender and receiver are the same. If they are the same, return an error response with status code 400 and message "You cannot send a gift voucher to yourself".

- Next, check whether the sender has enough balance to send the gift voucher. If the sender does not have enough balance, return an error response with status code 400 and message "Insufficient balance".

- Finally, send the gift voucher to the recipient.
  For this you should call the `createGiftVoucher()` function in the `/repositories/giftVoucherRepository.js` file. You need to pass a gift voucher object with the following attributes:

  - `id` - A unique id for the gift voucher
  - `senderId` - The id of the sender
  - `receiverId` - The id of the receiver
  - `amount` - The amount of the gift voucher
  - `issuedAt` - The date and time the gift voucher was issued
  - `status` - The status of the gift voucher. The status should be "unclaimed"

  Then in the `createGiftVoucher()` function, you should add the gift voucher to gift_voucher table in the database. Also you need to update the balance of the sender in the user table in the database.

  Finally `createGiftVoucher()` should return the created gift voucher. Here the returning object include `expiresAt` as well. The `expiresAt` attribute should be the current date plus 14 days. Then in the `sendGiftVoucher()` function, you should return the created gift voucher with status code 201.

  In order to create gift voucher object to pass data into and out of `createGiftVoucher()`, you can use the giftVoucher model in the `/models/giftVoucher.js` file. In the giftVoucher model, the `id` attribute should be a UUID and the `status` attribute should be "unclaimed". The `issuedAt` attribute should be the current date and time. The `expiresAt` attribute should be the current date and time plus 14 days.

** Tip - Implement the `expiresAt` calculation in the giftVoucher model in `/models/giftVoucher.js` file since it is a common calculation for all gift vouchers.

#### Request - `POST /api/gift-voucher`

```json
{
  "receiverEmail": "johnS@gmail.com",
  "amount": 300
}
```

#### Response for `POST /api/gift-voucher`

```json
{
  "data": {
    "id": "14ea3f7b-47b0-40fc-9cae-890f480b45aa",
    "amount": 300,
    "issuedAt": "2024-05-07T04:02:20.751Z",
    "expiresAt": "2024-05-21T04:02:20.751Z",
    "status": "unclaimed"
  }
}
```
### b. Get gift vouchers for recipient

In the application the recipient should be able to view all the gift vouchers they have received. Use `GET /api/gift-voucher/receiver` to get all the gift vouchers for the recipient. You can implement the `getGiftVouchersByReceiverId()` function in the `/controller/giftVoucherController.js` file to get all the gift vouchers for the recipient. 

#### Instructions

User id can be retried from req.user.

- First check whether the user has any gift vouchers. In order to implement this, you can call the `getGiftVouchersByReceiverId()` function in the `/repositories/giftVoucherRepository.js` file. You need to pass the receiver id to the `getGiftVouchersByReceiverId()` function. The `getGiftVouchersByReceiverId()` function should return all the gift vouchers for the receiver. If the receiver does not have any gift vouchers, return an error response with status code 404 and message "Vouchers not found".

- Next you need to modify the response to include the sender's full name and if the expiresAt is in the past, the status should be updated to "expired". You need to call `updateGiftVoucherStatus()` function in the `/repositories/giftVoucherRepository.js` file to update the status of the gift voucher. You need to pass a gift voucher object to the `updateGiftVoucherStatus()` function. 
Then in the `updateGiftVoucherStatus()` function, you should update the status of the gift voucher in the gift_voucher table in the database.


#### Response for `GET /api/gift-voucher/receiver`

```json
{
    "data": [
        {
            "id": "ad8b570b-0084-4e6e-9f26-aa5f8c17fbc2",
            "senderId": "da9347a6-2a7f-4573-be27-15f05569fb0d",
            "receiverId": "c784dd78-b26e-4cc0-9c8a-b84bdb4330b9",
            "amount": 200,
            "issuedAt": "2024-04-10T11:37:01.316Z",
            "expiresAt": "2024-04-24T11:37:01.316Z",
            "status": "expired",
            "senderName": "Matt Damon"
        }
    ]
}
```

### c. Claim a gift voucher

In the application the recipient should be able to claim a gift voucher. Use `PATCH /api/gift-voucher/claim/:id` to claim a gift voucher. You can implement the `claimGiftVoucher()` function in the `/controller/giftVoucherController.js` file to claim a gift voucher.

You can get the user id from the token, and you need to pass the voucher id as a path parameter in the URL.

#### Instructions

- First check whether the gift voucher exists. You can call the `getGiftVoucherById()` function in the `/repositories/giftVoucherRepository.js` file to get the gift voucher by id. If the gift voucher does not exist, return an error response with status code 404 and message `"Voucher not found"`.
- Then check whether the gift voucher receiverId is the same as the user id. If they are not the same, return an error response with status code 400 and message `"You are not the receiver of this voucher"`.
- Next check whether the gift voucher has already been claimed or expired.
  - If the gift voucher has already been claimed, return an error response with status code 400 and message `"Voucher already claimed"`.
  - If the gift voucher has expired, return an error response with status code 400 and message `"Voucher expired"`.
- Finally, change the voucher.status to "claimed" and pass the voucher object to `updateGiftVoucherAndUserBalance()` function in the `/repositories/giftVoucherRepository.js` file. In the `updateGiftVoucherAndUserBalance()` function, you should update the status of the gift voucher in the gift_voucher table in the database and update the balance of the receiver in the user table in the database.
- Then return the voucher object with status code 200.
