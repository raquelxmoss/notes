## Loop unrolling

Reference: I read the first half of [this Wikipedia](https://en.wikipedia.org/wiki/Loop_unrolling) page before running out of steam, but I think I got some value out of it.

I came across loop unrolling when I was reading about JIT compilation with LLVM. Loop unrolling is an optimisation technique that can be performed either manually by a programmer, or automatically by a compiler (or, I guess, another tool in the chain?).

What it does is makes your loop more manual and imperative. It makes the file size larger, but reduces loop overhead. I'm not entirely sure what the overheads are of a loop, but I'm guessing that it's things like asking "Is this loop done?" after every iteration of the loop, increasing the index of the next item (`i++`), and probably some other things.

By unrolling a loop, you can do things like run fewer iterations, run code in parallel (provided that the first loops don't affect subsequent loops), and other things that I don't understand yet (Branch penalty is minimised?).

There are some disadvantages — one of them is that the size of the file is increased. This isn't usually something that I have to think about, but it can be important when dealing with, for example, embedded applications.

If the code in the body of the loop involves function calls, it might not be possible to combine unrolling with function inlining (I haven't read about this yet, but I can pretty much guess from the name what that means). The reason is that the increase in code size might become too big. So, some trade-offs between those optimisations need to occur.

If the code in the loop contains branches, it can apparently be very slow. I have no more info on this yet.

Here's an example of manually unrolling a loop:

```javascript
// normal loop

let a = 10;

for (let i = 0; i < 100; i++) {
  a = a + 1;
}

// manually unrolled loop

let a = 10;
for (let i = 0; i < 100; i += 5) {
  a = a + 5
  // note, it might actually be like this, I'm not too sure
  // a = a + 1
  // a = a + 1
  // a = a + 1
  // a = a + 1
  // a = a + 1
}
```

