# Notes - 06 Lost password reset

> Working documents on figma : [Lost password reset diagrams and associated sketches](https://www.figma.com/file/G7Fm7WiOecw3n7MScbtSL9/Lost-password-reset?node-id=0%3A1)

## Multi user context 
In a multi user context, the admin user should have the possibility to choose the **organisation** trusted contacts settigns among the following options : 
- Each user is automatically the trusted contacts of other users within the organisation
- Admin user(s) is(are) automatically the trusted contact(s) for all organisation users
- None of the users are automatically trusted contacts of each others
By default Admin user(s) is(are) automatically the trusted contact(s) for all organisation users.

A client openning an account is considered as an admin user and can add other users. When a single user add at least 1 new user, the account is consered mutli user and admin is prompt to choose the organisation trusted contacts settings
cf. this [state machine diagram on trusted contact settings](https://www.figma.com/file/G7Fm7WiOecw3n7MScbtSL9/Lost-password-reset?node-id=74%3A1059)

All admins can access and change the organisation trusted contacts settings

If the organisation trusted contacts settings is on "Each user is automatically the trusted contacts of other users within the organisation" or "Admin user(s) is(are) automatically the trusted contact(s) for all organisation users": 
- users should be able to use their own password for the trusted contact procedure (even if they have to enter it again)
- when a new organisation user creates an account, he has to explicitly save trusted contact settings : he can choose to delete the automatically added trusted contacts, and add his own trusted contact, or keep both
