# PWAs with Angular: Case Study

## Prerequisites

You need a test web server, like ``http-server``:

```
npm i -g http-server
```

You also need a browser supporting service worker as well as background sync (e. g. Chrome or Firefox).

## Build and run

Service Worker are only activated for production builds.

```
npm install
npm run build
cd dist
http-server -o
```
# Remarks

The build is using ng build --prod and a custom webpack build that bundles the ngsw library together with custom service worker code for background synchronization. 

To communicate with the service worker for background sync, the apps writes into an indexeddb collection abstracted by Dexie.js. This collection acts as an "outbox" like in Email Clients.

In an real world scenario, it would also be preferable to have a way to look into this out box and to trigger sending everything by hand.

# Steps to try it out

Service Worker only work in in production builds!

Try to close the web server after loading and to disconnect from the internet. Refresh should work anyway. Change some ratings and reconnect. See that the changes are synced.

To send a push notification, switch to the console and copy the subscription object. Paste it into the ``send-push.js`` and run it using ``node send-push.js``.

To demonstrate the update machanismn, modify the app a bit and rebuild it. When you reload it, you'll see a snack bar telling you that an update is available. 

## Further notes

- Beginning with Angular + CLI 6, you can easily generate the web app manifest + an service worker setup with ``ng add @angular/pwa``.

## Known Issues

- For the sake of simplicity, the hotel records are cached as http requests using ngsw. It would be better to cache it in an indexeddb esp. the parts that can be modified by the application. 

