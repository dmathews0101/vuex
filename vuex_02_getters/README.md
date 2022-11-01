# vuex_02_getters

1. adding getters and using it
2. here there are two components in this project - registration, where we can register a user, and registrations, where we can see all registrations
3. here we are always fetching the registrations or the user array, in the computed property, 
4. we can outsource this logic, into our store, so that this code gets even shorter, that we dont have to filter here in the registration.vue file for example
5. that would be benefitial, because if we had another component, which also needs a list of all registered or unregistered users, then we would simply have to duplicate this code
6. duplicating code is not a good idea, instead outsourcing this filter into the store and then somehow simply getting the list of filtered users would be much better, and this is what a getter can do for us
7. we define getters in the store file, where we have the state, we simply add a new property, getters - is a javascript object, and there we simply define any name, - unregisteredUsers, which is a method, and here, like in a computed property, we pass the code which defines what unregistered users are and which in the end gives us back a list of unregistered users
8. a getter always needs to return something, 
9. vuex passes the state to each getter defined in our object here, so we can receive the state as an argument, which is passed automatically by vuex, and therefore we can then simply say, 
---
getters: {
        unregisteredUsers(state) {
            return state.users.filter((user) => {
                return !user.registered;
              });
        }
    }
10. this is returning a list of unregistered users
11. to use the getter in our component, here, we can simply define a computed property, and we need to use a computed property for this , and there we can still access the store, but now not the state directly, but instead the getters, and here, the unregistered users getter, not like a method, just like a property.
12. application still works the same, but we took the logic for filtering, for getting this list, and removed it from this component - registration.vue, and instead put it into the store, the place where it should be.
13. we can do the same for registrations, here we have 2 computed properties, so we can set up our store getters here too,  
        registrations(state) {
            return state.registrations; 
        },
        totalRegistrations(state) {
            return state.registrations.length;
        }
---
14. computed: {
    registrations() {
      return this.$store.getters.registrations;
    },
    total() {
      return this.$store.getters.totalRegistrations;
    },
  },

15. if we have multiple getters, or if we are using multiple getters in one component, as in registrations.vue file, there is an easier way to quickly map those getters to computed properties
16. vuex gives us a nice helper, we can import it, it is called mapGetters
import { mapGetters } from 'vuex';
17. mapGetters allows us to map our getters,.. now in the computed property in our vue instance, in this component, we can now say, mapGetters(), which is executed like a method, and it gets either an array or an object, depending on whether we want to keep the name of the getter in the store or want to assign it to a different name in our component
Array:
 mapGetters([
      // list of all getters we want to use
    ]), or
 mapGetters(['registrations', 'totalRegistrations']),
18. Map: in order to use a different name, in order to map it, we have to pass an object instead, here we simply have our name first , so the name we want to use in this component, then as a string again, the name in the store, the name of the getter,.. now we can get rid of the other two computed properties
19. mapGetters is a method, computed is an object, mapGetters gives us back an object, so what we can do is simply set mapGetters to be the value of this computed property
computed: mapGetters({
    registrations: "registrations",
    total: "totalRegistrations",
  }),
20. computed, a property in a vue component, simply expects to get an object and this will return us an object, an object with those mapped getters
21. and if we had used the array, without mapping it manually to the different names, behind the scenes , it would still have given us an object where we have the names mapped,... name and getter name would be the same then
22. if we had additional computed properties, mapGetters takes up our whole computed properties space in our instance, so of we had any other computed property, not related to a getter, we would add it using es6 syntax,
23. in this case, we have the spread operator ..., what this will do is it takes the object, mapGetters returns an object in the end, and simply pulls out the properties in this object and distributes them in this parent object,  
24. so it gets the properties out of the object returned by our getters and puts them into the computed property object, thus allowing us to add additional computed properties..
computed: {
  ...mapGetters({
    registrations: "registrations",
    total: "totalRegistrations",
  }),
  additional() {
  }
25. right now, this would not work because, this spread operator is not supported by this vue cli setup, as of now, we need a special package to support it ,babel-preset-stage-2 , because it is a stage 2 preset
26. npm install --save-dev babel-preset-stage-2
babel is the transpiler transpiling our es6 to es5 code, 
27. with that added, we also need to add it to the .babelrc file, here we need to add new array, holding this stage-2 preset
28. this will allow the app to compile correctly, though we need to restart the npm run dev process, because, we added something, we changed the build process
29. now we can use the mapGetters method to conveniently, get access to multiple getters and map them to our own properties, .. we can also map it manually as in the users() computed property in Registration.vue
30. we can use mutations, which is a better way of changing the state, because the way used here is not the optimal one