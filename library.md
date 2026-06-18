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


## OCL (Object Constraint Language)

### Syntax
context ClassName
inv ConstraintName: condition // The condition should be true

context Member:borrowBook(book):
inv ActiveMemberCanBorrow:
    self.status = MemberStatus::Active and Member.NumberOfActiveLoans >=1

### BankAccout Withdraw
Customer
---------
customerId: string
name: string

Account:
-------- 
accountNo:string
balance: double

Operation
----------
withDraw(amount: double)

inv --> Invariant
pre --> Precondition
post --> Postcondition

## Before Withdrawal 
    - Preconditon

context Account
inv NonNegativeBalance:
    self.Balance>=0

context Account:withDraw(amount: double)
pre SufficientBalance:
    amount > 0 and self.balance >= amount

context Account:withDraw(amount: double)
post BalanceUpdated:
     self.balance = self.balance@pre-amount





















