# EzPush Web Notifications

### Installation
1. Copy listed files to the root folder of your website:
  * [manifest.json](https://ezpush.techonlinecorp.com/SDK/manifest.json)
  * [sw.js](https://ezpush.techonlinecorp.com/SDK/sw.js)
2. Add `<link rel="manifest" href="manifest.json">` to the `<head></head>` section.
3. Optionally add other data about your website in *manifest.json*, learn more about [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest).
4. Download *ezpush.json* from Chrome/Firefox settings inside your App and place it to the root folder of your website.
5. Change `<Your Sender ID from https://console.firebase.google.com>` for each platform in *ezpush.json* file to your Sender ID.
6. Include JS-file:
    `<script src="https://ezpush.techonlinecorp.com/SDK/ezpush-client.js" async></script>`

The script will use *sw.js* and *ezpush.json* from the root folder of your website, it also take into consideration base URL from `<base>` element.

> You can rename **ezpush.json** file and put it to any directory that suites you. Path to ezpush.json should be provide in EzPush init method as shown below. 


### EzPush Web API
To call any API method use EzPush.push() syntax:
```javascript
EzPush.push(['methodName', ...options]);
````

#### Init EzPush
The code below can be avoided, then initialization will run with default options.
```javascript
window.EzPush = window.EzPush || [];
EzPush.push(['init', {
    subscribeOnInit: false,     // true by default
    language: ru,               // taken from  from window.navigator.language by default
    onSuccess: callback,        // function
    onError: console.error,     // function
    logEnabled: true,           // false by default
    configUrl: 'ezpush.json'    // optional, 'ezpush.json' by default
}]);
function callback() {
    if (EzPush.isSubscribed) {
        console.log('You are subscribed to push notifications.');
    } else {
        console.log('You are not subscribed to push notifications.');
    }
}
```
All settings here are optional. Function callback() is placed for example and can be avoided. You can use **EzPush.isSubscribed** in callback to get current subscribtion status.

#### Update User Id
```javascript
EzPush.push(['setUserAlias', "User Alias"]);
```
 
#### Update User Location
```javascript
EzPush.push(['updateLocation']);                           // current user location
EzPush.push(['updateLocation', -22.9109878, -43.7285266]); // custom longitude and latitude
 ```
#### Subscribe
```javascript
EzPush.push(['subscribe', {
    language: 'ro', // taken from  from window.navigator.language by default
    onError: function,
    onSuccess: function 
    }]);
```
#### Unsubscribe
```javascript
EzPush.push(['unsubscribe', {
    onError: function,
    onSuccess: function 
    }]);
```

#### Update User Tags
- **value** should always be String
- **type** can be "string" (by default), "number", "boolean", "date"

```javascript
EzPush.push(['updateUserTags', [
    {
        key: "custom_tag",
        value: "custom value" // only String allowed
    },
    {
        key: "string_tag",
        value: "text",
        type: "string"
    },
    {
        key: "number_tag",
        value: "42",
        type: "number"
    },
    {
        key: "boolean_tag",
        value: "true",
        type: "boolean"
    },
    {
        key: "date_tag",
        value: "2016-11-10 15:13:41.000",
        type: "date"
    }
]]);
```
