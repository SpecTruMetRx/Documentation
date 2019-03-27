# SpecTruMetRx Data Model

This is the *data modeling* document for the SpecTruMetRx Payments & Heathcare Analytics solution. Please add to and use this document to implement a scalable and consistent data model that will be encrypted and secure within the AWS Cloud.

## User Detail Data Dictionary

This table is used as a master list of users where we store mappings of all users to our [AWS Cognito User & Identity Pools]() with a UUID.

### User Detail Queries

1. How many `users` by `OrgType`?
	* Filer by: `ProvType`
	* Sort by: `EIN`

2. How many `users` by `ProviderType`?
	* Filer by: `OrgType`
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

