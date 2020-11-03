---
layout: post
title:      "Rails Nested Forms"
date:       2020-11-03 14:47:20 +0000
permalink:  rails_nested_forms
---


Some might say it is such a cliche to say that rails is magic but when you actually begin to scratch the surface of what the web application framework is capable of, it is not difficult to see why people tend to refer to it as magic.

Some of the outstanding things about rails are its abilities with form. Here will be taking a look at what rails nested forms are and how they are Implemented.

A nested form is a form within a form and it allows for the possibility to create the instance of a model through an associated model. 

It does not matter the association between the models: has_many, belongs_to, has_one or has_and_belongs_to_many associations can all have nested forms and the implementation is similar (a few minor changes exist depending on the association). 

For the purpose of this blog, we will be using a belongs_to association to build our nested form. Let's assume we are trying we have an association of a football club that has many fans and a fan belongs_to a football club (what kind of fan has more than one club).

We are going to try to create a nested form that allows us to create a new football club object using a fan form page.

Let's begin by showing the models. For the football club you may have;

```
class FootballClub < ApplicationRecord

    has_many :fans
		 # Attributes: name:string, motto:string
		
 end
```

and for the fans, you'd have;

```
class Fan < ApplicationRecord

    belongs_to :football_club
		
		 # Attributes: name:string
    
end
```


With the associations established we will also want to add the nested attributes model accepts_nested_attributes_for this will give the model to an attribute's writer football_club_attributes= as shown below:

```
class Fan < ApplicationRecord

    belongs_to :football_club
		
		accepts_nested_attributes_for :football_club
		
		 # Attributes: name:string
    
end
```

With the nested attribute model added, we would then go to our controller and add the the build_association method to the variable in the new model.

```
def new
    @fan = Fan.new
    @fan.build_football_club
  end
```

Now if you go to your form in the views it may currently look like this:

```
	
	= form_for @fan do |f|

  // Fan attributes

    = f.label :name
    = f.text_field :name  


  = f.submit

```

Now you will want to add the fields for the football fan association, rails provides the fields_for [form helper](https://guides.rubyonrails.org/form_helpers.html) to the form like this;

```

	= form_for @fan do |f|

  // Fan attributes

    = f.label :name
    = f.text_field :name  


  // football_club attributes
	
  = f.fields_for :football_club do |f|
	
    = f.label :name
    = f.text_field :name

    = f.label :motto
    = f.text_field :motto

		
		= f.submit
```

Now we have our forms all set up the the final step will be to update our [strong paramemters](https://edgeapi.rubyonrails.org/classes/ActionController/StrongParameters.html) to incdlude our nested attributes like so;

```
def fan_params
  params.require(:fan).permit(
    :name, 
    football_club_attributes: [ :name, :motto]
  )
end
```

And that's it rails allows us to create a nested form using the steps stipulated above.






	


