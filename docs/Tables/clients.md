### structure

The *clients* table consists of registered clients, with required information:

| Field name | Field type  | Description |
| :--- | :--- | :--- |
| *clientID* | **CHAR(32)** PRIMARY KEY | |
| *email* | **TEXT** NOT NULL; UNIQUE | Email stands as user's identity - should be matched by regex filter. |
| *emailVerified* | **BOOLEAN** NOT NULL; *false* by default | Determines whether the user's email is verified - if not, the user cannot use the service. |
| *forename* | **TEXT** NOT NULL | |
| *surname* | **TEXT** NOT NULL | | 
| *birthDate* | **DATE(DD-MM-YYYY)** NOT NULL | May seem redundant, as every user who is registered naturally is over 18 yrs old, but for legal reasons it is advised to store this information. |
| *accountCreated* | **TIMESTAMP(DD-MM-YYYY-hh-mm-ss)** NOT NULL | Timestamp, given by the database, when client is registered |
| *accountLastAccess* | **TIMESTAMP(DD-MM-YYYY-hh-mm-ss)** NOT NULL | Timestamp, given by the database, when client was last authenticated - may be used to delete unused accounts or for marketing purposes |

### functionalities

- ***addUser*** (TEXT **email**, TEXT **name**, TEXT **surname**, DATE(DD-MM-YYYY) **birthDate**) $\rightarrow$ BOOLEAN:
	- adds user record to this table
	- returns TRUE if user was successfully added, and FALSE if any argument is invalid/ill-formed, or the user with given email already exists
- ***userAuthorized*** (TEXT **email**) $\rightarrow$ BOOLEAN
	- triggers database to refresh *accountLastAccess* field
	- returns FALSE if user with given email was not found, TRUE otherwise
- ***emailVerified*** (TEXT **email**) $\rightarrow$ BOOLEAN:
	- toggles email verification state to *true*, which gives access to app's service
	- returns FALSE if user with given email was not found, TRUE otherwise
- ***emailNotVerified*** (TEXT **email**) $\rightarrow$ BOOLEAN:
	- toggles email verification state to *false*, which denied access to app's service
	- may be used when user wants to change their email
	- returns FALSE if user with given email was not found, TRUE otherwise
- ***removeUser*** (TEXT **email**) $\rightarrow$ BOOLEAN:
	- removes user record from this table, per given email
	- returns FALSE if user with given email was not found, TRUE otherwise
- ***getUserInfo*** (TEXT **email**) $\rightarrow$ BOOLEAN or TEXT:
	- returns all of user's data as a *string in JSON format*
	- if user with given email was not found, returns FALSE