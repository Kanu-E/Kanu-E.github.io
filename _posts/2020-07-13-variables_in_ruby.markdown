---
layout: post
title:      "Variables in Ruby"
date:       2020-07-13 19:50:57 -0400
permalink:  variables_in_ruby
---


In ruby, a variable is the name that can be assigned to an object we could refer to them as memory locations for data that can be used in a program. For exampe:

worlds_best_team  = "Liverpool FC".

Here the string "Liverpool FC" can be associated with the variable worlds_best_team therefore whenever ruby encounters worlds_best_team it will know that it should associate it with "Liverpool FC".


We have 4 different kinds of variables in ruby depending on the scope within which they operate; global  class, local and instance variables.

1. Global Variables exist within the entire scope of the program (it is believed that when programmers should not use global variables when writing their code and they should only be used by the interpreter). Global variables begin with $. Uninitialized global variables have the value nil and produce warnings with the -w option. 

Here is an example of the use of global variables 

$worlds_best_team = "Liverpool FC"

class Team
   def best_team
      puts "The best team in the world is  #$worlds_best_team
   end
end

team_object = Team.new
team_object.best team

The best team in the world is Liverpool FC

Ruby still knows the best team in the world is  Liverpool FC even though it is written outside the scope of the class.

2. Local Variables exist locally within the construct that they are inside and variables cannot be accessed outside that construct. For example if a local variable is declared within a method, it cannot be accessed outside that method. They begin with a lowercase letter or _.

Here is an example of a local variable

def the_best_team
   lfc = "Liverpool FC"
	 "The best team in the world is #{lfc}."
end

puts the_best_team 

The best team in the world is Liverpool FC.
=> nil

However;
puts lfc

Traceback (most recent call last):
        4: from /usr/local/rvm/rubies/ruby-2.6.1/bin/irb:23:in `<main>'
        3: from /usr/local/rvm/rubies/ruby-2.6.1/bin/irb:23:in `load'
        2: from /usr/local/rvm/rubies/ruby-2.6.1/lib/ruby/gems/2.6.0/gems/irb-1.0.0/exe/irb:11:in `<top (required)>'
        1: from (irb):11
NameError (undefined local variable or method `lfc' for main:Object)

This is because lfc is within the the_best_team method and as a local variable cannot be called out of it.


3. Class Variables are variables that are shared by all instances of a class and when one instance changes the value of the variable, it is available across different objects. Class variables can be thought of as global variables within the context of a single class.
They begin with the @@ sign


4. Instance Variables  are similar to Class variables but their values are local to specific instances of an object so as long as you are within the scope of the instance you can read the variable but no other part of your program. This is called internal state.
They begin with the @@ sign

Example for class and instance variable;

class Teams

@@no_of teams_lfc_is_better_than = 100

def initialize(name)
  @team_name = name
	@@no_of teams_lfc_is_better_than += 1
end

def teams_lfc_is_better_than
  puts  "Now #{@team_name} has been established Liverpool fc is better than #{@@no_of teams_lfc_is_better_than} teams."
end


end

abc_team = Teams.new(ABC FC )
xyz_team.teams_lfc_is_better_than
Now ABC FC has been established Liverpool fc is better than 101 teams.

xyz_team = Teams.new(XYZ FC )
xyz_team.teams_lfc_is_better_than
Now Xyz FC has been established Liverpool fc is better than 102 teams.













