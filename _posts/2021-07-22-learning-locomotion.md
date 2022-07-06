---
title: 'Learning Locomotion'
date: 2021-07-22
permalink: /posts/2021/07/learning-locomotion/
tags:
  - reinforcement learning
  - deep neural networks
  - locomotion
  - flappy bird
  - genetic algorithms
  - phase functioned neural networks
  - machine learning
  - hexapod
  - robot
  - cyborg
---

Imagine you were given a hexapod- a six legged robot that kind of looks like a cyborg spider. And someone asks you to program it to walk. Your first though might be to use a bunch of trigonometric formulae to control each of its joints. Such an approach is hard-coded, difficult to design (believe me, I've tried), and your hexapod would not be able to adapt very well to changing terrain or speed- or at least, it would not look very organic.
Fortunately, we live in an age where artificial intelligence can do the thinking for us. Described below are 3 methods that could be used to train a robot to move and balance itself as though it were real!

Phase Functioned Neural Networks
======
![alt text](/images/phasefunctionnn.jpeg|width=500px)

Neural Networks. Ah, I remember the day I first heard about them: an AI architecture quite literally inspired by brains.
When you first learn about AI, you will quickly realize that the only reason that they are feasible is because of the large amounts of data and computation power that is available today. Datasets are a set of questions and answers. The AI(a neural net, for example) is trained on datasets by looking at a question, giving an answer and comparing its answer with the right answer. It then computes derivatives(gradients) based on the error, and uses these to update itself. When it updates itself, it is learning, becoming better. Talk about learning from mistakes. The larger the dataset, the more experience the trained neural net will have.

So where does one obtain these datasets to train a neural net to walk? Motion Capture. Yes, the stuff they use to animate fictional characters in movies. A person wears a suit with markers on them and walks around while a camera records him/her. The marks on his/her suit are used to create the datasets that describe the position of all his/her joints at each frame/time-step. This data is then fed to a neural net to try and replicate his/her motion in different scenarios. This data is the answer to the question. I will talk about the question in just a second.
You may be wondering what the purpose of the phase function is. Think about walking: it has a pattern, a cycle. The pattern in each two steps you take is more or less identical to the next two steps. So, to give the neural net an awareness of where in the cycle it currently is, an input from a phase function is given. This can be a sinusoid. Intuitively, its like giving a robot a stopwatch so that it can decide whether its time to lift its leg up, put its foot down, push or stretch etc. Of course, this isn't sufficient information. The neural net can also take as input a description of the direction it wants to go and its current pose: where all its joints are, at what angle are they bent relative to each other etc. With the phase, direction and description of the current pose as inputs, a neural net can decide how to adjust its pose for the next time step(which can be in milliseconds, a resolution if you will). These inputs are the question and they are given to the neural net at each time step. The answer is then the pose in the next time step, as described in the previous paragraph. The neural net learns to give answers to the questions as it experiences through the dataset.

The dataset contains nuances in the walk cycles that can be thought of as experience that allows the neural net to learn to walk organically and adapt to different scenarios ie: every two steps it takes will not always be identical.
You may see more here: https://www.youtube.com/watchv=Ul0Gilv5wvY&ab_channel=Yoshiboy2
But what if you aren't a multi-million dollar company that can afford expensive motion-capture technology and the human resource required to design the datasets? What can you do without questions and answers? Read on :D

Genetic Algorithms
======
![alt text](/images/flappybird.gif)

This method is quite literally inspired by concepts of evolution, reproduction and natural selection: the weakest will die, the strongest will pass on their genes, and the species becomes optimal as it evolves across generations. I get the chills when I think about this in robot and AI contexts.
A specimen such as a flappy bird may be controlled by a neural net. The neural net is made up of a bunch of parameters, or numbers that can describe various learnt non-linear activation functions. Do not worry about this crazy jargon. All you need to know is that a neural net is made up of parameters(numbers) that will be updated as it learns.
The neural net will take as input a few pieces of information such as where it is, where is the next obstacle, and how wide is the gap. The neural net processes this and spits out a 1 or 0 to describe whether to flap or not, respectively. It will make this decision every couple of milliseconds(time-step), depending on the resolution.

You may realize that the correct answers would hence need to be 1s and 0s for every time-step. But we don't have these correct answers. What do we do?
We look at natural selection. We need to judge the specimen and quantify how well it performed until it died. This is where the fitness function comes in, and it can be as simple as the score of the flappy bird. The higher, the better.

When training this AI, there will usually be hundreds of specimens, each with their own randomly initialized neural nets. And they all race. When they all die, the specimens with highest scores are selected to breed, while the rest are deleted from memory.
How do they breed? Remember the parameters of the neural net I talked about earlier? Think of those numbers as the genes. Two randomly selected winning specimens will mix their parameters, like chromosomes and DNA. The parameters are exchanged, or even mutated using noise distributions. The result is an offspring that is built using the winning specimens' parameters. All the winning specimens will randomly produce a couple hundred new offspring i.e. the next generation. This next generation will then race again. And the cycle continues.

It's thanks to the fitness function(the high score) and the selection of wining specimens that the generations become better and better, they evolve, they optimize. And thanks to random breeding, they will hardly get stuck at local optima.

This is how you can achieve learned locomotion without actual datasets, without the right answers. Instead of evaluating every time step, you judge it based on how well it lived its entire life.

If you're interested in learning more about genetic algorithms, I highly recommend the book 'Hands-on Genetic Algorithms with Python by Eyal Wirsansky'.

Reinforcement Learning
======
![alt text](/images/ragdoll.gif | width=500)

This is a training technique you may have heard of in the context of training animals: You give the animal a reward when it does what you want, and punish it when it does something bad, and the animal figures out what it needs to do. If you apply this to AI, you can solve some really complex problems such as playing GO, playing League of Legends or even walking.

In Reinforcement Learning, we have an agent, which observes the environment and uses a policy(a neural net) to decide on an action to take. If the action leads to a desired state, the agent receives a reward.

The idea is similar to Genetic Algorithms in that there is a neural net(a policy) that decides on what action to take based on what the agent observes around it. If the action leads to something good, the agent receives a reward.

Many variants of RL algorithms exist, many choices can be made to its design. One such algorithm is the Actor Critic(A2C). The actor is just the policy neural net that takes actions, and the critic is another neural net that judges how well the actor's decision was. Both the actor and critic learn to do their job better as gradients are computed on the rewards that the agent receives.

The RL algorithm can be done in a Monte Carlo fashion where the policy updated after a whole life cycle(episode) or it can be done in a Temporal Difference fashion where it is updated after every time-step.

The difference between RL and Genetic Algorithms is that the updates in the latter are based on breeding concepts while the latter makes its updates using derivatives(gradients). The difference between RL and Phase Functioned Neural Nets is that the prior computes the gradients from the reward while the latter computes gradients based on an error.

Learning locomotion can be formulated as an RL problem where the state observed can be the robot's current pose(where it is, where are its joints, at what angle they are bent etc), the direction it wants to go, and the immediate terrain around it. The policy then processes all this information to take an action(how much to move each of its joints, and in which direction). The reward can be the total distance it covers.

RL algorithms are very powerful and really cool. They are especially used to solve complex problems where the correct answers are not always clear. For example, if you win a chess game, how would you know which move exactly led to victory. You really wouldn't. It's a bunch of carefully planned plus intuitive plus improvised moves that led to it. So you cannot always know what the 'right' move is at any given state.

Sometimes, the agents discover a glitch in the environment and learns to exploit it, as can be seen in this [Hide Go Seek](https://www.youtube.com/watch?v=n6nF9WfpPrA&ab_channel=It%27sBloodyScience%21) example.

Maybe we should be worried \:|

END OF LINE
