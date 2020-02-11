---
layout: post
title: Markov Models
subtitle: Hidden Markov Models
---
This is something I learned from my reinforcement learning course, but now time to referesh old memory.

Let's start with an example of first-order **Markov Models**, which is a chain-structured process where future states depend only on the current state, not in  the past. In other word, the value of xt only depends on x(t-1).

The thing we need for this model is that we actually know the state transition probability. This means when the subject takes next action, the probability is assured. Its not like the subject doesnt have a preference. Let us think about weather as an example. If we know the weather today, its sunny today, okay, we have three choices tomorrow, sunny again(0.8),rainy(0.05),cloudy(0.15). 

So, p(sunny|sunny) = 0.8, p(rainy|sunny) = 0.05, p(cloudy|sunny) = 0.15

#What is is used for? We can use it for sentence completion.

What is a second-order Markov chain? A particular observation xt depends on the values of the two previous observations x(t-1) and x(t-2).

I have explained the markov model with a simple example. What about some cute math? `P(xt|x1,x2,x3,....,xt-1) = P(xt|xt-1)`,so the probability of a sequence is:`P(x1,x2,x3,...,x3) = P(x1)P(x2|x1)P(x3|x2).....P(xn|xn-1)

Here, should insert a picture of hidden markov model. The vivid example would bethe dishonest casino model, we have to two considerations, one is the emission probabilities(which number you are gonna die). Another one is Transition probability(the casino player change from fair die to loaded die). Also, we need initial probability(fair or loaded die?). Another two photoes.
~~~
P(x,z|m)=p(x1,.....xn,z1,....zn)=p(z1)p(x1|z1)p(z2|z1)p(x2|z2).....p(zn|zn1)p(xn|zn)
~~~
Example would be x = 1,6,6,5,6,2,6,6,3,6 z= all fair/all loaded. Guess the finalprobability. P1 = 0.5x10-9 while P2 = 0.5x10-7. BOOB, 100 times larger than P1. So, there is a higher probability it is all loaded.





