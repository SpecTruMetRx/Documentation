# SpecTruMetRx Data Model

This is the *data modeling* document for the SpecTruMetRx Payments & Heathcare Analytics solution. Please add to and use this document to implement a scalable and consistent data model that will be encrypted and secure within the AWS Cloud.

## User Detail Data Dictionary

This table is used as a master list of users where we store mappings of all users to our [AWS Cognito User & Identity Pools]() with a UUID.

### User Detail Queries

1. How many `users` by `OrgType`?
	* Filer by: `ProvType`
	* Sort by: `CompanyName`

2. How many `users` by `ProviderType`?
	* Filer by: `OrgType`
	* Sort by: `CompanyName`

3. How many `users` for each `CompanyName`?
	* Filter by `OrgType`
	* Sort by `SSN` or `EIN`

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
|**Partition** Key| **Sort** Key| **LSI**: Attribute1 | **LSI**: Attribute2 | Attribute3 | Attribute4 | Attribute5 | Attribute6 | Attribute7 | Attribute8 | Attribute9 |
| awsId       | orgType | provType   |   CompanyName | firstName | lastName | ein | ssn | email | acquisitionSrc | memberSince |
| **String**: uuid | **String**: *Patient, Provider, Clinic, Dr., Insurer, Lender, Investor, SysAdmin* | **String**: *Behavior Analysts, Dental, OT/PT, Urgent-Care, Hospitals* | **String**: *Validate with ParserUtility* | **String** | **String** | **Number**: *Validate against IRS* | **Number**: *Validate against Dept Of State* | **String**: *Validate against ISO Standard & Domain Rules* | **String**: ** | **String**: Date() |

