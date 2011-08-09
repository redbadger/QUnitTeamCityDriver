QUnit TeamCity Driver
===================
QUnitTeamCityDriver allows [TeamCity](http://www.jetbrains.com/teamcity/) to execute [QUnit](http://docs.jquery.com/Qunit) JavaScript unit tests using [PhantomJS](http://www.phantomjs.org/).

PhantomJS is a headless WebKit with JavaScript API which means web pages (and thier JavaScript) can be executed from the command line without the need for an external browser.
QUnitTeamCityDriver provides a PhantomJS script which executes the .htm file hosting your QUnit tests and a driver script that outputs the results using [TeamCity
Service Messages](http://confluence.jetbrains.net/display/TCD65/Build+Script+Interaction+with+TeamCity), such that they appear on the *Tests* tab of a TeamCity build.

Adding QUnitTeamCityDriver to your project
--------------------------------------------
 1. Add QUnitTeamCityDriver to your project via NuGet which will add `QUnitTeamCityDriver.js` & `QUnitTeamCityDriver.phantom.js` to your `/Scripts` folder:

        PM> Install-Package QUnitTeamCityDriver
 2. If you don't already have one, create a page called `Tests.htm` to host your QUnit tests  
    Follow the instructions here: [http://docs.jquery.com/Qunit#Using_QUnit](http://docs.jquery.com/Qunit#Using_QUnit)
 3. Reference `QUnitTeamCityDriver.js` on `Tests.htm`.  It should be placed *after* the reference to the QUnit script.  
    This file does nothing if it is not run in the context of PhantomJS so your QUnit tests will continue to run unaffected in the browser.

        <head>
            <link rel="stylesheet" href="http://code.jquery.com/qunit/git/qunit.css" type="text/css" media="screen" />
            <script type="text/javascript" src="http://code.jquery.com/qunit/git/qunit.js"></script>
            <script type="text/javascript" src="Scripts/QUnitTeamCityDriver.js"></script>
        </head>

Configuring your TeamCity Build
-------------------------------
As both .js files are part of your solution, they should both arrive on  your build server when the latest sources are fetched.

 1. Download [PhantomJS](http://code.google.com/p/phantomjs/downloads/list) (Static) and copy it out to your build server, to a known location, for example: `C:\PhantomJS.`
 2. Add a "Command Line" Build Step to your build in TeamCity which executes Tests.htm via PhantomJS  
    **Command executable:** `C:\PhamtomJS\phantomjs.exe`  
    **Command parameters:** `\Scripts\QUnitTeamCityDriver.phantom.js Tests.htm`
 3. When run in the context of PhantomJS QUnitTeamCityDriver.js subscribes the QUnit's callback functions and outputs the results to TeamCity.

Notes
-----
 * Tested against phantomjs-1.2.0-win32-static.zip (June 26 2011)