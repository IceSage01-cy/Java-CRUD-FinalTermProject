# Java CRUD Final Term Project

A Java Swing desktop application for managing clients, products, and purchases. The project implements CRUD operations backed by a MySQL database and provides a simple buyer monitoring system interface.

## Features

- **Client management**
  - Add new clients
  - View client records
  - Update client information
  - Delete selected clients
  - Store first name, middle initial, last name, address, and gender

- **Product management**
  - Add products with a name, code, and category
  - View product records
  - Delete selected products
  - Choose from predefined categories such as Food, Supplies, Grocery, Amenities, and Attire

- **Purchase management**
  - Record client purchases
  - Select or search for clients and products
  - Store quantity, price, and purchase date
  - Update and delete purchase records
  - Export purchase data to `buys_export.csv`

- **Navigation**
  - Move between the client, product, and purchase screens from within the application

## Technologies Used

- Java 17
- Java Swing
- MySQL
- JDBC
- MySQL Connector/J 9.5.0
- Apache Ant / NetBeans project structure

## Project Structure

```text
Java-CRUD-FinalTermProject/
├── README.md
└── FinalTermExam/
    ├── Libraries/
    │   └── mysql-connector-j-9.5.0.jar
    ├── src/
    │   └── finaltermexam/
    │       ├── FinalTermExam.java
    │       ├── Product.java
    │       └── ManageBuys.java
    ├── nbproject/
    ├── build.xml
    ├── manifest.mf
    └── buys_export.csv
```

## Database Setup

The application expects a local MySQL database named `buyer_monitoring_system`.

Create the database and tables with the following SQL:

```sql
CREATE DATABASE buyer_monitoring_system;
USE buyer_monitoring_system;

CREATE TABLE clients (
    clientID INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    middle_initial VARCHAR(10) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    address VARCHAR(255) NOT NULL,
    gender VARCHAR(50) NOT NULL
);

CREATE TABLE products (
    productID INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(150) NOT NULL,
    code VARCHAR(50) NOT NULL,
    category VARCHAR(100) NOT NULL
);

CREATE TABLE buys (
    buyID INT AUTO_INCREMENT PRIMARY KEY,
    clientName VARCHAR(200) NOT NULL,
    productName VARCHAR(150) NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    date DATE NOT NULL
);
```

> The current Java source connects using `localhost:3306`, the database name `buyer_monitoring_system`, the MySQL user `root`, and an empty password. Update the connection settings in the Java classes if your MySQL configuration is different.

## Requirements

- Java Development Kit (JDK) 17 or later
- MySQL Server
- Apache NetBeans, or another IDE that supports Java Swing and Ant projects
- MySQL Connector/J

The repository includes the MySQL JDBC driver in `FinalTermExam/Libraries/mysql-connector-j-9.5.0.jar`.

## Running the Project in NetBeans

1. Start MySQL Server.
2. Create the `buyer_monitoring_system` database and tables using the SQL above.
3. Open Apache NetBeans.
4. Select **File > Open Project** and choose the `FinalTermExam` directory.
5. Verify that the MySQL Connector/J library is included in the project dependencies.
6. Right-click the project and select **Clean and Build**.
7. Run the project. The main class is:

```text
finaltermexam.FinalTermExam
```

The application opens on the client management screen.

## Building from the Command Line

From the `FinalTermExam` directory, run:

```bash
ant clean jar
```

The generated JAR file is placed in:

```text
dist/FinalTermExam.jar
```

To run the compiled application, ensure the MySQL JDBC driver is available on the runtime classpath and execute:

```bash
java -cp "dist/FinalTermExam.jar;Libraries/mysql-connector-j-9.5.0.jar" finaltermexam.FinalTermExam
```

On macOS or Linux, use `:` instead of `;` as the classpath separator:

```bash
java -cp "dist/FinalTermExam.jar:Libraries/mysql-connector-j-9.5.0.jar" finaltermexam.FinalTermExam
```

## Application Screens

### Client Dashboard

The client dashboard displays existing clients in a table and provides controls for adding, updating, and deleting client records. It also links to the product and purchase screens.

### Product Dashboard

The product dashboard displays product ID, name, code, and category. Products can be added and deleted from the database.

### Purchase Dashboard

The purchase dashboard displays purchase ID, client, product, quantity, price, and date. Purchases can be added, updated, deleted, and exported as CSV data.

## CSV Export

Selecting **Generate Receipt** on the purchase screen exports the currently displayed purchase records to:

```text
FinalTermExam/buys_export.csv
```

## Configuration Notes

Database connection settings are currently defined directly in the Java source files. For a production-ready version, move credentials and connection details to environment variables or a configuration file instead of storing them in source code.

## Known Limitations

- Database credentials are hard-coded for local development.
- Product records currently support deletion but do not include a product update workflow.
- Input validation is basic and should be expanded for invalid numbers, dates, duplicate codes, and missing records.
- The application requires the MySQL database to be running before it starts successfully.

## License

This project is provided for educational and academic purposes.
