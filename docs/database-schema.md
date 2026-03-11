# OpenLibrary Database Schema

## User

Represents a registered user of the platform.

Fields:

id (int, primary key)
name (string)
email (string, unique)
password (string)
avatarUrl (string, optional)
createdAt (datetime)
updatedAt (datetime)

Relationships:

User can own many books
User can create many listings
User can write many reviews

---

## Book

Represents a physical book owned by a user.

Fields:

id (int, primary key)
title (string)
author (string)
isbn (string, optional)
description (text)
ownerId (foreign key → User.id)
createdAt (datetime)

Relationships:

Book belongs to User
Book can have multiple listings

---

## Listing

Represents a book being sold.

Fields:

id (int, primary key)
bookId (foreign key → Book.id)
price (decimal)
condition (string)
status (available | sold | reserved)
createdAt (datetime)

Relationships:

Listing belongs to Book

---

## Transaction

Represents a purchase of a book.

Fields:

id (int, primary key)
listingId (foreign key)
buyerId (foreign key → User.id)
status (pending | completed | cancelled)
createdAt (datetime)

---

## Review

Represents feedback for a seller.

Fields:

id (int, primary key)
reviewerId (foreign key → User.id)
targetUserId (foreign key → User.id)
rating (1–5)
comment (text)
createdAt (datetime)
