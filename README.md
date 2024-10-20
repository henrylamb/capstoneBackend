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

### POST `/registration/admin`
**Description:** Registers a new user.

An endpoint to create a hiring manager from the perspective of the admin. 

**Request Body:**
```json
{
  "email": "string",
  "password": "string",
  "name": "string"
}
```

**Response:**
```json
{
  "id": "string",
  "role": "string"
}
```

  

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request. And in the cookie, the role must be admin.

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

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

---

### GET (Many) `/users/admin/{id}`
**Description:** Retrieves user details by ID.

User role of "admin" can read any user data which is related to the admin account. 

This request will make a read request to get all the users which have the admin_id value which matches with admin id which is provided with the endpoint. 

**Path Parameters:**
- `id` (required) – The ID of the user.

**Response:**
```json
[
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
]

```

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request. And in the cookie, the role must be admin.

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
**Response:**
```json
{
  "id": "string",
  "role": "string"
}
```

- **Cookie:** JWT token containing claims with `userId` and `role`

---

### PUT `/users/{id}`
**Description:** Updates user details.

User role of "user" won't be able to update other users' data. 

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

### PUT `/users/admin/{id}`
**Description:** Updates user details.

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

### DELETE `/users/{id}`
**Description:** Updates user details.

User role of "user" won't be able to update other users' data. 

User role of "admin" can update any user who has the same admin_id value as whats in the cookie. 

**Path Parameters:**
- `id` (required) – The ID of the user.

Returns 204 HTTP code.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

---

### DELETE `/users/admin/{id}`
**Description:** Updates user details.

User role of "user" won't be able to update other users' data. 

User role of "admin" can update any user who has the same admin_id value as whats in the cookie. 

**Path Parameters:**
- `id` (required) – The ID of the user.

Returns 204 HTTP code.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

## Job & Application Service

**Base URL:** `http://localhost:7000/api/`

## Job

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

Only a JWT which contains the value of the role of "hiring-manager" would be able to create a job posting. 

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

It can only be edited by the hiring manager, i.e., a user who created the job posting and has a JWT with the userId value that matches the job posting userId.

---

### PUT `/job/transfer`
**Description:** Updates an existing job listing.

**Request Body:**
```json
{
  "jobId": "int",
  "fromUserId": "int",
  "toUserId": "int",
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

**Authorization:** Requires JWT token in a cookie. The role in the JWT must be "admin". 

---

### DELETE `/job/{id}`
**Description:** Deletes a job listing.

**Path Parameters:**
- `id` (required) – The ID of the job.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `userId` of the job listing.

**Response:** HTTP status `204 No Content`.

It can only be edited by the hiring manager, i.e., a user who created the job posting and has a JWT with the userId value that matches the job posting userId.

---

### GET `/job/{id}/filter={filter}` - TODO
**Description:** Retrieves job listings based on a filter.

**Path Parameters:**
- `id` (required) – The ID of the job.
- `filter` (optional) – Filter criteria.


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
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the userId in the job record.

It can only be accessed by the hiring manager, i.e., a user who created the job posting and has a JWT with the userId value that matches the job posting userId.

---

### GET `/job/page?={page}&items?={items}` 
**Description:** Retrieves job listings based on pagination

**Path Parameters:**
- `page` (required) – page number
- `items` (optional) – number of items. Default 20. 

**Response:**
```json
{
  "content": [
    {
      "id": 1,
      "userId": 123,
      "department": "Engineering",
      "listingTitle": "Software Engineer",
      "dateListed": "2023-01-01T00:00:00Z",
      "dateClosed": "2023-01-31T00:00:00Z",
      "jobTitle": "Senior Developer",
      "jobDescription": "Develop and maintain software applications.",
      "additionalInformation": "Remote work available.",
      "listingStatus": "Open",
      "experienceLevel": "Senior"
    }
  ],
  "pageable": {
    "sort": {
      "sorted": true,
      "unsorted": false,
      "empty": false
    },
    "pageNumber": 0,
    "pageSize": 20,
    "offset": 0,
    "paged": true,
    "unpaged": false
  },
  "totalPages": 1,
  "totalElements": 1,
  "last": true,
  "size": 20,
  "number": 0,
  "sort": {
    "sorted": true,
    "unsorted": false,
    "empty": false
  },
  "numberOfElements": 1,
  "first": true,
  "empty": false
}
```

**Authorization:** Requires JWT token in a cookie.

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

It can only be accessed by the hiring manager, i.e., a user who created the job posting and has a JWT with the userId value that matches the job posting userId.

---

## Application

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

Only a JWT with the role of candidate would be able to view their own application. A JWT containing the role of hiring manager or admin would be able to view any application. 

---

### GET `/application/{id}/statistics`
**Description:** Retrieves application statistics by ID.

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
```

**Authorization:** Requires JWT token in a cookie. To access this endpoint the JWT needs to contain the "admin" role.

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

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `userId` in the request.

Only a candidate would be able to submit an application for a job. This role would be in the JWT

---

### PUT `/application/{id}` 
**Description:** Updates an existing job application.

**Request Body:**
```json
{
  "id": "int",
  "userId": "int",
  "dateApplied": "timestamp",
  "coverLetter": "text",
  "customResume": "text",
}
```
**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `id` in the request.

Only a candidate would be able to modify the fields in the request body.

---

### PUT `/application/manager/{id}`
**Description:** Updates an existing job application.

This is only for the manager. Its the endpoint which allows the manager to alter the status of the application

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

Only a candidate would be able to modify all the fields of the application. Whereas, a hiring manager would be able to ONLY update the applicationStatus value.

---


### DELETE `/application/{id}`
**Description:** Deletes a job application.

**Path Parameters:**
- `id` (required) – The ID of the application.

**Authorization:** Requires JWT token in a cookie. The `userId` in the token must match the `userId` of the application.

Only a user who has matching JWT userId value with the userId value within the application record would be able to delete it. 

**Response:** HTTP status `204 No Content`.

