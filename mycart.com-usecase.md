There is a website, mycart.com 

there are few producuces, mobiles, smarttvs , dresses , shhoes etccc. they are all based on the category 

- A custer can alwas enter the sytem , add the itesm to card
- can make an order, by paying for it.

- Items gets shipped to the given location at a given time.


- Findout the classes
- Findout Associations 
    1-1? 1-*, *-1, *-* 
- Findout Aggregations
- Findout Compositions
- Findout Dependencies


## Design

### Classes
- Customer
- Product
- Category
- Cart
- CartItem
- Order
- OrderItem
- Payment
- Shipment
- Address

## Associations

Customer 1 - 1 Cart

Cart 1 - * CartItem

Customer 1 - * Order

Order 1 - * Order Item

Product * - 1 Category

CartItem * - 1 Product

OrderItem * - 1 Product

Order 1 - 1 Payment

Order 1 - 1 Shipment

Shipment 1 - 1 Address 


## Aggregations

Category <>------ Product

Cutomer <>------ Address

## Composition

Cart ◆--- CartItem

Order ◆-- OrderItem

Order ◆-- Payment

Shipment ◆-- Order

## UML Design 

Customer  1 --- 1 Cart

Cart      1 --- * CartItem

Customer  1 --- * Order

Order     1 --- * Order Item

Product   * --- 1 Category

CartItem  * --- 1 Product

OrderItem * --- 1 Product

Order     1 --- 1 Payment

Order     1 --- 1 Shipment

Shipment  1 --- 1 Address 

Category  <>---- Product

Cutomer   <>---- Address

Cart      ◆----- CartItem

Order     ◆----- OrderItem

Order     ◆----- Payment

Shipment  ◆----- Order

