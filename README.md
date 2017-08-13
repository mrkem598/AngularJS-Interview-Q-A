
******
   ###   ![download](https://user-images.githubusercontent.com/23619819/29246909-621ede90-7fd4-11e7-8e9b-f226ea969487.png) ![download](https://user-images.githubusercontent.com/23619819/29246909-621ede90-7fd4-11e7-8e9b-f226ea969487.png)![download](https://user-images.githubusercontent.com/23619819/29246909-621ede90-7fd4-11e7-8e9b-f226ea969487.png)


******
##  Most common and proven success AngularJS-Interview-Questions
****
****
# 1. What are the basics steps to unit test an AngulatJS filter?
***
## Answer:
1. Inject the module that contains the filter.
2. Provide any mocks that the filter relies on.
3. Get an instance of the filter using $filter('yourFilterName').
4. Assert your expectations.

Dependency injection is a powerful software design pattern that Angular employs to compose responsibilities through an intrinsic interface. However, for those new to the process, it can be puzzling where you need to configure and mock these dependencies when creating your isolated unit tests. The open-source project “Angular Test Patterns” is a free resource that is focused on dispelling such confusion through high-quality examples.

This question is useful since it can give you a feel for how familiar the candidate is with automated testing (TDD, BDD, E2E), as well as open up a conversation about approaches to code quality.

Source:
https://github.com/daniellmb/angular-test-patterns/blob/master/patterns/filter.md
https://docs.angularjs.org/guide/unit-testing

***
## 2. What should be the maximum nomber of concurrent "watches"? How would you keep an eye on that number?
***
## Answer:
 To reduce memory consumption and improve performance it is a good idea to limit the number of watches on a page to 2,000. A utility called ng-stats can help track your watch count and digest cycles.

Jank happens when your application cannot keep up with the screen refresh rate. To achieve 60 frames-per-second, you only have about 16 milliseconds for your code to execute. It is crucial that the scope digest cycles are as short as possible for your application to be responsive and smooth. Memory use and digest cycle performance are directly affected by the number of active watches. Therefore, it is best to keep the number of watches below 2,000. The open-source utility ng-stats gives developers insight into the number of watches Angular is managing, as well as the frequency and duration of digest cycles over time.

Caution: Be wary of relying on a “single magic metric” as the golden rule to follow. You must take the context of your application into account. The number of watches is simply a basic health signal. If you have many thousands of watches, or worse, if you see that number continue to grow as you interact with your page. Those are strong indications that you should look under the hood and review your code.

This question is valuable as it gives insight into how the candidate debugs runtime issues while creating a discussion about performance and optimization.

Sources:
https://github.com/kentcdodds/ng-stats
http://jankfree.org
***
## 3. How do you share data between controllers?
***
## Answer:
Create an AngularJS service that will hold the data and inject it inside of the controllers.

Using a service is the cleanest, fastest and easiest way to test.
However, there are couple of other ways to implement data sharing between controllers, like:
– Using events
– Using $parent, nextSibling, controllerAs, etc. to directly access the controllers
– Using the $rootScope to add the data on (not a good practice)
The methods above are all correct, but are not the most efficient and easy to test.
There is a good video explanation on egghead.io.
***
## 4. What is the difference between ng-show/ng-hide and ng-if directives?
***
## Answer:
ng-show/ng-hide will always insert the DOM element, but will display/hide it based on the condition. ng-if will not insert the DOM element until the condition is not fulfilled.

ng-if is better when we needed the DOM to be loaded conditionally, as it will help load page bit faster compared to ng-show/ng-hide.

We only need to keep in mind what the difference between these directives is, so deciding which one to use totally depends on the task requirements.
***
## 5. What is a digest cycle in AngularJS?
***
## Answer:

In each digest cycle Angular compares the old and the new version of the scope model values. The digest cycle is triggered automatically. We can also use $apply() if we want to trigger the digest cycle manually.

For more information, take a look in the ng-book explanation: The Digest Loop and $apply

***
## 6. Where should we implement the DOM manipulation in AngularJS?
***
## Answer:
In the directives. DOM Manipulations should not exist in controllers, services or anywhere else but in directives.

***
## 7. Is it a good or bad practice to use AngularJS together with jQuery?
***
## Answer:
It is definitely a bad practice. We need to stay away from jQuery and try to realize the solution with an AngularJS approach. jQuery takes a traditional imperative approach to manipulating the DOM, and in an imperative approach, it is up to the programmer to express the individual steps leading up to the desired outcome.

AngularJS, however, takes a declarative approach to DOM manipulation. Here, instead of worrying about all of the step by step details regarding how to do the desired outcome, we are just declaring what we want and AngularJS worries about the rest, taking care of everything for us.

***
## 8. If you were to migrate from Angular 1.4 to 1.5, what is the main thing that would need refactoring?
***
## Answer:
Changing .directive to .component to adapt to the new Angular 1.5 components

***
## 9. How would you specify that a scope variable should have one-time binding only?
***
## Answer:
By using “::” in front of it. This allows the check if the candidate is aware of the available variable bindings in AngularJS.
***
## 10. What is the difference between one-way binding and two-way binding?
***
## Answer?
– One way binding implies that the scope variable in the html will be set to the first value its model is bound to (i.e. assigned to)

– Two way binding implies that the scope variable will change it’s value everytime its model is assigned to a different value

***
## 11. Explain how `$scope.$apply()` works?
***
## Answer:

 It will re-evaluates all the declared ng-models and applies the change to any that have been altered (i.e. assigned to a new value)

Explanation: $scope.$apply() is one of the core angular functions that should never be used explicitly, it forces the angular engine to run on all the watched variables and all external variables and apply the changes on their values
Source: https://docs.angularjs.org/api/ng/type/$rootScope.Scope
***
## 12. What directive would you use to hide elements from the HTML DOM by removing them from that DOM not changing their styling?
***
## Answer:
The ngIf Directive, when applied to an element, will remove that element from the DOM if it’s condition is false.
***
## 13. What makes the `angular.copy()` method so powerful?
***
## Answer:
It creates a deep copy of the variable.

A deep copy of a variable means it doesn’t point to the same memory reference as that variable. Usually assigning one variable to another creates a “shallow copy”, which makes the two variables point to the same memory reference. Therefore if we change one, the other changes as well

`Sources:`
– https://docs.angularjs.org/api/ng/function/angular.copy
– https://en.wikipedia.org/wiki/Object_copying
***
## 14. How would you make an Angular service return a promise? Write a code snippet as an example?
***
## Answer:
To add promise functionality to a service, we inject the “$q” dependency in the service, and then use it like so:

    angular.factory('testService', function($q){
	return {
		getName: function(){
			var deferred = $q.defer();

			//API call here that returns data
			testAPI.getName().then(function(name){
				deferred.resolve(name)
			})

			return deferred.promise;
		}
	}
      })

The $q library is a helper provider that implements promises and deferred objects to enable asynchronous functionality

Source: https://docs.angularjs.org/api/ng/service/$q
***
## 15. What is the role of services in AngularJS and name any services made available by default?
***
## Answer:
– AngularJS Services are objects that provide separation of concerns to an AngularJS app.
– AngularJS Services can be created using a factory method or a service method.
– Services are singleton components. All components of the application (into which the service is injected) will work with single instance of the service.
– An AngularJS service allows developing of business logic without depending on the View logic which will work with it.

Few of the inbuilt services in AngularJS are:
– the $http service: The $http service is a core Angular service that facilitates communication with the remote HTTP servers via the browser’s XMLHttpRequest object or via JSONP
– the $log service: Simple service for logging. Default implementation safely writes the message into the browser’s console
– the $anchorScroll: it scrolls to the element related to the specified hash or (if omitted) to the current value of $location.hash()
Why should one know about AngularJS Services, you may ask. Well, understanding the purpose of AngularJS Services helps bring modularity to AngularJS code.
Services are the best may to evolve reusable API within and AngularJS app

Overview:

AngularJS Services help create reusable components.
A Service can be created either using the service() method or the factory() method.
A typical service can be injected into another service or into an AngularJS Controller.
	##    Source:
– https://docs.angularjs.org/guide/services
– http://www.tutorialspoint.com/angularjs/angularjs_services.htm

***
## 16. When creating a directive, it can be used in several different ways in the view. Which ways for using a directive  do you know? How do you define the way your directive will be used?
***
## Answer:
When you create a directive, it can be used as an attribute, element or class name. To define which way to use, you need to set the restrict option in your directive declaration.

The restrict option is typically set to:

‘A’ – only matches attribute name
‘E’ – only matches element name
‘C’ – only matches class name

These restrictions can all be combined as needed:

‘AEC’ – matches either attribute or element or class name

For more information, feel free to check out the AngularJS documentation.

***
## 17. When should you use an attribute Vs an element?
***
## Answer:
Use an element when you are creating a component that is in control of the template. Use an attribute when you are decorating an existing element with new functionality.

This topic is important so developers can understand the several ways a directive can be used inside a view and when to use each way.

Sources: https://docs.angularjs.org/api/ng/service/$compile#directive-definition-object
***
## 18. How do you reset a `$timeout, $interval()`, and disable a `$watch()`?
***
## Answer:
To reset a timeout and/or $interval, assign the result of the function to a variable and then call the .cancel() function.

		var customTimeout = $timeout(function () {

 		 // arbitrary code
		}, 55);

		$timeout.cancel(customTimeout);                                                                                                                                                    

to disable $watch(), we call its deregistration function. $watch() then returns a deregistration function that we store to a variable and that will be called for cleanup

		var deregisterWatchFn = $scope.$on(‘$destroy’, function () {
    			// we invoke that deregistration function, to disable the watch
	    		deregisterWatchFn();
			});
			
***
## 19. Explain what is a `$scope` in AngularJS is?
***
## Answer:
Scope is an object that refers to the application model. It is an execution context for expressions. Scopes are arranged in hierarchical structure which mimic the DOM structure of the application. Scopes can watch expressions and propagate events. Scopes are objects that refer to the model. They act as glue between controller and view.

This question is important as it will judge a persons knowledge about a $scope object, and it is one of the most important concepts in AngularJS. Scope acts like a bridge between view and model.

Source: https://docs.angularjs.org/guide/scope

***
## 20. What are Directives?
***
## Answer:
Directives are markers on a DOM element (such as an attribute, element name, comment or CSS class) that tell AngularJS’s HTML compiler ($compile) to attach a specified behavior to that DOM element (e.g. via event listeners), or even to transform the DOM element and its children. Angular comes with a set of these directives built-in, like ngBind, ngModel, and ngClass. Much like you create controllers and services, you can create your own directives for Angular to use. When Angular bootstraps your application, the HTML compiler traverses the DOM matching directives against the DOM elements.

This question is important because directives define the UI while defining a single page app. You need to be very clear about how to create a new custom directive or use the existing ones already pre-build in AngularJS.

Source: https://docs.angularjs.org/guide/directive

***
## 21. What is DDO `Directive Difinition Object`?
***
## Answer:
DDO is an object used while creating a custome directive. A standard DDO object has following parameters.
		var directiveDefinitionObject = {
    			priority: 0,
  			  template: '<div></div>', // or // function(tElement, tAttrs) { ... },
   				 // or
   				 // templateUrl: 'directive.html', // or // function(tElement, tAttrs) { ... },
   			 transclude: false,
   			 restrict: 'A',
    			templateNamespace: 'html',
   			 scope: false,
  			  controller: function($scope, $element, $attrs, $transclude, otherInjectables) { ... },
  			  controllerAs: 'stringIdentifier',
  			  bindToController: false,
  			  require: 'siblingDirectiveName', // or // ['^parentDirectiveName', '?optionalDirectiveName', '?
			  ^optionalParent'],
    			  compile: function compile(tElement, tAttrs, transclude) {
    		  return {
    			    pre: function preLink(scope, iElement, iAttrs, controller) { ... },
        		    post: function postLink(scope, iElement, iAttrs, controller) { ... }
	      		}
      			// or
     			 // return function postLink( ... ) { ... }
   			 },
   			 // or
   			 // link: {
    			//  pre: function preLink(scope, iElement, iAttrs, controller) { ... },
    			//  post: function postLink(scope, iElement, iAttrs, controller) { ... }
    			// }
   			 // or
   			 // link: function postLink( ... ) { ... }
			  };"
