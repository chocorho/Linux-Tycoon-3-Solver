# Linux-Tycoon-3-Solver
Implementations and comparative analysis of different algorithms (in shell and/or python3) intended to automate a solution to Linux Tycoon 3 on GNU/Linux.

# Background / Origin

In early April 2022, famous open-source personality Bryan Lunduke releases [Linux Tycoon 3](https://lunduke.substack.com/p/linux-tycoon-3-the-os-wars-now-available?s=r). I decide to test it.

The first thing I notice is that it's a very slow-progressing game. I can consistently put my distro at the lowest number of bugs relative to the other distros, the highest comparative percentage of press attention, and a maxed-out Public Sentiment value (100/100)... and even then, I gain users at a rate of less than 100 users per round. In practice, this rate is always between 80 and 99 new users per round, but with an additional "bonus" being awarded during certain special events: a "New Release" granting 100, and a "military assault" granting 50. This might sound like a lot, but the total number of users is around 1 million! So 100 users per month implies that it takes no less than 8,000 "rounds" for the user to gain all users and win the market!

This leads me to wonder: can I write algorithms to speed up this game? Can I apply some middleware program, like AutoKey, or OCR, or something with or without some amount of reverse-engineering, in order to "feed the right inputs" to the game in order to "fast-forward" through the rounds. A tool-assisted speedrun, if you will!

# Roadmap

The general algorithm design would be:
1.    Take a screenshot of the game window;
2.    Call OCR (tesseract) to read text of the scenario;
3.    Make decision;
4.    Feed decision into the running game process;
5.    Take screenshot and run OCR again to confirm/process stat changes;
6.    Proceed to next Scenario;
7.    Return to step 1. Rinse, repeat.

## Approach 1: Hard-coded strategy (simple automation, shell)

I could use the following dependencies:

*   `xdotool` to feed keystroke inputs to the window;
*   `imagemagick` or another tool to save a screenshot of the Linux Tycoon window (`import` command);
*   `tesseract` to read the text from the game;
*   basic shell variables to monitor the stats and make decisions in real-time.

I have **my own pre-decided strategy** that I believe will win the game automatically, but I'd like to confirm that this is the case. Therefore, I could code up my existing strategy and leave it running until I reach a certain threshold (51% market share).

## Approach 2: Reinforcement Learning (pytorch extension, python 3)

Wouldn't it be impressive to *automatically derive* efficient strategies for playing the game over time?

We could do this using Deep Q Learning. I am looking into tutorials on Deep Learning and Neural Networks (which are two different concepts, though it is difficult to find examples taking a linear input rather than an image!) in addition to the python variaints of the same libraries listed in Approach 1.

# Lessons Learned

In the first few trials of running tesseract, I notice that the resulting output-text is sometimes inaccurate (reading `%` as `7` and `8` as `A`, etc.)! Therefore, it may behoove us to develop our own custom `tessdata`, rather than relying on the [default English training data](https://github.com/tesseract-ocr/tessdata/blob/main/eng.traineddata). It appears that [this blog post](https://pretius.com/blog/ocr-tesseract-training-data/) might be helpful to this endeavor.

# License

GPLv2

# Contact

chocorho: allLogarithmsEqual@protonmail.com

