---
layout: post
title:  "Rails App with a jQuery Front End "
date:   2017-06-30 21:35:01 -0400
---


The goal:   

The goal of this portfolio project is to continue building on our previous Rails portfolio project to include jQuery functionality. jQuery is a framework that was designed to make writing JavaScript easier. By utilizing jQuery it gives applications the ability to be dynamic. For example, when you are on Facebook (desktop) and you go to message someone it doesn't redirect you to a new page. Conveniently enough you are able to activate a little pop-up box, or modal and message someone all while scrolling through your feed. There are many tools that help us to accomplish this dynamic behavior. The tools I used in this project are very much low level and bare bones. Luckily some very talented programmers out there have written various libraries and frameworks for us to accomplish these dynamic features a bit more linearly but it is important to work at the low level to appreciate these abstractions. 

Big takeaways: 

It was really awesome to learn about and implement the flow of handing off information to the DOM to produce dynamic results. Serialization is the main contributor to this in that it allows for data on a particular page or form (depending on the http request) to be serialized into a JavaScript Object Model that allows the data to be appending it to the DOM. Of course you, the programmer, must format the data into valid html because that is what the DOM expects. This can be done through interpolation or create a method on the protype that does the formatting for you. For example to format a comment I created a method: 

```
      Comment.prototype.formatComment = function() {
      return `<h5> ${this.username} </h5> <center> <p> ${this.content} </p> </center><hr>`
    }
```

And I created a constructor to create a new comment for when I dynamically append it to the DOM: 

```
 function Comment(content, username) {
      this.content = content
      this.username = username 
    }
```

The logic that went into actually appending the data to the DOM was done through Ajax. Ajax is a client side script that communicates with the servers that is able to update parts of a page without needing a page refresh. Ajax uses the data serialized from JSON, a lightweight alternative to XML. Ajax isn't necessarily hard, you just have to be very organized in your thought process. For example while you are writing out a get or post request using Ajax you'll likely need to use the debugger and test as you go in the browser. With frameworks like React and Angular some of these nit picky details are abstracted away but as a professional web developer it is important to know what is going on under the hood. 

Experimenting with these different tools and building these functionalities from the ground up was a lot of fun. I look forward to using React to build flexible, dynamic user interfaces with a more lightweight, abstract description of what to render. 


