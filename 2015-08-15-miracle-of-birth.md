
# Part 1. The miracle of birth

Im not a savvy programmer. My background is in applied math and I'm mainly interested in data analysis, probability, combinatorics and linear optimization. Most of these disciplines require programming, but I prefer to concentrate more efforts in model design than in algorithm development.

For the past three years I've been using MATLAB in my job and my thesis, so I'm quite attached to it's sintaxis and find it's plots both beautiful and simple. I am well aware of it's limitations for data analysis too (non numeric data, anyone?), but I had learned to live with it. But I've changed jobs since and there's the license cost, so that's a little sad.

On the other hand there's `R`, which I've been using sporadically since I got out of college. This summer I got back to it and got fairly familiar with all the Rmigthy Wickham features such as `dplyr`,`tidyr` and of course `ggplot2`. This is what I've been using in my workflow for the past months and I'll most probably continue to for the foreseable future, but for some reason I'm not enjoying it.

So my mind turned to this thing called Python that I had read that is a thing --specially on John D. Cook's awesome [The Endeavour](http://www.johndcook.com/blog/) which you should read-- and I was thinking about learning. I had been reading a little bit when I realized that the name came from Monty Python; suddenly I was set on getting started.

I began searching for the best approach and decided to watch the nice history lesson from Scipy 2015 conference given by Jake VanderPlas in July --awesome timing.


    from IPython.display import YouTubeVideo
    YouTubeVideo('5GlNDD7qbP4')





        <iframe
            width="400"
            height="300"
            src="https://www.youtube.com/embed/5GlNDD7qbP4"
            frameborder="0"
            allowfullscreen
        ></iframe>
        




It catched my attention the enfasis on Python as a MATLAB killer wannabe by the creators of some of the libraries.

Anyway, basically by the time I finished watching this I knew the path I had to take. So I went on to install the mentioned [Anaconda distribution](http://continuum.io/downloads) that seems to have all the libraries needed for a good head start on data analysis (`scipy`), machine learning (`scikit-learn`), numerical stuff (`numpy`), plotting (`matplotlib`), etc. Installation is completely painless (I installed in Windows and Linux) and you can start right away. I started with this thing called `IPython Notebook`, or `Jupyter`, which is really awesome and I'm actually writing this post on it. *Basically it's a Markdown interface*.

Really, that's it. You just install the distribution, start `IPython Notebook` and click on "New". When you do, say `Hello` from me.


    print("Hello Python!!")

    Hello Python!!
    

Since I'm not really interested in `Python` as a programming language but as a scientific tool --for now--, in the next post I'll go directly into some libraries and start working on a problem.
