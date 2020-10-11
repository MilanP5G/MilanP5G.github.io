---
layout: post
title:      "Your Galaxy - My first React/Redux project"
date:       2020-10-11 15:05:30 +0000
permalink:  your_galaxy_-_my_first_react_redux_project
---


This has been a wonderful journey but by far the most turbulent! Dealing with React/Redux made this last project more of a tough one as they seem to be very abstract (especially when Redux comes into the picture). Nevertheless, I came through to build an application that can benefit both Samsung users and Samsung themselves. 

The application I created is called "Your Galaxy" which allows Samsung users to upload devices that they own and write out pros and cons. Users also have the ability to report any bugs they find along their usage journey. Great for Samsung, as they can collect this data to improve their next generation of devices and great for users, as they can get immediate help for any bugs/issues. 

Starting off with the backend, I used a Rails API with 3 models: `phones`, `posts` & `comments` (Users can add comments on their report posts to give updates to Samsung)

Moving onto the frontend, I first worked on creating a phone form, phone, phones and phone show component. Breaking down components into sub-components helps to understand how individual pieces of data function and helps deal with bugs better (something I definitely learnt whilst building Your Galaxy). In terms of these different components, posts and comments were very similar.

The attributes for a phone are: `title`, `image`, `pros` & `cons` and how does this link in with state and props?
Well the state is an instance of a component that controls its behaviour. So state is information within a component that can potentially change during the lifetime of its component. Those 4 'attributes' would then be the state values of phones and be passed down to child components as `props` (property values). While state is modified, props are 'read-only' - meaning they never change in components.

For example, here is my `Phones Component` that is being passed props (not being modified) to map over and display all the phones created:

```
const Phones = props => {

    return(
      <div>
        {props.phones.phones.map(phone => (
          <Phone phone={phone} key={phone.id} />
        ))}
        <Link to='/phones/add' >
            <button className='add-phone'>+</button>
        </Link>
      </div>
    );
};

export default Phones
```

Redux is where the road started to look more challenging but again, while getting my hands stuck into building, it started to make more sense!

As our application grows, having Redux manage state seems wise as it places our state in a central store that holds the entire state of the application, which we can then access specific data from, in several components where needed. This is definitely a great thing, as passing data to child components (if there are many) would become a nightmare and confusing!

Finally, I want to express how this final project was a big scare as I was struggling a lot, but with persistence I was able to create my application and will definitely add more features to it! I appreciate all that that I have learnt and glad I was able to read into and use aspects of React that weren't covered through the curriculum.



