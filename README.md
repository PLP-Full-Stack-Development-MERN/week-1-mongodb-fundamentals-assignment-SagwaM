**MongoDB Setup and Usage Guide**

Prerequisites

Ensure you have the following installed:

-MongoDB Community Server

-MongoDB Shell (mongosh)

-MongoDB Compass for GUI-based database management

*Installation Steps*

-Download MongoDB:

-Install MongoDB Community Server from the official website.

-Follow the installation instructions based on your operating system.

-Verify Installation:

Open a terminal or command prompt and run:

-mongod --version
-mongosh --version

If both commands return version numbers, MongoDB is successfully installed.

Start MongoDB Server:

Run the following command to start the MongoDB service:

mongod

Connect to MongoDB Shell:

Open another terminal and run:

mongosh

This connects you to the MongoDB instance.

**Database Setup**

1. Create a Database

use library

2. Create a Collection

library> db.books

3. Insert Data

db.books.insertMany([
  { title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Classic", ISBN: "978-0-7432-7356-5" },
  { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "978-0-452-28423-4" }
]);

4. Retrieve Data

 a) Get all books:

db.books.find({});

 b) Find books by author:

db.books.find({ author: "George Orwell" });

 c) Find books published after 2000:

db.books.find({ publishedYear: { $gt: 2000 } });

5. Update Data

 a) Update a book's published year:

db.books.updateOne({ title: "1984" }, { $set: { publishedYear: 1950 } });

 b) Add a new field (rating) to all books:

db.books.updateMany({}, { $set: { rating: 5.0 } });

6. Delete Data

 a) Delete a book by ISBN:

db.books.deleteOne({ ISBN: "978-0-7432-7356-5" });

 b) Remove all books in a genre:

db.books.deleteMany({ genre: "Dystopian" });

7. Aggregation Queries

 a) Total number of books per genre:

db.books.aggregate([
  { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
]);

 b) Average published year:

db.books.aggregate([
  { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
]);

c) Top-rated book:

db.books.aggregate([
  { $sort: { rating: -1 } },
  { $limit: 1 }
]);

8 Indexing

 a) Create an index on the author field:

db.books.createIndex({ author: 1 });

 b) Why use indexing?

Indexing improves query performance by reducing search time, making queries on indexed fields faster.

9) Additional Setup for an E-Commerce Database

-Create Users Collection
use e-commerce

e-commerce.users

Create Orders Collection

e-commerce.orders

Create Products Collection

e-commerce.products

*Insert Sample Data*

db.users.insertOne({
  name: "Alice Johnson",
  email: "alice@example.com",
  orders: []
});


**Troubleshooting**

Error: mongosh not recognized

Ensure MongoDB Shell (mongosh) is installed and added to the system PATH.

Query not returning expected results?

Check for typos in field names and values.

