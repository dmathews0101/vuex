# vuex_05_bonus

1. 2 additional tiny tweaks, or 2 - 3 things to know
2. in vuex documentation, vue developer tools, normal tools show us the components on the page - with the values used there, 
3. but we also have the vuex tab, here we can time travel through our list of states, to debug our application, and quickly see how the application looked like at another point of time
4. we can also see the payload of each commit and so on,.. we can also see the state of the commit,
5. we can also, if we dont want to jump back temporarily, but really reset our app, can simply click revert, and we are back to that state, or we can say we reverted that state
6. for example, if we unregister and then revert that, then we are back to that state ... so this is a great tool for debugging the app
7. if we look at the app at store.js file, this is not a complex app, but this store.js file is already somewhat big, and has a lot of code in it
8. we can split it up and we usually see it in bigger projects, there we typically create a new folder, which we can name store for example, or could also name it vuex and we can more the store.js file in there, but we can also create some other files here, one for the getters, one for the mutations, and one for the actions
9. now, with these extra files, what we can do is, for example ,.. in the actions file for example, export something, a default object, then we can go to the store.js file, to our actions, and simply copy that method, or all the methods we have there and put them as methods into the object we are exporting in this file,
10. then we can simply go to the store.js file, and import actions from the actions file, this actions object, and we can simply assign it as a value to our actions property, (actions:actions) .. or use es6 to automatically assign it (actions), since it has the same name
11. we can do the same for the mutations, so we can grab the whole mutations object here, go to the mutations.js file, export the default object here to the object we grabbed from store.js, and go to the store.js file to now import the mutations there, and we can assign them to the mutations property, or use es6 since the name is the same
12. and we can do the same for the getters, export default object that one here, and import the getters in the store.js file, and assign them here, again using es6 as a shortcut 
13. and with that, the store.js file is much leaner, now the app would be broken though because we also moved the store.js file, so we have to make sure to adjust the import in the main.js file too
14. now with that, if we save this, and go to the application, reload it, it is working like before, but now the store.js file is much leaner, and we have outsourced this into different files - mutations, getters, actions and so on
15. and with that, we can use vuex to improve our applications with that