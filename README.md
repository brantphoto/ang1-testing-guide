*currentlyAMess: true*

_When this is false this doc is ready for community input_

Primary Author: Brant Barger
## Testing Tools

http://jasmine.github.io/
http://jasmine.github.io/

##Testing Sandbox
http://plnkr.co/edit/gist:5301635?p=catalogue

##Testing Directives

###What the heck is a directive???

Well, if I you can see past the muck for a second its this: A string of HTML that is given its own scope (similar to a lexical scope based on a set of rules set up by Angular.

`var element = '<div></div>'`

The first thing that angular does is wrap each element in a JQ light rapper. Do you want to more info on Jake you like look here. That just is that this helps angular find the element and manipulate it.


###$compile

remember, you feed angular a magic string and it turns it into HTML, but as an example, maybe it sets the rules for the piece of html. Here’s a good example of a directive

`'<div vz-widget></div>'`
It takes the string and $compiles it into DOM. But vz-widget has given it scope.

Next you compile using the $compile service this takes your jqLite element and attaches a scope to it. You can create scope by utilizing the $rootScope service and created a new scope. $rootScope().new.

This gives the element a scope to exist in, which you shouldn’t confuse with the scope of the directive itself.

so

##Testing Controllers

###What does a controller do?
It really has two purposes:

First purpose is to utilize a certain date of service calling one of its methods then returning the data . The second purpose is to serve as a data store and manage state within the relevant relevant view. It's massively important to realize That when you're testing a controller you are only testing a controller. It's a known anti-pattern to use $ HTTP Directly inside of a controller. Instead, you will always utilize a data service with a method that will utilize the $http service. It may look like this. MyService.getData(); perhaps you have a quick handling directive that you're using in your Dom such as ng-click that is calling a method attached your controller really you just want to make sure when that method gets called that it's producing the right outcome. What is the right outcome?

###The 'right' outcome.

`scope.$digest();`

 The right outcome happens often in two phases.

 ####Part 1, Get the data via service Method

The first phase is that a data service is utilized by calling one of its methods. If you are using the $http service within your control or you are doing it wrong. Create your own service or factory and have that Service utilize the $http service. This method is often called with an argument or set of arguments with information provided from the Dom or sometimes the state of the controller. An example would be:

`MyService.getData({itemId: vm.itemId});`

There, we did the first thing right we made a contract that the data left the controller in the right format. This makes it possible to test services in isolation as it will be assumed that data gets to the service or factory in the right format.

 ####Part 2, Handle the data

The thing is there is often logic that occurs in the controller after the date is retrieved This testing guy is going to assume that was returned as a promise. $http which, Under the hood uses $q, is just a promise in disguise. This allows you To chain .then and .catch methods to manage behavior, whether data was successfully retrieved or not.

Imagine what confidence we have if we knew, within reason, that's our controller would be in control of the logical flow after the promise was resolved or rejected. This can be the case if we reject one popular concept: the concept of handling your http://within the service. That means using .then or .catch within the service. This could have unusual side effects when you try to use a.van in the controller


What about that part I can't test? the local function that does some other task?


## Testing Services

ervices and factories make it extremely easy to share code as well as isolating it for testing. In this section will talk about several different types of services. 1) Data services and 2) Data Sharing Services.

### Basic Service Testing
A service or factor is just an object but you return. This objects good have properties with any type of data type but most commonly they'll have many methods which contain logic that you'd like to share between many different parts of your app. Testing services is basic. Three steps:

1) Inject the module
2) Inject the service you want to test and set it to a variable, specifically a variable that is scoped to the top describe function of your specific test.
3) Call a method on the service
4) make assertions to see if the results match the expectations.

### Data Service

ll need some additional tools test data services but luckily and your provides: $httpBackend, this comes with the angular mocks library and you'll need to include it in your packagesttpbackend. This service will help you determine whether you've made the right type of HTP call and whether it's to the right route.

