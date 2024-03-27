---
layout: post
title:  "Test Creation Workflow"
date:   2024-03-05 13:33:23 -0500
categories: Testing
---
# The theory
When coding, you should always start with creating a test. There is at least two considerable advantages. First, it makes you think about what you really want to achieve. Secondly, it makes you think about how you want people to interact with your code.

When adding a feature, using a test-first approach (or TDD) will make you think about what the requirements are and not about the implementation. I know, thinking about the implementation is fun, but it's also a sinkhole where you will put a lot of time and effort on something that have a good chance to be more complex than necessary, poorly designed, and with a lot of time lost changing the code for all the discoveries that you will make while modifying the code. Back to the requirements, has Robert C. Martin says in Clean Craftsmanship. you should start with the simplest case and then specialise your tests while the code become more generalized. This is the best way to ensure not loosing time in implementation.

# Some pratices
## The context
Since you are likely not working with a green field project, we will also start with an existing project. So, consider the following Pong game where the only option is a two players game. We want to add the option to play with against a CPU.

{% highlight C++ %}

{% endhighlight %}

Following the theory, we will go with a test-first approach. First thing first, the requirements:
- When the player select _1 player_, player one will be controlled with the w,s keys and and player two will be controlled by a CPU.
- When the player select _2 players_, player one will be controlled with the w and s keys and player two will be controlled with the up and down arrows.
There is no mention about the intelligence of the CPU, so we should start with a dummy CPU, where the paddle just doesn't move. We are agile and this is the simplest increment I can came with.

So what is the first test what we should write? Should we go directly with testing the implementation of the CPU? I don't think so since the main goal is to allow a player to play versus a CPU and not freezing the behavior of the CPU. The first test would be to ensure that when _1 player_ is selected, the player 2 is a CPU. The best way to validate this will be to abstract the concept of player's controller using object oriented programming paradigm (OOP). The test will simply validate that we have instanciate a _CPUController_ object.

{% highlight C++ %}

{% endhighlight %}

Requirements for the 1 player mode requires that player one is controlled using the keyboard, validation that the first controller is a _KeyboardController_ was also added.

As you can see, this si not plugged into the production code yet. That's a great advantage, the new code can be reviewed before making change that could break the production. Let add the new code into the production code. This is more complexe because the actual code doesn't fit with the concept of having a controller to handle the paddle. The next step is to adapt the current code to our new reality. Again, you can see that the test represent how we want to interact with our code, not how it's implemented. So let start by encapsulating the behavior into the _KeyboardController_ class and plug the class.

{% highlight C++ %}

{% endhighlight %}

For those of you who are familliar with the design patterns, the IController, CPUController, and KeyboardController classes represent the strategy pattern.
