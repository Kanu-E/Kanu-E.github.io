---
layout: post
title:      "**Using Ruby Methods to Format User Input**."
date:       2020-07-08 19:33:17 +0000
permalink:  using_ruby_methods_to_format_user_input
---


While using any app, users require some level of flexibility, surely as a developer you'd want to limit what a user can input (that's what error messages are for);  but then again the users can input can come in different formats. Ruby being the brilliant language that it is has built in methods to help us reformat the user's input to giving the desired return.

In creating my "My LFC App, I used the strip and downcase methods to reformat users input.

Strip is a string Class method that takes in a string and returns a copy of the string after removing any a copy of str with leading and trailing whitespace.

Example:

 "    hello    ".strip
=> "hello"
 "\tgoodbye\r\n".strip
=> "goodbye"

Downcase is a method that takes in a string and returns a copy of the string with all uppercase letters replaced by their respective lowercase counterparts.

Example:

"HELLO".downcase
=> "hello"
"Goodbye".downcase
=> "goodbye"

A combination of the downcase and strip methods makes it so that any user input can be reformated so that any input will match the desired input.




