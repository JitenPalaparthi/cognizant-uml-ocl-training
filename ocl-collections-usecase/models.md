# uml models

Bank
----
name: String
location: String
ifsc: String

Customer
--------

name: String

age: Integer

Account
--------

accountNo: String

balance: Real

status: String

Transaction
-----------

amount: Real

type: String

## Relationships

- A customer can have many accounts
- An account can make many transactions

Customer 1 -----> 0..* Account

Customer
-------
accounts: Account[0..*]

Acoount  1 -----> 0..* Transaction

accounts: Set(Account)

### ocl 

self.accounts
self.transactions

- Example

Customer : Jiten

account1: type: Savings balance: 50000
account2: type: current balance: 150000
account3: type: loan.   balance: -2700

Set{account1,account2,account3}

- Collections have features
    - size, includes, count, includesAll , isEmpty,
    notEmpty, sum, exists, forAll, iterate

- Every customer must have atleast one account

```ocl
package Customer

# A custmer must have at least one account

context Customer
inv MinimumOneAccount:
    self.accounts->size() >=1

# A customer should not have zero accounts(not be isEmpty())

context Customer
inv HasAccounts:
    not self.accounts->isEmpty()
    <!-- not self.accounts-->size()=0
    self.accounts->size()<>0 -->

    # if isEmpty() returns true what does it mean?-> 

# For a customer all accounts should maintain a positive balance

context Customer
inv AllAccountsHavePositiveBalance:
    self.accounts->forAll(a | a.balance>0)

# A customer's one of the accounts should be SAVINGS

context Customer
inv AtleastOneSavingsAccount:
    self.accounts->exists(a | a.status='SAVINGS')

# a Customer's , select an account whose balance is more than 50000
the below can return objects whose balance >=50000, it can return multiple objects , {account1,account2} etc..
context Customer
inv SelectHigherBalanceAccounts:
    self.accounts->select(a | a.balance >=50000)

# Return only one account whose balance is greater than 50000

context Customer
inv SelectHigherBalanceAccount:
    self.accounts->any(a | a.balance>=50000)

# reject is opposite of select, select accounts those are not 'ACTIVE'

context Customer
inv SelectNotActiveAccounts:
    self.accounts->reject(a | a.status='ACTIVE')
    #self.accounts->select(a | a.status<>'ACTIVE')

# to extract only one property from a collection
# balances is a helper def, that can be used any where
context Customer
def: balances
    self.accounts->collect(a | a.balance) 

context Customer:
def: totalbalance
    self.balances->sum()
    # self.accounts->collect(a | a.balance)->sum()


# create a def, that would give the totalBalance of ACTIVE accounts for a customer

# sol -> get the collection of all active accounts, from there get the balances and get the sum of those balances

context Customer
def: TotalBalanceOfActiveAccounts:
    <!-- self.accounts->select(a | a.status='ACTIVE')->asSet()->collect(a | a.balance)->asBag()->sum() -->

    self.accounts->select(a | a.status='ACTIVE')->collect(a | a.balance)->sum()

# findout a customer is a good customer or not 
# 1.all the accounts to be ACTIVE
# 2.all the accounts should have more than 0 balance
# once the 1 and 2 are true , I consider isPrimary
# once the customer is primary one of the accounts should have more than eaual to 100000, consider as a Goodcustomer

context Customer
def isPrimay : Boolean
    self.accounts->forAll(a | a.status='ACTIVE') and
    self.accounts->forAll(a | a.balance > 0)

context Customer
def isGoodCustomer: Boolean
    self.isPrimay and 
    self.accounts->one(a | a.balance>=100000)

context Custimer
inv CheckGoodCustomer:
    self.isGoodCustomer

# Get the set of Good Customers

context Bank
def GoodCustomers: Set(Customer)
 self.customers->select(c | c.isGoodCustomer)

endpackage
```

<!-- we complicate even some simple conditions as below
a = 20
if (a>=10 == false) or (true and true)
// (true == false) -> false 
// (true and true) -> true
// false or true -> true
// -> true

if a>=10 -> true -->



