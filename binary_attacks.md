## 4.0 Introduction

When we mention a 'binary' file in Linux, we just mean that it's an executable file. The reason we call them binary files is because in Linux they aren't really .exe's. In Linux they are really ELF files (not like Legolas). It stands for Executable and Linking Format files. Linux doesn't really care about file extensions, so most often binary files in Linux won't have any file extension at all. A binary attack refers to using an executable file to make it do something it shouldn't normally do. This topic is hugely complicated, so we'll only go into the very basics.

## 4.1 Memory

First thing's first, we'll have to talk a bit about memory. Remember in the programming section, we said that a variable is just a box that you can put some data in? Well, that box is a section of memory on the computer.

In Python, you can just write:

`variable = "something"`

...and not worry about how much memory it takes up; Python handles all of that for you. In lower level programming languages, you actually have to say how much memory you expect to need. So in C you would write:

`char variable[10] = "something";`

In C, a string is actually just an array (in Python they are called lists) of characters. So by writing `char variable[10]` we're telling it to leave room for 10 characters in memory for this variable.

## 4.2 Buffer Overflow

Imagine you have a small glass in front of you and your friend tried to pour a whole 1 litre bottle of water into your glass. Of course, you know what's going to happen, right? It's going to reach the top of the glass and then start to overflow onto the table.

Just like with the glass, if you try to put something that's too large into a memory address that's too small, it's going to overflow the memory address. The program will crash, but actually it's worse than that. You see, the extra bit that overflowed is going to go into the next memory address and, if it still overflows there, it will go onto the next one and so on...

Let's have a look at an overflow in C:

```
char buffer[10] = "";
int test = 0;
scanf("%s", buffer);
```

This simple code creates a variable called `buffer` with room in its memory for 10 characters. It also creates another variable, this time an integer (whole number) called `test`. Then it called `scanf` which just asks a user to input something into the program. Whatever the user inputs, it saves it in the `buffer` variable.

So, if the user enters something less than 10 characters, everything is fine, but if the user puts in more than 10 characters, we have a problem. Let's say the user puts in a whole bunch of A's. If the user puts in enough A's then the value of `buffer` will be all A's, but it's also possible that the value of `test` will be overwritten with A's. Now `test` is an integer, so it can't hold an A value, but A written as a number is 41, so `test` could become `41414141`.

What's the big deal? Well, you can't do much with this as it stands, you're right. But at a more complicated level, you could put your own code into the memory of the program using this method. Once you can do that, the computer will be under your control.

### 4.3 Integer Overflow

An integer (whole number) can only be so big, because it has to fit in a memory address. What happens if you break the rule and create an integer that is too big to fit in the memory address? Scientifically speaking, weird stuff happens. The largest integer can depend on the system you are running on, but it is usually: `2147483647`. So, what happens if you go above that number?

Well, computers use something called a *sign bit* to tell if a number is negative or not. If you try to store a number that's too large in memory, it will overwrite the sign bit and can turn a positive number into a negative number! So you could theoretically add two positive numbers and end up with a negative number.
