# Library-Management-System-OOA-

## Project Overview
This project is a simplified **Library Management System** designed using **Object-Oriented Analysis (OOA)** principles. The system allows for:  

- Managing books and members  
- Borrowing and returning books  
- Tracking borrowing transactions    

The goal of this project is **analyzing requirements, breaking down the system into components, and modeling its architecture and behavior** before moving to full implementation.  

---

## Requirement Analysis

**Actors:**  
- Librarian / Admin  
- Member (Student or Teacher)  

**Key Use Cases:**  
- Search books by title/author  
- Borrow books  
- Return books  
- Add/remove books (Admin)  
- Register members  
- View borrowed books  
- Notify members of overdue books  

---

## System Architecture

**Major Components:**  
1. **UI Layer** – Handles user interactions (search, borrow, return)  
2. **Business Logic Layer** – Manages borrowing rules, notifications  
3. **Data Access Layer** – Stores and retrieves books, members, and transactions  

**High-Level Architecture Diagram:**  
Diagrams are included as images (Class Diagram / Use Case Diagram / Sequence Diagram / State Diagram)

---

## Object-Oriented Analysis

### Classes and Attributes

**Member Classes:**  

| Class      | Type     | Attributes                               | Methods                            |
|------------|---------|------------------------------------------|-----------------------------------|
| User       | Abstract | memberId, name, email, borrowedBooks     | borrowBook(), returnBook()        |
| Student    | Concrete | inherits User                             | –                                 |
| Teacher    | Concrete | inherits User                             | –                                 |
| Librarian  | Concrete | inherits User                             | addBook(), removeBook()           |


---

## Models

### Data Model

Represents how data is structured in the Library Management System.

```plaintext
Member
---------
memberId : int
name : string
email : string
borrowedBooks : list<Book>

Book
---------
bookId : int
title : string
author : string
status : string (Available, Issued, Returned)

BorrowTransaction
---------
transactionId : int
book : Book
member : Member
issueDate : date
returnDate : date
status : string (Open, Closed)


### Functional Model

Represents what the system does, i.e., the functions and responsibilities.

Member Functions:
- searchBook(title/author)
- borrowBook(bookId)
- returnBook(bookId)
- viewBorrowedBooks()

Librarian/Admin Functions:
- addBook(book)
- removeBook(bookId)
- registerMember(member)
- manageBorrowTransactions()
- notifyOverdueBooks()


### Behavioral Model

Represents how the system behaves over time and how objects interact.

1. Member searches for a book
2. System checks availability
3. If Available:
     - Member borrows book
     - BorrowTransaction created (status = Open)
     - Book status = Issued
4. Member returns book
     - BorrowTransaction status = Closed
     - Book status = Returned → Available
5. Admin notifications:
     - Overdue books → notify member

---

## Abstraction to Implementation

### Example: Book Class
```javascript
class Book {
  constructor(bookId, title, author) {
    this.bookId = bookId;
    this.title = title;
    this.author = author;
    this.status = "Available"; // Available, Issued, Returned
  }

  issue() {
    if (this.status === "Available") {
      this.status = "Issued";
      console.log(`${this.title} has been issued.`);
    } else {
      console.log(`${this.title} is not available.`);
    }
  }

  returnBook() {
    if (this.status === "Issued") {
      this.status = "Returned";
      console.log(`${this.title} has been returned.`);
    }
  }
}
