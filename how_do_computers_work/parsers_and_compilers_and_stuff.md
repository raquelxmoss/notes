While reading [this article](https://v8project.blogspot.de/2018/05/bigint.html) about adding BigInt support to V8, I was puzzled by this line.

> The parser would have to desugar -x to x * (-1n) if x is a BigInt — but the parser has no way of knowing what x will evaluate to.

My question was

_What exactly do they mean by ‘evaluate to’ here? The implication is that the parser ‘knows’ what a number evaluates to, but doesn’t ‘know’ what a BigInt evaluates to. Why is that?_

After some thinking, here is my explanation

- Why does this work with numbers?
  Numbers are stored basically as-is in a register or in memory. To get the value of a number (i.e. ‘evaluate it’, we just ask for it). So, the parser can happily do that.

- Why doesn’t it work with BigInts?
  As described in the article, BigInts are stored as several chunks, due to the limitations of bytes. To get the actual value of the BigInt (i.e. evaluate it), we have to do the multiplication described. However, since we’re just parsing at the moment, we can’t do that computation right here and now.

