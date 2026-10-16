# Transport Ticket Booking System

A web-based transport ticket booking system built using Python, Flask, HTML, and MySQL. The application allows users to register, log in, search for available transport options, book tickets, and view their bookings.

## Features

- User registration and login
- Dashboard for logged-in users
- Search for flights, trains, and buses
- Search transport options by source, destination, and journey date
- Different seat and class options for each transport type
- Automatic ticket price calculation based on the selected seat type
- Ticket confirmation after booking
- View previously booked tickets
- MySQL database integration

## Technologies Used

- Python
- Flask
- MySQL
- HTML
- Jinja2 templates
- MySQL Connector for Python
- python-dotenv

## Project Structure

```text
transport-ticket-booking-system/
├── templates/
│   ├── available_transports.html
│   ├── book_select.html
│   ├── confirm_booking.html
│   ├── dashboard.html
│   ├── login.html
│   ├── signup.html
│   ├── ticket_confirmation.html
│   └── view_tickets.html
├── app.py
├── populate_db.py
├── requirements.txt
├── .gitignore
└── README.md
```

## Requirements

Before running the project, install the following:

- Python 3
- MySQL Server
- MySQL Workbench (optional, for managing the database)
- Git (optional, for cloning the repository)

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/rajvard1507/transport-ticket-booking-system.git
cd transport-ticket-booking-system
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Configure the database

Start your MySQL server and connect to it using MySQL Workbench or the MySQL command-line client.

Create the database:

```sql
CREATE DATABASE transport_db;
USE transport_db;
```

Create the required tables:

```sql
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE flights (
    flight_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    from_city VARCHAR(100) NOT NULL,
    to_city VARCHAR(100) NOT NULL,
    day VARCHAR(20) NOT NULL,
    time VARCHAR(20) NOT NULL,
    base_price DECIMAL(10, 2) NOT NULL,
    available_tickets INT NOT NULL
);

CREATE TABLE trains (
    train_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    from_city VARCHAR(100) NOT NULL,
    to_city VARCHAR(100) NOT NULL,
    day VARCHAR(20) NOT NULL,
    time VARCHAR(20) NOT NULL,
    base_price DECIMAL(10, 2) NOT NULL,
    available_tickets INT NOT NULL
);

CREATE TABLE buses (
    bus_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    from_city VARCHAR(100) NOT NULL,
    to_city VARCHAR(100) NOT NULL,
    day VARCHAR(20) NOT NULL,
    time VARCHAR(20) NOT NULL,
    base_price DECIMAL(10, 2) NOT NULL,
    available_tickets INT NOT NULL
);

CREATE TABLE tickets (
    ticket_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    mode VARCHAR(20) NOT NULL,
    transport_id INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    gender VARCHAR(20) NOT NULL,
    seat_type VARCHAR(50) NOT NULL,
    journey_date DATE NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

### 5. Configure environment variables

Create a `.env` file in the project's root directory.

Add the following settings, replacing the example values with your own MySQL credentials and a randomly generated Flask secret key:

```dotenv
DB_HOST=localhost
DB_USER=your_mysql_username
DB_PASSWORD=your_mysql_password
DB_NAME=transport_db
FLASK_SECRET_KEY=your_random_secret_key
```

Keep this file private. Do not commit it to GitHub.

### 6. Populate the transport database

Run:

```bash
python populate_db.py
```

This script inserts sample flight, train, and bus records into the database.

**Warning:** The script deletes existing records from the `flights`, `trains`, and `buses` tables before inserting new sample data. Back up any data you want to keep before running it.

### 7. Run the application

Start the Flask application:

```bash
python app.py
```

Open the following address in your browser:

http://127.0.0.1:5000

Register an account to access the dashboard and booking features.

## Notes

- MySQL must be running before you start the application.
- The database tables must be created before running `populate_db.py`.
- The application uses sample transport data.
- Database credentials and the Flask secret key should be stored in environment variables rather than hardcoded in the source files.
- This project is intended as a learning project and may require additional security improvements before production use.

## License

No license has been specified for this project.