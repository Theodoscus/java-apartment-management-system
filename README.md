# Apartment Building Management System

A Java Swing desktop application for managing apartment-building operations such as utility bills, announcements, events, services, polls, messages, and user profiles.

The project was developed as an academic software engineering project and uses a MySQL database for storing users, buildings, apartments, bills, services, announcements, events, polls, reviews, and messages.

---

## Overview

This application is designed for the basic digital management of an apartment building. It provides different flows for residents and employees, allowing users to view building information, communicate with other building members, follow announcements and events, check shared utility expenses, and review available services.

The application is built as a Java desktop application using Swing forms created with NetBeans GUI Builder. It connects directly to a local MySQL database through JDBC.

---

## Main Functionality

### Email-Based Login

The application starts from the `Welcome_Page` screen.

Users log in by entering their email address. The system checks whether the email exists in the `user` table and then redirects the user based on their role:

* Employees are redirected to the employee home page.
* Tenants, owners, and managers are redirected to the main user home page.

The current logged-in user is stored in the `login_status` table.

---

### User Home Page

The main home page gives access to the following modules:

* Utility bill payment
* Announcements
* Events
* Services
* Polls
* Messages
* Profile management

---

### Utility Bills

Residents can view the current month’s shared utility bill for their apartment.

The utility bill page displays:

* Current month utility bill amount
* Payment status
* Available user wallet balance
* Button for payment
* Button for detailed bill analysis

When a user pays the bill, the application updates the bill status and subtracts the amount from the user’s wallet balance.

---

### Employee Utility Bill Publication

Employees have a separate home page where they can select a building and publish monthly utility bills.

The employee flow supports:

* Listing buildings from the database
* Selecting a building
* Entering the total shared utility bill amount
* Adding a short bill description
* Splitting the total amount across apartments based on apartment size
* Storing the building-level and apartment-level bill records in the database

The application also checks whether utility bills have already been posted for the selected building in the current month.

---

### Announcements

Users can view the latest announcement.

Authorized non-tenant users can create new announcements by entering:

* Announcement title
* Announcement content
* Target audience type

Announcements are stored in the database and displayed from the most recent entry.

---

### Events

Users can view building-related events.

The events module displays event information connected to the user’s building, including:

* Event description
* Start date
* End date
* Creator name
* Creator surname

---

### Services and Reviews

The services module displays available building services from the database.

Users can:

* View the list of services
* Open a selected service
* See its phone number and description
* Submit a rating and review for the service

Reviews are stored in the `review` table and linked to both the selected service and the logged-in user.

---

### Polls

The application includes a basic poll system.

Users can view the latest poll question and its available answers.

Authorized non-tenant users can create a poll by entering:

* Poll question
* At least two answer options
* Up to four answer options in total

Polls are stored in the database and shown from the most recent entry.

---

### Messaging

The messaging module supports three conversation types:

* Group conversation
* Conversation with the building manager/admin
* Conversation with the property owner

Messages are stored in the `message` table with:

* Message content
* Sent date
* Sender user ID
* Message type
* Receiver email

The group chat displays messages from tenants, managers, and owners who are connected to the same building.

---

### Profile Management

Users can view and update their profile information.

Editable profile fields include:

* Name
* Surname
* Email
* Description

Profile data is loaded from the `user` table and updates are written back to the database.

---

## Database

The project includes SQL files for creating and populating the database:

```text
apartease_db.txt
apartease_db_data.txt
```

The schema includes tables for:

* Users
* Buildings
* Apartments
* User-apartment relationships
* Announcements
* Events
* Messages
* Polls
* Poll choices
* Services
* Reviews
* Utility bills per building
* Utility bills per apartment
* Login status

---

## Tech Stack

| Technology             | Purpose                           |
| ---------------------- | --------------------------------- |
| Java                   | Main programming language         |
| Java Swing             | Desktop graphical user interface  |
| NetBeans GUI Builder   | Form design and project structure |
| MySQL                  | Database management               |
| JDBC                   | Database connectivity             |
| MySQL Connector/J      | Java-MySQL driver                 |
| Ant / NetBeans Project | Build and run configuration       |

---

## Project Structure

```text
apartment-building-management-system/
├── ApartEase/
│   ├── src/apartease/
│   │   ├── Welcome_Page.java
│   │   ├── HomePage.java
│   │   ├── EmployeeHomePage.java
│   │   ├── UtilityBills.java
│   │   ├── UtilityBillsForm.java
│   │   ├── AnnouncementPage.java
│   │   ├── EventsPage.java
│   │   ├── PageServices.java
│   │   ├── PollsPage.java
│   │   ├── MessagePage.java
│   │   ├── Profile.java
│   │   └── DBConnection.java
│   ├── nbproject/
│   ├── build.xml
│   └── mysql-connector-java-8.0.27.jar
├── Notification/
├── apartease_db.txt
├── apartease_db_data.txt
└── README.md
```

---

## How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/ChrisLoukas007/ApartEase.git
cd ApartEase
```

### 2. Create the MySQL Database

Import the database schema:

```sql
source apartease_db.txt;
```

Then import the sample data:

```sql
source apartease_db_data.txt;
```

### 3. Configure the Database Connection

Open:

```text
ApartEase/src/apartease/DBConnection.java
```

Update the connection settings according to your local MySQL installation:

```java
DriverManager.getConnection(
    "jdbc:mysql://localhost:3307/aparteasedb",
    "root",
    "your_password"
);
```

Make sure the MySQL port, username, and password match your system.

### 4. Open the Project in NetBeans

Open the `ApartEase/` folder as a NetBeans project.

The main class is:

```text
apartease.Welcome_Page
```

### 5. Run the Application

Run the project from NetBeans.

Use an email from the seeded `user` table to log in.

---

## Current Limitations

This project is an academic prototype and has some implementation limitations:

* Login is based only on email and does not include password authentication.
* Database credentials are hardcoded in `DBConnection.java`.
* Several SQL queries are built using string concatenation and should be replaced with prepared statements.
* The `login_status` table works as a simple single-user session mechanism.
* Some database fields used by the Java code should be checked against the provided SQL schema before running.
* The project is intended for local execution, not production deployment.

---

## License

This project was developed for academic purposes.
