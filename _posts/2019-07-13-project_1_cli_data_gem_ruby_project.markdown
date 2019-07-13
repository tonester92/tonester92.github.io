---
layout: post
title:      "Project 1: CLI Data Gem Ruby Project"
date:       2019-07-13 22:38:48 +0000
permalink:  project_1_cli_data_gem_ruby_project
---


Hello, this is my first project with the Flatiron School after learning Ruby for about two months. This project combined all of my learning in this topic. I decided to create a gem based off of my favorite dessert, flan. 

In this project, I was able to create an environment for my gem, create methods to intract with the gem, and to scrape data from real world applications. 


**1. Creating an enviroment for my gem:**

In the past doing homework, the enviroment was already created for me. However, this time I had the flexibility to construct my enviroment in any part of my coding. I decided to put my enviroment in recipe_flan.rb. I put it in this file because each file runs smoothly in this enviroment. 

```
require 'open-uri'
require 'nokogiri'
require 'pry'

require_relative "./recipe_flan/version"
require_relative './recipe_flan/recipe'
require_relative './recipe_flan/cli'
```

*Each require represents a file for my program to run. *

'open-uri' : opens the websites I pulled and helps with my scraping
'nokogiri': helps with my scraping
'pry': helps with my scraping

"./recipe_flan/version": loads the verison my program is in
'./recipe_flan/recipe': loads the recipe.rb file
 './recipe_flan/cli': loads the cli.rb file
 
 *In conclusion: *

One really has to play around with their enviorment to make their program work. This was the toughest part of my coding because require and require_relative are tricky and where you put them matters for your code to work.

**2. Creating methods to intract with the gem:**

Creating methods is not new to me, however, creating a method where I can intract with my data was different. After watching CLI Data Gem Walkthrough, https://www.youtube.com/watch?time_continue=946&v=lDExWIhYKI, I was able to get ideas for my code. I choose to stick to the "if" method in the video because I liked how my data was shown. 

```
def directions
    input = nil 
    while input != "exit"
      puts "Enter the number for the recipe you want or type exit to enter:"
      input = gets.strip.downcase
      
      if input.to_i > 0
        the_recipe = @recipes[input.to_i-1]
        puts "Name: #{the_recipe.name} 
        Ingredients: #{the_recipe.ingredients} 
        Directions: #{the_recipe.directions} 
        Reviews: #{the_recipe.reviews}"
      elsif input == "list"
        list_recipes
      else 
        puts "Not sure which one is the best? Type Number again. Or picked your favorite already? Type exit"
      end
    end
  end 
  
  def goodbye
    puts "Goodbye, Which One Is Better for You?"
  end
end 
```

This code above is my interactions. One can see that you can access the name, ingredients, directions, and reviews of the recipe. Once you see the directions you can type 1, to see recipe 1 or type 2, to see recipe 2. If one can not chose you will see the messgae in the else. And to exit one can type exit and see the goodbye message.

*In conclusion:*

This was the easiest part of the project because I have lots of experience building methods. 


**3. Scraping data from real world applications:** 

Scraping data is something that takes time to understand and execute. But once you get the hand of it, its not so bad. I had to scrape from two food common websites: the Food Network and the All Recipes. The data I choose to scrape was the name, ingredients, directions, and reviews.   

```
 def self.scrape_foodnetwork
    doc = Nokogiri::HTML(open("https://www.foodnetwork.com/recipes/tyler-florence/flan-recipe-1914016"))
    
    recipe = self.new  
    recipe.name = doc.search("h1.o-AssetTitle__a-Headline").text.strip
    recipe.ingredients = doc.search("div.o-Ingredients__m-Body").text.strip
    recipe.directions = doc.search("div.o-Method__m-Body").text.strip
    recipe.reviews = "73 reviews"
    recipe.url = "https://www.foodnetwork.com/recipes/tyler-florence/flan-recipe-1914016"
    
    recipe
  end
  
  def self.scrape_allrecipes
    doc = Nokogiri::HTML(open("https://www.allrecipes.com/recipe/20979/spanish-flan/"))
    
    recipe = self.new  
    recipe.name = doc.search("h1.recipe-summary__h1").text.strip
    recipe.ingredients = doc.search("li.checkList__line").text.strip
    recipe.directions = doc.search("span.recipe-directions__list--item").text.strip
    recipe.reviews = doc.search("span.review-count").text.strip
    recipe.url = "https://www.allrecipes.com/recipe/20979/spanish-flan/"
    
    recipe
  end
end
```

I used nokogiri and pry to scrape my data. This is the data I was able to come up with. While actually scraping my data, in the termial I need to get into the console to scrape. Once in the console, I put RecipeFlan::Recipe.scrape_(the website I picked) and then typed doc.to_html. Finally, I was able to scrape the html to find all the texts for my data. 

*In conclusion:*

This was really fun and I enjoyed scraping. 


*Favorite part: *
Scraping because it was a challenge that I appreciated.

*Dislike:*
Fixing the enviroment, gemspec, and giving the gem permission was upsetting for me because it was tough to get it to install in the terimal correctly. 

**In the end:**

This project has made me into a better student because I was able to put everything I learned in one assignment. However, I do know that because I am a new coder, my code can be adjusted and have room for improvement.  
