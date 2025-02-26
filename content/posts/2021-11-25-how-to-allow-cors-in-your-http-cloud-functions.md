---
title: How to allow CORS in your HTTP cloud functions
date: 2021-11-25 01:00:00
featuredImage: /post-images/2021-11-25-how-to-allow-cors-in-your-http-cloud-functions.webp
draft: false
tags:
  - Cloud Functions
  - Firebase
---

In the previous [article](http://localhost/wordpress/blog/getting-started-with-firebase-cloud-functions/), we have created our first cloud function.

You probably have noticed something interesting.

We can call our function via CURL, but not via fetch on the client.

![](/post-images/2021-11-image-5.webp)It is due to CORS policy.

Let's rewrite our code in the **functions/index.js** using official way from the firebase documentation.

![](/post-images/2021-11-image-6.webp)To this:

```javascript
const functions = require("firebase-functions");

// Create and Deploy Your First Cloud Functions
// https://firebase.google.com/docs/functions/write-firebase-functions

exports.helloWorld = functions.https.onRequest((request, response) => {
  response.set("Access-Control-Allow-Origin", "*");

  if (request.method === "OPTIONS") {
    // Send response to OPTIONS requests
    response.set("Access-Control-Allow-Methods", "GET");
    response.set("Access-Control-Allow-Headers", "Content-Type");
    response.set("Access-Control-Max-Age", "3600");
    response.status(204).send("");
  } else {
    response.send("Hello from Firebase!");
  }
});
```

We've configured some HTTP headers, and now we can get the data on the client via fetch.

But first to apply the changes, let's redeploy cloud functions:

```bash
firebase deploy --only functions
```

Now let's run some fetch call in the console.log

```javascript
fetch("https://us-central1-fir-project-3359f.cloudfunctions.net/helloWorld")
  .then((response) => response.text())
  .then((data) => console.log(data));
```

And it works!

![](/post-images/2021-11-image-7.webp)But don't you find it is a little bit redundant to write so much code?

Is there an easier way?

Actually, there is.

First, we need to install cors package in the functions folder

```bash
npm i cors
```

And then we need to import this package, and wrap our function with this package, so our code we'll look like this:

```javascript
const functions = require("firebase-functions");
const cors = require("cors")({ origin: true });

// Create and Deploy Your First Cloud Functions
// https://firebase.google.com/docs/functions/write-firebase-functions

exports.helloWorld = functions.https.onRequest((request, response) => {
  cors(request, response, () => {
    response.send("Hello from Firebase!");
  });
});
```

Make sure to import cors package like this, via passing origin parameter.

Otherwise, your code won't work.

## Quick update:

I found a simpler way without importing cors package.

Just add this line:

```bash
response.set("Access-Control-Allow-Origin", "*");
```

So, our final code looks like this:

```javascript
const functions = require("firebase-functions");

// Create and Deploy Your First Cloud Functions
// https://firebase.google.com/docs/functions/write-firebase-functions

exports.helloWorld = functions.https.onRequest((request, response) => {
  response.set("Access-Control-Allow-Origin", "*");
  response.send("Hello from Firebase!!!");
});
```
