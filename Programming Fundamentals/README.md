# Programming Fundamentals: Algorithms (Determining a Prime Number)

1. Work an instance yourself
2. Write down what you did
3. Generalize your steps
4. Test your steps
5. Translate to Code
6. Test Program
7. Debug Program

## The First Four Steps

### Step 1 (Work an instance yourself)

> The problem at hand

The first step in designing an algorithm is working a small example by hand, sometimes its best to draw a diagram to get a better feel and work it out more precisely. It may help to assign values, in this example we're trying to determine if a number is prime. Simply knowing 7 is prime contradicts the algorithm, the computer does not know, and needs to be told how to determine this number.

You may get stuck at this step, it happens, and this could mean one of two things.

First, the problem is *ill-specified*-- it is not clear what needs to be done. To resolve this, you need to determine how this problem needs to be solved. Ask around for more information if it helps.

Secondly, the problem may be difficult because you lack the *domain knowledge* required to solve the problem. Here it's best to research the problem, and get more information on the field or discipline the problem deals with. For this example, if you didn't remember the definition of a prime number then you'd be lacking domain knowledge-- in this case its mathematics. No amount of programming can overcome a lack of domain knowledge, instead you have to do some research on your part. This research can have any medium say Google, a Math textbook, a friend that's really good at math.

For this example we'll say we want to write a program to compute *x* raised to the *y* power. So we'd pick our values, say `x = 3` and `y = 4`, to get `3^4 = 81`.

### Step 2 (Write down what you did)

> The instances of the given problem

The second step is about writing down what you did to solve the problem in a particular instance. In other words, a very clear set of instructions that would allow any other individual to reproduce your answer for the given problem. If you did multiple instances in step one, you repeat them in step two multiple times to be as precise as possible before you generalize them, to ensure an accurate scenario reproduction. Think of a detailed chore list.

The difficultly of this step is determining *exactly* what you did to accomplish the problem. You may find it difficult because of how easy it can be to gloss over small details that when left out could easily cause another individual with lesser knowledge to get lost. Simply relying on your common sense, and holding others to your knowledge baseline can cause a loss of instruction. Humans can get by, but a computer would halt completely.

Returning to our *x* to the power of *y* example we might write the following steps for `x = 3` and `y = 4`.

```md
Multiply 3 by 3
>  You get 9
Multiply 3 by 9
>  You get 27
Multiply 3 by 27
>  You get 81
81 is your answer.
```

With precise steps we leave little guess work, which is ideal for an algorithm, but repetitive. Luckily Step 3 gets rid of the repetition, and since computers are naturally fluent in arithmetic, there's no extra steps required.

### Step 3 (Generalize your steps)

> The pattern Morty what does it mean??

Now that we've solved the problem(s) and written down the required steps, we're ready to generalize those steps into an algorithm. In Step 2 we solved specific instances, but now we need to find the pattern that allows us to solve the whole class. This is generally two activities, firstly we must take the values and abstract them into mathematical expressions. Say for Step 2 we multiplied 3 by something in each step. To generalize, we can replace 3 with *x*.

```md
Multiply x by 3
>  You get 9
Multiply x by 9
>  You get 27
Multiply x by 27
>  You get 81
81 is your answer.
```

Secondly, we can generalize by finding repetition, taking the same repeated steps and condensing them down to a single function. This includes refining steps that *almost* seem repetitive and making them truly repetitive to fit the pattern. In our 3^4 example, our steps are almost repetitive, multiplying *x* by *something* but something changes in each progression. So we generalize, refactoring *something* into a named variable with an initial value:

```md
Start with n = 3
n = Multiply x by n
n = Multiply x by n
n = Multiply x by n
n is your answer.
```

Now that we have the *exact* same step repeating three times, we can contemplate how many times this step repeats as a function of *x* and/or *y*. We must be careful not to jump to conclusion that it repeats *x* times because `x = 3`-- that's just a coincidence in this case. In actuality, this case repeats `y - 1` times. The reason for this is that we need to multiply 4\*3s together, and we already have one in *n* at the start, so we need `y - 1`  more. This leaves us the following generalized steps:

```md
Start with n = 3
Count up from 1 to `y - 1` (inclusive), for each number you count,
  n = Multiply x by n
n is your answer.
```

We need to make one more generalization of a specific value to a function of the parameters. We start with `n = 3`; however, we would not always want to start with 3. In the general case, we would want to start with `n = x`.

```md
Start with n = x
Count up from 1 to `y - 1` (inclusive), for each number you count,
  n = Multiply x by n
n is your answer.
```

Sometimes finding the pattern isn't easy, making generalization more difficult. When this happens, returning to Steps 1 and 2 may help. When in doubt, work more examples by hand to help find a pattern.

### Step 4 (Testing your algorithm)

After Step 3, we have a good idea of our algorithm and we're pretty sure it should work. However, it's possible that we missed something or messed up along the way. The purpose of Step 4 is to ensure the steps are accurate before proceeding to code. In order to accomplish this, we test our algorithm with different values than the ones the algorithm is based on. Using 3 and 4 would just give us an obvious answer we already accounted for. If the values differ, then something in the algorithm is wrong. The more test cases, the higher the confidence we have that the algorithm is correct.

A common mistake in Step 3 is a *mis-generalization*. For example, if we didn't remove the reliance on `x = 3` and repeating 3 times, it'd would only work when `x = y - 1`; otherwise we would count the wrong number of times adn get the wrong answer. By testing in Step 4, we'd most likely detect this problem.

Another common mistake is an oversight on potential unseen cases such as when `y = 0`. If you execute the algorithm by hand with `x = 2`, `y = 0`, you *should* get `2 ^ 0 = 1`; however you will get 2. Specifically, you will start with `n = x = 2`. We would then try to count up from 1 to `0 - 1 = -1`, of which there are no numbers.

To fix this, we revisit Steps 1 and 2 and for the case that failed (`x = 2`, `y = 0`). This case is a bit tricky since we just know that the answer is 1 without doing any work. The fact that the answer requires no work makes Step 2 a little different-- we just give an answer of 1. While this simplicity may seem nice, it actually makes it difficult to incorporate into our steps. We might be tempted to write the following:

```md
If y is 0 them
  1 is your answer
Otherwise:
  Start with n = x
  Count up from 1 to `y - 1` (inclusive), for each number you count,
    n = Multiply x by n
  n is your answer.
```

These steps explicitly check for the case that gave us a problem (`y = 0`), give the right answer for that case, then perform the more general algorithm. For some problems, there may be corner cases which require this sort of special attention. However, for this problem, we can do better. Instead, a better approach would be to realize that if we count no times, we need an answer of 1, so we should start *n* at 1 instead of *x*. In doing so, we need to count 1 more time (to y)-- to multiply by *x* one more time:

```md
Start with n = 1
Count up from 1 to y  (inclusive), for each number you count,
  n = Multiply x by n
n is your answer.
```
