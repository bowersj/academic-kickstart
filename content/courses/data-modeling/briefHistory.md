---
title: Overview
date: "2020-06-21"
lastmod: "2020-06-22"
draft: false
toc: true
type: docs
menu:
    courses:
        name: A Brief History
        weight: 10
---

## A Brief History

The history of data modeling is a broad topic, one that has been discussed
in much more detail than we will go into here. So why start with the 
history of data modeling? Well, because it provides a context for the 
rest of the lessons in this course, as well as helps to orient the less
experienced modeler. So, lets dive right in.

_A Long Time Ago in a Galaxy Far Far Away..._

Data Modeling was born. Setting aside the drama, data modeling has been 
around for a while so what is it and why should you care? [Data modeling
is a process](https://en.wikipedia.org/wiki/Data_modeling), wait what? 
That's right, data models evolve over time as do requirements so that 
means you have to work with and tweak your model again and again, 
even when you think it is finished and ready to go. That is probably one
of the most misunderstood parts of modeling data, you are never done.
There will always be changes that need to be made to your model to 
accommodate a new requirement or to improve performance. So, think of
it as a set of tasks you repeat over and over until you have refined
your thinking, and your model, to the point where your requirements are
met, and your boss is happy. That is until your boss comes back and 
either adds a new requirement or changes a pre-existing one, which will 
happen more than once. 

Ok data modeling is a process, but what's a model?
This is more difficult to define, here's what [wikipedia has to say](https://en.wikipedia.org/wiki/Data_model):

>A data model (or datamodel) is an abstract model that organizes elements of data and standardizes how they relate to one another and to the properties of real-world entities.

Ok, what does all this academic mumbo-jumbo really mean? Basically, a 
model is a way you can organize your thoughts, build rules, and relate
those rules to the real world. Let's look at an example, speed (and no 
not the drug). There is a whole discipline of science dedicated to 
studying motion, or speed, its called physics. Physics has rules, in
fact some of those rules are so foundational they are given names and then 
sometimes they are promoted to law status, Newton's 3 laws (or rules) for
example. With these rules you can then look at the world through force 
diagrams and vectors. This allows you to predicate how something will 
work and what it will do even before it actually happens. This is the 
power of models, they allow you to break down the world around us into
small parts and combine those small parts to get bigger parts. Eventually
though, just as in science, there are problems found with a portion of the
rules which leads to a drastic change of thinking. An example of this is 
Einstein's theory of relativity, it changed how physicists viewed the 
universe, or in other words it changed their model of the universe. So,
why does this relate to data modeling? Simple, because data modeling is a
science, and like every science it is based on models and has changed of the
years to accommodate new ideas. That is what we will discuss in this lesson,
how data modeling has changed over the years. 

If you haven't noticed the trend yet, models change. That is when it is most
painful because old rules are tossed aside, some or all, and new ones have to
be created. This happens with anything that is based on a model. So expect it.
As we look at the history of data modeling we will notice this too. So, where
did data modeling start? Well to be technical it started with statistics. But,
within the tech industry I believe it started with the main frame. [Main frames](https://en.wikipedia.org/wiki/Mainframe_computer)
are basically supped up servers. Now there are differences, but we won't get into
those here. The main point here is that they would model data on these super 
servers, and they would use [hierarchies](https://en.wikipedia.org/wiki/Hierarchical_database_model) 
to represent the real world. Why start with hierarchies and not something like 
tables? There is a simple fact, we think in hierarchies. We group things together
and say they are one thing all the time. Think of a computer, a computer has a
screen, a CPU, a GPU, ect... but I said computer which implies one thing yet
that one thing is comprised of many things. It gets better when you consider 
that each item in your computer also has components and sub-components. These 
relationships go on and on even passed the sub-atomic level, yet I referred to
the computer as one thing. This exercise of grouping things together into new
things doesn't just stop with engineering, it is everywhere. Just look at your
job, you have a boss, your boss probably has a boss, and so on until you get to
the almighty CEO who makes all the big decisions and leaves the smaller details
to his employees. That's a hierarchy. So, when they started modeling they
preserved all that rich data with in a hierarchy because it was easy to 
comprehend and showed owner ship.

You might be thinking, you can do that in tables, so why hierarchies? Well, you
can but what if I wanted to get everything related to a person and, being a
good tabular (relational) data modeler I normalized most tables, that would mean
I would have to join many tables together to get a view of a person, while with
hierarchies its already "joined" together. If that doesn't make sense yet, keep
reading. So modelers started with hierarchies for simplicity and to maintain all
that juicy relationship information. But there's a catch to all this nesting
that come with hierarchies; to see this lets look at some data.

```json
{
  "name": "Bob",
  "role": "CEO",
  "favorite_color": "red",
  "employee": [
    {  
      "name": "Francis",
      "role": "CTO",
      "favorite_color": "purple",
      "employee": [
        {
          "name": "Joe",
          "role": "product manager",
          "favorite_color": "magenta",
          "employee": [
            {
              "name": "Sarah",
              "role": "programmer",
              "favorite_color": "purple"
            },{
              "name": "John",
              "role": "programmer",
              "favorite_color": "blue"
            }
          ]
        }
      ]
    }
  ]
}
``` 

NOTE: SPLIT INTO MULTIPLE PARAGRAPHS
NOTE: ORGANIZE INTO SECTIONS
NOTE: ADD SECTION HEADINGS

After looking at this structure its easy to say that Francis, Joe, Sarah,
and John are all employees of Bob. Another example could be, what if I 
wanted to get all the employees who's favorite color is purple, same as 
before you would walk the hierarchy to find all the people who's favorite
color is purple. There's a problem here what if I wanted to get all the
bosses who have at least one employee who's favorite color is purple. That 
is when you have to not only walk down the tree but then back up. So, tree 
traversal is very important in hierarchies, but it is slow. Imagine now 
doing that across 100,000's of records like the one above, traversing down
then up, then across and so on until you have all the info you need. That's
a lot of code and a lot of traversing. All this code also means that someone
has to maintain it. To illustrate this here's a scenario. We have all this
data stored in hierarchies and everything is going great. We have a bunch of
applications (apps) working off our data traversing our fixed, that's right,
structures to get the data it needs. Then your boss comes along and says, I 
need to do some analytics but because of your structure it is running really 
slow. You need to change it, so we can meet our performance requirements. Ok,
not a problem, you say and happily go about designing new structures to meet
your bosses new requirements. After you finished designing your model you go
and implement it and before you know it you have a hoard of angry developers
in your office demanding you change your new model back to the old one 
because you broke all of their code. This highlights one of the pitfalls of
hierarchies, once you've written code to traverse it and you change the
hierarchy, you have broken all of your code and queries. This is why [E. F. Codd's](https://en.wikipedia.org/wiki/Edgar_F._Codd)
paper on relational modeling was, and still is, so ground breaking, he 
purposed a solution to the updating hierarchy problem mentioned above. His
solution is to flatten out the hierarchy and spread all the data across
flat structures, called tables. These flat structures did two things, 

* They helped to standardize the structure of data which makes queries with in
tables very efficient.
* They forced complex hierarchies to be flattend out thus loosing context and
forcing modelers to ask unnatural questions.

So how does [tabular (relational)](https://en.wikipedia.org/wiki/Relational_model) 
data work and how do you model it?

NOTE: TALK ABOUT GENERAL PRINCIPALS OF E.F. CODD'S PAPER
    - natural keys
    - relational modeling is modeling the relationships with in a table

NOTE: SHOW A SIMPLE RELATIONAL MODEL
NOTE: SHOW HOW IT IMPROVES ON HIERARCHIES
NOTE: SHOW HOW IT LOOSES INFORMATION AND REQUIRES MORE ABSTRACT THINKING


