---
layout: post
title:  "Rails 5 Api + React/Redux "
date:   2017-08-03 02:56:30 +0000
---


The final project for the Flatiron Full Stack Web Development course is to create a single-page web application using a cumulation of the skills developed throughout the course. I'm a big advocate for efficient workout routines so I decided to create an application where you can create an ongoing list of HIIT workouts.

In Rails 5 you have the ability to create an API only application which allows you to design your front-end however you like. Just specify with the --api flag:  

```
rails new new-application --api
```



I've designed the front end of my application using react. You can set this up quickly using **create-react-app**. [This](https://github.com/facebookincubator/create-react-app) repo will help get your app up and running. 

There are plenty of libraries out there to help with styling your application but [react semantic ui](https://react.semantic-ui.com/introduction) stood out. 

To use it in your application install the following dependencies: 

```
npm install semantic-ui-react --save
npm install semantic-ui-css --save
```

And then add the css to index.js:

```
import 'semantic-ui-css/semantic.css'
```

Once I had my models set up and some seed data I went ahead and tested that the data was being persisted as expected: 

```
 componentDidMount() {
    window.fetch('/workouts')
      .then(response => response.json())
      .then(json => console.log(json))
      .catch(error => console.log(error))
  }
    
```

At this point, it is time to decide how to handle state in your application. To load or *get* the workouts I used Redux. Redux can be thought of as a store in that it stores state at any given time of the objects you give it. Redux works especially well with React because it allows you to describe a UI as a function of state. 

The container component patterns are often used in react applications. A container components responsibility is to describe the data that should be produced or presented. This data is presented in HTML by a presentation component. The data that the presentation component receives is through what is known as props. Presentational components are often stateless. That is they are solely responsible for rendering the given data.

With this pattern of container and presentational components, it works as a separation of concerns and allows for easier extension of a given application. 

Building my first React application was a lot of fun! It was interesting to see how everything came together. Eventually I'd like to add user accounts using active admin and devise. If you want to take a peek at the details you can find my code [here](https://github.com/kkashuda/hiit-app).      


