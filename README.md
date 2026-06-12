# Online Reservation System 🚄

A lightweight, desktop-based **Online Reservation System** built in Java using the Swing GUI framework. This application features a modular design with user authentication, automated ticket booking, unique PNR generation, and a centralized in-memory database to simulate a seamless train ticketing experience.

---

## 📌 Features

* **Secure Access:** Lockout protection via an authorized Login Form.
* **Smart Auto-Fill:** Select a train number, and the system automatically fills in the corresponding train name.
* **Centralized Database:** Uses an in-memory data architecture to save, retrieve, and delete data instantly.
* **Dynamic PNR Generation:** Automatically creates a unique 5-digit Passenger Name Record (PNR) upon every successful booking.
* **Instant Ticket Lookup & Cancellation:** Enter a PNR to display the full passenger itinerary before confirming cancellation.

---

## 🛠️ Project Architecture & Modules

The application is structured into three main functional modules, managed smoothly via a single window interface (`CardLayout`):

1.  **Login Form:** Validates credentials (`admin` / `password`) before granting access to the system.
2.  **Reservation Form:** Gathers passenger inputs (Name, Age, Route, Class, Date) and commits the ticket to the central map.
3.  **Cancellation Form:** Fetches existing reservation details using a PNR number and purges the record upon user confirmation (**OK**).

---

## 🚀 How to Run the Project

### Prerequisites
* **Java Development Kit (JDK):** Version 8 or higher installed on your system.
* **Git:** (Optional) To clone the repository.

### Step-by-Step Execution

1.  **Clone or Download the Repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/Online-Reservation-System.git](https://github.com/YOUR_USERNAME/Online-Reservation-System.git)
    cd Online-Reservation-System
    ```

2.  **Compile the Java File:**
    ```bash
    javac OnlineReservationSystem.java
    ```

3.  **Run the Application:**
    ```bash
    java OnlineReservationSystem
    ```

---

## 🔑 Default Credentials

To access the system, use the following default authorized login details:
* **Username:** `admin`
* **Password:** `password`

---

## 📦 How to Build an Executable `.jar` File

If you want to pack this single-file source code into a clickable standalone application, run the following commands in your terminal:

1. Create a file named `manifest.txt` and add this line inside it:
   ```text
   Main-Class: OnlineReservationSystem
