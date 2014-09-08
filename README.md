Welcome to mi9service 
=====================

#### mi9service is written in C# using ASP.NET Web Api for mi9 coding challenge.

This repository contains 2 projects as below, an example in HMTL of service use and a sample technical document automatically generated from the code documentation.
1. mi9service project 
mi9service is the actual implementation of the service as per specification on []()
The project is hosted on  AppHarbor in the following address and automatically gets updated with any changes to this Git repository.
The project is also automatically being compiled on a Continuous Integration server () and the following badge shows the live build status of the project including the unit test results.
[![Build status](https://ci.appveyor.com/api/projects/status/lwu2aha3rmp44xqm)](https://ci.appveyor.com/project/mehdiromi/mi9service)
[![Test Results](https://ci.appveyor.com/api/projects/status/lwu2aha3rmp44xqm)](https://ci.appveyor.com/project/mehdiromi/mi9service/build/tests)

2. mi9service.Test
mi9service.Test is the unit test project for testing the service. The test result is available in the following address:
[https://ci.appveyor.com/project/mehdiromi/mi9service/build/tests](https://ci.appveyor.com/project/mehdiromi/mi9service/build/tests)


There is also a Node.js service developed for testing the service from another server. The Node.js project is located in a separate repository in the following URL: 
[https://github.com/mehdiromi/mi9client](https://github.com/mehdiromi/mi9client)


This is an example of consuming the exercise web service developed by Mehdi and hosted at [http://awesomeservice.apphb.com](http://awesomeservice.apphb.com).

The client application is written in Node.js on Express, Jade template and uses JQUERY for Ajax calls and  hosted on Heroku at [http://mi9client.heroku.com](http://mi9client.heroku.com).

The service is originally written in C# with ASP.Net Web Api 5.1.0 and the source code is avaialbe on github in the following repo:
[https://github.com/mehdiromi/mi9service](https://github.com/mehdiromi/mi9service)


How does this client app work?

* The initial input data is being read with a GET ajax call from a Node.js api from this service on [http://mi9client.heroku.com/samplerequest](http://mi9client.heroku.com/samplerequest) and updates input DOM element.
* The input data then is POSTed to the service on [http://awesomeservice.apphb.com](http://awesomenode.apphb.com) via ajax and updates the output DOM element.
* If any error occures, the error DOM element gets updates.


### Javascript ajax call :

On page load, a simple function reads the input data and then POST it to the service.

```
$(document).ready(function() {
            ReadDataAndPost();
        });

```


ReadDataAndPost initially calls [http://mi9client.heroku.com/samplerequest](http://mi9client.heroku.com/samplerequest) to GET the input data

```
function ReadDataAndPost() {
    var sampleInput;
    $.ajax({
        url: "samplerequest",
        type: 'GET',
        //data: JSON.stringify(Data),
        //crossDomain: true,
        async: true,
        cache: false,
        dataType: "json",
        //contentType: "application/json; charset=utf-8",
        success: function (data) {
            sampleInput = data;
            $("#input").html(JSON.stringify(sampleInput));
            //Post Data
            CallService(sampleInput);
        },
        error: function (error) {
            $("#input").html(error.responseText);
        }
    });
}
```

When input data ready, then it POSTs to the service at [http://awesomeservice.apphb.com](http://awesomeservice.apphb.com), and displays the returned data:
```
function CallService(sampleInput) {
    $.ajax({
        url: "http://awesomeservice.apphb.com",
        type: 'POST',            
        data: JSON.stringify(sampleInput),
        async: true,
        cache: false,
        dataType: "json",
        contentType: "application/json; charset=utf-8",
        beforeSend: function () {
        },
        success: function (data) {
            $("#output").html(JSON.stringify(data));
        },
        error: function (error) {
            $("#output").html(error.responseText);
        },
        complete: function () {               
        }
    });
}

```


This application is written by Mehdi Romi (mehdi.romi@gmail.com) and uses free resources for development and hosting.

