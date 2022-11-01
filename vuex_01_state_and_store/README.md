# vuex_01_state_and_store

1. vuex is an addon to vuejs, which makes state management easier
2. in the app component we are managing the whole state - registrations and users,
3. in registrations.vue file - can sign up, by clicking on register button, fires the registerUser method, this then emits an event 'userRegistered', and passes the user
4. it also sets the registered state on the user to true
5. user passed into registrations component as a prop 
6. we are listening to the userRegistrated event in App.vue, and when it is fired, we are triggering the userRegistered method here, there we are setting a date and we are pushing a new registration on our registrations array. 
7. when a user unregisters, then we are firing the user unregistered method and so on
8. state management in app.vue file - by passing props to the other components, and listening to their events
9. this method is preferred for smaller applications
10. for bigger applications, with more components, inteacting with users and registrations, and also with other parts of application state
11. state basically refers to the variables or the values of the certain properties, we want to keep around, because multiple components use them and the user interacting with our app changes them
12. a better pattern, add on, which handles this, is vuex for bigger applications
13. summary: how to get started with vuex, how to set it up, and how to use it in its very very basic and not yet final form
14. to set up vuex, go to the terminal and run : npm install --save vuex
15. now we can set up vuex in the main.js file, but a better convention is to do this in a store.js file
16. store because vuex is all about having a central store which holds our state and which allows us then to manage this state in the end, therefore we call this file store.js
17. to create a store here, import vue, vuex, add vuex as a plugin via the vue.use() method here, this will unlock some additional properties and methods we can use, and then to set up the store, export it because we want to use it outside of this js file and we can name it or store it in a constant named store. store is then created with the new keyword / operator
18. vuex package that we are importing has this Store object or constructor we can instantiate here. to the store, we need to pass a javascript object configuring the store. 
19. to configure such a store, every store has to have is the state, so this state property, this is a reserved word vuex will recognize, state is now a javascript object, and here we could have users and registrations.
---
export const store = new Vuex.Store({
    state: {
        registrations: [],
            users: [
                {id: 1, name: 'Max', registered: false},
                {id: 2, name: 'Anna', registered: false},
                {id: 3, name: 'Chris', registered: false},
                {id: 4, name: 'Sven', registered: false}
            ]
    }
})
---
20. now we are using a store
21. import the store in main.js file
22. then add that store to the root vue instance
23. with that, store is set up in the store.js file, initial state of that store is registered, and store was added to the main root vue instance, which manages the whole app, and with the store being registered there, we can access it from inside the application
24. to access it, in registration.vue file
25. we can remove props, and instead add a computed property, in the computed property of the vue instance of this component, we can give it any name, -users
26. $store is added because we are registering vuex here with vue.use()  
27. accessing the array of users from the store in the registration.vue file - this.$store.state.users;
28. can get rid of prop binding and event in app.vue
---
this.$store.state.registrations.push({
        userId: user.id,
        name: user.name,
        date: date.getMonth() + "/" + date.getDay(),
      });
29. manipulating the store and the state in the store like this is not a good practice
30. userRegistered can now be gotten rid of in App.vue
31. can remove props from registrations.vue and add a computed property - get our registrations, - which is also fetched from the store-state-there the registrations array
32. this gets the registrations from our global store, now when we unregister, 
33. const user = this.$store.state.users.find((user) => {
        return user.id == registration.userId;
      });
finds the user by its user id, which is saved in the registration
34. switch user registered to false, remove a registration 
35. change computed total property, can get rid of methods in App.vue, can get rid of computed property, data, prop passing and event listeners in app-registrations component
36. dont dissapear from the left, dont get marked as registered 
 users() {
      return this.$store.state.users.filter((user) => {
        return !user.registered;
      });
    },
37. now with vuex, and this central store and state, ... app.vue is more leaner, code is moved to other two components, our state - registrations and users array is kept in one central state, our store here, which we access from both the components
38. we dont have to emit events and pass props and so on