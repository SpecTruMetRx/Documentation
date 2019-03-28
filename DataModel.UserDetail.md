# SpecTruMetRx Data Model

This is the *data modeling* document for the SpecTruMetRx Payments & Heathcare Analytics solution. Please add to and use this document to implement a scalable and consistent data model that will be encrypted and secure within the AWS Cloud.

In using a **NoSQL** database like *DynamoDB*, our goal is to scale our *OnLine Transaction Processing (OLTP)* capabilities to meet the realtime demands of our users to process their requests with sub-second latency. We are optimizing denormalized and hierarchical data for compute processing & data streaming to instantiate real-time views that scale horizontally as built for OLTP.

Our decision to implement *DynamoDb* happens when we know our application's *data access patterns* precisely, and when they are repeatable, consistent, and simple queries like any: `SELECT * FROM [table]` type access patterns.

If the data needs to be reshaped with `JOIN` methods, then it would be best to consider [AWS RedShift]() as a `DataWarehouse` solution for any `data analytics` that has to be performed on the data. *OLTP* applications are ideal use cases for *NoSQL* data bases

When modeling a new data table, always model your partition and sort keys in a way that will let you model the table to support one of your primary access patterns. You always want the table to be able to query something that is interesting to the application.



## User Detail Data Dictionary

This table is used as a master list of users where we store mappings of all users to our [AWS Cognito User & Identity Pools]() with a UUID.

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

