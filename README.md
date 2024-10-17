# Capstone Backend

## User Service 

Most likely host: http:localhost:8000/

users/registration POST

Expected Body:

{
email: string 
password: string 
name: string
}

Response: 

Body: empty

Cookie: JWT (containing claims with userId and role)


users/{id}

id within the param

returns:

{
`id` int NOT NULL AUTO_INCREMENT,
  `full_name` varchar(50) DEFAULT NULL,
  `email` varchar(50) DEFAULT NULL,
  `address` varchar(100) DEFAULT NULL,
  `phone` varchar(25) DEFAULT NULL,
  `resume` text,
  `role` varchar(50),
}  

users/login

{
email: string 
password: string 
}

Response: 

Body: empty

Cookie: JWT (containing claims with userId and role)


users/{id}

expecting id param
Cookie which contains the jwt of the user

users/id?=id PUT
expecting id param
Cookie which contains the jwt of the user
{
  `full_name` varchar(50) DEFAULT NULL,
  `email` varchar(50) DEFAULT NULL,
  `address` varchar(100) DEFAULT NULL,
  `phone` varchar(25) DEFAULT NULL,
  `resume` text,
  `role` varchar(50),
  }



## Job & Application Service


job/id?=id 

requires id param 

response:

{
`id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `department` varchar(25) DEFAULT NULL,
  `listing_title` varchar(100) DEFAULT NULL,
  `date_listed` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `date_closed` timestamp NULL DEFAULT NULL,
  `job_title` varchar(45) DEFAULT NULL,
  `job_description` text,
  `additional_information` text,
  `listing_status` varchar(25) DEFAULT NULL,
  `experience_level` varchar(100) DEFAULT NULL,
}

job POST

requires body:

{
  `user_id` int DEFAULT NULL,
  `department` varchar(25) DEFAULT NULL,
  `listing_title` varchar(100) DEFAULT NULL,
  `date_listed` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `date_closed` timestamp NULL DEFAULT NULL,
  `job_title` varchar(45) DEFAULT NULL,
  `job_description` text,
  `additional_information` text,
  `listing_status` varchar(25) DEFAULT NULL,
  `experience_level` varchar(100) DEFAULT NULL,
  `model_resume` text,
  `model_cover_letter` text,
}

response: 

{
`id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `department` varchar(25) DEFAULT NULL,
  `listing_title` varchar(100) DEFAULT NULL,
  `date_listed` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `date_closed` timestamp NULL DEFAULT NULL,
  `job_title` varchar(45) DEFAULT NULL,
  `job_description` text,
  `additional_information` text,
  `listing_status` varchar(25) DEFAULT NULL,
  `experience_level` varchar(100) DEFAULT NULL,
  `model_resume` text,
  `model_cover_letter` text,
}

job PUT:

requires body:

{`id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `department` varchar(25) DEFAULT NULL,
  `listing_title` varchar(100) DEFAULT NULL,
  `date_listed` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `date_closed` timestamp NULL DEFAULT NULL,
  `job_title` varchar(45) DEFAULT NULL,
  `job_description` text,
  `additional_information` text,
  `listing_status` varchar(25) DEFAULT NULL,
  `experience_level` varchar(100) DEFAULT NULL,
  `model_resume` text,
  `model_cover_letter` text,
}

job/id?=id DELETE 

requires an id param 
requires the cookie with the JWT so that if the JWT and the user_id match then it the job will be deleted

returns 204 code 

job/id?=id/filter=?filter GET

job/id?=id/applications GET

expects id in the param of the job 

returns

list 
{
 `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `job_id` int DEFAULT NULL,
  `date_applied` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `cover_letter` text,
  `custom_resume` text,
  `application_status` varchar(45) DEFAULT NULL,
   `years_of_experience` int,
  `match_job_description_score` int,
  `past_experience_score` int,
  `motivation_score` int,
  `acedemic_achievement_score` int,
  `pegidre_score` int,
  `tragjectory_score` int,
  `extenuating_circumstances_score` int,
  `average_score` text,
  `review` text,
}


application/id?=id GET

expects id param

returns 

{
 `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `job_id` int DEFAULT NULL,
  `date_applied` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `cover_letter` text,
  `custom_resume` text,
  `application_status` varchar(45) DEFAULT NULL,
}

application POST

expects the below request body:

{
 `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `job_id` int DEFAULT NULL,
  `date_applied` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `cover_letter` text,
  `custom_resume` text,
  `application_status` varchar(45) DEFAULT NULL,
}

returns: 

{
 `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `job_id` int DEFAULT NULL,
  `date_applied` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `cover_letter` text,
  `custom_resume` text,
  `application_status` varchar(45) DEFAULT NULL,
}

application/id?=id PUT

expects the below body:

{
 `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `job_id` int DEFAULT NULL,
  `date_applied` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `cover_letter` text,
  `custom_resume` text,
  `application_status` varchar(45) DEFAULT NULL,
}

returns: 

{
 `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int DEFAULT NULL,
  `job_id` int DEFAULT NULL,
  `date_applied` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  `cover_letter` text,
  `custom_resume` text,
  `application_status` varchar(45) DEFAULT NULL,
}

application/id?=id DELETE

expects id param 
expects to have the JWT in the cookie that will hold the user_id which will need match 

returns 204




