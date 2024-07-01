# Train Booking System API

This RESTful API is designed for a train booking system, offering endpoints for user registration, login, seat booking, checking seat availability, and retrieving booking details. It is developed using Django and the Django Rest Framework.

## Installation

1. Clone the repository:
```
https://github.com/adarshkumar5776/railway_booking_system
```

2. Install the required dependencies:
```python
pip install -r requirements.txt
```

3. Run migrations to set up the database:
```python
python manage.py makemigrations
python manage.py migrate
```

4. Start the development server:
```python
python manage.py runserver
```

5. Access the API at `http://localhost:8000/`.

## Database Configuration
The system uses PostgreSQL with the following settings:

```python
'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'RailwayBookingSystem',
        'USER': 'postgres',
        'PASSWORD':'1234',
        'HOST':'localhost' 
    }
```

## Endpoints

### User Registration

- **Description:** Create a new user account using a username and email that have not been used before.

- **URL:** `/user/register/`
- **Method:** `POST`
- **Parameters:**
- `username` (string): User's username.
- `password` (string): User's password.
- `email` (string): User's email address.

### User Login

- **Description:** Authenticate and obtain an authentication token for a logged-in user.
- **URL:** `/user/login/`
- **Method:** `POST`
- **Parameters:**
- `username` (string): User's username.
- `password` (string): User's password.


### User Logout

- **Description:**Log out the authenticated user and invalidate/delete the authentication token.
- **URL:** `/user/logout/`
- **Method:** `POST`
- **Authorization:** Token-based authentication required.

### Add Train

- **Description:** Create a new train entry with a unique train number, starting point, destination, and total available seats.
- **URL:** `/add_train/`
- **Method:** `POST`
- **Parameters:**
- `train_number` (integer): Train number (unique).
- `source` (string): Source station.
- `destination` (string): Destination station.
- `total_seats` (integer): Total number of seats on the train.
- **Authorization:** Superuser authentication required.

### Book Seat

- **Description:** Books seats on a particualr train.
- **URL:** `/user/book_seat/`
- **Method:** `POST`

- **Parameters:**
- `train_number` (integer): Train number.
- `user_id` (integer): User's ID.
- `seat_count` (integer): Number of seats to book.
- **Authorization:** Token-based authentication required.

### Get Seat Availability

- **Description:** Retrieve seat availability information for trains traveling between a specified source and destination.
- **URL:** `/user/get_seat_availability/`
- **Method:** `GET`
- **Parameters:**
- `source` (string): Source station.
- `destination` (string): Destination station.
- **Authorization:** Token-based authentication required.

### Get Booking Details

- **URL:** `/user/get_booking_details/<int:id>/`
- **Method:** `GET`
- **Description:** Retrieve booking details for a particular user.
- **Parameters:**
- `id` (integer): User's ID.
- **Authorization:** Token-based authentication required.

## Authentication

- **Token Authentication:**
Authentication is necessary for accessing most endpoints, utilizing a token-based system. Users must log in to acquire a token, which needs to be included in the Authorization header for subsequent requests.
- **CSRF Token:** Certain endpoints require CSRF tokens to prevent CSRF attacks. Make sure to include the CSRF token in the request headers.



### Models

#### Train Model

The `Train` model represents a train in the system. It includes the following fields:

- `train_number`: An integer field representing the unique number assigned to the train.
- `source`: A character field indicating the origin station of the train journey.
- `destination`: A character field indicating the destination station of the train journey.
- `total_seats`: An integer field representing the total number of seats available on the train.
- `create_time`: A DateTime field automatically capturing the date and time when the train record was created.
- `update_time`: A DateTime field automatically capturing the date and time when the train record was last updated.

This model is used to manage information about trains, including their identification, origin, destination, total available seats, and timestamps for creation and updates.

#### Booking Model

The `Booking` model represents a booking made by a user for a specific train in the system. It includes the following fields:

- `user`: A foreign key field linking to the `User` model, representing the user who made the booking.
- `train`: A foreign key field linking to the `Train` model, representing the train for which the booking is made.
- `seat_count`: An integer field representing the number of seats booked by the user for the train.
- `create_time`: A DateTime field automatically capturing the date and time when the booking record was created.
- `update_time`: A DateTime field automatically capturing the date and time when the booking record was last updated.

This model is used to manage information about bookings made by users, including details such as the user who made the booking, the train for which the booking is made, the number of seats booked, and timestamps for creation and updates.
