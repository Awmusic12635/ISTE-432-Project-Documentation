* Milestone 1 - Requirements
* Dave Sanders; Alex Wacker; Anna Wesolowski
* September 8, 2016


## Glossary

* __Geocaching__ - A treasure hunting game in which players use GPS (Global Positioning System) to navigate and search for hidden items.
* __Logbook__ - A written record of those who has located a geocache.
* __Geocache__ - Also known as cache. A hidden item that usually contains a logbook for geocachers to sign.
* __Muggle__ - A person who is not a geocacher. The term, Muggle, comes from the Harry Potter series in which a person who is not magical.
* __Waypoint__- A longitude and latitude for a geocache.


## Current System

The existing geocaching system used by the geocaching club is a public 3rd party solution. This existing solution provides access to a large collection of geocaches from around the world. It features user accounts, find history, comments and social networking. 

While this existing solution is widely used and has a large data set, it faces restrictions in its fit to the club. It is not possible to set up club activities easily through it and coordinate the club’s members. The existing solution also faces a problem of having too large of a global scope. It covers the entire world which can lead to less fine-grained details that are specific to the rochester area. 


## Goals

* We plan to design and build an easy to use interface for geocachers who wish to locate local caches and find out all the information about them, as well as graphically display a map of where the cache is in the world. A stretch goal of ours is to also display how far away a cache is relative to the current location, as well as a path to get to it. Specific functionality will involve:

* We plan to add a system for which club events can be created that allow members to participate in. Example events could be: race to completion, general outing, and more. 

* Logbook will be used for geocachers to leave a comment and check in. For instance, geocachers may mention that they have found a geocache.


## Stakeholders

* Geocaching Members
    * They want to participate in a treasure hunting activity by navigating and finding a hidden item, which is geocache.
    * They want to find out more information about geocache. 

* Geocaching Club E-Board
    * They want to use the logger to keep a track of geocachers who have found a geocache.
    * They want to ensure that there are no problems with geocaching app.
    * Some E-Boards are geocachers, and they are interested in participating in a treasure hunting game.


## Scope

The scope of this product involves displaying geocachers information about logged caches in their area and allowing them to comment on them, log their visits, and register new cache locations. This app will be used for a single small geocaching club. That is to say that most things beyond local caches and their associated data is unneeded in the app’s output due to the local nature of the club. All new data created by this app is stored on its own database and not accessible to the greater geocaching community.


## Input

The following inputs will be used:

* Some user input will be received as users enter search queries.
* Additional user input will be received as users submit new geocaches, check-ins and comments.  
* Mapping and geolocation data from Google maps or a like service.
* Possible input from a 3rd party geocaching database to expand the result set returned to the users.



## Processing

* Searches will be run on user inputted locations to provide all geocaches in the specified area

* Comments will be shown and added for any viewed geocaches
* Checkins will be marked for users and their specific geocaches
* Historical data will be processed and stored to be able to create statistics on found geocaches


## Output

* For Geocaching Members: A searchable collection of geolocations, comments from any viewed geocachers, and checkins.

* For Geocaching Club E-Board: A searchable collection of logs, comments from any viewed geocachers, historical data and improved geocaches.


## Data Sources

* __[Google Maps API](https://developers.google.com/maps/)__ - An API offering map and geolocation information, including converting latitude and longitude values into an interactive map.

* __[OKAPI - Opencaching API](http://www.opencaching.us/okapi/introduction.html)__ - An API allowing developers to read public Opencaching data and and read/write private user-related data.
