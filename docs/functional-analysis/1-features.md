# Features (BDD)

We start defining our application by writing down several scenarios for specific features. These scenarios explain what should be possible and how the application should act. Following this method it allows us to find a general consensus about the behavior.

We will currently only focus on searching and adding information. The way this information is edited or deleted will be defined in a later stage.



## Glossary

```
    Glossary:
        - product A: a physical product
        - product B: a physical product which is a more ecological version of product A
        - resource A: a resource from which product A is made
        - resource B: a resource from which product B is made
        - footprint A: the ecological footprint of product A
        - footprint B: the ecological footprint of product B

```



## Feature: Look up information about a physical product

```
Feature: Look up information about a physical product
    As a consumer who needs to know the ecological footprint of a physical product
    I want to look up information about it
    So that I can decide whether to buy it or not, or buy an alternative
    

    # For anonymous users and authenticated users
    Background:
        Given I am an anonymous or authenticated user

    Scenario: Looking up information about product A
        Given product A exists in the application
        When I look up product A
        Then I see information about product A
        And I see resource A
        And I see footprint A
        And I see a recommendation for product B


    # For users that have been authenticated
    Background:
        Given I have logged into my account
                    
    Scenario: Looking up information about a non-existing product
        Given product A does not exist in the application
        When I look up product A
        Then I see a message explaining that product A does not exist
        And I see an incentive to add product A
  
```



## Feature: Receive recommendations about physical products

```
Feature: Receive recommendations about physical products
    As a consumer who would like to receive recommendations about a physical product
    I want to look up information about it
    So that I can become aware about the alternatives and improve my ecological footprint

    # For anonymous users and authenticated users
    Background:
        Given I am an anonymous or authenticated user

    Scenario: Looking up recommended alternatives to a certain physical product
        Given product A does exist in the application
        When I look up product A
        Then I see a list of recommendations based on product A

    # For users that have been authenticated
    Background:
        Given I have logged into my account

    Scenario: Looking up my personal recommended alternatives
        Given I have added at least one product to my personal list of products
        When I look up personal recommended products
        I see a list of recommended alternative physical products based on my personal list of physical products
  
```



## Feature: Calculate my ecological footprint

```
Feature: Calculate my ecological footprint
    As a consumer who would like to become aware of my ecological footprint
    I want to calculate it
    So that I can become aware about my impact and the urgency of taking measures
    

    # For users that have been authenticated
    Background:
        Given I have logged into my account
                    
    Scenario: Calculating my ecological footprint
        Given I have added at least one physical product to my product list
        When I calculate my ecological footprint
        Then I see a clear breakdown of my ecological footprint
        And I can see recommendations
                      
```



## Feature: Add a physical product

```
Feature: Add a physical product
  As a consumer who wants to add a product with all relevant information
  I want to add data about the product
  So everyone else who uses the system can use this information as well
  
 
    # For anonymous users
    Background:
        Given I am an anonymous user

    Scenario: Adding product A when not logged in
        Given I am not logged in
        When I want to add product A
        Then I see a message explaining I need to login
        And I see a way to login


  # For users that have been authenticated
    Background:
        Given I have logged into my account

    Scenario: Adding a non-existing product A when resource A is available
        Given product A does not exist in the application
        When I want to add product A
        Then I can fill in a form with relevant information
        And I can link resource A
        And I can link footprint A
        And I can save product A

    Scenario: Adding a non-existing product A when only resource B is available
        Given product A does not exist and some required resources are missing
        When I want to add product A
        Then I can fill in a form with all data
        And I can add the missing resource A
                    
    Scenario: Adding an existing product A
        Given product A does exist in the application
        When I want to add product A
        Then I see a message explaining that product A already exists
        And I see a message whether I want to edit it

```



## Feature: Add a resource

```
Feature: Add a resource
    As a consumer who wants to add a resource from which a product is made
    I want to add data about the resource
    So everyone else who uses the system can use this information as well


    # For anonymous users
    Background:
        Given I am an anonymous user

    Scenario: Adding resource A
        Given I am not logged in
        When I want to add resource A
        Then I see a message explaining I need to login
        And I see a way to login


    # For users that have been authenticated
    Background:
        Given I have logged into my account

    Scenario: Adding non-existing resource A
        Given resource A does not exist
        When I want to add resource A
        Then I can fill in a form with all required data
        And I can save product A
                
    Scenario: Adding existing resource A
        Given resource A does exist
        When I want to add resource A
        Then I see a message explaining that resource A already exists
        And I see a message whether I want to edit it

```

