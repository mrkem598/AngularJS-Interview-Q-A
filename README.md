# 25AngularJS-Interview-Questions
Have an upcoming AngularJS interview for a junior web developer position? Experienced developers at Codementor have gathered together to collaborate on this list of AngularJS interview questions to help you prepare for your AngularJS technical interview. Can you answer them all?
***
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
