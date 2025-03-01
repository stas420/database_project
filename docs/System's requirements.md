*Note: see **Overview** document, to get a grasp of idea and principles.*

The company, which would run a service similar to **Traficar**, needs *vehicles to rent*, a contractor providing *payment systems*, and also an *application* with a dedicated *administration system* for this purpose.

In this project, we focus on the last of these - a database system.

From company's point of view, needed resources are:
- *vehicles* to rent, with all needed legal and security actions taken;
- ***database*** storing:
	- *clients' information*, such as their name, surname, email, email verification status, date of birth and timestamps of account creation and last access;
	- *vehicles' information*, such as their model information (brand, name, type, pricing), renting status, colour, license plate, condition details, its geographical coordinates and mileage;
- *application for clients*, to provide a convenient way of using this service:
	- it should allow clients to register and unregister themselves or change their selected information on demand;
	- use the company's fleet offer with no flaws;
- *application for system administration*, which allows the company to manage their fleet and clients' information:
	- it should allow the company to automate renting system and control current state of their vehicles;
	- also, it should give access to client's information for the company's data administrators.

![[user_interaction.png]]
*Fig. 1 - user interaction and request diagram* (```/docs/note_attachments/user_interaction.png```)

![[backend_interaction.png]]
*Fig. 2 - backend database operations processing diagram* (```/docs/note_attachments/backend_interaction.png```)

Database is relational and organised in tables, as described in *docs/[[Tables List]]* document. Each table handles a set of function calls, which provide a convenient and safe way to automate the most-frequently used administration tasks, for both backend API and system administrators. 