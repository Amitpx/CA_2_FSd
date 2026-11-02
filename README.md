# Student Feedback Management API

A Node.js, Express, and MongoDB API for submitting student feedback, listing it
with pagination, and updating its review status.

## Setup

1. Install Node.js 18.11+ and MongoDB, then start MongoDB.
2. Install dependencies with `npm install`.
3. Copy `.env.example` to `.env` and set `MONGODB_URI` if your MongoDB URL differs.
4. Start the API with `npm start` (or `npm run dev` for development).

The API listens on port `3000` by default.

## Endpoints

### Submit feedback

`POST /api/feedback`

```json
{
  "studentName": "Amit",
  "courseName": "Backend Development",
  "message": "The session was helpful.",
  "rating": 5
}
```

Returns `201 Created`. All four fields are required; rating must be from 1 to 5.
New feedback starts with status `Pending`.

### List feedback

`GET /api/feedback?page=1&limit=10`

Both query parameters are optional (defaults: page `1`, limit `10`) and must be
positive integers. The response includes `feedback`, `currentPage`,
`totalRecords`, and `totalPages`.

### Update review status

`PATCH /api/feedback/:id`

```json
{
  "status": "Reviewed"
}
```

Allowed statuses are `Pending` and `Reviewed`. Returns `404 Not Found` when the
feedback ID does not exist and `400 Bad Request` for an invalid ID or status.

## Tests

Run the API tests with `npm test`. The route tests use a fake model, so they do
not require a running MongoDB instance.
