# SpecTruMetRx Data Model

[Video](https://www.youtube.com/watch?v=HaEPXoXVf2k)

This is the *data modeling* document for the SpecTruMetRx Payments & Heathcare Analytics solution. Please add to and use this document to implement a scalable and consistent data model that will be encrypted and secure within the AWS Cloud.

In using a **NoSQL** database like *DynamoDB*, our goal is to scale our *OnLine Transaction Processing (OLTP)* capabilities to meet the realtime demands of our users to process their requests with sub-second latency. We are optimizing denormalized and hierarchical data for compute processing & data streaming to instantiate real-time views that scale horizontally as built for OLTP.

Our decision to implement *DynamoDb* happens when we know our application's *data access patterns* precisely, and when they are repeatable, consistent, and simple queries like any: `SELECT * FROM [table]` type access patterns.

If the data needs to be reshaped with `JOIN` methods, then it would be best to consider [AWS RedShift]() as a `DataWarehouse` solution for any `data analytics` that has to be performed on the data. *OLTP* applications are ideal use cases for *NoSQL* data bases

Every table is like a catalog that has items with a set of attributes. Every item does not have to have the same set of *attributes*. However, every item, or row in a table, has to have a *partition key* defined as part of the table schema that will uniquely identify the item in the table.

Optionally, but more than likely required, you will need to declare a *sort key* attribute that will give you the ability to execute complex range queries aganist the items in the partition keys. You can think of the items with the partitions as a folder or a bucket with items. The sort key orders the items within the folder. When you query the partitions, or the folders, you can execute the queries with complex range operators.

When modeling a new data table, always model your partition and sort keys in a way that will let you model the table to support one of your primary access patterns. You always want the table to be able to query something that is interesting to the application. Partition keys both uniquely identify the item and build an unordered hash index while distributing items evenly, so that every table represents a unique and logical keyspace.

When querying the NoSQL DB providing the partition key as a condition of equality, so the system can find the correct storage node to get to so the DB can read the data needed by the user. Including the sort key will let the DB sort the data read in the partition to find the correct data to read faster.

* **Data Modeling:** Avoid relational design patterns and *use one table*.

* **MicroService Decoupling:** Use only one table for each service to capture data with *one round trip*. Simplify your query to use a `SELECT * FROM [table]` type access patterns.

* **Identify Primary Keys:** How will your items be inserted into and read from the table in your *microservice*? Overload items into partitions.

* **Define indexes for secondary access patterns:** In general, our DynamoDB cost and performance will be best if we restrict ourself to “gets” (key/value lookups on single items) and “queries” (conditional lookup on items that have the same partition key, but different range/sort keys). Scanning, where we indiscriminately gobble all items from a table, is a slow, expensive antipattern. Useful gets and queries [require useful indexes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-indexes.html).

## User Detail Data Dictionary

This table is used as a master list of users where we store mappings of all users to our [AWS Cognito User & Identity Pools]() with a UUID. Below is a list of the `attributes` we will store in the `UserDetail` service **DynamoDB** Table.:

* `awsId`: *String: Verify user authentication against AWS Cognito.*

* `orgType`: *String: list[]*

	- [ ] [*Patient*, *Provider*, *Clinic*, *ReferringPhysician*, *Insurer*, *Lender*, *Investor*, *UserServices*, *SystemAdmin*]

* `providerType`: *String: list[]*

	- [ ] [*ABA*, *Dental*, *OT/PT*, *UrgentCareFacility*, *Hospital*]

* `SpectrumHashId`: *String: Naming Convention to reflect different entities.*

	1. `orgType`.`providerType`.

* `CompanyName`: *String: Validate with CorporateParser Utility.*
* `firstName`: *String*
* `lastName`: *String*
* `systemRole`: *String*
* `authorizor`: *String*
* `ein`: *Number: Validate against IRS.*
* `ssn`: *Number: Validate against Dept. of State.*

* `npi`
* `medicaidProviderNum`

* `insuredUniqueId`
* `medicaidIdNum`
* `recipientId`
* `accountNum`: *Number: AHCA Cross Reference.*

* `birthdate`
* `treatmentAuthCode`

* `email`: *String: Validate against ISO & Domain rules.*
* `officePhone`:
* `cellPhone`:
* `Address Line1`
* `Address Line2`
* `Address Line1`
* `City`
* `State`
* `Country`
* `ZipCode`

* `acquisitionSrc`: *String: TBD*
* `memberSince`: *String: Date()*
* `lastLogin`: *String: Date()*
* `loginIPs`: *Number: list[]*
	- [ ] *Store & record the UNIQUE IP address for every successful login attempt*>
* `attemptedLoginIPs`: *Number: list[]*
	- [ ] [ *ip.address1.date()*, *ip.address2.date()* ] *Store & record the IP address for every UNsuccessful login attempt: 90-day TTL*

* `txnCount`

* `txnUSDVol`

* `claimUSDVol`




### User Detail Queries

1. How many `users` by `OrgType`?
	* Filter by: `ProvType`
	* Sort by: `EIN`

2. How many `users` by `ProviderType`?
	* Filter by: `OrgType`
	* Sort by: `EIN`

3. How many `users` for each `EIN`?
	* Filter by `OrgType`
	* Sort by `SSN`

4. Find `user` by `provType`.
	* Filter by:
		1. `DateJoined` < || > date()
	* Sort by: `user` by `txnCount` DESC

5. Find `user` by `provType`.
	* Filter by:
		1. `DateJoined` < || > date()
	* Sort by: `user` by `txnVolume` DESC

5. How many `users` by `acquisitionType`

6. How many `users` by `city`

#### User Detail Table

|TableName: | Users | - | - | - | - | - | - | - | - | MasterList |
|:----------|:-----:|:----------:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|**Partition** Key| **Sort** Key| **LSI**: Attribute1 | Attribute2 | Attribute3 | Attribute4 | **LSI**: Attribute5 | **LSI**: Attribute6 | Attribute7 | **LSI**: Attribute8 | **LSI**: Attribute9 |
| awsId       | orgType | provType   |   CompanyName | firstName | lastName | ein | ssn | email | acquisitionSrc | memberSince |
| **String**: uuid | **String**: *Patient, Provider, Clinic, Dr., Insurer, Lender, Investor, SysAdmin* | **String**: *Behavior Analysts, Dental, OT/PT, Urgent-Care, Hospitals* | **String**: *Validate with ParserUtility* | **String** | **String** | **Number**: *Validate against IRS* | **Number**: *Validate against Dept Of State* | **String**: *Validate against ISO Standard & Domain Rules* | **String**: ** | **String**: Date() |

