
## No framework
There is a convincing argument to be made that agentic workflows do not need to use a framework. 

Matt Williams makes this arugment in his video [Have You Picked the Wrong AI Agent Framework?](https://youtu.be/jLVl5V8roMU?si=jIrHkeQ4c9EkVTeV)

One of his key argument is that you in most cases already know the well-defined workflow to be followed and simplicity is much easier to maintain without a AI agent framework in these cases.
(and selectively use tools such as state machine [xstate](https://github.com/statelyai/xstate) or [dirty-json ](https://github.com/RyanMarcus/dirty-json)). 

Matt Williams believes AI agent frameworks are relevant "When you have a job that doesn't have a well-defined workflow where you need the model to do thinks close to reasoning" (but this is a small minority of solutions). 

There is plenty of truths to this, but not all of the arguments can be translated directly to an enterprise software setting. 
Here there right frameworks provide additional benefits for how the code is maintained and extended over its lifetime.

My major gripe with the frameworks so far, is that they are very opinionated in their abstractions and in many cases these abstraction add significant amount of complexity.