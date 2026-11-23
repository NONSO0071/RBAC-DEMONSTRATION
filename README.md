# RBAC-DEMONSTRATION
24/14643
Chinonso precious Anyaegbusim
Role-Based Access Control (RBAC)
A small Python program that demonstrates the basic idea of Role-Based Access Control using fictional users, roles and permissions.
What is RBAC?
In RBAC, permissions are not given to users directly. Permissions are grouped into roles, and each user is assigned a role. A user can only do what their role allows. This makes access easier to manage and audit: to change what a group of people can do, you change the role, not every individual user.
Project structure
rbac_project/
├── rbac.py     # roles, users, permission check and tests
└── README.md   # this file
Design
Role	View report	Edit report	Delete report	Add user
director	Yes	Yes	Yes	Yes
supervisor	Yes	Yes	Yes	No
clerk	Yes	Yes	No	No
visitor	Yes	No	No	No
User	Role
emeka	director
funke	supervisor
ibrahim	clerk
zainab	visitor
How the code works
Define roles and permissions. Permission is an Enum of allowed actions. Role holds a name and a set of permissions. User links a username to one role.
Check permissions. AccessControl.is_allowed(username, permission) finds the user, reads their role and returns True only if the permission is in that role. Unknown users are denied by default (the principle of deny by default).
Test the system. run_demo() prints a table of sample requests, and the TestAccessControl class checks the rules with unittest.
How to run
Requires Python 3.8 or newer. No extra libraries are needed.
python rbac.py
Sample output
STATUS   | USER      | ROLE       | PERMISSION
----------------------------------------------------
ALLOWED  | emeka     | director   | add_user
ALLOWED  | funke     | supervisor | delete_report
BLOCKED  | funke     | supervisor | add_user
ALLOWED  | ibrahim   | clerk      | edit_report
BLOCKED  | ibrahim   | clerk      | delete_report
ALLOWED  | zainab    | visitor    | view_report
BLOCKED  | zainab    | visitor    | edit_report
BLOCKED  | stranger  | unregistered | view_report
All unit tests should then pass.
Security ideas shown
Least privilege: each role has only the permissions it needs.
Deny by default: unregistered users get no access.
Separation of duties: only the director can add users.