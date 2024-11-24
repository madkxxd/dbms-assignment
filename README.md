# dbms-assignment

MYSQL COMMANDS:

CREATE TABLE Books (
    Book_ID INT PRIMARY KEY,
    Title VARCHAR(255),
    Author VARCHAR(255),
    Genre VARCHAR(100),
    Year_Published INT,
    Price DECIMAL(10, 2)
);

CREATE TABLE Members (
    Member_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Address VARCHAR(255),
    Contact VARCHAR(15),
    Email VARCHAR(100)
);

CREATE TABLE Staff (
    Staff_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Position VARCHAR(100),
    Contact VARCHAR(15)
);

CREATE TABLE Transactions (
    Transaction_ID INT PRIMARY KEY,
    Member_ID INT,
    Book_ID INT,
    Issue_Date DATE,
    Return_Date DATE,
    Status ENUM('Issued', 'Returned') DEFAULT 'Issued',
    FOREIGN KEY (Member_ID) REFERENCES Members(Member_ID),
    FOREIGN KEY (Book_ID) REFERENCES Books(Book_ID)
);

INSERT INTO Books (Book_ID, Title, Author, Genre, Year_Published, Price)
VALUES
(1, 'The Great Gatsby', 'F. Scott Fitzgerald', 'Fiction', 1925, 10.99),
(2, 'To Kill a Mockingbird', 'Harper Lee', 'Fiction', 1960, 7.99),
(3, '1984', 'George Orwell', 'Dystopian', 1949, 8.99),
(4, 'Moby Dick', 'Herman Melville', 'Adventure', 1851, 12.99),
(5, 'War and Peace', 'Leo Tolstoy', 'Historical', 1869, 15.99);

INSERT INTO Members (Member_ID, Name, Address, Contact, Email)
VALUES
(1, 'Aryan Patel', '123 MG Road, Mumbai', '9876543210', 'aryan.patel@example.com'),
(2, 'Akshay Sharma', '456 Banjara Hills, Hyderabad', '9123456789', 'akshay.sharma@example.com'),
(3, 'Priya Iyer', '789 Anna Nagar, Chennai', '9988776655', 'priya.iyer@example.com'),
(4, 'Sneha Rao', '321 Indiranagar, Bangalore', '9654321098', 'sneha.rao@example.com');


INSERT INTO Staff (Staff_ID, Name, Position, Contact)
VALUES
(1, 'Amit Kumar', 'Librarian', '9876543210'),
(2, 'Ravi Gupta', 'Assistant Librarian', '9123456789'),
(3, 'Neha Singh', 'Clerk', '9988776655');


INSERT INTO Transactions (Transaction_ID, Member_ID, Book_ID, Issue_Date, Return_Date, Status)
VALUES
(1, 1, 1, '2024-11-01', '2024-11-10', 'Returned'),
(2, 2, 2, '2024-11-05', '2024-11-12', 'Returned'),
(3, 3, 3, '2024-11-07', '2024-11-14', 'Returned'),
(4, 4, 4, '2024-11-08', '2024-11-15', 'Returned'),
(5, 1, 5, '2024-11-10', NULL, 'Issued');

add a new book;

INSERT INTO Books (Book_ID, Title, Author, Genre, Year_Published, Price)
VALUES (6, 'The Alchemist', 'Paulo Coelho', 'Adventure/Fantasy', 1988, 9.99);

update book info;

UPDATE Books
SET Price = 12.99
WHERE Book_ID = 6;

delete a book;

DELETE FROM Books
WHERE Book_ID = 6;

register a new member;

INSERT INTO Members (Member_ID, Name, Address, Contact, Email)
VALUES (5, 'Ravi Mehta', '123 Juhu, Mumbai', '9876543210', 'ravi.mehta@example.com');

update a member;

UPDATE Members
SET Address = '456 Bandra, Mumbai', Contact = '9123456789'
WHERE Member_ID = 5;

delete a member;

DELETE FROM Members
WHERE Member_ID = 5;

issue a book to a meemeber;

INSERT INTO Transactions (Transaction_ID, Member_ID, Book_ID, Issue_Date, Status)
VALUES (6, 2, 3, '2024-11-20', 'Issued');

return a book;

UPDATE Transactions
SET Return_Date = '2024-11-25', Status = 'Returned'
WHERE Transaction_ID = 6;

search for a book;

SELECT * FROM Books
WHERE Title LIKE '%Alchemist%';

search for a member;

SELECT * FROM Members
WHERE Name LIKE '%Ravi%';

view transaction history for a member;

SELECT * FROM Transactions
WHERE Member_ID = 2;


--html form to add new book--

<form action="add_book.php" method="POST">
    <label for="title">Title:</label>
    <input type="text" id="title" name="title" required>
    <label for="author">Author:</label>
    <input type="text" id="author" name="author" required>
    <label for="genre">Genre:</label>
    <input type="text" id="genre" name="genre" required>
    <label for="price">Price:</label>
    <input type="number" id="price" name="price" required>
    <button type="submit">Add Book</button>
</form>

--html code to search books by title--

<form action="search_books.php" method="GET">
    <label for="search">Search Books:</label>
    <input type="text" id="search" name="search" required>
    <button type="submit">Search</button>
</form>




--php code for handling new book insertion--

<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "library";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $title = $_POST['title'];
    $author = $_POST['author'];
    $genre = $_POST['genre'];
    $price = $_POST['price'];

    $sql = "INSERT INTO Books (Title, Author, Genre, Price) VALUES ('$title', '$author', '$genre', $price)";
    
    if ($conn->query($sql) === TRUE) {
        echo "New book added successfully!";
    } else {
        echo "Error: " . $sql . "<br>" . $conn->error;
    }
}

$conn->close();
?>

--to search books--

<?php
$conn = new mysqli("localhost", "root", "", "library");

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

if (isset($_GET['search'])) {
    $search = $_GET['search'];
    $sql = "SELECT * FROM Books WHERE Title LIKE '%$search%'";

    $result = $conn->query($sql);
    if ($result->num_rows > 0) {
        while ($row = $result->fetch_assoc()) {
            echo "Title: " . $row['Title'] . "<br>";
            echo "Author: " . $row['Author'] . "<br>";
            echo "Price: " . $row['Price'] . "<br><br>";
        }
    } else {
        echo "No results found!";
    }
}

$conn->close();
?>

- can connect to JavaScript later on along with more appealing UI-UX.

# BCA Machine Learning
# Megha Yadav 230160255032
