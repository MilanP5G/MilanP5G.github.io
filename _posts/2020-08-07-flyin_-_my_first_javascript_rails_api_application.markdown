---
layout: post
title:      "FlyIn - My first Javascript/Rails API Application"
date:       2020-08-07 12:32:50 -0400
permalink:  flyin_-_my_first_javascript_rails_api_application
---


I felt this was more of a rocky journey than my previous projects/applications. It's been a great learning curb for sure!

I decided to create an application that allows users to post up countries that they have visited along with places they have visited, within those countries. Each `place` would have a description of the place they visited.

My first job was to work on my backend. I decided to go for the two obvious models - `Country` & `Place` - and add their attributes. 

`Country` migrations ended up as:

```
class CreateCountries < ActiveRecord::Migration[6.0]
  def change
    create_table :countries do |t|
      t.string :name

      t.timestamps
    end
  end
end
```

`Place` migrations:

```
class CreatePlaces < ActiveRecord::Migration[6.0]
  def change
    create_table :places do |t|
      t.string :name
      t.string :description
      t.integer :country_id

      t.timestamps
    end
  end
end
```

As both countries and places would accept images, I used active storage to make it possible and therefore saving the image on the backend.

The backend was not so much of a pain (minus the active storage, which I had to play around with the controllers) but it was the JavaScript that was more of a long journey. 

I first created separate files for each class and a main file titled...you guessed it...the typical `index.js`. 
I had to write out the attributes within the constructor of the classes. The country would have an id, name and an image. The place would have an id, name, image, description and country id.

```
class Country {
  constructor(id, name, image){
    this.id = id
    this.name = name
    this.image = image
  }
...
}
```


```
class Place {
  constructor(id, name, image, description, country_id) {
    this.id = id
    this.name = name
    this.image = image
    this.description = description
    this.country_id = country_id
  }
	...
	}
	```
	
Next, I jumped straight into blocking out the functions of my application. Most of these functions would include ajax calls - `fetch` requests that take in a URL parameter to receive data from the backend, convert that data to `json` and then manipulate the json through another function.
	
For example, when I wanted to render all countries (as soon as a user views the page) I created a fetch function to collect all the countries created and then send those countries to the `renderCountry` function:

`
function fetchCountries(){
  fetch(`${BASE_URL}/countries`)
  .then(resp => resp.json())
  .then(countries => {
    for (const country of countries){
      let cntry = new Country(country.id, country.name, country.image_url)
      cntry.renderCountry()
    }
  })
}
`

I also used `static` methods which are called upon the class itself rather than the instances. I used a static method to create a delete action. I had to get the id of the object I am deleting, in order to delete the correct country/place and so it is removed on the backend as well as what is displayed to the user. An example of this static method is for the countries:

```
static deleteCountry(event) {

     let id = null
     if (event.target.classList.contains('dlte-btn')) {
       id = parseInt(event.target.dataset.id)
     } else {
       id = parseInt(event.target.parentElement.dataset.id)
     }

     fetch(`${BASE_URL}/countries/${id}`, {
       method: "DELETE"
     })
     .then(resp => resp.json())

     document.location.reload()
  }
	```
	
	Overall, this was a tough journey as there was a lot of difficulty with syntax, especially with fetch requests. I truly appreciate this project though as I have learnt a lot in a short space of time and have worked with a few elements outside of what I learnt through the curriculum.


