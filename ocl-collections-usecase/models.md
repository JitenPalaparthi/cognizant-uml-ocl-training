# uml models

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

Customer 1 -----> * Account

Acoount  1 -----> * Transaction

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



