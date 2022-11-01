# vuex_04_actions

1. this project now has central store, getters, mutations, but there is one limitation / possible limitation
2. if we had any async code being executed as part of a mutation, that wont work... mutations always have to run syncronously, 
3. and it makes sense because mutations are the methods directly manipulating our store, so it would be kind of bad if they had some async nature to them because that would mean that when we commit a mutation, it might not run immediately, so if we then get the value thereafter, it might not have changed yet, 
4. so therefore it makes sense that mutations have to run synchronously but what if we have some http call which gets us a value, which we then want to use in our commit, .. how would we handle this, because with mutations, as we use it right now, that is simply not possible, or not possible inside of our store at least, 
5. we could use actions to change this, 
6. summary: what actions are, how to use them and how we can combine them with asynchronous code
7. we can set up actions in the store.js file in the store, we can add a new property named actions and this also is an object, here we can choose any name for the actions, and we can name it register, and oftentimes we will have the same name for the action and the mutation, because is the action is kind of a middleman, running before we actually commit the mutation
8. here, the action also gets an argument, and this argument actually is the context of this action, the name is ofcourse up to us, the name we assign to this argument, but will be the context, ... and context is almost the same as the store, but not completely the same, therefore it is a different name, 
9. now on this context, we can simply run the commit method, : context.commit();, because it is almost the same as the store but not entirely, .. technically it is a different object, but it does have a commit method
10. and therefore here, we can commit the register mutation
11. now ofcourse, like a mutation, the action can also receive a payload, .. so either a payload object or the value itself, and then we can also pass this as a second argument to the commit method, because somehow we need to get that value to the mutation,
12. now, with that action set up, we can go to the registration.vue file, where we now directly commit the mutation, and here we can now instead, :
this.$store.dispatch, so like mutation, we are not calling action and then executing the action itself, instead no, we have to dispatch method and this means we dispatch the actions, 
13. here, we do need to pass the name of the action, which is register, and then, as a second argument, the payload, user.id,.. 
 methods: {
    registerUser(user) {
      this.$store.dispatch("register", user.id);
    },
  },
14. or alternatively, like with a mutation in the Registrations.vue file, we could also dispatch it with one single object where we have the type, as a set property, and then any other amount of properties we want to use, and in this case though, we need to make sure that here we are getting the payload in general, and we access our values like using find method, in the unregister method
15. in the action, we are dispatching it, the app behaves the exactly like before, .. what we gained here by using an action here is, right now, nothing, but now we can execute async code here inside register in actions.
16. inside of a mutation, we cant run asynchronous code, we always have to manipulate our state in a syncronous manner, but here in the action, before we actually commit it, we can run asynchronous code 
17. and we would have been able to run that simply in our component, before commiting, but then again, we would have that mixture of having some logic in our component and some logic in our store, we really want to have all the store and state related logic in our store though
18. therefore, we run the action here, or the code, we can simulate some async action by simply setting a timer over 1 second, and after that second is over, then we can commit register
19. with this approach, if we have a look, and click register, it takes 1 second, before it actually happen, unregistering happens instantly though, because it didnt set a timer there
20. so, here we can and we are allowed to run asyncronous code, in mutations we are not allowed to 
21. since we are mostly only interested in the commit method here, we dont have to get the full context object, we can also use another es6 feature called deconstruction, where we simply can use this syntax here { commit } - commit or any name we choose, to simply extract, and then the name of the property we want to extract, to directly extract that property from the object we are getting as an argument, throwing away the other properties, but if we dont need them, thats okay, and with that we can leave out the context thing, and directly get the commit method, in this case 
22. so this is an action here, running some async code, now since we dispatch our action here, in the registration.vue file, we have the same behaviour as before, with that we finished our vuex implementation using the state in our central store, using getters to get the state or get some values depending on that state, using mutations to change the state and using actions to trigger mutations possibly after running some async code before doing so 
23. how vuex works, why we might want to use it, and how we could use it