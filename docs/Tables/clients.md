### structure

The *clients* table consists of registered clients, with required information:

| Field name | Field type  | Description |
| :--- | :--- | :--- |
| *Email* | **string(128)** NOT NULL; UNIQUE KEY | Email stands as user's identity - should be matched by regex filter. |
| *EmailVerified* | **boolean** NOT NULL; *false* by default | Determines whether the user's email is verified - if not, the user cannot use the service. |
| *Name* | **string(128)** NOT NULL | |
| *Surname* | **string(128)** NOT NULL | | 
| *BirthDate* | **date(DD-MM-YYYY)** NOT NULL | May seem redundant, as every user who is registered naturally is over 18 yrs old, but for legal reasons it is advised to store this information. |
| *AccountCreated* | **date(DD-MM-YYYY-hh-mm-ss)** NOT NULL | Timestamp, given by the database, when client is registered |
| *LastAccess* | **date(DD-MM-YYYY-hh-mm-ss)** NOT NULL | Timestamp, given by the database, when client was last authenticated - may be used to delete unused accounts or for marketing purposes |

### functionalities

- ***addUser*** (string(128) **email**, string(128) **name**, string(128) **surname**, date(DD-MM-YYYY) **birthDate**):
	- adds user record to this table
	- the database sets fields as follows: 
	  ```Email = email, EmailVerified = false, Name = name, Surname = surname, BirthDate = birthDate, AccountCreated = getCurrentTime(), lastAcceess = getCurrentTime()```
- ***userAuthorized*** (string(128) **email**)
	- triggers database to refresh *LastAccess* field
- ***emailVerified*** (string(128) **email**):
	- toggles email verification state to *true*, which gives access to app's service
- ***emailNotVerified*** (string(128) **email**):
	- toggles email verification state to *false*, which denied access to app's service
	- may be used when user wants to change their email
- ***removeUser*** (string(128) **email**):
	- removes user record from this table, per given email
- ***getUserInfo*** ()
	- returns all of user's data as a *string in JSON format*