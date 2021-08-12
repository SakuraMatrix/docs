# DataStax Java Basic CRUD for Apache Cassandra

A basic CRUD Java application using the DataStax Java Driver for Apache Cassandra. The intent is to help users get up and running quickly with the driver.


## Prerequisites

- A running instance of Apache Cassandra on docker.
- Maven build automation tool.
- Java 8
- Docker

## Starting Cassandra Docker image

Pull Cassandra latest docker image,
run in command line:
```shell
    docker pull cassandra:latest
```

Run Cassandra image detach mode(run in background), on 
port 9042, name custom name(jcass) and image name , run in command line:
```shell
    docker run -d -p 9042:9042 --name jcass cassandra
```
## Running Cql on Docker
We can check our keyspace and tables running,
cql on our command line with the following command:
```shell
    docker exec -it jcass cqlsh
```
Where -it is interactive mode,
jcass is the custom cassandra image name,
and cqlsh is cql shell.

We can type cql commands directly, in our cql shell.
```shell
 SELECT * FROM keyspace.table;
```

## Maven
Maven dependencies:
```shell
    <dependencies>
        <dependency>
            <groupId>com.datastax.oss</groupId>
            <artifactId>java-driver-core</artifactId>
            <version>4.13.0</version>
        </dependency>
        <dependency>
            <groupId>com.datastax.oss</groupId>
            <artifactId>java-driver-query-builder</artifactId>
            <version>4.13.0</version>
        </dependency>
    </dependencies>
```


## Connecting to cluster Java

Inside your main method, insert the following code to build
your session:

```java
    try(CqlSession session = CqlSession
        .builder()
        .build()){}
```

## Creating Keyspace and Table

Inside your try block, insert the following code to 
create keyspace, if not exists, with replication factor : '1', 
and execute.

```java
// Create keyspace
    CreateKeyspace library = SchemaBuilder.createKeyspace("library")
        .ifNotExists()
        .withSimpleStrategy(1);

// Execute create Keyspace.
    session.execute(library.build());
```
After create keyspace inside try block, create table for our keyspace, using schema builder, if not exists,
with partition key, columns and respective data types, and
execute.

```java
// Create Table.
    CreateTable books = SchemaBuilder.createTable("library", "books")
        .ifNotExists()
        .withPartitionKey("isbn", DataTypes.INT)
        .withColumn("book_title", DataTypes.TEXT)
        .withColumn("book_author", DataTypes.TEXT)
        .withColumn("book_Quantity", DataTypes.INT)
        .withColumn("arrival_date", DataTypes.TIMESTAMP);

// Execute Create Table.
    session.execute(books.build());
```

## Creating object model

On a separate class create your object model, 
with custom state, custom constructor, with 
getters and setters. this is a book example:

```java
import java.time.Instant;

public class Book {
    // State
    private int isbn;
    private String title;
    private String author;
    private int quantity;
    private Instant arrival_date;

    // Constructor
    public Book(int isbn, String title, String author,
                int quantity, Instant arrival_date){
        this.isbn = isbn;
        this.title = title;
        this.author = author;
        this.quantity = quantity;
        this.arrival_date = arrival_date;
    }

    // Getters and Setters
    public int getIsbn() {
        return isbn;
    }

    public void setIsbn(int isbn) {
        this.isbn = isbn;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public Instant getArrival_date() {
        return arrival_date;
    }

    public void setArrival_date(Instant arrival_date) {
        this.arrival_date = arrival_date;
    }
}

```

## Creating Repository

Create a repository class, that
will handle the CRUD operations, set your table name.
We need a custom 
constructor with keyspace and session.

```java
public class BookRepository {
    private static final String TABLE_NAME = "books";
    private String keySpace;
    private CqlSession session;

    // Constructor
    public BookRepository(String keySpace, CqlSession session) {
        this.keySpace = keySpace;
        this.session = session;
    }
}
```


### Create
After our constructor we can create our first 
CRUD operation, we have to make a prepared statement,
with to Insert into keyspace and values. Then 
we bind the respective values, 
(the bind values follow the same order, as the '?' from our prepared statement)
. We get our values from our objects getters,
and finally we execute our bound statement.

```java
    // Create
    public void create(Book book) {
        // Statement
        PreparedStatement insertStatement = session.prepare(
                "INSERT INTO " + keySpace + "." + TABLE_NAME + "\n" +
                        "(isbn, book_title, book_author, book_quantity, arrival_date)\n" +
                        "VALUES (?, ?, ?, ?, ?)"
        );

        // Statement
        BoundStatement boundStatement = insertStatement.bind(
                book.getIsbn(),
                book.getTitle(),
                book.getAuthor(),
                book.getQuantity(),
                book.getArrival_date()
        );

        // Execute bound statement.
        session.execute(boundStatement);
    }
```

Back on our main class, inside our try block, we create a new book and new repository 
to run our create method.

```java
    // New book repository.
    BookRepository dao = new BookRepository("library", session);

    // New Book instance.
    Book siddhartha = new Book(2344, "Siddhartha", "Hermann Hesse",
            13, Instant.now());

    // Create.
    dao.create(siddhartha);
```

### Read

Back on our repository after our create method,
we do the same for our read method, but we store
our result, from execute session inside a ResultSet.
Then we use an enhanced for loop to loop trough,
and print out the result.

```java
    // Read.
    public void read(Book book) {
        // Statement.
        PreparedStatement readStatement = session.prepare(
                // UNCOMMENT for JSON result ('comment other SELECT statement')
//          "SELECT JSON * FROM" +
            "SELECT * FROM " +
             keySpace + "." + TABLE_NAME +
             " WHERE book_title = ? ALLOW FILTERING"
        // * Use ALLOW FILTERING keyword only for small datasets
        );
        
        // Statement.
        BoundStatement boundStatement = readStatement.bind(
                book.getTitle()
        );

        // Execute bound statement. Save result set.
        ResultSet rs = session.execute(boundStatement);

        // Loop trough result set and print results
        for (Row row : rs) {
            System.out.println(
                    row.getFormattedContents()
            );
        }
    }
```

Back on our main method, we run our read method
similar to our create method, inside our try block:
```java
    // New book repository.
    BookRepository dao = new BookRepository("library", session);

    // New book instance.
    Book siddhartha = new Book(2344, "Siddhartha", "Hermann Hesse",
            13, Instant.now());

    // Read.
    dao.read(siddhartha);
```

### Update

For our update crud operation, back on our repository class, we
can pass an extra argument for updating the chosen value.
```java
    // Update.
    public void update(Book book, int quantity) {
        // Statement.
        PreparedStatement updateStatement = session.prepare(
                "UPDATE " + keySpace + "." + TABLE_NAME + "\n" +
                        "SET book_quantity = ? WHERE isbn = ?"
        );

        // Statement.
        BoundStatement boundStatement = updateStatement.bind(
                quantity,
                book.getIsbn()
        );

        // Execute bound statement.
        session.execute(boundStatement);
    }
```
Back on our main method, we run our update method similar to our create method, inside our try block:
```java
    // New book repository.
    BookRepository dao = new BookRepository("library", session);

    // New book instance
    Book siddhartha = new Book(2344, "Siddhartha", "Hermann Hesse",
        13, Instant.now());

    // Update.
        dao.update(siddhartha, 21);
```

### Delete
For deleting, back on our repository class, we create a prepare statement
passing our book instance and using the partition key as 
identifier. 
```java
    // Delete.
    public void delete(Book book) {
        // Statement.
        PreparedStatement deleteStatement = session.prepare(
                "DELETE FROM " + keySpace + "." + TABLE_NAME + "\n" +
                        "WHERE isbn = ?"
        );

        // Statement.
        BoundStatement boundStatement = deleteStatement.bind(
                book.getIsbn()
        );

        session.execute(boundStatement);
    }
```
Back on our main method, we run our delete method similar to our create method, inside our try block:
```java
    // New book repository.
    BookRepository dao = new BookRepository("library", session);

    // New book instance.
    Book siddhartha = new Book(2344, "Siddhartha", "Hermann Hesse",
            13, Instant.now());    
    
    // Delete.
    dao.delete(siddhartha);
```

## Sources
- Mehrab's classes.
- Discord Group Java Reactive S21.
- [DataStax docs](https://docs.datastax.com/en/developer/java-driver/4.13/manual/core/)
- [Cassandra quickstart](https://cassandra.apache.org/_/quickstart.html)
- [DataStax Statements](https://docs.datastax.com/en/developer/java-driver/4.13/manual/core/statements/) 
- [DataStax quickstart repo](https://github.com/beccam/quickstart-java)
