# Lab6 

**Learning objective**: 
- To use type-variables when defining functions. 
- To use the Optional data type

**Prerequisite**
1. Daml SDK installed and setup
2. Daml Fundamentals Training: Functional Programming in Daml - Lessons 1 to 11 completed.

## Problem statement 1
*This problem focuses on defining a new data-type and a type-class, and using the Optional data type*

Define a data type named **Account** that has two fields: **ownerId** of type Text and **balance** of type Decimal. 

Now we need a typeclass named **SafeAccount** that has a function **safeQuery** that takes an **account** and a Text for **id**. If the id matches with the one in the account, then it returns the balance amount. If it doesn't then it returns 'None'. 

Here is the script to test the Account data-type, SafeAccount class, and safeQuery function:

```
testSafeAccount = script do 

    let myAccount = Account with 
            ownerId = "123"
            balance = 100.00

        myBalance1: Optional Decimal = safeQuery myAccount "123"

    debug $ myBalance1

    let myBalance2: Optional Decimal = safeQuery myAccount "234"

    debug $ myBalance2

    return ()
```

The expected output is:

```
Trace: 
  Some 100.0
  None
```

## Problem statement 2
*This problem applies the concept of typeclasses and type-variables.*

A credit card company issues loyalty points to its credit card users. However it issues special points when the card is used to pay for air-travel or dining. These special points have a special property that they can be redeemed to earn dollars. 

Write a function named **redeemPoints** which takes points earned either through air-travel or dining and converts them to a number based on the formula shown below:

| Type of points     | $ Conversion formula |
|--------------------|---------------------|
| Air-travel points  | points X 10         |
| Dining points      | points x 5          |


### Suggested Design

Create a data-type called **AirtravelPoint** that has just one field named count of type Int. Similarly, create another data-type called **DiningPoint** with just one field named count of type Int. 

Create a type-class named **Redeemable** with a function **redeem**.

Make AirtravelPoint and DiningPoint instances of Redeemable, making their redeem functions return a Decimal value based on the formula given in the table above. 

Then test your code using the script given below:

```
testRedeemable = script do 
    let myTravelPoints = AirtravelPoint with 
            count = 500

        myDiningPoints = DiningPoint with 
            count = 5000

        myTotalRedeemedPoints: Decimal = redeem myTravelPoints + redeem myDiningPoints

    debug  myTotalRedeemedPoints 
   
    return()
```

The expected output is:

```
Trace: 
  30000.0
```