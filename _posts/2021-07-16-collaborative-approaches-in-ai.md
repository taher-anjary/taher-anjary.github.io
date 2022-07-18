---
title: 'Collaborative Approaches in AI'
date: 2021-07-22
permalink: /posts/2021/07/collaborative-approaches-in-ai/
tags:
  - graph neural networks
  - deep neural networks
  - attention mecahnism
  - transformer
  - SLAM
  - autonomous driving
---


I believe that in order for a system to be successful in large scale contexts, the system must learn to collaborate. The idea makes sense considering how the human species dominated the earth because we learnt to cooperate. We see this in nature as well; Packs of wolves and prides of lions learnt to hunt together as teamwork proved to be more efficient and effective. Ant colonies can join themselves to form bridges or rafts when faced with appropriate obstacles. Amazing! Don't you think?

<img src="/images/apes-together-strong.jpeg" width="700">

Similar trends are being used in the field of AI. In this article, I'll briefly describe some of them:

Transformers
======
<img src="/images/optimus-prime.jpeg" width="700">

Transformers are all the rage these days. And no, they have nothing to do with the Autobots or the Decepticons (I was disappointed too). They use something called Attention mechanisms: Imagine an AI system playing chess. If the AI is trained using attention mechanisms, intuitively, it just means that each piece on the chess board will focus on all the other pieces with a certain weight. Essentially, how much 'attention' to pay to each other before making a decision. This makes sense, right? You would need to know where all the other chess pieces are, where the opponent's King is with respect to my King, will my knight be devoured by the Rook if I move my Bishop etc. This is an oversimplification of the architecture, but this is the general idea. 

Transformers are very powerful. They've revolutionized the world of Machine Translation- Yes, a Transformer is what helps Google translate Turkish to English and back because it is way smarter at it than I am. And now they're moving into other fields such as Computer Vision for tasks such as generating catchy captions for your next Instagram post.

Graph Neural Networks
======

Let's use the same idea as a chess playing AI. In Graph Neural Networks(GNNs), each chess piece would be represented as a node. Each node will then send 'messages'  about itself to other nodes. And each node would then update itself based on all the messages it receives from the other nodes, thereby becoming aware of the other chess pieces. The AI would then use the updated information within the nodes to make its next move. The idea is similar to attention mechanisms. And indeed, attention mechanisms can be implemented as GNNs. The difference is that graphs are more of an optimization framework, while Transformers are more of a Deep Learning method.

Multi-Vehicle SLAM
======

Simultaneous Localization and Mapping(SLAM) is a technique used by autonomous agents such as self riving cars and robots to map out all the obstacles in its environment, while figuring out where within that environment it is. This is necessary so that something like a self-driving car can figure out how to avoid crashing into something. Most SLAM use cameras as the primary source of input. And herein lies the problem: Have you ever tried to overtake someone on the road only to realize there are other cars blocking your way? This happens because the other cars were not in your 'line-of-sight'. If care is not taken, dangerous accidents can occur if a self-driving car cannot see everything. It would help if the car had x-ray vision or something, right? There is another way: Multi-Vehicle SLAM. What happens here is that each vehicle collects information about the obstacles that it CAN see, and then relays that information to other vehicles. Each vehicle then combines all this information, in real-time, to construct a more global representation of its environment. It's like having many eyes in different places, and each eye has its own brain, and each brain can see with all the other eyes, simultaneously. Isn't that meta?

Directive?
======
<img src="/images/cute-robot.png" width="700">
I've been doing research in the field of computer vision, which is unsurprisingly challenging. I cope by seeing the similarities between AI algorithms and mother nature. It motivates me to think that we can literally play Dr. Frankenstein and mix ideas from nature and science to create truly intelligent things. Science fiction movies have played a big role in getting me where I am so far: Terminator, I-robot, TRON legacy, WALL-E just to name a few. Let's just always remember to incorporate the 3 laws of robots into our mad creations so that we don't end up with a SkyNet situation:
* A robot may not injure a human being or, through inaction, allow a human being to come to harm
* A robot must obey the orders given it by human beings except where such orders would conflict with the First Law
* A robot must protect its own existence as long as such protection does not conflict with the First or Second Laws

Other than that, I hope you all found this article to be a pleasant overview of some of the latest trends that I've noticed in the field of AI. Let me know if you want me to write about anything in particular. I love forming comparisons to nature and going nuts with it.

/**> END OF LINE_**
