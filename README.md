# Python Matters

Over the past 40 years or so I have used many different programming languages.
I started on university with Algol60, followed by APL and Fortran,
and of course there was the ubiquitous Basic on my hobby computer.
Later I worked with Pascal, C, C++, Java, and to a lesser extent C#, Lisp, Perl, and some others.
But my favourite language for the last 20 years or so is Python.

Why Python? For me it is the fact that Python allows me to focus on ideas, on algorithms, and on solutions,
without being sidetracked by necessary boiler plate and administration.
And it still amazes me that in Python I can pick up work that I have not touched for several months,
and continue working on it as if I had only taken a lunch break.
I know other people have the same experience; I have seen this described as "Python fits my brain".

But there is another, somewhat related aspect that also intrigues me: Python is the only programming language
I know of that presents an almost leakfree abstraction of the underlying computer
(see the [law of leaky abstractions](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)).
What I mean by that is that Python does not allow you to can gain information
about the underlying computer through the constructs offered by the language.

To illustrate this point: in C it is quite simple to determine if a computer is big-endian or little-endian:
One way is to define a union, so that a character array and a short overlay each other.
Then you give the short a well-chosen value, and look at the components of the character array to
determine where the high-order and low-order bytes of the short go.

```
int main()
{
  union
  {
    char c[2];
    short i;
  } leaky;
  ;
  leaky.i = 0x0100;
  printf(x.c[0] == 1 ? "Big endian\n" : "Little endian\n");
  return 0;
}
```

Such a construct is simply impossible in Python. The only way you can get to the underlying
machine in Python is through the use of modules.
The `struct` module in the standard library allows you to deduce the native byteorder of your machine.
And of course there is the `sys` module that provides all kinds of platform-specific information.
But the point is that Python - unlike C - does not allow you to do so using only Python language constructs.
