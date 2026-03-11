# OpenLibrary Database Schema

## User

Represents a registered user of the platform.

### Fields

* **id** (int, primary key, auto-increment)
* **name** (string)
* **email** (string, unique)
* **password** (string)
* **avatarUrl** (string, optional)
* **createdAt** (datetime)
* **updatedAt** (datetime)

### Relationships

* A **User** can own many **Books**
* A **User** can create many **Listings**
* A **User** can write many **Reviews**

---

## Book

Represents a physical book owned by a user.

### Fields

* **id** (int, primary key, auto-increment)
* **title** (string)
* **author** (string)
* **isbn** (string, optional)
* **description** (text)
* **ownerId** (foreign key → `User.id`)
* **createdAt** (datetime)

### Relationships

* A **Book** belongs to a **User**
* A **Book** can have multiple **Listings**

---

## Listing

Represents a book being sold.

### Fields

* **id** (int, primary key, auto-increment)
* **bookId** (foreign key → `Book.id`)
* **price** (decimal)
* **condition** (string)
* **status** (enum: `available | sold | reserved`)
* **createdAt** (datetime)

### Relationships

* A **Listing** belongs to a **Book**

---

## Transaction

Represents a purchase of a book.

### Fields

* **id** (int, primary key, auto-increment)
* **listingId** (foreign key → `Listing.id`)
* **buyerId** (foreign key → `User.id`)
* **status** (enum: `pending | completed | cancelled`)
* **createdAt** (datetime)

### Relationships

* A **Transaction** belongs to a **Listing**
* A **Transaction** references the **User** who made the purchase

---

## Review

Represents feedback for a seller.

### Fields

* **id** (int, primary key, auto-increment)
* **reviewerId** (foreign key → `User.id`)
* **targetUserId** (foreign key → `User.id`)
* **rating** (integer, range 1–5)
* **comment** (text)
* **createdAt** (datetime)

### Relationships

* A **Review** is written by a **User** (`reviewerId`)
* A **Review** targets another **User** (`targetUserId`)
