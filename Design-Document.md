* ISTE 432
* Design Document
* Professor McQuaid
* Team ADA
* Alex Wacker, David Sanders, Anna Wesolowski

# 1. Team Members and Roles 
* Alex Wacker: Database, backend and server infrastructure
* David Sanders: Server-side developer, Documentation Specialist
* Anna Wesolowski: Front-End Developer, Design

# 2. Background

The local college geocaching club has used a 3rd party geocaching solution for many years, however they have been running into problems with it for quite some time. The 3rd party system is public for anyone in the world to use, and therefore tries to please everyone. Because of this the existing solution is more suited for individual users, instead of a club as a whole. The club has been struggling with membership recently due to a lack of events and thinks a new system that is tailor suited for them will help increase membership and participation. 

# 3. Project Description

GeoChap is a specialized web application made for the use of a single geocaching club. Its functionality includes an interface that displays local caches and all associated metadata, a map of where the cache is in the world, an event planner for the club to organize hunts, a logbook for cachers to leave comments on, and a method for registering new cache locations for the club.

GeoChap strives to be lightweight and responsive, as one of our stretch goals is to also display how far away a cache is relative to the current location, as well as a path to get to it. The product is web-based and will be accessible for mobile users but will not have a mobile app.

The website will include a simple login system, and each user can gain “Accomplishments” through participation in events. These accomplishments are displayed on their public profile.



# 4. Project Requirements
    
1. A map display for geocachers to view and/or locate certain caches and seek information about them. 
2. Logbook for geocachers check in. 
3. Can comment on check ins
4. A system where club events are managed and created for geocaching members to join.
5. User Account System
6. Separate Permissions for Users and Admins
7. Admins have a management panel
8. Help System
9. Glossary of Terms
10. Getting Started Guide
11. How to use GeoChap
12. Integration of 3rd party geocaching data
13. Accomplishment System
14. Tracks top users stats
15. Awards badges / achievements
16. Profiles
17. User profiles with information about them
18. Stats
19. Accomplishments done
    
                    
# 5. Business Rules

1. A user must have a user account
2. An admin login is also a user login
3. Accomplishment progress only applies to the first check in
4. A user can check in to the same cache more than once
5. New geocache locations must be approved by an admin
6. Unvalidated users cannot create new caches
7. Users must check in at cache before commenting
8. Only an administrator can create an event
9. Comments are limited to 1000 characters
10. Newly created geocaches must include, size and location



# 6. Technologies Used
    * HTML/CSS
    * JS
    * PHP
    * MySQL
    * Laravel


# 7. Timeline

The GeoChap development team will primarily be meeting every Thursday at 4:45 to work on the current project milestone, as well as out of class for some coding work. Our documentation book will be reassessed as we progress and will be updated as needed. We will progress through the project in the following steps:

* Milestone 2: Design and Design Patterns – 9/29 (Fri) @ 11:59pm

  * Finish the first version of design document and include anticipated pattern usage.

* Milestone 3: Layering – 10/7 (Fri) @ 11:59pm
  * Begin the basic structure of the back end.

* Milestone 4: Exception Handling – 10/21 (Fri) @ 11:59pm
  * Further expand upon the application structure and begin to add error testing and failure handling functionality.

* Milestone 5: Performance and Refactoring – 11/4 (Fri) @ 11:59pm
  * Give the application a presentable front end and and improve the performance of the application. 

* Milestone 6: Testing – 11/18 (Fri) @ 11:59pm
  * Finish any remaining parts of the application and test it to make sure there are no bugs.

* Milestone 7: Deployment, Packaging – 11/25 (Fri) @ 11:59pm
  * Minor touch ups and stretch features.

* Finalized Code - 12/9 (Fri) @ 11:59pm
  * Wrap up the code.

# 8. Design Patterns
                

## Iterator pattern:

Laravel provides functionality for abstracting database query results into PHP object arrays. Those arrays, an instance of the Iterator pattern, will be used by our program on the business layer.

## Memento pattern:

We would be using the memento pattern to be a sort of checkpoint in saving the state of in progress form data that is being entered on the creation of new events or geocaches. In the event that someone accidentally leaves the page prematurely, their information will be retained. 
    
        
     
