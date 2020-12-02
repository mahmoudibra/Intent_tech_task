# Intent Technology Task

## State Management

**Question 1:**

Describe the pros and cons of different state management solutions to maintain synchronization between local data state for each user of Basket, and a backend service ? 

**Answer:**

We are having a lot of state management solution that we can use to implement this sync between local and remote data lets start by defining most of them and there pros and cons in general: 

#### setState
  
This is the default state management approach that came with flutter, it helps us to rebuild our widget tree if there are any changes. 

##### pros: 
- very easy to understand. 
- perfect for small projects. 
- a great way to handle the ephemeral state.

##### cons: 
- Not good while handling a global or group state for example if you want a state change in the child widget reflect a change on upper widgets. 
- If the app goes large having a set state will prevent your app from calling smoothly and will be a big maintenance issue. 
- most of the time using the set state as state management drives people to mix UI with logic.

#### ScopedModel and Provider
    
From my point of view, ScopeModel and Provider both of them are working to deliver and pass data downside the tree rather than making this job manually, Provider gives more functionality and Flixebility above ScopeModel. 

##### pros: 
- by following this pattern business logic and UI are totally separated from each other. 
- setup data flow downside the tree without any effort. 
- you don’t have to build the whole UI for every change, we can rebuild only a single widget inside the child widget without rebuilding all the trees.

##### cons: 
- changing state of an object will be triggered every time by default, even if you don’t want to trigger this change.

#### Bloc pattern
    
Much more an architecture than Provider, scope model, set state, it’s something similar to MVVM, and MVI, is based on using a stream that process some action and another stream that exposes this results to the UI. I usually prefer to use it with Provider to expose Bloc to the UI. 

##### pros: 
- Code easy to read.
- Code easy to maintain. 
- Code easy to debug. 
- Code easy to test. 

##### cons: 
- Time-consuming. 
- More boilerplate code. 
- Can’t rebuild specific child widget that the new state only will reflect on it.

From my point of view, I will choose Bloc as a state management pattern, with the usage of Provider pattern for exposing Block class to the UI in an easy way, It seems that using Provider from performance matter is better because we can rebuild only a single widget that should be affected by changing the state, in Bloc we rebuild the whole children and we don’t have this deep control, but I prefer code readability, maintainability and easy to test over this very little performance difference. 


**Question 2 :**

Consider potential issues a user may experience that would influence the state management system you would choose ? 

**Answer:**

If the UI is too complex and deep, rebuilding the whole UI every time state changes using Bloc it may cause in old devices with poor specs some performance issue.



## Widgets and Deployment Targets

**Question 1:**

Describe a project, folder and file structure to effectively build and maintain widgets for mobile and web extension targets ?

**Answer:**

In terms of a project, folder, and file structure it will always remain the same from my point of view whether if we are building a mobile app only or a mobile app that supports web or web extensions, almost all the tricky part will be on the widget itself, I will assume that the architecture follows separation on concerns principle and it totally separates all our business logic from our views or UI parts, for example, I would love to follow Uncle bob clean architecture and Bloc pattern for UI and business logic separation 

The two things that I will take to my mind while designing the same code base for mobile and web is the third party integrations, they will be a different way of implementation between mobile(android/ios) and web, so I will take to my mind to design an abstract contract to be implemented and executed on different ways depends on the current target whether mobile or web. 

The same concept goes for how to access native browser APIs, accessing native APIs will be different between mobile and web.


**Question 2 :**

Discuss what you believe are the most important considerations for widgets that deploy to different targets such as mobile and web ? 

**Answer:**

From my point of view, the most important consideration is going to be around how should we build a responsive widget that should be smart enough to rebuild itself in different ways based on the different screen sizes and layout especially the big difference between mobile and web.  

Flutter provides build-in responsive design widget and packages to help us design complex user interface for different screen sizes, like Material BreakPoint, Aspect Ratio, Layout orientation,  Layout Builder, Media Query, Fitted Box.  

we can also use  responsive_framework | Flutter Package.
It has an AutoScale feature, that shrinks and expands your layout proportionally, preserving the exact look of your UI. This eliminates the need to manually adapt layouts to mobile, tablet, and desktop.


## Asynchronous Dart
 
From my point of view, using Isolate/threads in dart will introduce a layer of complexity if we overusing them, so when to use isolates, We should use them whenever you think there is a lot of computation that needs to be offloaded from the main thread. 

For example: 
* Let say you want to execute a network call and you want to process that data that you just received. and that data contains about a million records that alone will hang your UI.
* You have some image processing tasks that you want to do on-device these kinds of tasks are highly computational as they have to deal with lots of number crunching operations which may lead to frozen UI or legginess in UI.

**Question 1:**

Describe the pros and cons of using Dart isolate asynchronously manage animation event loops

**Answer:**

##### pros: 
- As long as there's a computation in animation, then switching this computation into Isolate should increase app performance. 

##### cons: 
- Using a lot of Isolate will introduce a layer of complexity in any codebase. 
- Isolates don't share any state and can only communicate using message passing.

**Question 2:**

consider and discuss potential implications of using Dart isolate in this way on codebase structure, maintainability and testing

**Answer:**

As mentioned in the previous answer, introducing Isolate will add a layer of complexity to our codebase, code maintainability will be the same if communication with any Isolate task will be through a will abstracted layer, so it's a matter of abstraction, for the testing part the challenge should be on testing if two threads Main and Isolate are actually communicating with each other with the correct data or not. 



