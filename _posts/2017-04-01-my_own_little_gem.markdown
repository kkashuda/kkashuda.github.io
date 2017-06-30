---
layout: post
title:  "Building a Ruby Gem "
date:   2017-03-31 22:53:59 -0400
---


 My first portfolio project for Flatiron School was to build my own Ruby gem! Let me tell you, I was intimidated. I put it off for a little while and went on to other sections of the course. Sometimes I do that when I am nervous. I wish I hadn't though because once I got into it, it was a lot of fun! It did take some set up, though. For instance, I was completely naive to the idea of a gem even though I had been using them in labs since starting to learn Ruby. Luckily the program offers a step-by-step guide to building a gem and that was a lifesaver! The tutorial showed how to take all of the right tools out of your toolbox and when to use them. 
 

The process started by using a really nice tool, Bundler! Essentially bundler set up the skeleton of your ruby gem by simply entering `bundle gem my_gem` in the command prompt. Upon doing that bundler sets up a perfect environment for your gem (e.g. needed files and directories). 

After that, it was about what do I want my gem to *do*? 


Well, I decided hey, I like trivia, so that means I must like facts! Why not a gem that generates random facts? So I did that. Except it wasn't just as easy as *that*. But, with what all I've learned in terms of OO principles, my general knowledge of Ruby, and having experimented with web scraping I definitely knew it was possible!


So, I went through the example video again. After watching it I set up my requirements. The big one being my web scraping tool Nokogiri. Thank the web for Stack Overflow because web scraping is not always easy and when something in programming isn't easy, help can usually be found there! 

Anyway, a little ahead of myself. After I set up the requirements, I started working on my CLI class. I initially hard-coded all of the menu options, but once I got into the scraping I generated the menu from the data I scraped directly from the site: 
<br>
<br>

```
  def menu
    @categories = Facts::TheFacts.scrape_categories
    index = 0
    @categories.each do  |category|
      puts "#{index} - #{category}"
      index += 1
    end

    if $started == false
      puts "Go ahead and enter 0-12, and a random fact will be generated specific to the category!"
      puts "If you need to see the list of options again, enter 'list', or if you're ready to exit enter 'exit'."
      puts

      $started = true
    end
  end
```

<br>
<br>
I know you are probably looking at that global variable and thinking was it necessary? Well, it seemed to be the cleanest way to tell if the user had been given instructions on how to use the menu because I didn't want it to be repetitive. From what I've read, global variables should not be used if an accidental reassignment of the value could cause an issue with the functionality of the program. In this case, I felt safe enough to use it and didn't see a threat in doing so.  

During the process, I tried very hard to keep my methods meaningful in the sense that they each had their own clear-cut contribution to the program. That way if any issues arose, they would be easier to pinpoint. This became increasingly important when I began working on the web scraper.

Below are two methods from my scraping class. The first one, *scrape_categories*, is designed to scrape the text that describes the various categories of facts the site offers. Unlike other languages I've worked with (e.g. Java, C++) Ruby allows you to put both a readable and meaningful amount of functionality into one line of code. It makes the process of figuring out the problem at hand a lot of fun! 

The second method *scrape_links* is doing a lot of work in that it is scraping at an iterative level. The idea of scraping a web page through iteration was kind of mind-blowing at first, but Stackoverflow cleared that up luckily and reminded me of the handy tool, *map*! 
<br>
<br>

```
def self.scrape_categories
    doc = Nokogiri::HTML(open("http://www.generatefacts.com/"))
    categories = []
    doc.css("div.category-box a").children.each do |t|
      categories << t.text unless t.text.include?("\r"+"\n") # thanks for being awesome Ruby!
    end
    categories
  end
    

  def self.scrape_links
    doc = Nokogiri::HTML(open("http://www.generatefacts.com/"))
    find_links = doc.css('div.category-box a[href]')
    links = find_links.map {|element| element["href"]}
    @links = links.uniq
  end
```

<br>
<br>
After those two methods all that was left was scraping individual categories for facts. I also had one helper method: 
<br>
<br>
```
# woo, helper methods helping out!
 def self.index(index)
    self.scrape_links
    @category = "http://www.generatefacts.com#{@links[index]}"
    self.scrape_category
  end
```
<br>
<br>
This method helped out perfectly. When users pick a category the order in which the links are scraped match up perfectly with the given menu. It's the small things. 

And wah lah! 

The bottom line is building CLI applications in Ruby is FUN! Once I go through the code review I know some things will be brought to my attention to help me improve next time I build a gem! That's the wonderful thing about learning, it never ends, and certainly not when it comes to software development and technology in general!  
<br>
<br>
<center>![](http://2.bp.blogspot.com/--UEJsagNOIo/Uztx7grVyxI/AAAAAAAAAGk/hcG7azhn9x4/s1600/fd3d970c53aa6ae1dfdda0c2aa7c344c883bf5455bf924fdb6e3d8b1f4983385.jpg) </center>
<br>
<br>
