# User Detail

This table is used as a master list of users where we store mappings of all users to our [AWS Cognito User & Identity Pools]() with a UUID.

## User Detail Queries

1. How many `users` by `OrgType`?
	* Filer by: `ProvType`
2. How many `users` by `ProviderType`?
	* Filer by: `OrgType`
3. How many `users` for each Corporate Name?
	* Sort by `SSN` or `EIN`
4. Get `user` by `provType`. Filter by:
	* Joined < || > date()
	* `user` by `txnCount` DESC
	* `user` by `txnVolume` DESC
5. Get `user` by `acquisitionType`
6. Get total `users` by `city`

### User Detail Data Dictionary




### Table
|Table: |
|:------|
|Partition Key|Sort Key| Attributes |
|:------------|:-------|:-----------|
| awsId | orgType | testAttr |
