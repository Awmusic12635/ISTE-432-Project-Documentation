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
### Exceptions

```html
<div id='errorbox'></div>
<form>
 <!-- LOGIN FORM DETAILS HERE -->
</form>
```

* Can be related to user login, though mostly handled in the business layer. 

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
### Exceptions
```php
public function checkUser($a) {
        If ($a == null){
            throw new Exception(‘This’ . $a . ‘ does not exist.’);
        } else {
            return echo “User exists.”;
        }
    }
```

This function checks whether an user exists or not. If user exists, it continues onto user’s homepage (GeoCache). Otherwise, it throws an exception and prints an error saying that this user does not exist.

* Validation - Check if user exists and then login if all correct (Access Authorization)
  * Exception if login is invalid:
  * Handles itself
* Characters within comments must be no longer than 1000
  * Handles itself
* Validates whether a person is an admin to create events
  * Handles itself
* Validates check ins before leaving comments
  * Handles itself
* preg_match for PHP (password, username, email, comments)
  * Handles itself



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

### Exceptions:
* SQL exception
  * Thrown to next layer above
* The requested data doesn’t exist
  * Handle itself
```php
public function render($request, Exception $e) {
    if ($e instanceof \App\Exceptions\DbUpdateException)
        return ‘REPLACE THIS’; // Do something if this exception is thrown here.
    return parent::render($request, $e);
}
```

## Performance

Much of the code we had written so far has left very little room for refactoring. We instead decided to focus more on improving the performance of the underlying infrastructure. 

    We started by using PHP 5, as it is one of the most common versions of PHP and often the default used on most servers. We later discovered that the latest version, PHP 7, was able to offer dramatic performance improvements, often displaying load speed increases of up to 33%. With this in mind, we upgraded the default version on our system to PHP 7. 
    
Like most programs that utilize a database, our backend used MySQL. We decided to replace this with MariaDB, a drop-in replacement for MySQL that has a number of performance improvements built into it. We simply installed it on top of MySQL and MariaDB took care of the rest. We also increased the built-in database cache values since the application we are building is also very heavily focused on reads instead of writes. Increased caching will allow our application to perform better when handling repeated queries.

Laravel has native support for Memcached, so it was decided to put that between our database and application to cache our database queries in memory. This dramatically improved I/O because the data rarely had to hit the disk and was instead served out of memory. We then decided to replace our Apache web server with NGINX, since it more often than not is quite a bit faster. To push the caching even further, it was decided to then put Varnish, an HTTP accelerator, in front of our web server to further cache generated pages and make it so less requests actually need to hit the web server. Though this only works for when users are not logged in. Some of the VCL used can be seen below.

```
backend default {
    .host = "127.0.0.1";
    .port = "8080";
}

acl purge {
    "127.0.0.1";
    "localhost";
}

sub vcl_recv {
    # handle purge requests
    if (req.request == "PURGE") {
        if (!client.ip ~ purge) {
            error 405 "Not allowed.";
        }

        ban("req.url ~ "+req.url+" && req.http.host == "+req.http.host);
        error 200 "OK";
    }

    if (req.url ~ "\.(png|gif|jpg|swf|css|js)$") {
        return(lookup);
    }

    # the cookie will persist until it expires (see your laravel session config)
    if (req.http.Cookie ~ "laravel_session") {
        return(pass);
    }

    # else ok to fetch a cached page
    return (lookup);
}

sub vcl_fetch {
    # strip the cookie before the static file is inserted into cache.
    if (req.url ~ "\.(png|gif|jpg|swf|css|js)$") {
        unset beresp.http.set-cookie;
    }

    # remove some headers we never want to see
    unset beresp.http.Server;
    unset beresp.http.X-Powered-By;
    unset beresp.http.X-Pingback;
    set beresp.do_esi = true; /* Do ESI processing */
    set beresp.ttl = 10m;

    # don't cache response to posted requests or those with basic auth
    if (req.request == "POST" || req.http.Authorization) {
        return (hit_for_pass);
    }

    # Laravel always adds a session cookie - we remove it with middleware and check it here
    # Do this before checking the page state but after post
    if (beresp.http.X-No-Session ~ "yeah") {
        unset beresp.http.set-cookie;
    } else {
        # do not cache responses which are for logged in users
        return (hit_for_pass);
    }

    # only cache status ok
    if (beresp.status != 200) {
        return (hit_for_pass);
    }

    # else ok to cache the response
    return (deliver);
}

sub vcl_deliver {
    if (obj.hits > 0) {
        set resp.http.X-Cache = "HIT";
    } else {
        set resp.http.X-Cache = "MISS";
    }

    unset resp.http.Via;
    unset resp.http.X-Varnish;
}

sub vcl_hit {
    if (req.request == "PURGE") {
        purge;
        error 200 "OK";
    }
}

sub vcl_miss {
    if (req.request == "PURGE") {
        purge;
        error 404 "Not cached";
    }
}
``

We took the opportunity to minify our JavaScript files to reduce the amount of time the system needed to parse them. To improve the loading of some of the larger assets that regularly need to be downloaded by our users, we place them on a global CDN, which is often closer to the user than our web server is and can be served from around the world via anycast. The same was done with the DNS of the website so that the lookup time for DNS resolution was consistently fast. The main web server itself was placed in New York City so as to be closer to our user base than that of those hosted elsewhere in the country.

Time to full first page load is often one of the big reasons that users leave a site before it finishes loading. To help solve this problem, we introduced more dynamic loading of resources. JavaScript script tags were moved to the bottom of the page so it would begin rendering before the JavaScript needed to take effect. Lazy loading of images was also introduced so that images were only loaded in as the user scrolled down through the page. To further improve image load times, we highly compressed the images with no visible change in quality to reduce their size, allowing them to be loaded much faster. The images were also then properly resized on disk so that the browser did not have to load full sized images and then resize it locally on its own. It was also decided to use image sprites to combine many of the images into a single file that could then be referenced via CSS.

Many browsers limit how many connections can be made to a single domain at a time (oftentimes 2-3). We added additional subdomains to hold assets, allowing more downloading of site assets in parallel. We also tried to use prefetching of content where possible so that when the user would click to another page, we would already have a large amount of the content loaded in the background on their system. We implemented AJAX where possible to give more of the illusion of speed (though it did add some speed), as full page loads were not always needed. We also attempted to rewrite as many of the JavaScript animations / dynamic changes as possible into CSS. This placed less of a computing load on the client browser and helped to avoid CPU spikes that can be taxing on client machines.

We did experiment with a RAM disk for all files, though later decided it was not worth the hassle when standard Linux page cache would likely do it well enough. The disk powering the server, however, was switched from a HDD server to one powered by SSD. This dramatically increased the random I/O speed and disk latency access. It was then decided that instead of using web fonts that our users had to download, we would use one of the default fonts that are built into most systems.

For our application, single threaded performance was needed the most (vs multicore). In most web applications many of the tasks are not done through multithreading and require linear processing. This makes a higher single threaded performance value more beneficial over high multi core performance. We switched our server from one being powered by a Xeon E5 server clocked at 2.4Ghz to that of a Xeon E3 server clocked at 3.6Ghz. Though the Dual E5 server node had more overall CPU power, the higher clock rate of the E3 cores allowed us to feel the benefit of the improved single-threaded performance in our application. The DDR3 RAM was also swapped for DDR4 RAM. Though the performance of this change was less notable than many of the other changes, each additional performance we were able to achieve was helpful.

Finally, we decided to switch from a fully virtualized VM to a container. A VM is a virtual server that full virtualizes the operating system as well as all the hardware involved. It also runs its own kernel. This has the advantage of being able to run more software but it does come with a cost, performance. Fully virtualized disks are slower than that of containers. A container is similar to that of a VM in that it has its own isolated version of an operating system, except that it does not virtualize the hardware. It instead borrows that from the host node and also shares the kernel with the host node. This frees up more resources to use for driving your application and dramatically improves responsiveness of the server as a whole.

## Testing

We decided to use the testing framework PHPUnit.de to write the unit tests for our program. We tried to test the activites that could be the most prone for error and important parts of our application logic.

### Login Test

One of the most important tests that can be run in a multiuser system is that users are actually able to login. 

#### Good Login
In the test of a good login we make a new user, visit the login page and then enter that correct login information. We then assert that the user is redirected back to the main page to verify they are logged in. To make this easier we are not hashing the password for the test.

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
use App\User;

class LoginTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {

        //create new user
        $testuser = new User();
        $testuser->username = "AWacker";
        $testuser->email="alex@alexwacker.com";
        $testuser->password="thissosecureandtotallyhashed";
        $testuser->is_admin=true;
        $testuser->is_mod=true;

        $testuser->save();

        $this->visit('/login')
            ->type('AWacker', 'username')
            ->type('thissosecureandtotallyhashed', 'password')
            ->press('Login')
            ->seePageIs('/');
    }
}


```

#### Bad Login

Similar to the correct login test we set it up in the same mannor. However in this case we do not enter the correct login information and make the assertion that the user is not redirected to the main page and is instead back to the login page. It is just as important to test that a user can get in as it is to make sure those with the incorect information cannot login. 

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
use App\User;

class BadLoginTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {

        //create new user
        $testuser = new User();
        $testuser->username = "AWacker";
        $testuser->email="alex@alexwacker.com";
        $testuser->password="thissosecureandtotallyhashed";
        $testuser->is_admin=true;
        $testuser->is_mod=true;

        $testuser->save();

        $this->visit('/login')
            ->type('AWacker', 'username')
            ->type('thisisactuallynotthepasswordhaha', 'password')
            ->press('Login')
            ->seePageIs('/login');
    }
}

```

### New Cache Creation

With our site being a geocaching website we need to get new geocaches from somewhere. In our case users can submit new geocaches once their account has been confirmed and enabled. 

#### New Cache Authorized

Similar to last time we will be testing both authorized and unauthorized users by filling out a web form as that specific user. 

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;

class NewCacheAuthTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
        //make authorized user
        $user = factory(App\User::class)->create();
        $user->enabled=true;

        $this->actingAs($user)
            ->visit('/newcache')
            ->type('The best cache ever', 'name')
            ->type('94.234324234,-35.74352343', 'location')
            ->type('small', 'size')
            ->type('traditional', 'type')
            ->type('small', 'size')
            ->type('like fo reals this is short yo', 'short_description')
            ->type('like fo reals this is the longest description that could be possible yo. but I am a creative fellow 
            and I need to express my art in the form of comments that is where I actually discuss the true meaning of 
            life and that is death and sad because I am sad my gosh what has my life become I am the excessive of 
            computer I am good my friend said so. ', 'long_description')
            ->press('Create')
            ->assertResponseOk();
    }
}

```

#### New Cache Not Authorized

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;

class NewCacheUnAuthTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
        //make unauthorized user
        $user = factory(App\User::class)->create();

        $this->actingAs($user)
            ->visit('/newcache')
            ->type('The best cache ever', 'name')
            ->type('94.234324234,-35.74352343', 'location')
            ->type('small', 'size')
            ->type('traditional', 'type')
            ->type('small', 'size')
            ->type('like fo reals this is short yo', 'short_description')
            ->type('like fo reals this is the longest description that could be possible yo. but I am a creative fellow 
            and I need to express my art in the form of comments that is where I actually discuss the true meaning of 
            life and that is death and sad because I am sad my gosh what has my life become I am the excessive of 
            computer I am good my friend said so. ', 'long_description')
            ->press('Create')
            ->assertResponseStatus(403);
    }
}

```

### Check In Test

Another very large part of our user's interactio with our website is allowing them to checkin to various geocaches. In this test we create a user and then checkin as that user on the first geocache and make sure it goes through correctly.

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;

class CheckinTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
        //create new user
        $testuser = new User();
        $testuser->username = "AWacker";
        $testuser->email="alex@alexwacker.com";
        $testuser->password="thissosecureandtotallyhashed";
        $testuser->is_admin=true;
        $testuser->is_mod=true;

        $testuser->save();

        $this->actingAs($testuser)
            ->visit('/cache/1/checkin')
            ->type('Wow this was a cool one', 'comment')
            ->press('Checkin')
            ->assertResponseOk();
    }
}

```

### Search Test

Our users need to be able to find new geocaches in an easy manner. For this we use a search function. To test this we create a new geocache and then have the test run a search for that specific cache just as a user would and then checks to make sure it shows up. 

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
use App\Cache;

class SearchTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {

        $testcache = new Cache();
        $testcache->name="testitem1";
        $testcache->approved=true;
        $testcache->save();

        $this->visit('/search')
            ->type('testitem1', 'searchbox')
            ->press('Search')
            ->see('testitem1')
            ->dontSee('Cache not found');
    }
}

```

### Cache Admin Approval

In our system new geocaches must be approved by an admin before they are publically viewable. To test this we first create a new geocache item. From there we then use our search feature to assert that the item is not viewable. If that is true it moves on making a new test user to view the admin page and approving all pending requests. It then reruns the same search this time asserting that the cache is now visible.

```php
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
use App\Cache;
use App\User;


class ApproveCacheTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
        $testcache = new Cache();
        $testcache->name="testitem1";
        $testcache->save();

        $this->visit('/search')
            ->type('testitem1', 'searchbox')
            ->press('Search')
            ->see("Cache not found")
            ->dontSee('testitem1');

        //make authorized user
        $user = factory(App\User::class)->create();
        $user->enabled=true;
        $user->is_admin=true;
        $user->save();

        $this->actingAs($user)
            ->visit('/admin/pendingapproval')
            ->press('Approve All')
            ->assertResponseOk();

        $this->visit('/search')
            ->type('testitem1', 'searchbox')
            ->press('Search')
            ->see('testitem1')
            ->dontSee('Cache not found');


    }
}

```

