## My First Progressive Web App
#### Created this app with help from Google Codelab
**Link to codelab:** 
https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/

#### Notes:
- I love to hear other perspectives and get feedback :)

  If you also tried this Google Codelab, or followed this workshop, please let me know your thoughts and suggestions. If you notice anything obsolete or wrong, I'll be really grateful if you would point it out to me, just send me a short quick email :D

- I like to try new things :)

  If you have any idea for a PWA and would like to collaborate / require guidance and assistance please send an email to me (My github profile has the details)

- You can create your first PWA by carefully following instructions in this README (or following the Codelab linked above) - Simple ! :)

  The pre requisites mentioned are recommended but not necessary for this demo app.

- This is not merely a copy paste of the Codelab :)

  I have executed each step and studied them carefully, adding in my twists, suggestions and recommendations where helpful

- Excuse me for imperfections.

  I've created this for learning and teaching others. It is not meant to be a professional / production app. The purpose is to learn and try the essentials of PWA.

- Tip to those who embark on new learning / coding journeys
  
  Never give up, never, ever, ever! (No matter how many obstacles you face, keep going!)
  Tough times never last, but tough people do >:)

- All credits to Google and all people involved in producing and serving this Codelab :)



#### Prerequisites
1. A recent chrome browser
2. Knowledge of HTML, CSS, JavaScript, and Chrome DevTools

#### Workshop aims:
1. Create and add a web app *manifest*.
2. Provide a simple offline experience.
3. Provide a full offline experience.
4. Make your app installable. 

#### Workshop

Link to the codebase (Github Repository):
https://github.com/googlecodelabs/your-first-pwapp.git

##### Get a key for Dark Sky API
    This is the source of the weather data (Dark Sky)

- To test your API Key is working fine and, you are able to fetch data using this key
Replace DARKSKY_API_KEY with the API key you obtain and visit the url
URL: https://api.darksky.net/forecast/DARKSKY_API_KEY/40.7720232,-73.9732319

##### Get the code from Github repository
- Either set up local environment (**Recommended, if** you want to play with different settings and platforms)
- Use glitch (app collaboration platform on the web) for quick environment setup and preview within the browser itself.

**Local environment setup is preferred, so steps for this are below**
- Download the source code from (Link is available in codelab also):
https://github.com/googlecodelabs/your-first-pwapp/archive/master.zip
- Navigate to the folder of the project
- Run npm install to install the dependencies.
- Edit *server.js* and enter your DarkSky API key in the required line of code
- Run **node server.js** to start the server on Port 8000
- Open Google chrome and visit the URL: http://localhost:8000/
- Play around with the web app

**Things to try out**:
- Add a new city
- Delete a city
- Refresh the page (refresh button provided)
- See how it works on the desktop browser full window vs resize the browser window to minimum width and suitable height (mimic a mobile app screen)
- What happens when you go offline
- Open Chrome DevTools (right click on web page and click inspect), go to the *network* tab and see how it shows up on reloading, and adding / deleting cities
change the throttle to *Slow 3G* and do the above, see how it behaves
- Add a delay to the forecast server by changing the value of <FORECAST_DELAY> in *server.js*

**Alternative - If using glitch (can try but not recommended)**
- Goto https://glitch.com, create account Click on New Project and select
*Clone from Git Repo*. Enter the Github URL (link to codebase) here
- Once the project has loaded, go to the **.env** file and update it with the DarkSky API key
- Click Show Live to see the PWA in action

##### Audit with Lighthouse
Lighthouse is an easy to use tool to help improve the quality of your sites and pages.
It has Audits for 
- Performance
- Accessibility
- Progressive Web Apps
- SEO
- etc
Each Audit has a reference doc explaining why the audit is important as well as how to fix it.

View the audit reports and focus on the audit for PWA
We will fix the issues highlighted by the PWA audit report

3. Create a web app manifest
- This will take care of the following points highlighted by Audit report
    - web app manifest does not meet the installability requirements
    - is not configured for a custom spash screen
    - does not set an address-bar theme colour

- The web app manifest is a JSON file that gives the developer control on how the app appears to the user. This gives the web app additional features like:
    - Tell the browser you want the app to open in a standalone window (**display**)
    - Define what page is opened when the app is first launched (**start_url**)
    - Define how app looks like in the dock or app launcher (**short_name**, **icons**)
    - Create a spash screen (**name**, **icons**, **colours**)
    - Tell the browser to open window in landscape or potrait mode (**orientation**)

- create a file manifest.json inside the public directory of the project
Copy paste the below code.
```
{
  "name": "Weather",
  "short_name": "Weather",
  "icons": [{
    "src": "/images/icons/icon-128x128.png",
      "sizes": "128x128",
      "type": "image/png"
    }, {
      "src": "/images/icons/icon-144x144.png",
      "sizes": "144x144",
      "type": "image/png"
    }, {
      "src": "/images/icons/icon-152x152.png",
      "sizes": "152x152",
      "type": "image/png"
    }, {
      "src": "/images/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    }, {
      "src": "/images/icons/icon-256x256.png",
      "sizes": "256x256",
      "type": "image/png"
    }, {
      "src": "/images/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }],
  "start_url": "/index.html",
  "display": "standalone",
  "background_color": "#3E4EB8",
  "theme_color": "#2F3BA2"
}
```
- Note: The manifest supports an array of icons for different screen sizes

- Note: To be installable, Chrome requires that you provide at least a 192x192px icon and a 512x512px icon. But you can also provide other sizes. Chrome uses the icon closest to 48dp, for example, 96px on a 2x device or 144px for a 3x device.

4. Link the created web app manifest
- Tell the browser about the manifest file by adding a link tag in each page of the app
Add the following line to the <*head*> element in your **index.html** file

```
<!-- Add link: rel manifest-->
<link rel="manifest" href="/manifest.json">
```

Tip:
Chrome DevTools provides a quick, easy way to check your manifest.json file. Open up the Manifest pane on the Application panel. If you've added the manifest information correctly, you'll be able to see it parsed and displayed in a human-friendly format on this pane.

5. Add meta tags and touch icon for iOS as Safari does not yet support manifest.

```
<!-- Add iOS meta tags and icons -->
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="apple-mobile-web-app-title" content="Weather PWA">
<link rel="apple-touch-icon" href="/images/icons/icon-152x152.png">
```

6. Set the meta description

- The Audit report (SEO section) pointed out that: *Document does not have a meta description*

- Descriptions can be displayed in Google's search results. High quality unique descriptions can make your results more relevant to search users and can increase your search traffic. 

- Add the following meta tag to the head of your document
```
<!-- Add meta description here -->
<meta name="description" content="A sample weather app">
```

7. Set the address bar theme colour
- Audit report pointed out that *Does not set an address bar theme colour*. 
- For an immersive user experience it is recommended to set theme of your address bar to match the colours of your brand

- To set the theme colour for  mobile, Add the following meta tag to the head of your document
```
<!-- Add meta theme colour-->
<meta name="theme-colour" content="#2F3BA2" />
```

Now that all these fixes (for various issues reported in the Audit), verify that these are indeed no longer issues by running the Audit again:
Rerun the web app, reload the browser page and rerun the Audit. Confirm that the issues pointed out are no longer an issue.
The following will be the status (most likely)
```
SEO Audit
✅ PASSED: Document has a meta description.

Progressive Web App Audit
❗FAILED: Current page does not respond with a 200 when offline.
❗FAILED: start_url does not respond with a 200 when offline.
❗FAILED: Does not register a service worker that controls page and start_url.
✅ PASSED: Web app manifest meets the installability requirements.
✅ PASSED: Configured for a custom splash screen.
✅ PASSED: Sets an address-bar theme color.
```

8. Provide a basic offline experience with a service worker
- Must not show that app is offline, rather some basic behaviour which may range from
    - A simple (custom) offline page
    - read only experience with previously cached data
    - fully functional offline experience that syncs when the network connection is restored.

- For this we will create a service worker
- **Warning**: Service worker functionality is only available on pages that are accessed via HTTPS (http://localhost and equivalents will also work to facilitate testing).

Add an offline page to the app
If the user tries to load the app while offline, it will show a custom page instead of the browser default offline page (Chrome dinosaur)

The following audits will be passed by doing this
- current page does not respond with a 200 when offline
- **start_url** does not respond with a 200 when offline
- Does not register a service worker that controls page and **start_url**

    Note: In the next section, we'll replace our custom offline page with a full offline experience. This will improve the offline experience, but more importantly, it'll significantly improve our performance, because most of our assets (HTML, CSS and JavaScript) will be stored and served locally, eliminating the network as a potential bottleneck.

    Note:
    Features provided via service workers (considered a progressive enhancement) should be added only if they are supported by the browser. Example: With service workers you can cache the app shell and data so that it is available even when the network isn't. 
    When service workers are not supported, the offline code is not called, and the user gets a basic experience.
    Using feature detection to provide progressive enhancement 

- Register the service worker by adding the following to public/index.html
```
if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
        navigator.serviceWorker.register('service-worker.js').then((reg) => {
            console.log('Service worker registered.', reg);
        });
    });
}
```

This code checks to see if the service worker API is available. If it is, the service worker at **/service-worker.js** is registered once the page is loaded.

The **scope** of service worker controls which files the service worker controls, i.e. from which path it will intercept requests. The default **scope** is the location of the service worker file and extends to all directories below.
NOTE: The service worker is placed in the root directory (so it will be able to control requests from all web pages in this domain)

- Precache offline page 
Tell the service worker what to cache (an offline page)
Create a simple offline page **public/offline.html**
This page will be displayed when the device is offline.

In *public/service-worker.js* add the path to offline page (*/offline.html*) in the **FILES_TO_CACHE** array. Note both service-worker.js and offline.html are inside the *public* directory

```
const FILES_TO_CACHE = [
    '/offline.html',
];
```

Update the **install** event to tell service worker to pre cache the offline page.
```
self.addEventListener('install', (evt) => {
  console.log('[ServiceWorker] Install');
  // CODELAB: Precache static resources here.
  evt.waitUntil(
    caches.open(CACHE_NAME).then((cache) => {
      console.log('[ServiceWorker] Pre-caching offline page');
      return cache.addAll(FILES_TO_CACHE);
    })
  );
  self.skipWaiting();
});
```
Notes:
The install event opens the cache with **cache.open()** and provides a cache name
Providing a name helps version files and separate data from cached files so that we can update one without affecting other.

Once cache is open, cache.addAll() is called, which takes a list of URLs, fetches them from the server and adds the response to the cache.
If any individual request fails during cache.addAll() it will reject caching anything.
Therefore if the install step succeeds, the cache will be consistent, otherwise if it fails for any reason, it will automatically try again the next time service worker starts up.

- Open DevTools and Go to Application Tab and click on Service Workers section (left)
There was no service worker before, but now there is. Reload the page and the service worker should be shown
The status shows a number, which is unique to every run. Anytime service worker updated the number in status will change. 

9. Clean up old offline pages. 
- Use the **activate** event to clean up any old data in our cache. This ensures that the service worker updates the cache whenever any of the app shell files change.
In order for this to work, the CACHE_NAME variable (at top of service-worker.js) needs to be incremented 

- Add the following code to the **activate** event in *service-worker.js* file
```
evt.waitUntil(
    caches.keys().then((keyList) => {
        return Promise.all(keyList.map((key) => {
            if (key !== CACHE_NAME) {
                console.log('[ServiceWorker] Removing old cache', key);
                return caches.delete(key);
            }
        }));
    })
);

```
    Note:
    The updated service worker takes control immediately because our install event finishes with self.skipWaiting(), and the activate event finishes with self.clients.claim(). Without those, the old service worker would continue to control the page as long as there is a tab open to the page.

10. Handle failed network events

Now we will handle fetch events, and use a *network, falling back to cache* strategy from the offline cookbook (references in last section)

![network falling back to cache](offline_network_fallback_cache.png)

This strategy entails:
The service worker will first try to fetch the resource from the network, if that fails, it will return the offline page from cache.

- Add the following to service-worker.js
```
if (evt.request.mode !== 'navigate') {
    // Not a page navigation, bail out.
    return;
}
evt.respondWith(
    fetch(evt.request).catch(() => {
        return caches.open(CACHE_NAME).then((cache) => {
            return cache.match('offline.html');
        });
    })
);
```
Explanation of above code:
The **fetch** handler only needs to handle page navigations, so other requests are dumped out of the handler and dealt with normally by the browser.
But if the request.**mode** is 'navigate', use **fetch** to try to get the item from the network.
If it fails, the **catch** handler opens the cache with **caches.open(CACHE_NAME)** and uses **cache.match('offline.html')** to get the precached offline page. The result is then passed back to the browser using **evt.respondWith()**

NOTE: wrapping the **fetch** call in **evt.respondWith()** prevents the browser from applying the default fetch handling. It tells the browser that I myself want to handle the response. If you dont call **evt.respondWith()** inside a fetch handler, you will just get the default network behaviour!

- Reload the app and Open the Service Workers in the Application tab of Chrome DevTools
Go to the cache storage pane in the Application tab.
Right click on the pane and say refresh caches. The cache file shows up. Open it and you can preview the cached data.

11. Test out the offline mode
Go back to Service Workers page in DevTools, then click on Offline checkbox.
This causes a warning symbol to show next to Network tab which means there is no network (offline)
Now refresh the browser page, and the custom offline page we created shows up instead of the default chrome dinosaur page!.

12. Audit the app again, Run lightout Audits to see the results:
Expected results:
```
SEO Audit
✅ PASSED: Document has a meta description.

Progressive Web App Audit
✅ PASSED: Current page responds with a 200 when offline.
✅ PASSED: start_url responds with a 200 when offline.
✅ PASSED: Registers a service worker that controls page and start_url.
✅ PASSED: Web app manifest meets the installability requirements.
✅ PASSED: Configured for a custom splash screen.
✅ PASSED: Sets an address-bar theme color.
```

13. Provide a full Offline experience:
Key Point: Designing for offline-first can drastically improve the performance of your web app by reducing the number of network requests made by your app, instead resources can be precached and served directly from the local cache. Even with the fastest network connection, serving from the local cache will be faster!

- Pre-requisite: Understand the next section

**Service worker lifecycle:**

![Service Worker lifecycle](serviceworker_lifecycle.png)

1. event: **install**
The first event a service worker gets is install. It's triggered as soon as the service worker executes, and is called only once per service worker.
If you alter your service worker script, the browser considers it a different service worker, and it'll get its own install event.

Note: Typically the **install** event is used to cache everything that is required for the app to run.

2. event: **activate**
The service worker will receive an **activate** event everytime it starts up. The main purpose of this event is to configure the service worker's behaviour, clean up any resources left behind from previous runs (eg. old caches) and get the service worker ready to handle network requests (for example the fetch event described below)

3. event: **fetch**
This event allows the service worker to intercept any network requests and handle requests. It can go to the network to get the resource, or pull it from it's own cache, generate a custom response or other options (Check out the offline cookbook for various strategies, reference link below)

- **Updating a Service Worker**:
The browser checks to see if there is a new version of your service worker on each page load.
If it finds a new version, that is downloaded and installed in the background, BUT it is not activated.
It sits in the **waiting** state, **until** there are **no longer any pages open that use the old service worker**.
As all pages using the old service worker are closed, the new service worker gets activated and takes control

- **Choosing the right caching strategy**
This depends on the type of resource you are trying to cache and how you might need it later.
Note: For this Project we will split the resources to cache in *2 categories*
1. Resources we want to pre-cache
2. Data that we will cache at runtime

- Caching Static resources
Pre caching static resources is similar to what happens when a desktop or mobile app is installed. The resources required to run the app are installed or cached on the device so that it can run later, whether there is network connection or not.

For our app, we will pre cache all the static resources when the service worker is installed (So that everything required to run the app are stored on the users device)

To ensure our app loads *lightning fast*, we will use the **cache-first** strategy
(refer to caching strategies in offline cookbook)
Instead of going to the network to get the resources, they are pulled from the local cache. Only if it is not available in cache we will try to get it from the network.

**Benefit** of this strategy:
    Pulling from the local cache ensures there is no network variability. No matter what kind of network the user is on, the key resources we need to run the app are almost immediately available

**Caution:** In this sample, static resources are served using a cache-first strategy, which results in a copy of any cached content being returned without consulting the network. While a cache-first strategy is easy to implement, it can cause challenges in the future.

- The **stale while revalidate** strategy is ideal for certain types of data and works well for our app. *It gets data on screen as quickly as possible, then updates that once the network has returned latest data*. Stale while revalidate means we need to kick off two asynchronous requests:
1. one to the cache
2. one to the network
![stale while revalidate strategy](offline_stale_while_revalidate.png)

Under normal circumstances, the cached data will be returned almost immediately, providing the app with recent (but not latest) data it can use. Then when the network request returns, the app will be updated using latest data from the network

For our app this *stale while revalidate* strategy **provides a better experience than** the *network falling back to cache* strategy, because the user does not have to wait until network request times out to see something on screen.
They may initially see older data, but as soon as network request returns, the app will be updated with the latest data.

- **Update App Logic**

Since the app needs to do 2 asynchronous requests: one to cache and one to network,
the app uses **caches** object available in **window** object to access the cache and retrieve the data. 
Note: The **caches** object *may not be available in all the browsers*, and if its not, the *network request should still work* 
So this is an excellent example of Progressive content

- Update the **getForecastFromCache()** to check if the **caches** object is available in the global **window** object, and if it is, request the data from cache

- Add the following code to the *public/scripts/app.js* file inside the function:
getForecastFromCache()
```
if (!('caches' in window)) {
    // no caches object found. Will not request cache.
    return null;
}
const url = `${window.location.origin}/forecast/${coords}`;
return caches.match(url).then((response) => {
    if (response) {
        return response.json();
    }
    return null;
}).catch((err) => {
    console.error('Error getting data from cache', err);
    return null;
});
```

- Modify updateData() so that is makes 2 calls, to the following:
1. getForecastFromNetwork()
2. getForecastFromCache()

```
getForecastFromCache(location.geo).then((forecast) => {
    renderForecast(card, forecast);
});
```

Therefore, our app makes 2 asynchronous requests for data:
one from the cache, and one via a fetch. If data found in cache it will be returned and rendered immediately, and when the fetch responds, the card will be updated with latest data directly from the weather API.
Note: Both cache request and fetch request end with a call to update the forecast card.
How does the app know whether it's displaying the latest data? this is handled in the following code from renderForecast()
```
// If the data on the element is newer, skip the update.
if (lastUpdated >= data.currently.time) {
    return;
}
```
Everytime a card is updated, the app stores the timestamp of the data on a hidden attribute on the card. The app just bails out if the timestamp already set on the card is newer than that of the data that was passed to the function.

14. Pre cache our app resources.

- Add a constant **DATA_CACHE_NAME** in the service worker so that we can separate our applications data from the app shell. When the app shell is updated, and older caches removed, our application data will remain unaffected.
Note: If your data format changes in future you need a way to handle that and ensure the app shell and content stay in sync.

- Update the **CACHE_NAME** to next version as we will change our static resources as well
```
Note: In order for our app to work offline, we need to precache all the resources it needs to run, this will also benefit the app performance.
Instead of having to get all of the resources from the network, the app will be able to get them from local cache, eliminating issues or delays due to any network variability.
```

**What is an app shell?** - By this time you need to know this
(More on the link given in references below)
```
An application shell (or app shell) architecture is one way to build a Progressive Web App that reliably and instantly loads on your users' screens, similar to what you see in native applications.

The app "shell" is the minimal HTML, CSS and JavaScript required to power the user interface and when cached offline can ensure instant, reliably good performance to users on repeat visits. This means the application shell is not loaded from the network every time the user visits. Only the necessary content is needed from the network.
```

- Update the **FILES_TO_CACHE** array with the list of files
Particularly:
    - '/' (the app root directory, so that the app project structure is also cached, and then you can point out to other files relative to the app root directory)
    - index.html
    - scripts/* (contains app.js and install.js)
    - styles/* (contains all css and other style / theme related files)
    - images/* (contains all the static images for app.)

```
const FILES_TO_CACHE = [
    '/',
    '/index.html',
    '/scripts/app.js',
    '/scripts/install.js',
    '/scripts/luxon-1.11.4.js',
    '/styles/inline.css',
    '/images/add.svg',
    '/images/clear-day.svg',
    '/images/clear-night.svg',
    '/images/cloudy.svg',
    '/images/fog.svg',
    '/images/hail.svg',
    '/images/install.svg',
    '/images/partly-cloudy-day.svg',
    '/images/partly-cloudy-night.svg',
    '/images/rain.svg',
    '/images/refresh.svg',
    '/images/sleet.svg',
    '/images/snow.svg',
    '/images/thunderstorm.svg',
    '/images/tornado.svg',
    '/images/wind.svg',

];
```
Note: '/offline.html' added previously to FILES_TO_CACHE has been removed. Why?

Since we are manually generating the list of files to cache, everytime we update a file, we must update the **CACHE_NAME**.

**offline.html** has been removed from the list of **FILES_TO_CACHE** because our app now has all the necessary resources to work offline, and we will never need to show the offline page again!

**Caution:** In this sample, we hand-rolled our own service worker. Each time we update any of the static resources, we need to re-roll the service worker and update the cache, otherwise the old content will be served. In addition, when one file changes, the entire cache is invalidated and needs to be re-downloaded. That means fixing a simple single character spelling mistake will invalidate the cache and require everything to be downloaded again—not exactly efficient.
**Workbox** handles this gracefully, by integrating it into your build process, only changed files will be updated, saving bandwidth for users and easier maintenance for you!

- Update **activate** event handler
To ensure our activate event doesnt accidentally delete our data, in the activate event handler of service-worker.js, replace the the below statement with with the statement given below that!

```
if (key !== CACHE_NAME) {}
```
```
if (key !== CACHE_NAME && key !== DATA_CACHE_NAME) {}
```

- Update the **fetch** event handler

Need to modify the service worker to intercept requests to the weather API and store their responses in the cache so we can easily access them later. 

In the *stale while revalidate* strategy, we expect the response from network request to be the 'source of truth', If it cant get response from network request, it  is okay to fail as we already have fetched the latest data from cache.

Update the fetch event handler to handle requests to the data API seperately from other requests...

```
// CODELAB: Add fetch event handler here.
if (evt.request.url.includes('/forecast/')) {
  console.log('[Service Worker] Fetch (data)', evt.request.url);
  evt.respondWith(
      caches.open(DATA_CACHE_NAME).then((cache) => {
        return fetch(evt.request)
            .then((response) => {
              // If the response was good, clone it and store it in the cache.
              if (response.status === 200) {
                cache.put(evt.request.url, response.clone());
              }
              return response;
            }).catch((err) => {
              // Network request failed, try to get it from the cache.
              return cache.match(evt.request);
            });
      }));
  return;
}
evt.respondWith(
    caches.open(CACHE_NAME).then((cache) => {
      return cache.match(evt.request)
          .then((response) => {
            return response || fetch(evt.request);
          });
    })
);
```
Explanation of the above code (changes made to fetch handler in *service-worker.js*)
```
The code **intercepts the request and checks if it is for a weather forecast**. If it is,use fetch to **make the request**. Once the **response is returned, open the cache, clone the response, store it in the cache, and return the response to the original requestor**.

We need to remove the evt.request.mode !== 'navigate' check because we **want our service worker to handle all requests** (including images, scripts, CSS files, etc), not just navigations. If we left that check in, only the HTML would be served from the service worker cache, everything else would be requested from the network.
```

**Try the app now:**
Refresh the page to ensure that you've got the latest service worker installed, then save a couple of cities and press the refresh button on the app to get fresh weather data.

Then go to the Cache Storage pane on the Application panel of DevTools. Expand the section and you should see the name of your static cache and data cache listed on the left-hand side. Opening the data cache should show the data stored for each city.

Then, open DevTools and switch to the Service Workers pane, and check the Offline checkbox, then try reloading the page, and then go offline and reload the page.

If you're on a fast network and want to see how weather forecast data is updated on a slow connection, set the FORECAST_DELAY property in server.js to 5000. All requests to the forecast API will be delayed by 5000ms.

![Cached App Data](cached_app_data.png)

**Verify changes with Lighthouse**
Run the Audit again, the results will be as follows:

SEO Audit
✅ PASSED: Document has a meta description.

Progressive Web App Audit
✅ PASSED: Current page responds with a 200 when offline.
✅ PASSED: start_url responds with a 200 when offline.
✅ PASSED: Registers a service worker that controls page and start_url.
✅ PASSED: Web app manifest meets the installability requirements.
✅ PASSED: Configured for a custom splash screen.
✅ PASSED: Sets an address-bar theme color.

##### Add an Install Experience
In Chrome, a Progressive Web App can either be installed through the three-dot context menu, or you can provide a button or other UI component to the user that will prompt them to install your app.

Useful Tip: Since the install experience in Chrome's three-dot context menu is somewhat buried, we recommend that you **provide some indication within your app to notify the user your app can be installed, and an install button to complete the install process**.

In order for a user to be able to install your Progressive Web App, it needs to meet certain criteria. The easiest way to check is to use Lighthouse and make sure it meets the installable criteria. Such as the following

- Uses HTTPS.
- Registers a service worker that controls page and start_url.
- Web app manifest meets the installability requirements. 

  **NOTE: By now your PWA should already meet these criteria (if all steps followed).**

Todo: 
Key Point: For this section, enable the Bypass for network checkbox in the Service Workers pane of the Application panel in DevTools. When checked, requests bypass the service worker and are sent directly to the network. This simplifies our development process since we don't have to update our service worker while working through this section.

Add *install.js* to *index.html*
```
<!-- CODELAB: Add the install script here -->
<script src="/scripts/install.js"></script>
```

- Listen for **beforeinstallprompt** event

If the add to home screen criteria are met, Chrome will fire a beforeinstallprompt event,that you can use to indicate your app can be 'installed', and then prompt the user to install it. Add the code below to listen for the beforeinstallprompt event:

In public/scripts/install.js
```
// CODELAB: Add event listener for beforeinstallprompt event
window.addEventListener('beforeinstallprompt', saveBeforeInstallPromptEvent);
```

- Save event and show Install button

In our saveBeforeInstallPromptEvent function, we'll save a reference to the beforeinstallprompt event so that we can call prompt() on it later, and update our UI to show the install button.

- Show the prompt, hide the button

When the user clicks the install button, we need to call .prompt() on the saved beforeinstallprompt event. We also need to hide the install button, because .prompt() can only be called once on each saved event.

In public/scripts/install.js inside function installPWA(evt) add the following.
```
// CODELAB: Add code show install prompt & hide the install button.
deferredInstallPrompt.prompt();

// Hide the install Button as it had been called (it cant be called twice)
evt.srcElement.setAttribute('hidden', true);
// installButton.setAttribute('hidden'); // this could be another alternative?
```

Explanation: Calling **.prompt()** will show a modal dialog to the user, asking them to add your app to their home screen.

- Log the results

You can check to see how the user responded to the install dialog by listening for the *Promise* returned by the **userChoice** property of the saved beforeinstallprompt Event. The Promise returns an object with an **outcome** property
after the user has responded to the prompt shown.

In public/scripts/install.js inside installPWA() function
```
  // CODELAB: Log user response to prompt.
  deferredInstallPrompt.userChoice.then((choice) => {
    if (choice.outcome === 'accepted') {
      console.log('User accepted A2HS prompt', choice);
    } else {
      console.log('User dismissed A2HS prompt', choice);
    }
    deferredInstallPrompt = null;
  });
```

- Log all install events

In addition to installing your PWA through the install prompt, users can also install it via other ways like browser function (eg 3 dot menu in Chrome)
To track these events listen for the appinstalled event

```
// CODELAB: Add event listener for appinstalled event
window.addEventListener('appinstalled', logAppInstalled);
```

Update the logAppInstalled function. Here use a console.log() for simplicity. In a production app you may be required to use your analytics software.

- Update the logAppInstalled(evt)

```
function logAppInstalled(evt) {
  // CODELAB: Add code to log the event
  console.log('Weather App was installed.', evt);
}
```

##### Update the Service Worker
- Update the CACHE_NAME in your service-worker.js since you made changes to files already cached.

- Try the app now:

Let's see how our install step went. To be safe, use the **Clear site data** button in the Application panel (**Clear Storage** section) of DevTools to clear everything away and make sure we're starting fresh. If you previously installed the app, be sure to uninstall it, otherwise the install icon won't show up again.

- Bonus: Detecting if your app is launched from the home screen

The **display-mode** media query makes it possible to apply styles depending on how the app was launched, or determine how it was launched with Javascript

```
@media all and (display-mode: standalone) {
  body {
    background-color: yellow;
  }
}
```

It's also possible to detect if the display-mode is standalone from Javascript

```
if (window.matchMedia('(display-mode: standalone)').matches) {
  console.log('display-mode is standalone');
}
```

- For Safari: To determine if app was launched in standalone mode from Safari, you can use Javascript to check:
```
if (window.navigator.standalone === true) {
  console.log('display-mode is standalone');
}
```

- Updating App Icon and Name:
On Android when WebAPK is launched, Chrome will check the currently installed manifest against the live manifest. If an update is required, it will be queued and updated (once device being charged and connected to Wifi)

- Test the A2HS experience

**Helpful:** You can manually trigger the beforeinstallprompt event using Chrome DevTools.
This makes if possible to see the user experience, understand how the flow works, or debug the flow. If PWA criteria are not met, Chrome will throw an exception in the console and the event will not be fired.

**Caution:** Chrome has a slightly different install flow for desktop and mobile. Although the instructions are similar, testing on mobile requires remote debugging; without it, Chrome will use the desktop install flow.

- Tip:
The easiest way to test if the beforeinstallprompt event will be fired, is to use Lighthouse to audit your app, and check the results of the **User Can Be Prompted To Install The Web App** test.

- Uninstalling your PWA:

Remember, the beforeinstallevent doesn't fire if the app is already installed, so during development you'll probably want to install and uninstall your app several times to make sure everything is working as expected.

Android
On Android, PWAs are uninstalled in the same way other installed apps are uninstalled.

Open the app drawer.
Scroll down to find the Weather icon.
Drag the app icon to the top of the screen.
Choose Uninstall.
ChromeOS

On ChromeOS, PWAs are easily uninstalled from the launcher search box.
Open the launcher.
Type " Weather " into the search box, your Weather PWA should appear in the results.
Right click (alt-click) on the Weather PWA.
Click Remove from Chrome...
macOS and Windows

On Mac and Windows, PWAs may be uninstalled through Chrome.
In a new browser tab, open chrome://apps.
Right click (alt-click) on the Weather PWA.
Click Remove from Chrome...
You can also open the installed PWA, click the the dot menu in the upper right corner, and choose Uninstall Weather PWA…


##### More reading

- More on Chrome DevTools
https://developers.google.com/web/tools/chrome-devtools/?utm_source=dcc&utm_medium=redirect&utm_campaign=2018Q2

- Responds with a 200 when Offline [Chrome DevTools][Audit][PWA]
https://developers.google.com/web/tools/lighthouse/audits/http-200-when-offline?utm_source=lighthouse&utm_medium=devtools

- How to do an Accessibility Review 
Tools and tests in Chrome Dev Tools for Accessibility audit may not be enough, 
as accessibility is a subjective and sensitive quality. Manual usability tests, UX review etc are required.
https://developers.google.com/web/fundamentals/accessibility/how-to-review?utm_source=lighthouse&utm_medium=devtools

- More on web app Manifest 
    - https://developer.mozilla.org/en-US/docs/Web/Manifest#Members
    - https://developers.google.com/web/fundamentals/web-app-manifest/


-  Service workers: An Introduction
https://developers.google.com/web/fundamentals/primers/service-workers/

- Debugging Service Workers
https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/

- Service worker registration
https://developers.google.com/web/fundamentals/primers/service-workers/registration

- The offline cookbook
https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/
(Section: *Network falling back to cache*)
https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/#network-falling-back-to-cache

- Service Worker Lifecycle 
https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle

- Updating the Service Worker:
https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#updates

- Stale while revalidate strategy (offline cookbook section)
https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/#stale-while-revalidate

- What is an **app shell**?
https://developers.google.com/web/fundamentals/architecture/app-shell

- Installability criteria for PWAs:
https://developers.google.com/web/fundamentals/app-install-banners/#criteria

- Detecting if your app is launched from Home screen / **display-mode** media query
https://developers.google.com/web/fundamentals/app-install-banners/#detect-mode

- Get started with Remote Debugging on Android using Chrome
https://developers.google.com/web/tools/chrome-devtools/remote-debugging/

- Guide to remote debugging on Android using Chrome (For viewing your PWA in mobile)
https://medium.com/@michaelgannon_89769/beginners-guide-to-remote-debugging-android-devices-using-chrome-ded1d3aca11a


Further reading

- High-performance service worker loading
https://developers.google.com/web/fundamentals/primers/service-workers/high-performance-loading

- Service Worker Caching Strategies Based on Request Types
https://medium.com/dev-channel/service-worker-caching-strategies-based-on-request-types-57411dd7652c
