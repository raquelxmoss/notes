# What's the difference between blocks, procs, and lambdas?

Note: [this is a good reference](http://awaxman11.github.io/blog/2013/08/05/what-is-the-difference-between-a-block/)

What do they have in common? They are all examples of closures in Ruby. 

## What's special about a block?

- A block is _not_ an object, while procs and lambdas are. This means that with blocks, we cannot assign them to variables, or call methods on them. They really only make sense as a method call.
- You can only have one block in an argument list

## What's special about a Proc?

- A proc is an instance of a Proc class. That means that we can assign it to a variable and all methods on it.
- You can have many procs in an argument list
- A proc doesn't check the number of arguments it's given. This means that you can pass extra args and it will silently ignore them. If a proc requires and argument and none is passed, the proc will return nil.
- Returning from a proc will do a 'hard' return (my phrase) — e.g. it will bail out of your method if you're calling the proc inside of a method.

## What's special about a Lambda?

- A lambda is also an instance of a Proc class, but it's a particular type of proc.
- Lambdas care about how many arguments they are given. If you pass too many arguments, you'll get an argument error. If you fail to pass a required argument, the lambda will fail noisily.
- Returning from a lambda will land you back in the previous context (e.g. if you call a proc that's inside a method, you'll land back in the method and continue).

