---
layout:     post
title:      "First crawl"
subtitle:   "On simulation and loops"
date:       2015-08-19 12:00:00
author:     "Eardil"
header-img: "img/post-bg-01.jpg"
---
I've never liked learning languages (programming or otherwise). The way I learned english and any phrase I know from any other language (elen sila lumenn omentielvo!) is by watching movies or reading books/blogs. As for programming languages, I have learned by having to solve problems so I'll do just that. In these initial posts I'll learn by hitting walls and finding the most straightforward tools to break them. After that I'll try to find the standard practices for them.

## The birthday candle problem
I follow Brent Yorgey's [The Math Less Traveled](http://mathlesstraveled.com/) and I've just read his post on [The birthday candle problem](http://mathlesstraveled.com/2015/08/07/the-birthday-candle-problem/), as it sounds fun I decided to start my first introduction to Python by trying to run some simulations from it. You can read more about it on his post, but I'll quote him on the problem:

>A birthday cake has $n$ lit candles. At each step you pick a number $1 \leq k \leq n$ uniformly at random and blow out $k$ candles. If any candles remain lit, the process repeats (using a new value of $n$). As a function of $n$, what is the expected number of rounds needed to blow out all the candles?

I began this blog by saying that I wanted first of all to replace my need of MATLAB, so what I did was first to write some MATLAB code and I'll try to reproduce it. I wrote the most straightforward code I came up with. Here it is:

``` Matlab
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% PARAMETERSOF THE SIMULATION %
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
obs=100; % Number of observations to estimate expected value for each n
N=300; % Max number of candles


%%%%%%%%%%%%%%%%%%%%%%
% PART 1: SIMULATION %
%%%%%%%%%%%%%%%%%%%%%%
K=zeros(N,1); % For storing the expected values

for n=1:N % Iterate for each number of candles
    ki=0; % To save number of rounds
    for j=1:obs % Generate observations
        ni=n;
        k=0; % Number of steps in this observation
        while ni>0 % Keep doing while there are lit candles
            k=k+1; % Add one more step
            ni=ni-floor((rand()*ni))-1; % Blow candles!
        end
        ki=ki+k; % Sum of rounds
    end
    K(n)=ki/obs; % Average rounds for this number of candles
end

%%%%%%%%%%%%%%%%%%%%
% PART 2: PLOTTING %
%%%%%%%%%%%%%%%%%%%%
plot(K) % Plot the estimates of expected value
hold on

%%%%%%%%%%%%%%%%%%%%%
% PART 2: MODELLING %
%%%%%%%%%%%%%%%%%%%%%
aaa=fitlm(1:N,exp(K)); % Fit a linear model to exp(k) (believe me, it looks logaritmic)

% FINAL PLOT
plot(1:N,log(aaa.Fitted)) % Fit fitted values (believe me, it looks great)
xlabel('n')
ylabel('Average rounds')
```

I put it for reference for those who would like to run it. Now the quest to find everything I need begins.

It seems that if I want to do numeric stuff I need to load a certain library called `numpy`. It's my first library load. Yay!


    ##################
    import numpy as np
    ##################

### Random numbers
If I want to blow out candles I need some random numbers. Inside numpy, there's this thing called `random` that has a function called `random_integers` that can generate some sequence of random numbers exactly how I need: given some $n$ generate a number between $1$ and $n$. I'll work with $n=10$.


    ##################
    n = 10
    print(np.random.random_integers(1,n,))
    ##################

    7
    

To see it better lets generate 5 numbers.


    ##################
    print(np.random.random_integers(1,n,5))
    ##################

    [ 1  8 10  6  4]
    

It looks kinda...long. Maybe later I'll learn some way to clean it up.

### Loops
Anyway now I have some random numbers and need a `while` loop to keep blowing out candles until there's none left.


    ##################
    n=10
    k=0
    while n>=1:
        k+=1
        r=np.random.random_integers(1,n)
        print("Round %s: From %s candles, I blow out %s." % (k,n,r))
        n=n-r
    ##################

    Round 1: From 10 candles, I blow out 5.
    Round 2: From 5 candles, I blow out 1.
    Round 3: From 4 candles, I blow out 3.
    Round 4: From 1 candles, I blow out 1.
    

Now lets make $M$ simulations to get an estimate of the expected value via the mean. Here, `range(min,max)` generates a sequence of numbers $min, min+1,\dots,max-1$


    ##################
    n=10
    M=4
    Kj=np.zeros(M)
    
    for j in range(0,M):
            ni=n
            k=0
            while ni>=1:
                ni=ni-np.random.random_integers(1,ni)
                k+=1
            Kj[j]=k
    print(Kj)
    print("The average is: %s." % np.mean(Kj))
    ##################

    [ 3.  5.  2.  2.]
    The average is: 3.0.
    

### Functions
Now I'll define it as a function to call it easily by the number of initial candles $n$ and the number of simulations $M$.


    ##################
    n=10
    M=4
    
    def candles(n,M):
        Kj=np.zeros(M)
        for j in range(0,M):
            ni=n
            k=0
            while ni>=1:
                ni=ni-np.random.random_integers(1,ni)
                k+=1
            Kj[j]=k
        return np.mean(Kj)
    
    K = candles(n,M)
    print("With %s candles and a sample size of %s, I needed %s average rounds." % (n,M,K))
    ##################

    With 10 candles and a sample size of 4, I needed 4.0 average rounds.
    

With this I can easily make simulations for lots of values of $n$. Let's try for $n=1,2,\dots,10$ with a sample size of $M=1000$. 


    ##################
    M=1000
    N=10
    
    K=np.zeros(N)
    for n in range(1,N+1):
        K[n-1]=candles(n,M)
        print("With %s candles, I needed %s rounds on average." % (n,K[n-1]))
    ##################

    With 1 candles, I needed 1.0 rounds on average.
    With 2 candles, I needed 1.527 rounds on average.
    With 3 candles, I needed 1.849 rounds on average.
    With 4 candles, I needed 2.037 rounds on average.
    With 5 candles, I needed 2.261 rounds on average.
    With 6 candles, I needed 2.41 rounds on average.
    With 7 candles, I needed 2.613 rounds on average.
    With 8 candles, I needed 2.684 rounds on average.
    With 9 candles, I needed 2.794 rounds on average.
    With 10 candles, I needed 2.996 rounds on average.
    

Now I've completed part 1 of the code. In the next post I'll plot and model the data.

---

Remember that you can get this [IPython Notebook](https://github.com/eardil/Blog_Code/blob/master/2015-08-20-first-crawl/2015-08-20-first-crawl.ipynb) and others at my [Github Page](https://github.com/eardil).
