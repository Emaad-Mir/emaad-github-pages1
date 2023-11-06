---
title: Tri 1 Final + Reflection
comments: true
layout: post
description: This blog contains the results of the College Board Quiz for trimester 1 of CSA and any corrections I made for questions I got wrong (with explanations) or questions that I had to think about/look up. 
type: tangibles
courses: { csa: {week: 12} }
categories: [C1.4]
---


# Overview and Final Score

As we approach the end of trimester 1, we were assigned to complete a 40 question College Board test as a part of our final for AP CSA (yay!). After taking the test, I got my score out of 40 and reviewed any questions that I got wrong to check for the explanations.

For the 2014 Practice Test on College Board, I earned a 39/40 (97.5%), which is a score that I am very pleased with, as shown in the results report below:

![]({{site.baseurl}}/images/results.png)

The purpose of this blog is to review questions that I got wrong or even questions that I got right but had to think about them or even look them up online before answering them correctly. 

## Questions to Review

### Question 9 (Incorrect)

Question 9 on the test involved a code block that was intended to calculate the sum of a 1D array. We were asked to find what code segment from the choices given would best replace the missing code segment. The question is shown below:

![]({{site.baseurl}}/images/question9.png)

The correct answer was B, which was ```sum += key[i-1]```. I, however, ended up getting the question wrong and chose option C, which was ```sum += key[i]```. While taking the test, my first instinct was C and I simply chose C and moved on without really bothering to check my answer. Looking back at the question after I have taken the test and have had it scored, I realize why I made the mistake I did. In answering the question, I forgot the fact that the loop started at i = 1 and not i = 0. Because the loop starts at i = 1, we have to make the expression inside the bracket i-1 so that the element at index 0 is included in the final sum of the array. If we tried using the code segment that I chose, the element at index 0 would be excluded from the sum. Also, when key.length reaches i, an ArrayIndexOutOfBoundsException will be thrown. While the mistake I made is a small one, it is important that I review more and more questions like this for the future, as understanding how to do all of these problems correctly will ensure that I don't make a mistake like this on the actual AP CSA exam in May. 

### Question 12 (Correct, But Took Time)

Question 12 involved substrings within a method called mystery. The question is shown below:

![]({{site.baseurl}}/images/question12.png)

The correct answer to this question was C, which was "optr". Looking at the code, the method mystery is supposed to return the index k of every odd numbered index (1, 3, 5, 7) as a whole string. While I did manage to get this question correct without searching it up, the only issue was that I had to be very careful in keeping track of what was happening to the string as it was being assembled. If I at any point lost track or made a mistake, I would have to start over or end up choosing the incorrect answer. Even though I was able to answer this question correctly, I think it is important that I include this question in my blog as it is very likely that much of the questions on the multiple choice section will require me to trace the code. In other words, it is possible that I will have to keep track of certain things going on in the code block and make sure that I don't make any mistake while doing so. 

### Question 17 (Correct, But Took Time)

Question 17 involved shifting a set of elements (integers) in a 1D array called nums. The question asked to choose the answer that correctly represents what output is shown after running the program. The question is shown below:

![]({{site.baseurl}}/images/question17.png)

The correct answer to this question was C, which was ```{1, 2, 3, 5, 6, 7, 7}``. Even though I was able to get this question correct and the concept behind this question was not particularly difficult, this question was similar to question 12 in that I had to keep track of everything as it goes through the for loop. If I at any point lost track of something or made a mistake in what values were changed, I could have potentially chosen the wrong answer. It is essential that I review questions like these and expose myself to these types of multiple choice questions to ensure that I don't end up making a mistake on the actual exam. 

### Question 23 (Correct, But Took Time)

Question 23 involved a method named manipulate that does something to a List called animals. One important thing to note is that according to the explanation for this question, List is no longer tested on the AP CSA exam, with ArrayList being tested instead. Nevertheless, I thought that this question would be good to review, considering that it requires you to also think about what is happening to the list. Question 23 is shown below:


![]({{site.baseurl}}/images/question23.png)

The correct answer to this question was option B, which was ```["bear", "zebra", "bass", "cat", "koala", "baboon"]```. To summarize what the method manipulate does, it essentially iterates through each animal in the List and uses an if statement to determine if the animal in the List contains the letter b. If it does, then that animal is removed from the list and added to index 1. If it does not, then the animal stays where it is within the List. Similar to the previous questions that I reviewed, the concept behind this question was not particularly difficult. The only issue about this question was keeping track of everything that was going on. Previously, I would just try to play out everything that the algorithm is doing with certain values all in my head. However, thanks to my experience in AP CSP, I have learned about the importance of writing everything out to make it easier to visualize, which I ended up doing here. Because of this, I had a bit of an easier time answering this question compared to the others and was able to arrive at the correct answer of B. Despite this, it is important to review questions similar to this (maybe not with List, but ArrayLists), as that will ensure that I am strong in answering questions in regards to the concepts that this question tests. 

### Question 25 (Had to Look Up)

Question 25 involved something called RBox Interfaces. The purpose of this program, according to the question, is to see if one Box can fit inside the other. The question then asked us to choose the answer corresponding to the code segment that will allow us to a user of the box class to see if one Box can fit inside another. This question is shown below:

![]({{site.baseurl}}/images/question25.png)

The correct answer to this question was D, which was I and II only. I ended up having to look up this question, as I really had no knowledge on what interfaces in Java were and how they were supposed to work. While the explanation for this specific question notes that interfaces are no longer tested on the AP CSA exam, I think that it is still good to review it for the sake of knowing it for future real world appliances. According to the explanation, option D is correct because "Choice I provides the user access to the height, width, and depth of a box through the accessor methods getHeight, getWidth, and getDepth. This allows comparisons to be made in each of the three dimensions to determine if one box can fit inside another box. Choice II provides the user with methods smallerHeight, smallerWidth, and smallerDepth that let the user know if one box is smaller than the other in each of the three dimensions. Choice III provides the user with the getSurfaceArea and getVolume methods which provide the surface area and volume of a box. Unfortunately, a box with a smaller surface area or volume is not necessarily small enough to fit inside another box with a larger surface area or volume." Now when I look at the explanation, this question makes a lot more sense to me. 

### Question 40 (Had to Look Up)

Question 40 involved the use of a method called whatsItDo with String parameters and substrings. The question asked what the output would show after making a call to the method with the string ```WATCH```. Question 40 is shown below:

![]({{site.baseurl}}/images/question40.png)

The correct answer to question 40 was C, which was

```
W

WA

WAT

WATC

```

This question was different from me in that I only looked up the answer to this question because I was not entirely sure if my initial answer was correct. I originally thought that the answer choice B, which was essentially the reversed version of option C. Thankfully, it was good that I looked it up, as many people who answered this question agreed that the correct answer was C. Now when I look back at the question, I realize that the call to the whatsItDo method assigns to temp a substring of ```WATCH``` starting from 0, hence why the first line is W, WA, and so on. This was a really good question for me to look back on, as while I was able to choose the correct answer, it was because I had to look it up before I finally understood why the correct answer was the correct answer, not because I understood it the first time. 


# Reflection

Overall, even though there were a couple of questions that I got wrong or had to look up on the test, I am very pleased with the scored that I received, as it indicates that I have a solid understanding of everything that we have learned in CSA over the past three months. I think that many of the lessons that we have had over the past four to five weeks a played a significant role in helping me do well on this test, as even though I went into this class with knowledge about Java, it was nice to have a little refresher on key concepts. I believe that the student-taught lessons served as those refreshers for me, hence allowing me to perform very well on this test without getting most of the questions wrongs or having to look them up. Beyond the test that I took for the individual review, I have had a lot of memories, both funny and absolutely horrendous, of AP CSA this trimester. One noteworthy memory was Varalu finding out that we had the ability to alter the Canvas home page for Mr. Mort's AP CSA class. It was hilarious, as it all started with just our table making edits before the entire class caught up and realized that they too could make edits. To this day, I believe that our entire group linked all of our blogs on the page as well as many other miscellaneous pages. One exhausting memory was hands down the passion project. Even though it was fun to build a robot with my fellow group mates, some of whom are very experienced in robotics and electrical engineering in general, my part of the project came with several hours of hard work staying up late. I am sure that many of my other group members can attest to also doing this. Overall, this trimester of AP CSA was a balance between fun and exhaustion and I look forward to creating many new memories with (hopefully) the same people if not different group members. 