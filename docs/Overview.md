*Note: we recommend reading these docs with [Obsidian](https://obsidian.md).*
# Team
- Aleksander Brzykcy: <abrzykcy@student.agh.edu.pl>
- Paweł Młodkowski: <mlodkowskip@student.agh.edu.pl>
- Stanisław Niemczewski: <sniemczewski@student.agh.edu.pl>

# Idea 

This project is to provide a database system for an external application, which as a whole provides a service inspired by **Traficar** - convenient, short-term car renting.

The company, which would run such service, would provide *legal*, *ready-to-go*, *fully fuelled* cars, with *valid insurance*, which shall also be properly tagged (with QR codes, for example).

Clients **must** be *over 18 years old*, *must have a valid driver's license* and need to ==provide their *payment card details* in the app==[^1].

From the client's point of view, everything should look as follows:
1. (*If not already registered*) Register to the system through an app;
2. Find a suitable vehicle nearby and reserve it for time they need to reach it:
	- The reservation options allow for a few different rent plans, as provided by the company, f.e. *whole day* or *no limits* - this determines the service price;
	- If the client needs more time, they can extend it;
	- If the client wants to cancel the reservation, they may do it anytime with no consequences;
4. After they reach the car, the client needs to identify it with the application (with QR codes, as mentioned), which then would unlock the vehicle;
5. The built-in system in the vehicle charges per travelled kilometer, and does not include any time-related fees;
6. After the client is done with renting, they need to stop the rent with an application - the payment is automatically calculated and charged from the provided card directly.

# Project

The database project would consist of tables and functionalities, as provided in ==the following documents *(to be added)*==. The language of choice is ==*(to be added)*==. The database's scheme is to meet the **2NF** standard.

The documentation consists of the whole system's life cycle:
- requirements analysis;
- base sketch and diagrams;
- implementation;
- tests with required documentation.

The work is organised as follows:
==*(to be added)*==

[^1]: Do we need card information, or some kind of other info to process payments?