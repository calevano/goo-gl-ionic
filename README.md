# goo-gl-ionic
I wanted to shorten urls for the social network Twitter, but did not want to go to a website and do this manually , you could use an API of " bitly ", "hootsuite" or another, but I wanted to make it simple, that when you click share by Cordova plugin " SocialSharing " and thus be able to shorten my share without drawbacks twitter.

I'm using Wordpress APIs , and well I have to shorten urls when I want to share the news with a social network and looks cleaner too.

Acquiring and using an API key

Requests to the Google URL Shortener API for public data must be accompanied by an identifier, which can be an API key.

To acquire an API key:

* 1.- Go to the Google Developers Console (https://console.developers.google.com).
* 2.- Select a project, or create a new one.
* 3.- In the sidebar on the left, expand APIs & auth. Next, click APIs. In the list of APIs, make sure the status is ON for the Google URL Shortener API.
* 4.- In the sidebar on the left, select Credentials.

place this in the index.html, but you must place before the .js where is the controller.
```html
<script src="https://apis.google.com/js/client.js"></script>
<script src="js/app.js"></script>
<script src="js/controllers.js"></script>
<script src="js/directive.js"></script>
<script src="js/factory.js"></script>
<script src="js/service.js"></script>
```

```html
<button class="button button-flat icon-facebook pull-right c-white f-s-1-5em c-6"
        ng-click="shareNewspaper(newspaper.title.rendered,newspaper.link)"
></button>
```

```javascript
$scope.shareNewspaper = function(notice_,link_){
      var api_key = '[YOU_API_KEY_GOOGLE_SHORTEN_URL]';
      load();
      function load() {
          gapi.client.setApiKey(api_key);
          gapi.client.load('urlshortener', 'v1').then(makeRequest);
      }
      function makeRequest() {
        var request = gapi.client.urlshortener.url.insert({
            'longUrl': link_
        });
        request.then(function(response) {
          if(CONFIG.isANDROID || CONFIG.isIOS){
            var msj = notice_+' Read it here: ';
            var url = response.result.id;
            $cordovaSocialSharing.share(msj, null, null, url);
          }else{
              Funciones.popupAlert("Available for Android and IPhone");
          }
        }, function(reason) {
            console.log('Error: ' + reason.result.error.message);
        });
      }
  };
  ```
 
