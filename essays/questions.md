---
layout: essay
type: essay
title: "The Format of Awesome Questions: Tips and Tricks"
# All dates must be YYYY-MM-DD format!
date: 2025-01-28
published: true
labels:
  - Questions
  - Answers
  - StackOverflow
---

<img width="300px" class="rounded float-start pe-4" src="../img/question.png">

## That horrible feeling of rejection.

Who amongst us students has once asked a question so bad that they got an equally negative response? I sure did. Thinking back on those embarrassing times still makes me cringe years later. Whether you fear rejection or are willing to ask any question no matter the response, it is very important to understand the process of asking great questions, especially in a STEM field such as computer science. Many online resources are available to help anyone if they have a related programming question, but one still needs to remember that there is also a proper etiquette online for asking great questions. 

## A professional online community of hackers.

StackOverflow is primarily known as the most QNA website for computer programmers. Known as the website that saves the day of many software developers, it is no surprise that many questions are asked frequently on the website. Those who ask questions on StackOverflow also note that while a good question will garner a lot of upvotes and support from the community, a bad question will bring downvotes and ridicule from those who would also be happy to answer great questions. This brings the question of, how to ask a great question on a website that prides itself in being a forum of high standard. Luckily, we can easily see the effect of great vs awful on the website itself when searching for answers.

## Easy example of an awesome inquiry with an equally awesome response:

Finding questions that everyone loves to answer is not a difficult task on StackOverflow. Sorting by most upvoted, we can take a look at the top question that has been asked: Why is processing a sorted array faster than processing an unsorted array?

With more than 27 thousand upvotes, this question clearly helped many and reached many more, so let's examine why it is such a good question. 

In the following example, we examine the components of a great question and an equally great response as a result of the question.

```
In this C++ code, sorting the data (before the timed region) makes the primary loop ~6x faster:

#include <algorithm>
#include <ctime>
#include <iostream>

int main()
{
    // Generate data
    const unsigned arraySize = 32768;
    int data[arraySize];

    for (unsigned c = 0; c < arraySize; ++c)
        data[c] = std::rand() % 256;

    // !!! With this, the next loop runs faster.
    std::sort(data, data + arraySize);

    // Test
    clock_t start = clock();
    long long sum = 0;
    for (unsigned i = 0; i < 100000; ++i)
    {
        for (unsigned c = 0; c < arraySize; ++c)
        {   // Primary loop.
            if (data[c] >= 128)
                sum += data[c];
        }
    }

    double elapsedTime = static_cast<double>(clock()-start) / CLOCKS_PER_SEC;

    std::cout << elapsedTime << '\n';
    std::cout << "sum = " << sum << '\n';
}
Without std::sort(data, data + arraySize);, the code runs in 11.54 seconds.
With the sorted data, the code runs in 1.93 seconds.
(Sorting itself takes more time than this one pass over the array, so it's not actually worth doing if we needed to calculate this for an unknown array.)

Initially, I thought this might be just a language or compiler anomaly, so I tried Java:

import java.util.Arrays;
import java.util.Random;

public class Main
{
    public static void main(String[] args)
    {
        // Generate data
        int arraySize = 32768;
        int data[] = new int[arraySize];

        Random rnd = new Random(0);
        for (int c = 0; c < arraySize; ++c)
            data[c] = rnd.nextInt() % 256;

        // !!! With this, the next loop runs faster
        Arrays.sort(data);

        // Test
        long start = System.nanoTime();
        long sum = 0;
        for (int i = 0; i < 100000; ++i)
        {
            for (int c = 0; c < arraySize; ++c)
            {   // Primary loop.
                if (data[c] >= 128)
                    sum += data[c];
            }
        }

        System.out.println((System.nanoTime() - start) / 1000000000.0);
        System.out.println("sum = " + sum);
    }
}
With a similar but less extreme result.

My first thought was that sorting brings the data into the cache, but that's silly because the array was just generated.

What is going on?
Why is processing a sorted array faster than processing an unsorted array?
The code is summing up some independent terms, so the order should not matter.

```

## Wow.

A feature I noticed right off the bat is the length of the question. Compared to an average Google or AI search prompt, the length of this question trumps those of simple inquiries by a wide margin. Taking a closer look, it is extremely easy to see what the questioner needs help with. They are looking to find the reason why sorting the data first makes the primary loop run around 6 times faster. This question is very specific with helpful comments in the source code so that whoever is answering will know exactly what the questioner is referring to. Not only that, the questioner demonstrates his progress towards solving the problem by providing his attempt in another coding language, which shows viewers that the questioner has really put thought into this problem. Precise, informative, and comprehensive, this question is a shining example of what a great programming question really looks like, and can be applied in in-person discussion as well.

The following is the top answer for this question with over 35 thousand upvotes. (even more than the question!) We will not examine this answer in this article, but I know you may learn something new with this beautiful answer to this equally awesome question, as I sure have.

```

You are a victim of branch prediction fail.

What is Branch Prediction?
Consider a railroad junction:

Image showing a railroad junction Image by Mecanismo, via Wikimedia Commons. Used under the CC-By-SA 3.0 license.

Now for the sake of argument, suppose this is back in the 1800s - before long-distance or radio communication.

You are a blind operator of a junction and you hear a train coming. You have no idea which way it is supposed to go. You stop the train to ask the driver which direction they want. And then you set the switch appropriately.

Trains are heavy and have a lot of inertia, so they take forever to start up and slow down.

Is there a better way? You guess which direction the train will go!

If you guessed right, it continues on.
If you guessed wrong, the driver will stop, back up, and yell at you to flip the switch. Then it can restart down the other path.
If you guess right every time, the train will never have to stop.
If you guess wrong too often, the train will spend a lot of time stopping, backing up, and restarting.

Consider an if-statement: At the processor level, it is a branch instruction:

if(x >= 128) compiles into a jump-if-less-than processor instruction.

You are a processor and you see a branch. You have no idea which way it will go. What do you do? You halt execution and wait until the previous instructions are complete. Then you continue down the correct path.

Modern processors are complicated and have long pipelines. This means they take forever to "warm up" and "slow down".

Is there a better way? You guess which direction the branch will go!

If you guessed right, you continue executing.
If you guessed wrong, you need to flush the pipeline and roll back to the branch. Then you can restart down the other path.
If you guess right every time, the execution will never have to stop.
If you guess wrong too often, you spend a lot of time stalling, rolling back, and restarting.

This is branch prediction. I admit it's not the best analogy since the train could just signal the direction with a flag. But in computers, the processor doesn't know which direction a branch will go until the last moment.

How would you strategically guess to minimize the number of times that the train must back up and go down the other path? You look at the past history! If the train goes left 99% of the time, then you guess left. If it alternates, then you alternate your guesses. If it goes one way every three times, you guess the same...

In other words, you try to identify a pattern and follow it. This is more or less how branch predictors work.

Most applications have well-behaved branches. Therefore, modern branch predictors will typically achieve >90% hit rates. But when faced with unpredictable branches with no recognizable patterns, branch predictors are virtually useless.

Further reading: "Branch predictor" article on Wikipedia.

As hinted from above, the culprit is this if-statement:
if (data[c] >= 128)
    sum += data[c];
Notice that the data is evenly distributed between 0 and 255. When the data is sorted, roughly the first half of the iterations will not enter the if-statement. After that, they will all enter the if-statement.

This is very friendly to the branch predictor since the branch consecutively goes the same direction many times. Even a simple saturating counter will correctly predict the branch except for the few iterations after it switches direction.

Quick visualization:

T = branch taken
N = branch not taken

data[] = 0, 1, 2, 3, 4, ... 126, 127, 128, 129, 130, ... 250, 251, 252, ...
branch = N  N  N  N  N  ...   N    N    T    T    T  ...   T    T    T  ...

       = NNNNNNNNNNNN ... NNNNNNNTTTTTTTTT ... TTTTTTTTTT  (easy to predict)
However, when the data is completely random, the branch predictor is rendered useless, because it can't predict random data. Thus there will probably be around 50% misprediction (no better than random guessing).

data[] = 226, 185, 125, 158, 198, 144, 217, 79, 202, 118,  14, 150, 177, 182, ...
branch =   T,   T,   N,   T,   T,   T,   T,  N,   T,   N,   N,   T,   T,   T  ...

       = TTNTTTTNTNNTTT ...   (completely random - impossible to predict)
What can be done?

If the compiler isn't able to optimize the branch into a conditional move, you can try some hacks if you are willing to sacrifice readability for performance.

Replace:

if (data[c] >= 128)
    sum += data[c];
with:

int t = (data[c] - 128) >> 31;
sum += ~t & data[c];
This eliminates the branch and replaces it with some bitwise operations.

(Note that this hack is not strictly equivalent to the original if-statement. But in this case, it's valid for all the input values of data[].)

Benchmarks: Core i7 920 @ 3.5 GHz

C++ - Visual Studio 2010 - x64 Release

Scenario	Time (seconds)
Branching - Random data	11.777
Branching - Sorted data	2.352
Branchless - Random data	2.564
Branchless - Sorted data	2.587
Java - NetBeans 7.1.1 JDK 7 - x64

Scenario	Time (seconds)
Branching - Random data	10.93293813
Branching - Sorted data	5.643797077
Branchless - Random data	3.113581453
Branchless - Sorted data	3.186068823
Observations:

With the Branch: There is a huge difference between the sorted and unsorted data.
With the Hack: There is no difference between sorted and unsorted data.
In the C++ case, the hack is actually a tad slower than with the branch when the data is sorted.
A general rule of thumb is to avoid data-dependent branching in critical loops (such as in this example).

```
 
For questions of this caliber, it is only fair that they get a similar response. The top-rated response dives deep into the specifics of the problem to ensure that everyone understands at the end.

## You have seen the do's, what about the dont's?

While there are many questions that are answered just fine by the StackOverflow community, the following is a prime example of something that simply cannot be answered very well, nor would it encourage people to dedicate time to answer the problem.

```

I have created a static webpage using HTML, CSS, and Bootstrap, and now I want to make it dynamic by adding filter functionality.

I have a section where clicking on a filter option should display only the relevant content, while hiding the rest. However, I am struggling to implement this using JavaScript.

I have taken references from multiple websites but couldn't understand the solution.

<insert 100 lines of unspecific code here that I will not show here>

```
## Oof.

Although this question is also very long, it contains just 4 broad sentences and the rest is a super long collection of unorganized code. The questioner wants to make his webpage dynamic by adding filter functionality, but the code provided does not state where or how he wants this to be implemented. The first time I saw this question I thought, a saint would have to devote a lot of time to really answering this question, but not me! The questioner also states that he visited multiple websites but still cannot understand the solution. This is a vacuous sentence that only serves to give the questioner a marginal amount of merit which will still not encourage anyone to tackle this extremely broad and unclear problem. Maybe try ChatGPT next time?

Unsurprisingly, this question did not get a single answer and was closed for being too broad. 

## Links for the StackOverflow questions:

https://stackoverflow.com/questions/11227809/why-is-processing-a-sorted-array-faster-than-processing-an-unsorted-array
https://stackoverflow.com/questions/79396229/converting-a-static-webpage-to-dynamic
