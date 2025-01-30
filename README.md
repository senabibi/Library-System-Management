# Library Management System using SQL - P2

[![Contributors](https://img.shields.io/github/contributors/senabibi/LibrarySystemManagement)](https://github.com/senabibi/LibrarySystemManagement/graphs/contributors)
[![Forks](https://img.shields.io/github/forks/senabibi/LibrarySystemManagement)](https://github.com/senabibi/LibrarySystemManagement/network/members)
[![Stargazers](https://img.shields.io/github/stars/senabibi/LibrarySystemManagement)](https://github.com/senabibi/LibrarySystemManagement)
[![Issues](https://img.shields.io/github/issues/senabibi/LibrarySystemManagemen)](https://github.com/senabibi/PostgresqlTopTen/issues)
[![MIT License](https://img.shields.io/github/license/senabibi/LibrarySystemManagemen)](https://opensource.org/licenses/MIT)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Nursena%20Bitirgen-blue)](https://www.linkedin.com/in/nursena-bitirgen-5743341b9/)

## Table of Contents

1. [About The Project](#about-the-project)
   - [Objectives](#objectives)
2. [Getting Started](#getting-started)
   - [Prerequisites](#prerequisites)
   - [Installation](#installation)
   - [Database Setup](#database-setup)
3. [Usage](#usage)
4. [Roadmap](#roadmap)
5. [Contributing](#contributing)
6. [License](#license)
7. [Contact](#contact)
8. [Acknowledgments](#acknowledgments)

---

## About The Project

The **Library Management System using SQL** project demonstrates the use of SQL to design and implement a system to manage library data. This includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries for efficient data retrieval. The project is intended to help users understand database management, relationships between tables, and best practices for SQL querying.

### Objectives

- **Set up the Library Management System Database**: Create and populate the database with tables for branches, employees, members, books, issued status, and return status.
- **CRUD Operations**: Perform Create, Read, Update, and Delete operations on the data.
- **CTAS (Create Table As Select)**: Utilize CTAS to create new tables based on query results.
- **Advanced SQL Queries**: Develop complex queries to analyze and retrieve specific data.

---

## Getting Started

### Prerequisites

- [PostgreSQL](https://www.postgresql.org/download/): You’ll need PostgreSQL to run this project.
- [Visual Studio Code](https://code.visualstudio.com/): A recommended IDE for code editing and running scripts locally.
- [Brave](https://brave.com/): A recommended browser for optimal viewing and performance of the project docs and demos.

### Installation

1. Download and install PostgreSQL from the [official PostgreSQL website](https://www.postgresql.org/download/).
2. Download and install Visual Studio Code from the [official website](https://code.visualstudio.com/).
3. Once installed, configure the PostgreSQL database to integrate with the project files.

### Database Setup

Run the following SQL commands in your PostgreSQL environment to set up the database:

```sql
DROP TABLE IF EXISTS branch;
CREATE TABLE branch 
(
branch_id VARCHAR(10) PRIMARY KEY,
manager_id VARCHAR(10),
branch_address VARCHAR(30),
contact_no VARCHAR(15)
);

DROP TABLE IF EXISTS employess;
CREATE TABLE employess
(
	emp_id VARCHAR(10) PRIMARY KEY,
	emp_name VARCHAR(30) ,
	position VARCHAR(30),
	salary INT,
    branch_id VARCHAR(25)
	);

DROP TABLE IF EXISTS books;
CREATE TABLE books
(
	isbn VARCHAR(20) PRIMARY KEY,
	book_title VARCHAR(75),
	category VARCHAR(10),
	rental_price FLOAT,
	status VARCHAR(15),
	author VARCHAR(35),
	publisher VARCHAR(35)
);
ALTER TABLE books
ALTER COLUMN category TYPE VARCHAR(20)

DROP TABLE IF EXISTS members;
CREATE TABLE members
(
	member_id VARCHAR(10) PRIMARY KEY,
	member_name VARCHAR(25) ,
	member_address VARCHAR(75),
	reg_date DATE
);

CREATE TABLE issued_status
(
issued_id VARCHAR(10) PRIMARY KEY,
issued_member_id VARCHAR(10),
issued_book_name VARCHAR(75),
issued_date DATE,
issued_book_isbn VARCHAR(25),
issued_emp_id VARCHAR(10)
);
DROP TABLE IF EXISTS return_status;
CREATE TABLE return_status
(
	return_id VARCHAR(10) PRIMARY KEY,
	issued_id VARCHAR(10),
	return_book_name VARCHAR(75),
	return_date DATE,
	return_book_isbn VARCHAR(20)
);

---FK
ALTER TABLE return_status
ADD CONSTRAINT fk_issued_status
FOREIGN KEY (issued_id)
REFERENCES issued_status(issued_id);
```

## Usage

<div align="center">
    <img src="https://github.com/senabibi/LibrarySystemManagement/blob/main/ERD.png" alt="Library Management System ERD">
</div>

To use the **Library Management System** project, follow these steps to set up and run the system:

### 1. **PostgreSQL Installation:**
   - Ensure that PostgreSQL is installed on your system. If it's not already installed, you can download it from the [official PostgreSQL website](https://www.postgresql.org/download/).

### 2. **Creating the Database:**
   - After installing PostgreSQL, you need to create the `library_db` database by running the following SQL command in your PostgreSQL environment:

     ```sql
     CREATE DATABASE library_db;
     ```

   - Once the database is created, you can use the following SQL script to set up all the necessary tables for the library management system:

     ```sql
     CREATE TABLE branches (
         branch_id SERIAL PRIMARY KEY,
         branch_name VARCHAR(100) NOT NULL,
         location VARCHAR(200) NOT NULL
     );

     CREATE TABLE employees (
         employee_id SERIAL PRIMARY KEY,
         first_name VARCHAR(50) NOT NULL,
         last_name VARCHAR(50) NOT NULL,
         email VARCHAR(100) UNIQUE NOT NULL,
         branch_id INT,
         FOREIGN KEY (branch_id) REFERENCES branches(branch_id)
     );

     CREATE TABLE members (
         member_id SERIAL PRIMARY KEY,
         first_name VARCHAR(50) NOT NULL,
         last_name VARCHAR(50) NOT NULL,
         email VARCHAR(100) UNIQUE NOT NULL,
         membership_date DATE NOT NULL
     );

     CREATE TABLE books (
         book_id SERIAL PRIMARY KEY,
         title VARCHAR(100) NOT NULL,
         author VARCHAR(100) NOT NULL,
         category VARCHAR(50),
         branch_id INT,
         FOREIGN KEY (branch_id) REFERENCES branches(branch_id)
     );

     CREATE TABLE issued_books (
         issue_id SERIAL PRIMARY KEY,
         book_id INT,
         member_id INT,
         issue_date DATE NOT NULL,
         return_date DATE,
         FOREIGN KEY (book_id) REFERENCES books(book_id),
         FOREIGN KEY (member_id) REFERENCES members(member_id)
     );
     ```

   - These SQL commands will create the tables for managing branches, employees, members, books, and issued books. Be sure to replace any placeholder values if necessary.

### 3. **Menu-Driven Interface:**
   - Once the database is set up, the system will provide a menu-driven interface allowing you to perform different operations, such as:
     - **Add new books** to the library collection
     - **Register new members** into the system
     - **Issue and return books** for members
     - **Update book, employee, and member information**
     - **View library reports** like the number of books issued, overdue books, etc.

### 4. **Exploratory Data Analysis (EDA):**
   - Explore the data in the database, perform checks for missing values, and use SQL queries to analyze different aspects of the library system, such as:
     - Total number of books in the library
     - Books issued by a specific member
     - Members who have overdue books

### 5. **Running Business Queries:**
   - Use the provided SQL queries to retrieve and analyze data, such as:
     - Retrieve all books issued to a specific member:
       ```sql
       SELECT books.title, issued_books.issue_date, issued_books.return_date
       FROM books
       JOIN issued_books ON books.book_id = issued_books.book_id
       WHERE issued_books.member_id = 1;
       ```

     - Find all books overdue in a specific branch:
       ```sql
       SELECT books.title, issued_books.return_date
       FROM books
       JOIN issued_books ON books.book_id = issued_books.book_id
       JOIN branches ON books.branch_id = branches.branch_id
       WHERE issued_books.return_date < CURRENT_DATE
         AND branches.branch_name = 'Main Branch';
       ```

     - Calculate the total number of books issued by category:
       ```sql
       SELECT books.category, COUNT(*) AS total_books_issued
       FROM books
       JOIN issued_books ON books.book_id = issued_books.book_id
       GROUP BY books.category;
       ```

### 6. **Exiting the Interface:**
   - After completing the analysis or performing the desired operations, you can exit the interface and the PostgreSQL session.

Feel free to explore and interact with the **Library Management System** project by performing CRUD operations and running business queries to answer specific questions about the library's operations.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Roadmap

- [ ] **PostgreSQL Setup:** Ensure PostgreSQL is installed and configured on your system for project development.
- [ ] **Database Setup:** Run the provided SQL scripts to set up `library_db` and tables such as `branches`, `employees`, `members`, `books`, and `issued_books`.
- [ ] **Perform CRUD Operations:** Use SQL commands to add, update, and delete records for books, members, and employees.
- [ ] **Query Data:** Write SQL queries to explore the library data, check for missing values, and understand relationships between entities.
- [ ] **Test and Debug:** Test the system and ensure all queries work as expected and the operations function properly.
- [ ] **Documentation:** Document the steps for setting up the database, writing queries, and analyzing the library data.

This roadmap will guide you through understanding, interacting with, and testing the **Library Management System** project. Follow these steps to explore the system and manage the library’s operations efficiently.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Contributing

Contributions are what make the open-source community an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have any suggestions for improvements, feel free to fork the repository, create a pull request, or open an issue with the "enhancement" tag. Also, don't forget to give the project a star! Thank you!

### Steps to Contribute:
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/FeatureName`)
3. Commit your Changes (`git commit -m 'Add new feature'`)
4. Push to the Branch (`git push origin feature/FeatureName`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Contact

Nursena Bitirgen - [LinkedIn](https://www.linkedin.com/in/nursena-bitirgen-5743341b9/)

Project Link: [https://github.com/senabibi/LibrarySystemManagement](https://github.com/senabibi/LibrarySystemManagement)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Acknowledgments

The development of the **Library Management System** project was made possible thanks to the following:

* **PostgreSQL Knowledge:** Thanks to PostgreSQL for providing a powerful relational database system for managing the library data.
* **SQL Skills:** Special thanks for developing SQL skills to create and manipulate tables and queries.
* **Database Design:** Acknowledgment for learning and implementing the database design, including relationships between tables.
* **Exploratory Data Analysis (EDA):** Thanks for learning data exploration techniques to check for missing values and gain insights from the library data.
* **Testing and Debugging:** Recognition for testing and ensuring all queries function as expected.
* **Documentation:** Grateful for the opportunity to create detailed documentation, ensuring users can easily set up and use the system.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## How to Use

1. **Clone the Repository:** Clone the repository from GitHub.
2. **Set Up the Database:** Run the SQL scripts provided in the `database_setup.sql` file to set up the necessary tables and database (`library_db`).
3. **Run Queries:** Use the SQL queries provided in the `queries.sql` file to perform various data retrieval and analysis tasks.

