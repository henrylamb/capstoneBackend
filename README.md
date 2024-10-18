# Capstone Backend API Documentation

## User Service

**Base URL:** `http://localhost:8000/users/`

### POST `/registration`
**Description:** Registers a new user.

This is for normal users. For hiring managers and admins, these would be created through a registration endpoint, and then the admin in the frontend would do a PUT request to update the users' role to hiring manager or admin in the case of super-admin.

**Request Body:**
```json
{
  "email": "string",
  "password": "string",
  "name": "string"
}
```

**Response:**
- **Body:** Empty
- **Cookie:** JWT token containing claims with `userId` and `role`

---

### GET `/users/{id}`
**Description:** Retrieves user details by ID.

User role of "user" won't be able to read other users' data. 

User role of "manager" can read any user data. 

**Path Parameters:**
- `id` (required) – The ID of the user.

**Response:**
```json
{
  "id": "int",
  "fullName": "varchar(50)",
  "email": "varchar(50)",
  "address": "varchar(100)",
  "phone": "varchar(25)",
  "resume": "text",
  "department": "varchar(50)",
  "role": "varchar(50)"
}
```

---

### POST `/login`
**Description:** Authenticates the user.

**Request Body:**
```json
{
  "email": "string",
  "password": "string"
}
```

**Response:**
- **Body:** Empty
- **Cookie:** JWT token containing claims with `userId` and `role`

---

### PUT `/users/{id}` - ?
**Description:** Updates user details.

User role of "user" won't be able to update other users' data. 

User role of "admin" can update any user who has the same admin_id value as whats in the cookie. 

**Path Parameters:**
- `id` (required) – The ID of the user.

**Request Body:**
```json
{
  "fullName": "varchar(50)",
  "email": "varchar(50)",
  "address": "varchar(100)",
  "phone": "varchar(25)",
  "resume": "text",
  "department": "varchar(50)",
  "role": "varchar(50)"
}
```

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

---

### DELETE `/users/{id}` - ?
**Description:** Updates user details.

User role of "user" won't be able to update other users' data. 

User role of "admin" can update any user who has the same admin_id value as whats in the cookie. 

**Path Parameters:**
- `id` (required) – The ID of the user.

Returns 204 HTTP code.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

## Job & Application Service

## Job

**Base URL:** `http://localhost:8000/api/`

### GET `/job/{id}`
**Description:** Retrieves job details by ID.

**Path Parameters:**
- `id` (required) – The ID of the job.

**Response:**
```json
{
  "id": "int",
  "userId": "int",
  "department": "varchar(25)",
  "listingTitle": "varchar(100)",
  "dateListed": "timestamp",
  "dateClosed": "timestamp",
  "jobTitle": "varchar(45)",
  "jobDescription": "text",
  "additionalInformation": "text",
  "listingStatus": "varchar(25)",
  "experienceLevel": "varchar(100)"
}
```

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

---

### POST `/job`
**Description:** Creates a new job listing.

**Request Body:**
```json
{
  "userId": "int",
  "department": "varchar(25)",
  "listingTitle": "varchar(100)",
  "dateListed": "timestamp",
  "dateClosed": "timestamp",
  "jobTitle": "varchar(45)",
  "jobDescription": "text",
  "additionalInformation": "text",
  "listingStatus": "varchar(25)",
  "experienceLevel": "varchar(100)",
  "modelResume": "text",
  "modelCoverLetter": "text"
}
```

**Response:**
```json
{
  "id": "int",
  "userId": "int",
  "department": "varchar(25)",
  "listingTitle": "varchar(100)",
  "dateListed": "timestamp",
  "dateClosed": "timestamp",
  "jobTitle": "varchar(45)",
  "jobDescription": "text",
  "additionalInformation": "text",
  "listingStatus": "varchar(25)",
  "experienceLevel": "varchar(100)",
  "modelResume": "text",
  "modelCoverLetter": "text"
}
```
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.
---

### PUT `/job/{id}`
**Description:** Updates an existing job listing.

**Request Body:**
```json
{
  "id": "int",
  "userId": "int",
  "department": "varchar(25)",
  "listingTitle": "varchar(100)",
  "dateListed": "timestamp",
  "dateClosed": "timestamp",
  "jobTitle": "varchar(45)",
  "jobDescription": "text",
  "additionalInformation": "text",
  "listingStatus": "varchar(25)",
  "experienceLevel": "varchar(100)",
  "modelResume": "text",
  "modelCoverLetter": "text"
}
```

**Response:** Same as the request body with updated values.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

---

### DELETE `/job/{id}`
**Description:** Deletes a job listing.

**Path Parameters:**
- `id` (required) – The ID of the job.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `userId` of the job listing.

**Response:** HTTP status `204 No Content`.

---

### GET `/job/{id}/filter={filter}`
**Description:** Retrieves job listings based on a filter.

**Path Parameters:**
- `id` (required) – The ID of the job.
- `filter` (optional) – Filter criteria.

---

### GET `/job/{id}/applications`
**Description:** Retrieves a list of applications for a specific job.

**Path Parameters:**
- `id` (required) – The ID of the job.

**Response:**
```json
[
  {
    "id": "int",
    "userId": "int",
    "jobId": "int",
    "dateApplied": "timestamp",
    "coverLetter": "text",
    "customResume": "text",
    "applicationStatus": "varchar(45)",
    "yearsOfExperience": "int",
    "matchJobDescriptionScore": "int",
    "pastExperienceScore": "int",
    "motivationScore": "int",
    "academicAchievementScore": "int",
    "pedigreeScore": "int",
    "trajectoryScore": "int",
    "extenuatingCircumstancesScore": "int",
    "averageScore": "text",
    "review": "text"
  }
]
```
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.
---

## Application

**Base URL:** `http://localhost:8000/application/`

### GET `/application/{id}`
**Description:** Retrieves application details by ID.

**Path Parameters:**
- `id` (required) – The ID of the application.

**Response:**
```json
{
  "id": "int",
  "userId": "int",
  "jobId": "int",
  "dateApplied": "timestamp",
  "coverLetter": "text",
  "customResume": "text",
  "applicationStatus": "varchar(45)"
}
```
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.
---

### POST `/application`
**Description:** Submits a new job application.

**Request Body:**
```json
{
  "id": "int",
  "userId": "int",
  "jobId": "int",
  "dateApplied": "timestamp",
  "coverLetter": "text",
  "customResume": "text",
  "applicationStatus": "varchar(45)"
}
```

**Response:** Same as the request body with created values.
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.
---

### PUT `/application/{id}`
**Description:** Updates an existing job application.

**Request Body:**
```json
{
  "id": "int",
  "userId": "int",
  "jobId": "int",
  "dateApplied": "timestamp",
  "coverLetter": "text",
  "customResume": "text",
  "applicationStatus": "varchar(45)"
}
```
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.
---

### DELETE `/application/{id}`
**Description:** Deletes a job application.

**Path Parameters:**
- `id` (required) – The ID of the application.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `userId` of the application.

**Response:** HTTP status `204 No Content`.

