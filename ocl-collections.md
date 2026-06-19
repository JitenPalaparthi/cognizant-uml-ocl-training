# OCL Collections

- Associations
    - One-One // Not a collection
    - One-Many
    - Many-One
    - Many-Many

    - Aggregations
    - Compositions
    - Dependencies

   - OCL Collections Types

        - Set 

            - noduplicates (unique)
            - unordered
            - Set{1,2,3,4,5,1,2} , duplicates are removed 
            - Set{1,2,3,4,5} can be
            - Set{3,4,1,2,5} 
            - self.accounts
            - Set(accounts)

        - Bag
            
            - Allows duplicates
            - unordered
            - Bag{1,2,3,4,5,1,2}
                can be
            - Bag{2,1,3,5,4,2,1}

        - Sequence

            - ordered collection
            - allows duplicates
            - Sequence(10,20,20,30)

        - OrderedSet
            - noduplicates (unique)
            - ordered
            - OrderedSet{1,2,3,4,5,1,2} , duplicates are removed 
            - OrderedSet{1,2,3,4,5} cannot be
            - OrderedSet{3,4,1,2,5}  // order matters

            Collection
---------------------------------            
    |           |            |
    |           |            |
---------     -----      ---------   
Set            Bag        Sequence
OrderedSet
---------     -----      ---------





