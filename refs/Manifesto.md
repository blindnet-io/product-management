**1.Divide and Minimize**
The less the software system knows, the smaller the risk of exposure.

Software architects should design client-server applications in such a way that only necessary user information is known by the server, and the functionality of the system can be delivered without revealing additional user information to a centralized entity. The software design must clearly distinguish two categories of user data:

the user data the system must have the knowledge of in order to deliver promised functionality, and
the user data exchanged between system users directly, but not with the system itself.

The second type of user data, when unencrypted, must only reside on the user's hardware. If stored at a centralized location, it must be encrypted in such a way that it can be decrypted only by the user on the user-controlled hardware.

**2.End-to-End Encrypted Transfers**
Software engineers must ensure only intended users can access and understand user data when it transits through the Internet.

User data, when transiting between any two endpoints, must be encrypted end-to-end.

**3.Zero-Trust Third Party Services**
Third party solutions must ensure participants’ anonymity. They should not be able to interpret data at any time during the service period.

A service provider that protects and executes data transfers must ensure that those transfers remain anonymous between any number of senders and receivers. All parties and their identities must remain private so that no external party can identify the endpoints of a transfer.

The data transfers must remain private to all, including the service provider itself. Transfer parties can trust the service provider to protect data in transit and have zero-trust with the data itself.

**4.No Loss of Functionality, No Increase in Friction**
Nothing prevents modern software from delivering superior, intelligent functionality to the user, while still applying the core data privacy principles. The era when users had to trade privacy for functionality is over.

Designing a software system for privacy must not limit the functionalities offered to users. Data privacy principles must be implemented in a wide range of applications - from machine learning to personalization.

Designing a software system for privacy must not create friction in the user experience. Data privacy principles need to ensure a seamless execution of system functions. Further, data privacy principles must guarantee that the service provider only operates with minimum user data in order to provide full functionality.
