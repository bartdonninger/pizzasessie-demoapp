> This is a work on progress.

# Introduction

This is a quick demostration of Vue.js application created for a local developer meeting.

The idea here is not to be complete, but to quickly be able to show a group of developers how to setup and get their feet wet writing and running VueJS applications.

## Install NodeJS

NodeJS can be installed in two different ways depending on your preference.

- Go to the [NodeJS](https://nodejs.org/en/) website and select the latest version, download it and then run the installer. (Suggestion: install it on C: for compatibility)
- Use [Chocolatey](https://chocolatey.org/install) and after that use the commands:

```bash
choco install nodejs

choco install nodejs.install
```

For Visual Studio support you might also want to install

- [Vue.js Pack 2017](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.VuejsPack-18329) for Visual Studio 2017 or [Vue.js Pack](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.VuejsPack) for Visual Studio 2015
- [Webpack Task Runner](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebPackTaskRunner)

Both of these were created by Matts Kristensen from Microsoft.

## Create a VueJS-webpack boilerplate project

Go to [Vue-templates Github](https://github.com/vuejs-templates/webpack) repository and follow the instructions on setting up and scaffolding a basic vue-webpack-boilerplate project or execute the following commands in a commandshell (make sure you run the commandshell as the administrator).

```bash
# Install the vue-cli application using NPM (the -g commandline switch means install globally).
npm install -g vue-cli

# Create a vue.js application with your own chosen application name.
vue init webpack <project name>

# Go into the project folder.
cd <project name>

# Run the Npm development-server.
npm run dev
```

## Vue.js Instance lifecycle

Now that you have a working Vue.js application, we'll have a look at the life cycle of a Vue.js application.

Vue.js uses a virtual DOM. In a Virtual DOM application, changes to the UI are first pushed to a Virtual DOM before the Virtual DOM is rendered to the browser. Vue.js can be used with many other frameworks as it's main focus is the UI. As such it can be used to build sophisticated SPA's (Single Page Applications).

The life cycle of a Vue.js application contains various steps at which point, you as the developer, can interact with the Vue.js application. In Vue.js these steps are called Instance lifecycle hooks.

![alt text](https://vuejs.org/images/lifecycle.png "Vue.js Instance lifecycle")
(image taken from the [Vue.js guide](https://vuejs.org/v2/guide/instance.html))

The points at which you, as the developer, can interact with the Instance lifecycle are

- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestroy
- destroyed

Most of the time you will only be using the created or mounted hooks as most others are limited in scope as to what you can actually do.

> One thing to keep in mind is that, if you're using jQuery and you wish to directly manipulate parts of the DOM using jQuery, you might find that your changes are not persisted when the virtual DOM is rendered to the browser. Any changes to the DOM have to be done through using one or two-way databinding for the changes to persist through the rendering phase. Later on we'll see how one or two-way databinding works in Vue.js.

For more information regarding the Vue.js Instance lifecycle see the [Vue.js documentation](https://vuejs.org/v2/guide/instance.html)

## Demo application

If we look at the folder structure of the demo application created by vue-cli application we notice a few things.

In the root of the project folder there is an **index.html**. This is the starting point for our Vue.js application. Most of the time you will leave this file alone, as everything you would want to do should be done somewhere else. In most cases all you would want to do in the index.html file is update the header information to reflect what your site needs.

You will also notice the **build** folder. The **build** folder contains the files needed by **NPM** to be able to actually run you application. **NPM** uses [Webpack](https://webpack.js.org/) to build and run your application. Once setup there is very little you'll need to do to keep it working.

The config folder contains the configuration files needed by [Webpack](https://webpack.js.org/) to configure your application for the correct environment. For development purposes you will most of the time use the **dev.env.js** file.

The **node_modules** folder can be ignored as it contains the **Node** modules that your application uses.

The, for us, most interesting folder is the **src** folder. In the root of the **src** folder you will find **App.vue** and **main.js**. So how does Vue.js know where to start loading the application?

If you look at **webpack.base.conf.js** in the **build** folder you will find this entry

```bash
entry: {
    app: './src/main.js'
}
```

This section tells **Webpack** to start the application using the **main.js** file as it's entry point. If we look at the **main.js** file in the **src** folder we see that **App.vue** is imported and referenced at the end of **main.js** as a component.

```bash
import App from './App'

components: { App }
```

We also see that **Vue.js** itself is imported into **main.js**

```bash
import Vue from 'vue'
```

By default, if a website is loaded for the first time, a webbrowser like Chrome, Firefox or Edge will always look for an index.html. This is how the loading chain of **Vue.js** starts.

You might be wondering at this point how **Vue.js** knows which component to load as it starts up. If you look at **index.html** you will notice this bit of HTML.

```bash
<div id="app"></div>
```

The id here is **app**. This id is also the name of **App.vue**.

```bash
<script>
export default {
  name: 'app'
}
```

So **main.js** is the starting point of our application and it's telling **Vue.js** to load **App.vue** as the starting or main component. You can however modify **App.vue** to do the things you would like to do at the starting of your application. You can, for instance, grab some data from a WebAPI if you need the data at the start of the application. Most of the time however, you are not going to modify **App.vue** too heavily as most of the data you will want to retrieve can be retrieved in **components** as well.

This leaves us with one thing that needs to be mentioned. How do you actually load components? Basically there are two common ways of loading components.

- You can create a component and add it to a **Vue** file as a component.
- You can create a router view and include it in your application

To see what a basic component looks like, take a look at **HelloWorld.vue** in the **components** folder.

In the **src** folder we also find a **router** folder. Inside the **router** folder we find an **index.js**. This is the entry point for the router in our **Vue.js** application. The router used by default in **Vue.js** application is [Vue-router](https://github.com/vuejs/vue-router). You can find the documentation for [Vue-router](https://github.com/vuejs/vue-router) on the official **Vue.js** [Vue-router](https://router.vuejs.org/en/) page.

## Lets create our Vue.js application

We'll create a simple webapplication that will display a list of 5 cryptocurrencies with an icon, a value and a short description.

For our application to be kind of useful, a simple WebAPI has been added that will return static data. The WebAPI can be started by opening the **pizzasessie-webapi** project in Visual Studio 2015 or 2017 and pressing F5 to start it.

The [WebAPI](https://github.com/mhartsuiker/pizzasessie-webapi) returns a list of cryptocurrencies. We're going to create a component that will display the information retrieved from the [WebAPI](https://github.com/mhartsuiker/pizzasessie-webapi).

## Sources used for this document

- [vuejs-templates/webpack](https://github.com/vuejs-templates/webpack)
- [Vue.js guide v2.x](https://vuejs.org/v2/guide/)
- [Vue-router](https://router.vuejs.org/en/)
- [Curated list of Vue information](https://github.com/vuejs/awesome-vue)
- [Mastering markdown](https://guides.github.com/features/mastering-markdown/)
- [Cryptocurrency icons](https://github.com/cjdowner/cryptocurrency-icons)
