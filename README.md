- composer install ( Required )

- php artisan migrate ( Create DB ) Note: Start MySQL

- php artisan serve to run app

- php artisan serve --host=ip ( Other Option )


### POST `/api/register`

* **Description:** Register a new user.
* **Auth:** Not required
* **Request Body:**

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "secret",
  "password_confirmation": "secret",
  "age" : "30",
  "gender":"male",
  "phone_number":"02394848",
  "role":"default: patient"
}
```

* **Response:**

  * `201 Created` – User registered successfully.
  * `422 Unprocessable Entity` – Validation failed.

---

### POST `/api/login`

* **Description:** Log in a user and retrieve an access token.
* **Auth:** Not required
* **Request Body:**

```json
{
  "email": "john@example.com",
  "password": "secret"
}
```

* **Response:**

  * `200 OK` – Login successful, token returned.
  * `401 Unauthorized` – Invalid credentials.

---

### POST `/api/logout`

* **Description:** Log out the current authenticated user.
* **Auth:** Required (Bearer Token)
* **Request Body:** *None*
* **Response:**

  * `200 OK` – Logout successful.

---

### GET `/api/dashboard`

* **Description:** Retrieve authenticated user dashboard info.
* **Auth:** Required (Bearer Token)
* **Request Body:** *None*
* **Response:**

  * `200 OK` – Dashboard data.

---

### POST `/api/forgot-password`

* **Description:** Request password reset code via email.
* **Auth:** Not required
* **Request Body:**

```json
{
  "email": "john@example.com"
}
```

* **Response:**

  * `200 OK` – Reset code sent.
  * `404 Not Found` – Email not associated with any user.

---

### POST `/api/verify-reset-code`

* **Description:** Verify the reset code sent via email.
* **Auth:** Not required
* **Request Body:**

```json
{
  "email": "john@example.com",
  "code": "123456"
}
```

* **Response:**

  * `200 OK` – Code verified.
  * `400 Bad Request` – Invalid code.
  * `404 Not Found` – No reset request found.

---

### POST `/api/reset-password`

* **Description:** Reset the user password using the verification code.
* **Auth:** Not required
* **Request Body:**

```json
{
  "email": "john@example.com",
  "code": "123456",
  "password": "newpassword",
  "password_confirmation": "newpassword"
}
```

* **Response:**

  * `200 OK` – Password reset successful.
  * `400 Bad Request` – Invalid reset attempt.

---

### GET `/api/auth/{provider}/redirect`

* **Description:** Redirect to social auth provider.
* **Auth:** Not required
* **Response:**

  * Redirect to provider login page.

---

### GET `/api/auth/{provider}/callback`

* **Description:** Handle callback from social auth provider.
* **Auth:** Not required
* **Response:**

  * `200 OK` – Authenticated and token returned.

---

### POST `/api/rays`

* **Description:** Upload a ray image or information.
* **Auth:** Required (Bearer Token)
* **Request Body:
```json
{
    "image": "required",
    "temperature" :"37",
    "systolic_bp" : "40",
    "heart_rate" : "60",
    "has_cough" : "true",
    "has_headaches" :"true",
    "can_smell_taste" : "true",
}
```
* **Response:**

  * `201 Created` – Ray uploaded.

---

### GET `/api/rays`

* **Description:** Get list of rays for authenticated user.
* **Auth:** Required (Bearer Token)
* **Response:**

  * `200 OK` – List of rays.

---

### POST `/api/appointments`

* **Description:** Book an appointment with a doctor.
* **Auth:** Required (Bearer Token)
* **Request Body:**

```json
{
  "doctor_id": 3,
  "appointment_time": "2025-07-21 14:30:00"
}
```

* **Response:**

  * `201 Created` – Appointment booked.
  * `409 Conflict` – Time slot already taken.

---

### GET `/api/appointments/available`

* **Description:** View available appointment slots.
* **Auth:** Not required
* **Response:**

  * `200 OK` – List of available slots.

---

### GET `/api/appointments/my`

* **Description:** Get user's appointments.
* **Auth:** Required (Bearer Token)
* **Response:**

  * `200 OK` – User appointments returned.

---

### GET `/api/me`

* **Description:** Get authenticated user profile.
* **Auth:** Required (Bearer Token)
* **Response:**

  * `200 OK` – Profile data.

---

### PUT `/api/me`

* **Description:** Update authenticated user profile.
* **Auth:** Required (Bearer Token)
* **Request Body:
```json
{
  "name": "John Doe",
  "email": "john33@example.com",
  "password": "secret",
  "password_confirmation": "secret"
  "age":"30",
  "gender":"male",
  "phone_number":"02394848",
  "role":"default: patient",
  
}
```
* **Response:**

  * `200 OK` – Profile updated.

---

### GET `/api/doctors`

* **Description:** List all doctors.
* **Auth:** Required (Bearer Token)
* **Response:**

  * `200 OK` – Doctors listed.

---

### GET `/api/doctor/patients`

* **Description:** Get all patients for authenticated doctor.
* **Auth:** Required (Bearer Token)
* **Response:**

  * `200 OK` – Patients listed.

---

### POST `/api/doctor/notes`

* **Description:** Add a note to a patient.
* **Auth:** Required (Bearer Token)
* **Request Body:
```json
{
  "patient_id": 5,
  "note": "The patient has a mild fever and requires rest.",
  "ray_id": "2"
}
```
* **Response:**

  * `201 Created` – Note added.

---

### PUT `/api/doctor/notes/{id}`

* **Description:** Update a note.
* **Auth:** Required (Bearer Token)
* **Request Body:
```json
    {
  "note": "Updated medical note text here"
  
}
```
* **Response:**
  * `200 OK` – Note updated.

---

### DELETE `/api/doctor/notes/{id}`

* **Description:** Delete a note.
* **Auth:** Required (Bearer Token)
* **Request Body:

* **Response:**

  * `200 OK` – Note deleted.

---

### GET `/api/doctor/patients/{id}/notes`

* **Description:** Get all notes for a specific patient.
* **Auth:** Required (Bearer Token)
* **Request Body:


* **Response:**


  * `200 OK` – Notes returned.

---

### GET `/api/doctor/rays/{id}/ai`

* **Description:** Get AI interpretation of a specific ray.
* **Auth:** Required (Bearer Token)


* **Response:**

  * `200 OK` – AI results returned.

---

### POST `/api/doctor/patients/status`

* **Description:** Set/update the status of a patient.
* **Auth:** Required (Bearer Token)
* **Request Body:** *(patient\_id, status, etc.)*
* **Response:**

  * `200 OK` – Status updated.

---


