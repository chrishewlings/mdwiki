# COMP 353 Midterm Summary

## Definitions

|Term|Definition|Characteristics|
|----|----------|--------------|
|Database|Collection of organized data on persistent storage.||
|Database Management System (DBMS)| A complex software package to store and manage databases.|<ul><li>**Access & Manipulation**: Convenient, efficient, and secure.</li><li>**Programming interface**: Users can create, query, and modify data.</li><li>**Persistent Storage**: Storage of data over long period of time.</li><li>**Transaction management/recovery**: Controls access with ACID principles.</li></ul>|
|Database System| Database + DBMS||
|ACID|Atomicity, Consistency, Isolation, Durability||
|Instance| Current content of the database||
|Schema| Structure of the data, described by some model||
|Data Independence| Ability to modify definition of schema at one level, without affecting definitions at a higher level.|<ul><li>**Logical Data Independence**: Ability to modify logical schema without requiring rewrite of programs</li><li>**Physical Data Independence**: Ability to modify physical schema without causing conceptual schema or applications to be modified.</li></ul>|
|Data Definition Language (DDL)|Language or notation for defining a database schema||
|Data Manipulation Language (DML)|Language for accessing and manipulating data||
|Cartesian Product| Set of all pairs \\((a,b)\\) such that \\(a \in R\\) and \\(b \in S\\)|`SELECT * FROM t1,t2`|
|Entity Set|||
|Key|Attibute(s) that uniquely identify an entity within its entity set.||
|Weak entity set| An entity set without sufficient attributes to form a key.|Uses a set of attributes (*discriminator*) along with a key of a strong entity to form its key.|


## History

|System|Pros|Cons|
|------|----|----|
|File Processing Systems|<ul><li>Simple to implement</li><li>Leverages existing filesystem</li></ul>|<ul><li>Wastes space (stores fields in multiple files)</li><li>Inconsistent: Field may be updated in one file, but not another</li><li>No single coherent language</li></ul>|
|Database Systems|<ul><li>Minimizes data redundancy</li><li>Concurrent access</li><li>Centralized control</li><li>Security and authorization</li><li>Integrity and reliability</li><li>Data abstraction and independence</li></ul>||

## Models

|Model|Real-world example|
|-----|------------------|
|Entity-Relationship Model|<ul><li>Oracle</li><li>IBM</li><li>Informix</li><li>Microsoft</li><li>Sybase</li></ul>|
|Object-Oriented Data Model|<ul><li>ObjectStore</li><li>Postgres</li></ul>|
|Logical Data Model|<ul><li>Datalog</li></ul>|


## Levels of Abstraction

|Name|Description|
|----|-----------|
|View (external)| Describes how users **see** the data|
|Conceptual| Defines the logical structure|
|Physical| Describes the storage structure and indices of data|

## DBMS Architecture

- The **query processor** handles:
    - Queries
    - Modifications (schema or data)
- The **query optimizer**, together with the QP:
    - Find the best plan to process the query
    - Issue commands to storage manager
- The **storage manager**:
    - Obtains information requested from data storage
    - Modify the information on the data storage when requested.
- The **Transaction Manager**:
    - Responsible for data consistency
    - Ensure simultaneous queries do not interfere with one another
    - Ensure data integrity under exceptional circumstances (power failure, etc)


## Query languages

### SQL

#### Revisions

- First developed at IBM (1976).
- Revised to first standard: SQL-86 (1986)
- Revised again to second standard: SQL-92 (1992)
- Latest standard: SQL-99/SQL3.

#### Schema (Data Definition Language) 

##### Creating tables

```sql
CREATE TABLE Star (
    name CHAR(30),
    address VARCHAR(255),
    gender CHAR(1),
    birthdate DATE
);
```

|Type|Definition|
|----|----------|
|`INT`/`INTEGER`|Single integer number.|
|`REAL`/`FLOAT`|Single floating point number|
|`DECIMAL(n,d)`/`NUMERIC(n,d)`|`n` denotes total number of characters, `d` denotes number following decimal point.|
|`CHAR(n)`/`BIT(b)`| Fixed length character/bit string, padded if not enough characters.|
|`VARCHAR(n)`/`BIT VARYING(n)`|Variable length strings up to `n` characters.|
|`DATE`|`YYYY-MM-DD`|
|`TIME`|`HH:MM:SS`|

##### Altering existing tables

- Adding columns:

```sql 
ALTER TABLE Star ADD phone CHAR(16);
```

- Removing columns:

```sql
ALTER TABLE Star DROP COLUMN phone;
```

Note: A column cannot be dropped if it is the only remaining one.

##### Attribute Properties

|Property|Result|
|--------|------|
|`NOT NULL`| Must have a real value.|
|`DEFAULT`| Defines a default value for attribute, if it is not provided.|


#### Queries (Data Manipulation Language)

##### Selection

```sql

SELECT ...
FROM ...
WHERE ...
```

```sql
SELECT ID
FROM Student
WHERE firstName = 'John' AND GPA > 3;
```

###### Qualifiers

- Following `WHERE`, comparison operators may be used:
    - Arithmetic comparisons: `=, <>, <, >, <=, >=`
    - Arithmetic operators: `+,-,*,/`
    - Boolean operators: `AND,OR,NOT`

###### Basic Aggregation:

- `NULL`s are ignored.

|Operator|Action|
|--------|------|
|`SUM`|Returns sum of all values in column|
|`AVG`|Returns \\( \frac{SumOfValues}{numOfValues} \\)|
|`MIN`|Returns smallest value in column|
|`MAX`|Returns largest value in column|
|`COUNT`|Returns number of values, including duplicates. Use `DISTINCT` to not count dupes.|

Examples:
```sql
SELECT AVG(netWorth)
FROM Exec
```

```sql
SELECT COUNT(DISTINCT name)
FROM Exec;
```

###### `GROUP BY`

- `NULL`s are counted.
- Whatever aggregation used in the `SELECT` statement will be applied only within groups.
- Used to group the tuples according to the value of a column.
- Example: What is the total length in minutes of films produced by each studio?

```sql
SELECT studioName, SUM(length)
FROM Movie
GROUP BY studioName;
```

###### `HAVING`

- The `HAVING` keyword allows us to choose a group based on a property of the group.

- Example: For those producers who made at least one film prior to 1930, list the total length of the films produced.
```sql
SELECT Exec.name, SUM(Movie.length)
FROM Exec, Movie
WHERE producerC# = cert#
GROUP BY Exec.name
HAVING MIN(Movie.year) < 1930;
```

###### `ORDER BY`

- Allows a grouping/relation to be displayed in a specified order.

Example: For those producers who made at least one film prior to 1930, list the total length of the films produced, in ascending order of name.

```sql
SELECT Exec.name, SUM(Movie.length)
FROM Exec, Movie
WHERE producerC# = cert#
GROUP BY Exec.name
HAVING MIN(Movie.year) < 1930
ORDER BY Exec.name ASC;
```

##### Insertion

Given schema: `StarsIn (title, year, starName)`

- Adding single elements:

```sql
INSERT INTO StarsIn (title,year, starName)
VALUES (’The Maltese Falcon’, 1942, ’Sydney Greenstreet’);

// OR //

INSERT INTO StarsIn
VALUES (’The Maltese Falcon’, 1942, ’Sydney Greenstreet’);
```

- Adding multiple elements:

```sql
INSERT INTO StarsIn
VALUES (filmName1,date1,starName1),
       (filmName2,date2,starName2),
       ...,
       (fileNamen,daten,starNamen);

```

- Adding a full set:

```sql
INSERT INTO Studio(name)
SELECT DISTINCT studioName
FROM Movie
WHERE studioName NOT IN (SELECT name
                         FROM Studio);
```

##### Deletion

- Deleting single elements:
```sql
DELETE FROM StarIn
WHERE title = ’The Maltese Falcon’ AND
starName = ’Sydney Greenstreet’;
```

- Deleting multiple elements : Delete from `Studio` those studios not mentioned in `Movie`.

```sql
DELETE FROM Studio
WHERE name NOT IN (SELECT StudioName
FROM Movie);
```

##### Updating

Example: Modify table Exec by attaching the title ‘Pres. ’ in front of the name
of every movie executive who is also the president of some studio.

```sql
UPDATE Exec
SET name = ’Pres. ’ || name 
WHERE cert# IN (SELECT presC#
                FROM Studio);
```


## Data Models

### Entity-Relationship

- Graphical approach
- Allows **n-ary** relationships.

#### Primitives

![Primitives for ER model](./images/ermodel.png)

#### Relationships

|Types|Representation|Meaning|
|-----|--------------|-------|
|A (many-one) B| \\(\Box \rightarrow \Box\\)| Each entity in \\(A\\) is related to **at most one** entity in \\(B\\).|
|A (one-one) B | \\(\Box \leftrightarrow \Box\\) | Each entity in \\(A\\) is related to **at most one** entity in \\)B\\), and vice versa.|
|A isa B| \\(A \triangleright B\\) | \\(A\\) inherits from \\(B\\)|

- Sometimes it is more appropriate to associate attributes with a relationship rather than an entity set.

- An inherited entity has whatever attributes any of its components have, and participates in whatever relationships its components participate in. 

#### Constraints

- **Single-value** constraints are requirements that a value be unique.
    - e.g. The value for \\(A\\) must exist, if \\(A\\) is part of the key.
    - The value for \\(A\\) is optional otherwise.
- **Referential integrity** constraints are requirements that a value referred to must actually exist.
    - e.g. A movie studio must always exist in `Studio`
    - If someone is a CEO, the studio they run must exist in `Studio`
    - Looks like \\(\Box -\diamond \rightarrow \Box \leftarrow -\Box \\)
- **Relationship degree** constraints restrict the number of entities in the entity sets in the relationship.
    - e.g. A student may enroll in \\(\leq 5\\) courses, represented by writing the constraint along the relationship line.
- **Domain** constraints require that the value of an attribute must be within a specific set of values.

### Object-Oriented

- Only allows defining **binary** relationships.
- An object must be a member of exactly one class. 

### Converting to Relational Data Model

1. For each entity set \\(E\\), create a **relation schema** with the same name and set of attributes.  
    - ![entity set to schema](./images/entityset_to_schema.png)
    - becomes:
    - Courses (__courseNumber__, name, credits)
2. For each relationship \\(R\\), create a **table** with the same name.
    - The set of attributes of the relation includes:
        - Key attributes of **each attached entity set**
        - Any attributes \\(R\\) may have
    - ![relationship to table](./images/relationship_to_table.png)
    - becomes: 
    - EnrolledIn(__ID__,__courseNumber__,grade)
3. For each weak entity set \\(W\\), create a **relation schema** with all the attributes of \\)W\\) as well as any key attributes of strong entity sets it's attached to. 
    - ===add img===

#### Determining the Key of a relationship

- If \\(R\\) is a binary relationship betweeen \\(E1,E2\\):
    - If \\(R\\) is Many-to-Many, the keys of \\(E1,E2\\) together form the key of \\(R\\).
    - If \\(R\\) is Many-to-One from \\(E1\\) to \\(E2\\), The key of \\(E1\\) is part of the key of \\(R\\).
    - If \\(R\\) is One-to-One from \\(E1\\) to \\(E2\\), then either the key of \\(E1\\) or the key of \\(E2\\) is part of the key of \\(R\\), but not both. 

#### Dealing with *isa* hierarchies

##### E/R approach

- For each entity set \\(E\\), create a table \\(e\\) with attributes \\(a\\) such that:
    - \\(a\\) belongs to \\(E\\)
    - \\(a\\) is the key attribute of the parent relation

##### Object oriented approach

===add contents===

##### Null approach

- Use a single relation with all values of any attached entity sets.
- An object is represented by a typle that has `NULL` in each attribute that is not defined for that entity.
- May allow efficient query processing but wastes space.




