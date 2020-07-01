# Ready-to-use Node.JS REST API and Automation Engine for moderation of indecent images.

With the vastly growing number of apps on the market, Content Moderation is becoming a heavy task that takes too much time and effort. That combined with the fact that advances in technologies brought Machine Learning closer to single developers inspired our team to build an **fully functional Open-Source Content Moderation service with ReactJS based Admin Panel** and make content moderation a piece of cake!

We've put the thoughts into a realization and built up three components, each one more advanced than the previous. No matter if you only need [Image Classification REST API](https://github.com/SashiDo/content-moderation-image-api), the REST API + Automation logic from this repo or the full-fledged product with ready-to-use React-based Admin panel(coming soon) - all you need to do is clone the respective repository, maybe customize a bit and deploy to your production app. The solution is simple, effective and can be easily integrated into every project even if this is your first encounter with Machine Learning. 

<br />

# Examples & Demos

## Automation Engine 

An example of how the Automation Engine makes a decision based on the Moderation Preferences we've set and the REST API Image Classification.

![](https://media-blog.sashido.io/content/images/2020/07/nsfw-4.png)


## Image Classifiaction REST API 

These are the examples and the demos how the REST API classifies images for some of the classes. For the other classes we think you should experiment by yourself ... you know what I mean ;).

<table align="center">
  <tbody>
    <tr>
      <th align="center">Image Source</th>
      <th align="center">Image Source</th>
      <th align="center">Image Source</th>
    </tr>
    <tr>
      <td align="center">
        <a
          href="https://nsfw-demo.sashido.io/api/image/classify?url=https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/41a516cc1141cdaf775a5cfa083dcb26_thumbnail.png">
          <image
            src="https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/41a516cc1141cdaf775a5cfa083dcb26_thumbnail.png" />
        </a>
      </td>
      <td align="center">
        <a
          href="https://nsfw-demo.sashido.io/api/image/classify?url=https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/a3115074f603c99770d376f3e6d0f72e_thumbnail.png">
          <image
            src="https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/a3115074f603c99770d376f3e6d0f72e_thumbnail.png" />
        </a>
      </td>
      <td align="center">
        <a
          href="https://nsfw-demo.sashido.io/api/image/classify?url=https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/355a4b37b8a657dd09f3f50816481cca_thumbnail.png">
          <image
            src="https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/355a4b37b8a657dd09f3f50816481cca_thumbnail.png" />
        </a>
      </td>
    </tr>
    <tr>
      <th align="center">Classification Result</th>
      <th align="center">Classification Result</th>
      <th align="center">Classification Result</th>
    </tr>
    <tr>
      <td>
<pre>[{
  "className": "Neutral",
  "probability": 0.93821
}, {
  "className": "Drawing",
  "probability": 0.05473
}, {
  "className": "Sexy",
  "probability": 0.00532
}, {
  "className": "Hentai",
  "probability": 0.00087
}, {
  "className": "Porn",
  "probability": 0.00085
}]</pre>
      </td>
      <td>
<pre>[{
  "className": "Sexy",
  "probability": 0.99394
}, {
  "className": "Neutral",
  "probability": 0.00432
}, {
  "className": "Porn",
  "probability": 0.00164
}, {
  "className": "Drawing",
  "probability": 0.00006
}, {
  "className": "Hentai",
  "probability": 0.00001
}]</pre>
      </td>
      <td>
<pre>[{
  "className": "Drawing",
  "probability": 0.96063
}, {
  "className": "Neutral",
  "probability": 0.03902
}, {
  "className": "Hentai",
  "probability": 0.00032
}, {
  "className": "Sexy",
  "probability": 0.00001
}, {
  "className": "Porn",
  "probability": 0.00005
}]</pre>
      </td>
    </tr>
    <tr>
      <td align="center"><a href="https://nsfw-demo.sashido.io/api/image/classify?url=https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/41a516cc1141cdaf775a5cfa083dcb26_thumbnail.png">Neutral Demo</>
      </td>
      <td align="center"><a href="https://nsfw-demo.sashido.io/api/image/classify?url=https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/a3115074f603c99770d376f3e6d0f72e_thumbnail.png">Sexy Demo</>
      </td>
      <td align="center"><a href="https://nsfw-demo.sashido.io/api/image/classify?url=https://mqfy379g6xncpc3va4epdzkfsxf0vs.files-sashido.cloud/355a4b37b8a657dd09f3f50816481cca_thumbnail.png">Drawing Demo</>
      </td>
    </tr>
  </tbody>
</table>
<br />


# How it works

This service is built in Node.JS with Mongo DB and Parse Server. You can use it in a standard Express app, but keep in mind that the file structure of the repo is Parse specific. The code is organized in a ```src``` folder and ```src/cloud/main.js``` is the root file for the service.

## REST API

The REST API works with [NSFW.JS](https://github.com/infinitered/nsfwjs) classification, which uses [Tensorflow](https://www.tensorflow.org/js) pre-trained ML models. Given an URL, it returns predictions how likely the image falls into each of the classes - Drawing, Neutral, Sexy, Porn and Hentai. More details on the usage and logic behind you can fin in [this blog post](https://blog.sashido.io/content-moderation-service-with-nodejs-tensorflowjs-and-reactjs-part-1-restful-api-service/). 

## Automation Engine

The Automation Engine's purpose is to check how the classification of a certain image corresponds to the parameters you’ve set as safe for your project. 

### 1. Moderation Preferences

In the beginning, it is essential to define which of the five NSFW classes and values can contain disturbing images and require moderation, i.e. which prognoses are considered safe and which toxic for your users. As there are no specific standards and Moderation Preferences are strictly individual for different projects, we'll advise you to think carefully. 

To illustrate what's the idea and setup, let's imagine we need to set preferences for Clothes Styling app. Users upload outfits and exchange fashion ideas. We can assume the type of photos should be mainly Neutral...and some sexy pics during beach season. So we will add all other classes to our moderation preferences. Something like:

```JSON
{  
  "Sexy": { "min": 0.6, "max": 1 },
  "Drawing": { "min": 0.4, "max": 0.8 },
  "Porn": { "min": 0.4, "max": 0.8 },
  "Hentai": { "min": 0.2, "max": 0.8 }
}
```
**The Automation Engine will auto-reject all images that are classified above the `max` limit set in our preferences and approve all that are below the `min` value.** More details on how to fine-tune the parameters for your project you can find in the article [here](https://blog.sashido.io/content-moderation-service-with-nodejs-and-tensorflow-part-2-moderation-automation/).

The moderation preferences will be saved into a moderationScores config parameter for the production application, as that will allow you to modify them on the fly if needed. 

### 2. Automation Business Logic

The Automation Engine is implemented with [Parse Server Cloud Code Trigger](https://docs.parseplatform.org/cloudcode/guide/#aftersave-triggers). An afterSave trigger, hooked to the user-generated collection automatically checks newly uploaded photos and marks them as either safe, deleted or for moderation. The afterSafe contains logic for getting the predictions from the API and info if an image is safe or toxic for your users, according to the parameters that you define. Based on all data passed, the decision is made and the result is saved to your database.

![](https://media-blog.sashido.io/content/images/2020/07/auto_readme2.gif)

N.B.! The afterSave automation is hooked to a collection UserImage by default. To use straight away after deployment, you should either keep the same class name or change with the respective one [here](https://github.com/SashiDo/content-moderation-automations/blob/master/src/cloud/triggers.js#L3).

### 3. DB Schema

To store automation results, you need to add the following columns to the DB collection that stores users’ images(UserImage in our case). 

**isSafe(Boolean)** - if an image is safe according to the moderation preferences, the Automation Engine will mark ```isSafe - true```. 

**deleted(Boolean)** - all inappropriate images that are over the ```max``` values of the moderation preferences, are marked ```deleted - true```. Those pictures won’t be automatically deleted from the file storage. If you do not want to keep track of disturbing images, implement the deletion logic into the afterSave.   

**moderationRequired(Boolean)** - All images that are neither toxic nor safe require manual moderation!

**NSFWPredictions(Array)** - stores the NSFW classification for this image.

The automation engine will take care to fill those respectively, once a photo is uploaded. 🙂


# Installation & Configuration

## Requirements:

- Node.JS >= 10.2.1

- Mongo DB

- Parse Server

## Download the project

Clone the repo:

```
git clone https://github.com/SashiDo/content-moderation-automations.git
```

## Set Environment Variables

Copy the env.example to .env file and set the environment variables for your local environment with your favorite editor:

```
cp env.example .env
```

Place your MongoDB URI. If your app is hosted at SashiDo, you can use the database URI of your SashiDo project. Find the connection string from the app's Dashboard -> App Settings. Same goes for the files URL.

## Install Dependencies

As this is a full-featured example, all dependencies are present to the package.json. You only need to run:
```
npm install
```

## Start the project

```
npm run dev
```

**If everything is okay you should see an output similar to this one**:

```
[nodemon] 2.0.4
...
[nodemon] starting `node index index.js`
✨  Built in 2.55s.
node-pre-gyp ...
...
Running on http://localhost:1337
⠙ Building index.js...The NSFW Model was loaded successfuly!
✨  Built in 16.41s.
```

If you see the output above, you are ready to play with the Automation Engine! 🙂

# Usage

For seamless integration on any platform, the project offers clear Express routes communication. Also, you can easily query pictures based on their status from any of the Parse Server SDKs. 

## API Routes

We’ve created **express endpoints, which works with the Image Classiffication and Moderation Automation** and facilitates the integration into a project through the REST API.

- Get NSFW predictions at /api/image/classify with the following cURL request.

```sh
curl http://YOUR_PARSE_SERVER_URL/api/image/classify?url=https://nsfw-demo.sashido.io/sexy.png
```

- Check if an image is safe or toxic, NSFW predictions are also included in the response :), at /api/image/is_safe.

```sh
curl http://YOUR_PARSE_SERVER_URL/api/image/is_safe?url=https://nsfw-demo.sashido.io/sexy.png
```

## Query User Images

Check the examples below on how to query images from Parse SDKs.

### Parse JS SDK

- GET Images that require **manual moderation**:

```js
const query = new Parse.Query("UserPicture");
query.equalTo("moderationRequired", true);
query.find().then((results) => {
 console.log(results);
});
```

- GET Images that are **non-disturbing** for your audience:

```js
const query = new Parse.Query("UserPicture");
query.equalTo("isSafe", true);
query.find().then((results) => {
 console.log(results);
});
```

- GET Images that **may be not suitable** for your customers:

```js
const query = new Parse.Query("UserPicture");
query.equalTo("isSafe", false);
query.find().then((results) => {
 console.log(results);
});
```

- GET Images that are **toxic** for your users:

```js
const query = new Parse.Query("UserPicture");
query.equalTo("deleted", true);
query.find().then((results) => {
 console.log(results);
});
```
Basically these are the filters you will need. As they can be queried from the client-side thorugh any of the Parse SDKs, we'll share some examples how to get images that are for manual moderation from Android, iOS and Parse REST API.

### Android SDK

```java
ParseQuery<ParseObject> query = ParseQuery.getQuery("UserPicture");
query.whereEqualTo("moderationRequired", true);
query.findInBackground(new FindCallback<ParseObject>() {
    public void done(List<ParseObject> UserPicture, ParseException e) {
        if (e == null) {
            Log.d("isSafe", "Safe images retrieved");
        } else {
            Log.d("isSafe", "Error: " + e.getMessage());
        }
    }
});
```

More information about how to work with the Android SDK can be found in the [official docs](https://docs.parseplatform.org/android/guide/#queries).


### iOS SDK
```swift
let query = PFQuery(className:"UserImage")
query.whereKey("moderationRequired", equalTo:true)
query.findObjectsInBackground { (objects: [PFObject]?, error: Error?) in
    if let error = error {
        // Log details of the failure
        print(error.localizedDescription)
    } else if let objects = objects {
        // The find succeeded.
        print("Successfully retrieved images for moderation")
        }
    }
}
```
More information about how to work with the Parse iOS SDK can be found in the [official docs](https://docs.parseplatform.org/ios/guide/#queries).


### REST API
```sh
curl -X GET \
  -H "X-Parse-Application-Id: ${APPLICATION_ID}" \
  -H "X-Parse-REST-API-Key: ${REST_API_KEY}" \
  -G \
  --data-urlencode 'where={"moderationRequired": true}' \
  http://localhost:1337/1/classes/UserImage
});
```

More details on REST Queries you can find in the oficial [Parse REST API Guide](https://docs.parseplatform.org/rest/guide/#queries). And SashiDo users can test REST requests from a super-friendly [API Console](https://blog.sashido.io/introducing-the-api-console/) that’s built in the Dashboard.


# Deployment

## Parse.Configs for production

Set the following [Parse.Configs](https://parseplatform.org/Parse-SDK-JS/api/master/Parse.Config.html) for your production server. 

- **moderationScores** object should be saved as a Parse.Config, so preferences can be updated on the fly. 

- **moderationAutomation option** of boolean type that allows enabling/disabling content moderation automation. 


## Environment Variables for production

   For production, you need to set the **NSFW model URL**, **NSFW Model Shape size** and variable for **Automation Configs caching**.
   
   - SashiDo stores three NSFW models, each one you can set easily using the following URLs:

     
| Model URL                                                   | Size   | Shape Size | Accuracy |
| :---------------------------------------------------------- | :----: | :--------: | :------: |
| https://ml.files-sashido.cloud/models/nsfw_inception_v3/    | Huge   | 299        | 93%      |
| https://ml.files-sashido.cloud/models/nsfw_mobilenet_v2/90/ | 2.6 MB | 224        | 90%      |
| https://ml.files-sashido.cloud/models/nsfw_mobilenet_v2/93/ | 4.2 MB | 224        | 93%      |
     
 *Please note the Inception_v3 model used for this projects has high RAM/CPU consumption. While the two mobilenet models are far more lightweight.*

### Choose the model and set the following environment variables for your live server:

```sh
TF_MODEL_URL =  MODEL_URL
TF_MODEL_INPUT_SHAPE_SIZE = MODEL_SHAPE_SIZE
CONFIG_CACHE_MS = CONFIG_CAHE_IN_MILISECONDS

# Example
TF_MODEL_URL = "https://ml.files-sashido.cloud/models/nsfw_mobilenet_v2/93/"
TF_MODEL_INPUT_SHAPE_SIZE = 224
CONFIG_CACHE_MS = 10000
```

## Code Deployment

   - **In SashiDo** - This is probably the simplest way to deploy the code in production. At SashiDo we have implemented an automatic git deployment process following the [The Twelve-Factor App](https://12factor.net/) principle.

Connect your [SashiDo app with GitHub](https://blog.sashido.io/how-to-start-using-github-with-sashido-for-beginners/) and next the code can be easily deployed with two simple commands for adding a remote branch and pushing changes.

    git remote add production git@github.com:parsegroundapps/<your-pg-app-your-app-repo>.git
    git push -f production master


   - **On other providers** - Basically, you need to follow the same steps as for SashiDo Deployment. Simply follow the requirements of your hosting provider when setting environment variables for production and deploying the code.
   

# What's next?

   - **Admin Panel** - The final touch of our moderation system, where all images in need of moderation are stacked up in a beautiful interface that allows you to make decisions with just a click. - **Coming Soon...** Until release, check the [demo](https://nsfw-demo.sashido.io/moderator)!
   
# Contribution

   Thanks for looking at this section. We’re open to any cool ideas, so if you have one and are willing to share - fork the repo, apply changes and open a pull request.:)

# License

Copyright © 2020, CloudStrap AD. See [LICENSE](https://github.com/SashiDo/content-moderation-automations/blob/master/LICENSE) for further details.
