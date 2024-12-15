# GayakTag
## About the project

GayakTag is a software to tag the singers in an audio clip. The software is teachable which means that you can upload a few samples of a singer and GayakTag can identify those singers later in any unknow audio clip.
You dont need a lot of training samples to register a new singer. Only a few samples (~10) would be sufficient.

In this document we would start from scratch. This will cover every step of the process. Starting from understanding the problem, articulating it, requirement analysis, background research, technical design and finally to the implementation. 

It depends on your interest. You can go through all of it if you are interested in the technology, or you can cut to the good part. Just download the software and try it out for fun.

## Understanding The Problem:

So lets imagine this as a website where you upload an audio clip of a song and it shows you the singer along with the timestamp.
So on the surface we will have a web application for users to interact with it.
So lets imagine the whole thing as having two logical units:
1) Interface 
2) inference engine

We will come to the interface later on. lets first think about the inference engine.

### Inference Engine

Given an audio clip prefereably containing some song, the inference engine will produce a list of singers along with the timestamps where they appear.
Mathematically this can be represented as 
Let I = Ordered Set( frames)
and let F = inference function therefore
F(I) = Set(start_timestamp, end_timestamp, singer)
We will use a ML model for doing this inference.

For the users perspective the Inference Engine has two modes:
1. Registration mode
2. Inference mode

#### Registration Mode
Its not practical that we retrain the ML model everytime a new singer is introduced.
We need to have a some basic training to start with. A basic training would mean that our model knows how to identify speech and the speaker at a very generalized level.
Then we will tune this mmodel to identify certain singers. With this the model will be ready for usage.

The crucial question arises now. What should the model be?
We will list down a few possible strategies and run experimenets on those. the results thereafter will determine our decision.

Lets also think about the problem a bit. What are the usual problems types? Namely classification, clustering or generation. 
This task looks like a classification problem inherently. Its supervised, that is we have a annotated dataset to teach it. This rules out the possiblity of clustering. For us the singers are the classes and the model have to identify the classes for the samples. 
Can this be a generation task? Interesting angle. So instead of giving pre-defined classes we can teach the model to generate the name of the singer. There are multiple loopholes or concerns here and this demand a thorough discussion. We will actually run extensive experiments on this.


Well, so we come down to two approaches:
1. classification problem
2. Generation problem

# Approaches for developing the ML model for inference
## Classification Problem:

Lets go back to the very basics. Let imagine a classification problem as this 
input : X where X is a tensor or N-dimensional matrix
output : y where y is a vector corresponding to the classes

So our model maps X to y
Pretty basic stuff ! So lets define the X for us.
Had our problem been like some prediction being made froma sequence of numbers, this is a no brainer. But here we have audio clips as input and strings as output.
Well we will one-hot encode the string classes and get a vector consisting of numbers, well thats a no-brainer. 
The trickier aspect is to deal with the audio clip.


So we have to vectorize audio signals. What it means is that we take the audio signal and convert it into a matrix comprising of numbers. we will figure out how to do that. Lets have a section separately for that.

Before we proceed any further, lets figure out some datasets for training our model. We will try to search for suitable datasets in the internet. But we are are unlucky we will create a dataset ourselves. 

[Day 2]





