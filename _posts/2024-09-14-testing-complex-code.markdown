---
layout: post
title:  "Testing Complex Code"
date:   2024-09-14 19:33:23 -0500
categories: Testing, DDD, Domain-Driven Design
---

# The Idea

# The Problem
You have inherited a complex code base and you need to change a functionality. You find the place where you want to add the new code and you change the code to add the behavior. After testing manually, you want to add automated tests around your newly written code. This is where the problem starts. You realize that you need to instantiate a ton of boiler plate code that don't relate to simple behavior you want to validate.

Here is an example of what it could look like:

TODO: Add code for the cross section and anonymize it.

```cpp

```

# The Solution

As a disciplined software developer, you take a test-first approach and you start by writing a test that will reflect how an external actor will interact with your code.

```cpp

```

This test is simple and easy to understand. It is also easy to write and it is not tided to the implementation details. Not being tied to the implementation details is really important because it allows you to change the implementation details without having to change the tests. Another side-effect of this is that it forces you to create code that matches the behaviour abstractions instead of having the behaviour matches the code because the code is hard to change.

Back to the test, the first thing to realize is that only what is needed is instantiated. By limiting to what is truly needed forces you to create decoupled code. Decoupled code allows you to go faster later as it leverage reusability, flexibility, maintainability, and testability.

TODO: Write an article on how decoupling leverage reusability, flexibility, maintainability, and testability?

TODO: Write an article on the difference between functional and object-oriented behaviour. 

Sometime, a behaviour can requires a lot of dependencies. Those cases are sign that you need higher abstractions. A discussion with the domain experts can help you understand what are the right abstractions.

Now we start implementing the code behind our test. Let start by making the code compile.

```cpp	

```

Now we make the test pass with little code as possible.

```cpp

```

Great! We now have a test that passes. Let assume that our new code is fully tested and it does everything that we want. With the new code, it is easy to cover all the corner cases of the new behaviour. Let plug it into the existing code. But first we will create a complex test case with all the boiler plate code to instantiate everything that is needed at least for one happy path and hopefully for one unhappy path if possible. Here for simplicity, we will only focus on achieiving one happy path.

The main goal of this test is not to validate the behaviour but to validate that the new behaviour is called and that its inputs and outputs are attached correctly to the existing code. This test will be hard to write, hard to maintain, fragile and probably flaky. At least you will not have many tests of this kind and they will tend to be eliminated over time as your code design will improve.

TODO: Write about the difference between code design and architecture.

Here is what the test could look like:

```cpp

```

Following this test, let add the new behaviour to the existing code. First, we plug the new behaviour in the existing code. and 

TODO: I am stuck here as I have no idea how to present the fact that I am using a value object / entity and I am not talking about the repository. 
I could use an example with the functional part and then with the load/save part and afterward the real test.
I should probably start with the initial code and extract the part of the repository and than the functional part.
I see an issue for both approach, using test-first approach, it implies that people can come up with good design. With the refactoring approach, it implies that people can extract good design.
With the test-first approach, I can put emphasis on what a non-programmer can do.
My approach can be a merge of the 2, the first part is the functional part and the second part, the larger test can help extract the key abstrations.
