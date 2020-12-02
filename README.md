# Intent Technology Task

## State Management

**Question 1:**

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



**Question 2 :**

Consider potential issues a user may experience that would influence the state management system you would choose ? 

**Answer:**

If the UI is too complex and deep, rebuilding the whole UI every time state changes using Bloc it may cause in old devices with poor specs some performance issue.



## Widgets and Deployment Targets

**Question 1:**

Describe a project, folder and file structure to effectively build and maintain widgets for mobile and web extension targets ?

**Answer:**

In terms of project, folder and file structure it will always remain the same from my point of view whether if we are building a mobile app only or a mobile app that supports web or web extensions, almost all the tricky part will be on the widget itself, i will assume that the architecture follow separation on concerns principle and it totally separates all our business logic from our views or UI parts for example i would love to follow Uncle bob clean architecture and Bloc pattern for UI and business logic separation 

The two things that i will take to my mind while designing the same code base for mobile and web is the third party integrations, they will be different way of implementation between mobile(android/ios) and web, so i will take to my mind to design an abstract contract to be implemented and executed on different ways depends on the current target wether mobile or web. 

The same concept goes for how to access native browser apis, accessing native api’s will be different between mobile and web.


**Question 2 :**

Discuss what you believe are the most important considerations for widgets that deploy to different targets such as mobile and web ? 

**Answer:**

From my point of view the most important consideration are going to be around how should we build a responsive widget that should be smart enough to rebuild it self on a different ways based on the different screen sizes and layout especially the big difference between mobile and web.  

Flutter provides build-in responsive design widget and packages to help us design complex user interface for different screen sizes, like Material BreakPoint, Aspect Ratio, Layout orientation,  Layout Builder, Media Query, Fitted Box.  

we can also use  responsive_framework | Flutter Package.
It has an AutoScale feature, that shrinks and expands your layout proportionally, preserving the exact look of your UI. This eliminates the need to manually adapt layouts to mobile, tablet, and desktop.



## Asynchronous Dart
 
From my point of view, using Isolate/threads in dart will introduce a layer of complexity if we over using them, so when to use isolates, We should use them whenever you think there is a lot of computation that needs to be offloaded from the main thread. 

For example: 
* Let say you want to execute a network call and you want to process that data that you just received . and that data contains about million records that alone will hang your UI.
* You have some image processing tasks that you want to do on-device these kinds of tasks are highly computational as they have to deal with lots of number crunching operations which may lead to frozen UI or legginess in UI.


**Question 1:**

Describe the pros and cons of using Dart isolate asynchronously manage animation event loops

**Answer:**

##### pros: 
- As long as there's a computation in animation, then switching this computation into Isolate should increase app performce. 

##### cons: 
- Using a lot of Isolate will introduce layer of complexity in any codebase. 
- Isolates don't share any state and can only communicate using message passing.



