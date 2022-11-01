# vuex_03_mutations

1. mutations, is a tool which allows us to edit the state in a better way 
2. here we have methods where we actually manipulate the state, we can improve this
3. in Registration.vue, here when we register a user, we are changing the registration state on the user itself, and we are pushing a new registration with the date of that registration, to our registrations array
4. we can move that code to store.js, we edit the state through something called a mutation, because it mutates, it changes the state
5. we can add mutations, just like we add getters by adding the mutations property to our store and with that added here, we can now set up a mutation, for example the register mutation
6. now, like the getters, this receives the current state, and it needs that because it will change it,.. here, we can copy in the code ..
7. now in the register mutation, we are changing the user state, but we dont know which user, therefore, we have to pass it to the mutation
8. one cool thing about mutations is that we can pass the user or any payload, so as a second argument we can get any payload we pass, this can be an object or just a value 
---
 mutations: {
        register(state) {
            const date = new Date();
            const user = state.users.find(user => {
                user.id = userId
            });
            user.registered = true;
            const registration = {
                userId: userId,
                name: user.name,
                date: date.getMonth() + "/" + date.getDay(),
            };
            state.registrations.push(registration);
        }
    }
9. this is a mutation, now making sure that we added the state in a different way, we can do the same for the method in the registrations.vue file
10. unregister method gets the state and the id of the registration / userId, .. but before, we have to search for the user, set user registered to false, and find the right registration
        unregister(state, userId) {
            <!-- search the user by user id -->
            const user = state.users.find(user => {
                return user.id == userId;
            });
              user.registered = false;
              <!-- find right registration -->
              const registration = state.registrations.find(registration => {
                return registration.userId == userId;
            })
            <!-- alternatively we can use findIndex() to directly get the index -->
            state.registrations.splice(state.registrations.indexOf(registration), 1);
        }
11. now to call a mutation, we dont call the mutation directly, so in the method which gets fired when we click on the register button, we can access this.$store.commit(); , and commit can be called in two ways, the first argument is the name of the mutation as a string, .. here it is the register mutation, that we want to call, and the second argument is the payload, here, it is simply the user.id, though, that could also be an object or an array, or anything,.. this is one way of calling it
12. in the registrations.vue file, the other way is : this.$store.commit(); and here we can pass an object, where we have a type property, which now is the name of the mutation, then the second property is the payload - userId
---
methods: {
    unregister(registration) {
      this.$store.commit({
        type: "unregister",
        userId: registration.userId,
      });
    },
  },
13. so now this works, but now using mutations to have a better way and a preferred way of accessing and manipulating the state in the store, 
14. with that we have improved the project even more, now our logic is mainly in the store ,and in the components we have very less code,.. that is the good thing about using vuex, having our logic in one central place and if we now want to make changes, or use the same mutation to make the same edit, from multiple places in our app, it is now very easy, because all we now have to do is call commit, or if we want to get a value, we can call that getter and it is very easy to manage the project.
15. but there is one big limitation to mutation - async