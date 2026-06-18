## Basic Design

- Customer
    - Account
        - properties
            - balance: Real
            - minimumBalance: Real
            - status: String
            - isActive: Boolean
            - overDraftAllowed: Boolean 
                Note: Assume overDraftAllowed is true then additional 10000 is alloed to be debited

        - Operations
            - withDraw(amount: Real): Boolean
            - deposit(amount: Real): Boolean

## OCL 

package Banking

    # For the current Account object,Balance must be greater than or equal to zero.

    context Account
    inv PositiveBalance:
        self.Balance>= 0
    
    # Every account object , must always have a non-negative minimumBalance

    context Account
    inv MinimumBalanceValid:
        self.minimumBalance>=0
    
    # if the account is active, it must have the enough balance
    context Account
    inv ActiveAccountRule:
        self.isActive = true and self.Balance >= self.minimumBalance
    
    context Account
    inv ValidStatus:
        self.status = 'ACTIVE' or self.status = 'ACTIVE_LEEN'
    
    # if the account status is blocked, then the account must not be active

    context Account
    inv BlockAccountNotActive:
        self.status = 'BLOCKED' implies not self.isActive
    
    # if the account status is ACTIVE or 'ACTIVE_LEEN, then the account must be active (isActive )

    context Account
    inv AccountActive:
        self.staus ='ACTIVE' or self.status = 'ACTIVE_LEAN' implies self.isActive

    # account cannot be active and blocked at the same time, only one must be true.

    context Account
    inv EitherActiveOrBlocked:
        self.active = 'ACTIVE' xor self.active = 'BLOCKED'
        <!-- self.active = 'ACTIVE' and self.active <> 'BLOCKED' -->
    
    # if overdue is allowe on an account, balance can go upto -10000.
        otherwise,balance must be above the minimum balance

    context Account
    inv BalanceRule:
        if self.overdueAllowed then
            self.balance>=-10000
        else
            self.balance >= self.minimumBalance
        endif

    # pre condition to withdraw before going perform that operation it has to check , sufficient balance is there
    
    context Account:withdraw(amount: Real):Boolean
    pre AccountValidTowithDraw:
        self.balance >= amount  

    # post conditon, after withdrawal the new balance should be the old balance - amount

    context Account:withdraw(amount: Real):Boolean
    post BalanceReduced:
        self.balance = self.balances@pre - amount
    
    # if withdraw returns true, then the balance must be reduced

    context Account:withdraw(amount: Real):Boolean
    post ReturnsTrue:
        result = true implies self.balance = self.balances@pre - amount

    # availableBalance is a calculated reusable value
    context Account
    def: availableBalance:Real = 
        if self.overDraftAllowed then
            self.balance+10000
        else
            self.balance
        endif
        
    # using the definition called availableBalance
    context Account:withdraw(amount:Real):Boolean
    pre EnoughBalance:
        amount <= self.availableBalance


endpackage




