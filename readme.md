# FlavorNet

## Table of Contents
- [Introduction](#introduction)
- [Technologies](#technologies)
- [The Data](#the-data)
- [Algorithms](#algorithms)
 

## Introduction

FlavorNet is an interactive reference that allows users (molecular gastronomy geeks) to discover flavor pairings based on flavor compound analysis. By modeling the relationships between flavor compounds, ingredients, ingredient prevalence, recipes and regional cuisines, users are able to discover new, possibly non-intuitive flavor combinations or ingredient substitutions. Combinatorial analysis also allows users to experiment with mapping flavor profiles within the context of a given cuisine. For example, a search for ingredient pairings with "egg" in Russian cuisine would return different ingredient combinations than a search for "egg" in Vietnamese cuisine. 

![Demo](https://github.com/levi006/FlavorNet/blob/master/static/img/runthrough.gif)

## Technologies

**Backend**

Python, Flask, SQLAlchemy, SQLite, AJAX

**Frontend**

D3.js, Javascript, Jinja, Jquery, HTML, CSS, Bootstrap

## The Data

The source data sets for the project are publicly available on [YY Ahn's](http://yongyeol.com/) website. The recipe data sets were scraped from the recipe aggregator sites allrecipes.com, epicurious.com and menupan.com.

The data can be characterized as follows: 

-1,529 ingredients
-1,106 flavor compounds (each ingredient could have anywhere from 1 to hundreds of flavor compounds. For example, "egg" contains 49 flavor compounds, while "black tea" has 239 flavor compounds).
-1,169,685 possible ingredient pairs from a total of 55,786 recipes
-200,011 ingredient pairs when calculated within their respective cuisines 


## Algorithms 

#### Comparing Ingredients

To figure out what ingredients pair well ("well" defined by the number of flavor compounds the two ingredients share in common) I used Sqlalchemy to query a local SQLite database and limited the results to the first ten matches in descending order of most to least shared flavor commpounds.
 

#### Comparing Ingredients within a Cuisine

I decided in favor of creating a relational table that tracked ingredient pairs within a given cuisine and the number of times the respective ingredient pair and cuisine appeared in all the recipes in the data set.     

The itertools library was instrumental to track all possible discrete ingredient pair-cuisine combinations and discard duplicate permutations (i.e. "broccoli and kale in Italian cuisine" is the same as "kale and broccoli in Italian cuisine" and should not be counted separately). 

Once this table was created, given an input ingredient and cuisine, users would be able to discover the most commonly combined ingredients characteristic to the cuisine. For example, a search with "lemon" and "Italian" will yield different ingredient pairs than "lemon" and "Asian". 

Using the <a href="http://bl.ocks.org/mbostock/4339184">Reingold-Tilford tree</a> visualization, users can click to explore the flavor profile generated by their search. For example, a search with "lemon" in "Italian" cuisine will yield a list that includes "artichoke" and "vanilla", which will yield very different flavor profiles as illustrated below. 

![image:](https://github.com/levi006/FlavorNet/blob/7119a3029c0acb4f3373c666a0ad33d27280faf0/static/img/Italian%20flavor%20profile.png)




