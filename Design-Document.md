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
15. Accomplishment badges on profiles
16. Profiles
17. User profiles with information about them
18. Stats
19. Search bar to search for geo caches. 

    
                    
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



# 6. Technologies Used:
    * HTML/CSS
    * JS
    * PHP
    * MySQL
    * Laravel
    
## Data Sources:
    * Google Maps API
    * Open Geo Cache API


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
    
        
# Layering

## Presentation Layer
    For the basis of our presentation layer, our views are arranged in more of a hierarchy and do not specifically refer to a class, rather they are more similar to a template. 
    
### Admin View (/admin)
* While an administrator is also a user, the user that is marked as an admin has a specific panel area they are able to access and use for specific additional functions. 
* Modify Event View (/admin/event)
 * The administrator is able to load a page to add, delete, or modify events inside of the administrator panel.
* Modify Accomplishment View (/admin/acc)
 * The administrator is able to load a page to add, delete or modify accomplishments inside the administrator panel.
 
### Club Member (Profile) View (/profile)
* Add Cache View (/addcache)
 * The GeoChap user is able to register a new geocache with the site, providing all location and cache data through a form for submission.
* Check In View (/checkin)
 * The GeoChap user is able to check in at specific caches to show that they have been there. They may leave a comment on that cache’s logbook.
* Edit Profile View
 * The GeoChap user is able to edit his/her profile information anytime.
 
### Public (Domain) View (/)
* Detailed Cache View (/cache/<id> )
 * Public is able to see detailed cache data.

### Presentation layer code for the code of displaying the user login



```html 
<!-- app/views/login.blade.php -->

<!doctype html>
<html>
<head>
<title>Login</title>
</head>
<body><

{{ Form::open(array('url' => 'login')) }}
<h1>Login</h1>

<!-- if there are login errors, show them here -->
<p>
    {{ $errors->first('email') }}
    {{ $errors->first('password') }}
</p>

<p>
    {{ Form::label('email', 'Email Address') }}
    {{ Form::text('email', Input::old('email'), array('placeholder' => 'alex@alexwacker.com')) }}
</p>

<p>
    {{ Form::label('password', 'Password') }}
    {{ Form::password('password') }}
</p>

<p>{{ Form::submit('Submit!') }}</p>
{{ Form::close() }}
```


## Business Layer
    
### User Class

The User class will represent users table in the database that are used to sign in and out of the application. It will also enforce the roles of requiring certain permissions to do some tasks. 

### Cache Class

The Cache class will represent the caches table in the database. It is the record of all the objects placed in the real world. It will enforce the business rules, such as a new cache having to be approved before it can be shown to all other users. 

### Events Class

The Events class will represent the events table in the database. It is a record of each time an administrator has created an event object. Also, it will be implemented to enforce the business rules by allowing only an administrator to create an event.

### Check-Ins Class (includes comments)

The Checkins class will represent the checkins table in the database. It is a record of each time a user has visited a cache object. It will also enforce the business rules, such as a user being able to checkin to a cache more than once.

### Accomplishments Class

The accomplishments class will represent the accomplishments table in the data that is a record of all the accomplishments that a user has fulfilled. It will enforce the business rules, such as only the first cache checkin being counted towards the completion of an accomplishment.

Business Layer Check if user exists and then login if all correct:


```php
    $userdata = array(
        'email'     => Input::get('email'),
        'password'  => Input::get('password')
    );

  if (Auth::attempt($userdata)) {

    //I’m in, Doc
 } 
```

## Data Layer
### Laravel Eloquent ORM
The data layer is mixed in with the service layer to a degree. Laravel provides something they call the “Eloquent ORM” that maps the class objects we create to records in the database. When new objects are created and their .save() methods are called, new records are created in the database. When a record is pulled from the database it is cast back to the specific object class we created.

### how we would create a new user

```php

$user = new User();
$user->email = “alex@alexwacker.com”;
$user->is_admin=true;

$user->save();
``` 
