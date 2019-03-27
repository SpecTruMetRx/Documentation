# User Detail

This table is used as a master list of users where we store mappings of all users to our [AWS Cognito User & Identity Pools]() with a UUID.

## User Detail Queries

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

### User Detail Data Dictionary




### Table
|TableName: | Users | | | | MasterList |
|:----------|:-----:|:----------:| | | |
|Partition Key| Sort Key| Attribute1 | Attribute2 | Attribute3 | Attribute4 |
| awsId       | orgType | provType   |   provType |   provType |
