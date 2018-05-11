I asked the Ruby community for an explanation of Class Inheritance vs Prototypal Inheritance. This was @eoinkelly's wonderful reply.

> I think they are technically similar solutions which come from different world views. In class based inheritance the “class objects”  are objects which know how to do only one thing - make instances. Class object don’t do any of the actual work, the instances do. If you need some work done, you have to talk to a class-object which will make you an instance to do the work. Furthermore the class objects are the only ones allowed to make instances. There is a strict caste system in place - an instance does work but can never make more instances to help it (it can ask a class to make those instances but it cannot make them itself).

A Class object contains instructions on how to make an instance of a class. A Class object knows how to make `Dog.new`. The instance of dog does the actual work, e.g. `dog.bark`. An instance cannot make another instances. A dog does not know how to make another dog, it has to ask the dog Class object for a new dog.

> We can think of prototypal inheritance as a more egalatarian society. Any object can make new instances by cloning itself - the ability to create instances is not concentrated in the class objects anymore. This is an extremely flexible system. Every object in memory is potentially a new type and can be the parent of its own type heirarchy.

Not so with Prototypal. Our instance of dog could clone itself to make a new dog, if it wanted to (question: why would it want to?).

> As you can imagine this level of flexibility could lead to crazy-town. When every object in memory can be a type then trying to reason about your system could become hellish.

Yeah :confused:

> Most developers are comfortable modelling systems in terms of “classes make instances, instances do work”. Coupling that with the potential chaos of “every object can be a new type” means that in reality the full flexibility of prototypal inheritance is rarely used.

I think its lack of use is why I don't know much about it

> Instead we kinda rebuild the society of the class objects because it is easier to reason about a system when the “can make new instances” job is partitioned off into one kind of object.

> Javascript is leaning into this pattern with the ES6 `class` syntax. By providing `class` syntax sugar for creating functions which can create objects, JS is signalling that you should think about your objects in that “classes make instances, instances do work” way.

Indeed. I am fairly used to working with classes in ES6, because on the surface it works the same as Ruby, though I know that this is syntactic sugar and that the stuff under the hood is different.

> The prototypal purists decry that it ruins the beautiful flexibility & simplicity of prototypal inheritance - see anything on the internet by Eric Elliot e.g. https://medium.com/javascript-scene/the-heart-soul-of-prototypal-oo-concatenative-inheritance-a3b64cb27819 .

I have not read this article because I cannot be bothered right now.

> My view is that prototypal inheritance suffers from every single of the same problems as class-based inheritance. Despite what some functional programming blog posts would have us think, nobody seriously programming in an OO style has embraced deep inheritance hierarchies as a good idea since the early ’00s. 



> The extra flexibility that prototypal inheritance provides, while elegant in and of itself, has potential to make things confusing and in a world where we treat inheritance as an occasional treat, nobody cares.

Is it elegant? Why is it elegant? I should probably read the Eric Elliot article.