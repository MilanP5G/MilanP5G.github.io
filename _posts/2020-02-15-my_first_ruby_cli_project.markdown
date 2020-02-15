---
layout: post
title:      "My first Ruby CLI Project!"
date:       2020-02-15 19:34:06 +0000
permalink:  my_first_ruby_cli_project
---


  I must admit, this was a journey of many blocks and long hours trying to figure out the best way to implement my code from scratch. Nevertheless, it was a really good experience and definitely a big learning curve for me.

  I wanted to create an application that displays the three most popular books from His Divine Grace AC Bhaktivedanta Swami -  a spiritual teacher who spread the Kṛṣṇa Consciousness movement in the western world during the 1970's. I thought this would be a great way to express two things that are very important to me - his teachings and coding.

  Firstly, I knew that I would need 3 files with a class each and so started with the `Vedabase class`. The `Vedabase class` initializes with a title of a book and includes a class variable `@@all` containing all instances of a book. Secondly, I would need a `Scraper class` that scrapes the titles of each book from the following website =>(http://https://vedabase.io/en/library/). I also scraped the introductions of each book from a different page through the same website. Thirdly, creating my `CLI class` that allows the user to interact with the application.
	
  Within the `CLI class`, I called upon the titles from the `Scraper class` to create instances within the Vedabase class.  I then called upon the `.all` method from the Vedabase class to retrieve all the instances and listed them in a method. I also created a method to update the instances with an introduction attribute that is displayed on the 2nd level of the application.
	
  Going back to my `Scraper class`, I was constantly going back and forth as I could not seem to find the perfect formatting for it when it is displayed in the terminal. I also had an option to scrape 3 pages with a title & introduction or 4 pages, one with the list of books and 3 with an introduction each. I chose to settle with scraping 4 pages.
	
  In the `CLI class`, I created different methods which "puts" the titles for the user to choose from, a message for invalid inputs, an option to return to the main menu and/or leave the application. Once the user leaves the application, they receive a message to visit a website if they would like to know more or purchase the books.
	
  This project was definitely tricky at times but I'm grateful for the process and all that I have learnt along the way.
