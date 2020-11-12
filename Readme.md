## NodeJS PWA Boilerplate

This boilerplate might be of ones interest who is not in the mood to dive deeper into Angular, Vue, React, Ember a.s.o., and just want to get started with ECMAScript, Vanilla JavaScript or jQuery as he or she is used to it.

With this boilerplate you can create a **Progressive Web App** (PWA) that is based upon NodeJS and the Express framework. On the client side you have to deal with jQuery and MaterializeCSS, which of course you can change. CSS pre-processing is accomplished using a SASS compiler. And responsible for the app-alike offline experience is a tool called Workbox.

### Requirements

Download the resources from the repository into an empty folder:
```
$ mkdir your_project_folder
$ cd your_project_folder
$ git init
$ git pull https://github.com/dahas/node_pwa_boilerplate.git
```

Install SASS support globally:

```
$ npm i -g node-sass
```

Install the dependent libraries:
```
$ npm i
```

### Usage

When you start creating your own project you probably want to monitor changes on the client- and on the server-side scripts simultaniously. Therefore split your console into two and run the following commands each in one instance:

```
$ npm run dev // Console 1
$ nodemon server // Console 2
```

Before you deploy your stuff run the build command. It compresses your JavaScript code and creates/updates the ServiceWorker. With deploy you push everything to your Git repository and to your hosting provider afterwards:

```
$ npm run build
$ npm run deploy // Deploys to Heroku (Customize it to suit your needs in package.json)
```

To simply start serving, run this:

```
$ npm start
```

Enter the following URL in the web browser to launch your project:  
**http://localhost:8000**

<hr>

### Create your own app  

##### HTML

Put all HTML files directly into the **public** folder. Do not use subfolders.

##### CSS

Check out the **sass** folder and the scss files named with "_custom". Put your custom styles into these files.

##### JS

The main Javascript file is within the **src** folder. You write your code there and import modules using the ES6 syntax.

##### Routing

Routes are configured in `app.js` using the express framework. 

##### Manifest

In `manifest.json` you set the name of your app.

<hr>

### Create icons

Visit [realfavicongenerator.net](https://realfavicongenerator.net). Follow the instructions and replace the related images in the public folder with those from the zip file. Ignore the included manifest.

### Use another CSS framework

Instead of MaterializeCSS you can install any other css framework that you prefer. If the other framework supports scss as well open and edit styles.scss which you find in the "sass" folder. Replace the MaterializeCSS entry so it points to the main scss file of the new library. Also import the JS file if it is a module in "src/register.js".

### Offline first

The nice thing about a PWA is that you can use it offline like a native app on a mobile device or on the desktop. But to achieve this behaviour you have to cache all the required files in a special way. You can do this with a so-called ServiceWorker.

Since caching can be annoying during the development process I highly recommend to activate it at the earliest shortly before the deploy. Therefore the ServiceWorker is disabled by default. You have to activate it manually: set `enableServiceWorker = true;` in "src/register.js". Then run the following command to generate the public ServiceWorker (public/sw.js) with the latest precache manifest:

```
$ npm run sw-update
```

Open the "Application" tab in the developer tools of your browser. There you can check whether the ServiceWorker is running correctly. In rare cases Workbox may not recognize all of the files to be cached automatically. When that happens, manually add these files to the array `additionalManifestEntries` in "workbox-config.js":

```
"additionalManifestEntries": [
    { "revision": rndStr(), "url": "FILE_PATH" }
]
```

> NOTE: Whenever you add, remove or modify files while the ServiceWorker is enabled you have to execute `$ npm run sw-update` manually in the console to update the public ServiceWorker and to rebuild the cache.