---
title: Hashmaps Finished Lesson Hacks
comments: true
layout: post
description: Here are my finished hacks for the hashmaps lesson on 12/13
type: plans
courses: { csa: {week: 16} }
categories: [C1.4]
---



# Popcorn Hacks Complete

1. Come up with a real world example in which collections are used! Write your answer below:

One real world example in which collections are used is managing a library's inventory system, specifically with a List or Set. The library has a variety of books that can be sorted by attributes like title, author, and availability status. A collection like a List or Set could be used to represent the entire inventory of books and allow us to sort the books by some of these attributes. 

2. What can we do if we want to assign multiple values to a single key? Do it below!: 

If we wanted to assign multiple values to a single key, we could make an Array or ArrayList. Code below:

Before

```java
import java.util.HashMap;  

public class ShoePrices {
    public static void main(String[] args) {

        HashMap<String, Double> hashMap = new HashMap<>();

        hashMap.put("Nike", 41.97);
        hashMap.put("Nike", 80.97); // overrides 41.97 
        hashMap.put("Adidas", 69.99);
        hashMap.put("Vans", 55.00);

        double value = hashMap.get("Nike");
        System.out.println("A Nike shoe would cost " + value); // will only print 80.97 since that price has overridden 41.97
    }
}

ShoePrices.main(null);
```

After

```java
import java.util.HashMap;
import java.util.List;
import java.util.ArrayList; // use List to assign multiple values to a single key

public class ShoePrices {
    public static void main(String[] args) {

        HashMap<String, List<Double>> hashMap = new HashMap<>();

        hashMap.computeIfAbsent("Nike", k -> new ArrayList<>()).add(41.97);
        hashMap.computeIfAbsent("Nike", k -> new ArrayList<>()).add(80.97);
        hashMap.computeIfAbsent("Adidas", k -> new ArrayList<>()).add(69.99);
        hashMap.computeIfAbsent("Vans", k -> new ArrayList<>()).add(55.00);

        List<Double> nikePrices = hashMap.get("Nike"); // gets the prices of everything named Nike
        System.out.println("Prices for Nike shoes: " + nikePrices); // displays both prices, 41.97 and 80.97
    }
}

ShoePrices.main(null);
```


3. List all of the JPA methods that you see in the PersonJpaRepository.java file and what their purpose is.

- Person findByEmail(String email)
    - Purpose: To retrieve the data of a Person object based on the email of the Person. 
- List<Person> findAllByOrderByNameAsc();
    - Purpose: Fetches a list of all Person objects in ascending order by their name. Can be useful if you want to display the names of users in an order list.
- List<Person> findByNameContainingIgnoreCaseOrEmailContainingIgnoreCase(String name, String email);
    - Purpose: Used to find all Person objects whose name contains the given string name (not case sensitive) or whose email contains the given string name (also not case sensitive case). 
- Person findByEmailAndPassword(String email, String password);
    - Purpose: Retrieves the data of a Person object based on the matching email and password of the Person. 
- List<Person> findByLikeTermNative(String term);
    - Purpose: Searches the Person table for any records that contain a given string (argument term in this case). It can be almost be thought of (at least for me) as like a Ctrl F, since we have the ability to look for a certain phrase or series of characters within a large text. Similarly, this methods allows us to have more complex searching methods, especially in large data bases.



4. Explain in your own words what the relationship between `Person` objects and `PersonRole` objects is. Why is this relevant to collections? (Hint: In the code above, multiple `PersonRole` objects are stored within a `Person` object's roles attribute.)

The relationship between Person objects and PersonRole objects is a many-to-many relationship, which is managed in Java in this repository through the JPA (Java Persistence API) file and in the database through a join table. This is relevant to the collections we have learned about as it involves managing groups of related data (i.e. roles for each person) in an efficient and structured way.


5. Where do you see "tutorial_id" on the table? What does it represent in relation to the leftmost "id" column?

I can see the tutorial_id in a column of the note table when I look inside the sqlite.db file. The leftmost "id" column in the note table is typically the primary key of the Note entity. Each note has its unique ID (id) and is associated with a Person (i.e. tutorial_id). The id column identifies each Note, while tutorial_id links it to its corresponding Person (hence why we only see numbers in the tutorial_id column).

![]({{site.baseurl}}/images/Screenshot(117).png)


# Homework Hacks Complete

## Overview

For my hacks, I decided to create a data base that was all about TV shows. Specifically, TV shows, actors, and genres. Below are some screenshots of my sqlite data tables as well as some of the code I used to construct the data tables with their different columns and attributes.

## Screenshots

The first screenshot is a many to many relationship between the TV show and the genre of the TV show, as shown below:

![]({{site.baseurl}}/images/Screenshot(109).png)

Here is the code segment that I used to create this relationship (mainly with the @ManyToMany):

```java
@ManyToMany(fetch = FetchType.LAZY)
@JoinTable(
  name = "tvshow_genre",
  joinColumns = @JoinColumn(name = "tvshow_id"),
  inverseJoinColumns = @JoinColumn(name = "genre_id")
)
```

The next screenshot below shows the use of a JSONB column for episodes of a show, which is the column that has the curly brackets and colons:

![]({{site.baseurl}}/images/Screenshot(112).png)

Here is the code segment that I used to include the episodes JSONB column:

```java

@JdbcTypeCode(SqlTypes.JSON)
    @Column(columnDefinition = "jsonb")
    private Map<String, Map<String, Object>> episodes;

```

The rest of the screenshots below are of some of my other sqlite data tables that I made:

![]({{site.baseurl}}/images/Screenshot(108).png)

![]({{site.baseurl}}/images/Screenshot(111).png)


## Extra Notes Beyond the Lesson

Collections in SQL Databases

 - Relational Databases
    - Collections are used to organize and manage data, especially in SQL Server Agent and Integration Services
    - Group objects sharing the same parent object and constructed from the same class, like ColumnCollection containing all Column objects of a Table
    - Useful for iterating through data for operations such as setting properties or displaying connections​​​​
    - Relational databases defined by ACID (Atomicity, Consistency, Isolation, Durability) characteristics, setting them apart from non-relational databases.
       - Ensure data integrity and consistency in transactions.
    - Essential in relational databases, primary keys uniquely identify each row in a table
       - Primary keys ensure each data piece is unique, crucial for differentiating records and maintaining data accuracy.
    - Often, primary keys are system-generated to ensure uniqueness and to simplify data management.
    - Relational databases allow for easy data manipulation (i.e. CRUD operations) and offer robust security features to restrict unauthorized access​​

- Document-Oriented Databases (e.g., MongoDB)
    - Collections group related documents sharing a common structure.
    - FUnlike fixed-schema tables in relational databases, collections can contain documents with varying structures, accommodating different data types.
    - Collections can be scaled across multiple servers, aiding in handling large data volumes.
    - Considerations include data access patterns, growth rate, and sharding for manageability and performance​​.
    - Dynamic Schema: Unlike relational databases, document-oriented databases like MongoDB offer dynamic schemas, enabling varied document structures within the same collection.
    - Data in document oriented databases are modeled and represented as JSON-like documents -> enhancing flexibility and scalability.
    - Advanced indexing features in document-oriented databases facilitate efficient querying and data retrieval.
    - These databases typically support replication and data distribution across multiple servers or nodes, enhancing data availability and fault tolerance.

- Many-to-One Relationship in JPA
    - @ManyToOne Annotation indicates a many-to-one relationship between entities, such as Person and PersonRole.
    - @JoinColumn Annotation specifies the foreign key column (tutorial_id) in the note table linking to the Person entity.
    - Primary Key vs. Foreign Key: The "id" column is the primary key of each Note, while tutorial_id establishes the relational link to Person​​.
    - In a many-to-one relationship, the foreign key in the child entity (e.g., tutorial_id in Note) references the primary key of the parent entity (e.g., id in Person).
    - These relationships ensure data integrity and enforce referential integrity within the database.
    - The @OnDelete(action = OnDeleteAction.CASCADE) annotation indicates cascade operations, such as deleting all child entities (i.e. notes) when the parent entity (person) is deleted.
    - This relationship pattern efficiently organizes data, especially in scenarios where one entity (i.e. person or tv show) is associated with multiple dependent entities (notes or genres).
    - The @JsonIgnore annotation often used in many-to-one relationships helps optimize data queries by preventing unnecessary data loading.







