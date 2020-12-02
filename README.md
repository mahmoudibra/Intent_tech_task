# Intent Technology Task

# State Management

**Question:**

Describe the pros and cons of different state management solutions to maintain synchronization between local data state for each user of Basket, and a backend service ? 

**Answer:**

We are having a lot of state management solution that we can actually use to implement this sync between local and remote data lets start by defining most of them and there pros and cons in general: 

#### setState
  
This is the default state management approach came with flutter, it helps us to rebuild our widget tree if there’s any changes. 

##### pros: 
- very easy to understand. 
- perfect for small projects. 
- a great way to handle ephemeral state.

##### cons: 
- Not good while handling a global or group state for example if you want a state change in child widget reflect a change on upper widgets. 
- If the app goes large having set state will prevent your app from calling smoothly, and will be a big maintenance issue. 
- most of the time using set state as state management drives people to mix UI with logic.

#### ScopedModel and Provider
    
From by point of view ScopeModel and Provider both of them are working to deliver and pass data downside the tree rather than making this job manually, provider gives more functionality and Flixebility above ScopeModel. 

##### pros: 
- by following this pattern business logic and UI are totally separated from each other. 
- setup data flow downside the tree without any effort. 
- you don’t have to build the whole ui for every change, we can rebuild only a single widget inside child widget without rebuilding all the tree.

##### cons: 
- changing state of an object will be triggered every time by default, even if you don’t want to trigger this change.

#### Bloc pattern
    
Much more an architecture than provider, scope model, set state, it’s something similar to MVVM, and MVI, it based on using stream that process some action and another stream that expose this results to the UI. i usually prefer to use it with Provider to expose Bloc to the UI. 

##### pros: 
- Code easy to read.
- Code easy to maintain. 
- Code easy to debug. 
- Code easy to test. 

##### cons: 
- Time consuming. 
- More boilerplate code. 
- Can’t rebuild specific child widget that the new state only will reflect on it.  

From my point of view i will chose Bloc as a state management pattern, with usage of Provider pattern for exposing Block class to the UI in an easy way, It seems that using provider from performance matter is better because we can rebuild only a single widget that should be affected by changing the state, in Bloc we rebuild the whole children and we don’t have this deep control, but i prefer code readability, maintainability and easy to test over this very little performance diffrence. 
