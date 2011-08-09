QUnitTeamCityDriver
===================
QUnitTeamCityDriver allows [TeamCity](http://www.jetbrains.com/teamcity/) to execute [QUnit](http://docs.jquery.com/Qunit) JavaScript unit tests using [PhantomJS](http://www.phantomjs.org/).

PhantomJS is a headless WebKit with JavaScript API which means web pages (and thier JavaScript) can be executed from the command line without the need for an external browser.
QUnitTeamCityDriver provides a PhantomJS script which executes the .htm file hosting your QUnit tests and a driver script that outputs the results using [TeamCity
Service Messages](http://confluence.jetbrains.net/display/TCD65/Build+Script+Interaction+with+TeamCity), such that they appear on the *Tests* tab of a TeamCity build.

Setup (NuGet)
-------------
-TODO-

Setup (Manual)
--------------
 1. Download [PhantomJS](http://code.google.com/p/phantomjs/downloads/list) and copy it out to your build server to a known location, for example: C:\PhantomJS.
 2. Include QUnitTeamCityDriver.js on the .htm page that hosts your QUnit tests.  It should be placed *after* the reference to the QUnit script.  
    This file does nothing if it is not run in the context of PhantomJS so your QUnit tests will continue to run unaffected in the browser.
 3. Add a "Command Line" Build Step to your build in TeamCity  
    **Command executable:** C:\PhamtomJS\phantomjs.exe  
    **Command parameters:** \Scripts\QUnitTeamCityDriver.phantom.js Tests.htm

Notes
-----
 * Tested against phantomjs-1.2.0-win32-static.zip (June 26 2011)