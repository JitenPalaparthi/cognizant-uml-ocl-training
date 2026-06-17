## Entities/Classes
- Member
- Book
- Loan
- Library

## Enum Design

MemberStatus
------------
ACTIVE
BLOCKED
EXPIRED

BookStatus
-----------
AVAILABLE
BORROWED
DAMAGED
LOST

LoanStatus
-----------
ACTIVE
RETURNED
OVERDUE

## Class Design

Member
-------
memberId string
name string
email string
status MemberStatus
maxAllowedLoads 

Book
-----
bookId string
title string
author string
isbn string
status BookStatus

Loan
-----
loanId string
borrowedDate date
dueDate data
returnDate date
status LoanStatus

Library
--------
libraryId string
name string
location string

## Association

Library 1 - * Book

Library 1 - * Member

Member  1 - * Loan

Book    1 - * Loan

## Aggregation

Library ◇ Book

Library ◇ Member

## Composition

Member ◆--- * Loan

## Dependencies

Member ---> Book

Loan   ---> Book

## Operaations

Member
------

borrowBook(book: Book): Loan
returnBook(book: Book): Boolean
canBorrow(): Boolean

Book
-----
markBorrow(): void
markAvailable(): void
isAvailable(): boolean

Loan
-----
closeLoan(returnDate:date): void
isoverDue(): boolean

Library
-------
addBook(book:Book): void
registerMember(member:Member):void




















