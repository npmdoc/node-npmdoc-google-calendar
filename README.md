# api documentation for  [google-calendar (v1.3.2)](https://github.com/berryboy/google-calendar)  [![npm package](https://img.shields.io/npm/v/npmdoc-google-calendar.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-google-calendar) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-google-calendar.svg)](https://travis-ci.org/npmdoc/node-npmdoc-google-calendar)
#### Google Calendar API for Node.js

[![NPM](https://nodei.co/npm/google-calendar.png?downloads=true)](https://www.npmjs.com/package/google-calendar)

[![apidoc](https://npmdoc.github.io/node-npmdoc-google-calendar/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-google-calendar_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-google-calendar/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-google-calendar/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-google-calendar/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "bugs": {
        "url": "https://github.com/berryboy/google-calendar/issues"
    },
    "dependencies": {
        "express": "~3.3",
        "needle": "~0.5",
        "passport": "~0.1",
        "passport-google-oauth": "~0.1"
    },
    "description": "Google Calendar API for Node.js",
    "devDependencies": {
        "async": "~0.2.9",
        "mocha": "~1.13.0",
        "should": "~2.0.2"
    },
    "directories": {},
    "dist": {
        "shasum": "a275fc65fc4989551a6a454875e7c07532f72776",
        "tarball": "https://registry.npmjs.org/google-calendar/-/google-calendar-1.3.2.tgz"
    },
    "gitHead": "e3d2f2360909855ae11130d5127fb6c907678ee4",
    "homepage": "https://github.com/berryboy/google-calendar",
    "main": "./GoogleCalendar",
    "maintainers": [
        {
            "name": "wanasit",
            "email": "wanasit@berrysoftstudio.com"
        }
    ],
    "name": "google-calendar",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/berryboy/google-calendar.git"
    },
    "scripts": {},
    "version": "1.3.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module google-calendar](#apidoc.module.google-calendar)
1.  [function <span class="apidocSignatureSpan">google-calendar.</span>GoogleCalendar (access_token)](#apidoc.element.google-calendar.GoogleCalendar)



# <a name="apidoc.module.google-calendar"></a>[module google-calendar](#apidoc.module.google-calendar)

#### <a name="apidoc.element.google-calendar.GoogleCalendar"></a>[function <span class="apidocSignatureSpan">google-calendar.</span>GoogleCalendar (access_token)](#apidoc.element.google-calendar.GoogleCalendar)
- description and source-code
```javascript
function GoogleCalendar(access_token){

  this.request  = function(type, path, params, options, body, callback) {

    var url = 'https://www.googleapis.com/calendar/v3'+path+'?access_token='+access_token;

    params = params || {}
    options = options || {}
    options.json = true;

    type = type.toUpperCase();
    if(body && typeof body !== 'string') body = JSON.stringify(body);


    for(var k in params){
      url += '&'+encodeURIComponent(k)+'='+ encodeURIComponent(params[k]);
    }

    needle.request(type, url, body, options, responseHandler);

    function responseHandler(error, response, body) {
      if(error) return callback(error, body);
      if(body.error) return callback(body.error, null);
      return callback(null, body);
    }
  };

  this.acl      = new Acl(this.request);
  this.calendarList = new CalendarList(this.request);
  this.calendars = new Calendars(this.request);
  this.events   = new Events(this.request);
  this.freebusy = new Freebusy(this.request);
  this.settings = new Settings(this.request);
}
```
- example usage
```shell
...

#### AccessToken & Authentication

This library requires Google API's [Access Token](https://developers.google.com/accounts/docs/OAuth2) with calendars [scope](https
://developers.google.com/google-apps/calendar/auth).

'''javascript
var gcal = require('google-calendar');
var google_calendar = new gcal.GoogleCalendar(accessToken);
'''

To get 'accessToken', use another authentication framework such as [passport](https://github.com/jaredhanson/passport) (recommended
, but not required) for OAuth 2.0 authentication. You can take look at the example code in [example](https://github.com/berryboy
/google-calendar/tree/master/example) folder.

'''javascript
var GoogleStrategy = require('passport-google-oauth').OAuth2Strategy;
var passport = require('passport');
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
