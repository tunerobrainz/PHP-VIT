# PHP-VIT
A Minimal PHP template engine. 13 JULY 2017.

** VIT ** let's you seperate your frontend code from your backend code. Saving you from all the hassles of writing PHP code alongside HTML codes. VIT features a very simple syntax that looks somewhat similar to JSON: the _curly braces_. Example: ` <title>{{ title }}</title>`. We built this for the sole purpose of making things easier and faster for developing most of our web pojects.

## Why use Vit?
It's basic, simple and easy to use. If you need to code a simple website under a Professional and very nice/clean code (as I really enjoy doing), this PHP template engine will be very useful in order to *start on good basis* and *save time and money*.


## Help

If you have problems you can use the Wiki or raise an issue. You can also checkout a forum we made for VIT: http://www.gdevit.com/f52/phpvit

## Contributing

You can freely contribute with us on this project as it is open source, you can do that by joining our community: http://www.gdevit.com/f52/phpvit or by contacting us via email: gdevstorm@gmail.com || 2nerobrainz@gmail.com


## Requirements, Installation, Configuration & Setup:


You need a working server with PHP 7.0+ configured, if you don't have this, [CLICK HERE.](http://www.apachefriends.org/en/xampp.html) And follow the steps for the necessary installation on your machine.


Create a config.php file and setup VIT 

```php
require_once __DIR__.'/VIT/VITAutoload.php';

$vitConfig = array('binder' => ['{{','}}'], 'dir' => '/path/to/template');

try {

    $vit = new VIT\VIT($vitConfig);
    
} catch(VIT\Exception\Config $e) {

    echo $e->getMessage();
}
```

Now, let's create a simple page using VIT

index.php
```php
#include config.php
require_once 'config.php';

try {

    #Assign a variable to vit
    $vit
        #Assign a title variable
        ->('title', 'VIT Demo page')
        
        #Compile and build template
        ->build('index');

} catch (VIT\Exception\Build $e) {

    die($e->getMessage());
}
```

In '/path/to/template' directory, create 'index.vit'
```
<!DOCTYPE html>
<html>
    <head>
        <title>{{ title }}</title>
    </head>
    <body>
        Hello!!! Welcome to VIT!
    </body>
</html>
```

## Working with VIT

#### Assign variables
Direct assign
```
$vit->assign('title', 'VIT');
$vit->assign('description', 'PHP Template System');
```
Multi-Assign
```
$vit->assign([
    'title' => 'VIT',
    'description', 'PHP Template System'
]);
```

#### Comments
VIT can be commented
```
{{!-- This is a VIT Comment --}}
```
#### Arrays, Object
(Objects are changed to arrays once assigned to vit).
```php
$vit->assign('info', ['title' => 'VIT', 'type' => 'Demo']);
```

Then in vit file we can have something like this
```
Hey, this is {{ info[title] }} and we are working on the {{ info[type] }}
```

Looping through arrays
```php
$vit->assign('lists', ['a', 'b', 'c', 'd']);

$vit->assign('data', ['name' => 'Dammy', 'nick' => 'nex', 'age' => '10', 'lang' => 'PHP', 'buddy' => 'Tunero', 'buddy_age' => '998']); //Spaces are not supported.
```
And in vit
```
{{#each $lists as list}}
    {{ list }} <br>
{{/endeach}}

{{#each $data as key,val}}
    {{ key }}: {{ val }}<br>
{{/endeach}}
```
Result:
```
a
b
c
d

name: Dammy
nick: nex
age: 10
lang: PHP
buddy: Tunero
buddy_age: 998
```

#### Filters
VIT variable can be filtered using PHP functions

PHP
```php
$vit->assign('name', 'dammy');
```
VIT
```
{{!-- Use filters without args --}}
{{ name | strtoupper }}

{{!-- With args --}}
{{name | substr(0, 3) }}
```

Result:
```
DAMMY

dam
```

Filters can also be used directly inline with strings
```
{{ "Hello World!" | strtoupper }}
```

Result:
```
HELLO WORLD!
```

#### Includes
VIT let's you include vit files in '/path/to/template/includes'
Once VIT is correctly configured, the includes directory will be automatically created.

Create 'header.vit' in the includes directory

header.vit
```
This is the header file
```

Let's include the header in the 'index.vit' file created earlier
```
{{#include header}}
```
Multiple files can be included, for example, we create a 'nav.vit' file which contains all navigation links

nav.vit
```
<nav>
    <a href="#">Home</a>
    <a href="#">Download</a>
  </nav>
```

Now let's include the header and nav files in the index

index.vit
```
{{#include header,nav}} //Each file must be seperated with a comma ','
```

## LICENCE

**PHP-VIT** is free and unencumbered TEMPLATE ENGINE released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute it, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, we dedicate this code and all copyright interest
to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
codes under copyright law.

**THE CODES IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL WE BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE CODES OR THE USE OR
OTHER DEALINGS WITH THIS CODE.**


*Thanks. With Love in our hearts...*


