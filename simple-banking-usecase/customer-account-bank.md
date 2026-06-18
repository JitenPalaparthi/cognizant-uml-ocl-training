## Basic Design

- Customer
    - Account
        - properties
            - balance: Real
            - minimumBalance: Real
            - status: String
            - isActive: Boolean
            - overDraftAllowed: Boolean

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

 

endpackage

<!-- 5 xor 3 --> 5^3

XOR.          AND.        OR
5 = 0101      0101       0101
3 = 0011      0011       0011
--------    -------     ------- 
6 = 0110.   1=0001      7=0111 -->


