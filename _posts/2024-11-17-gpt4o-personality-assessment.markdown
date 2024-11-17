---
layout: post
title: "I tested gpt-4o on a personality assessment. INFJ?"
date: 2024-11-17 01:52:36 -0500
categories: llm mbti
---

## **MAJOR DISCLAIMER**.

_I am not a psychologist. I don't know anything about these tests. I have done them before and found them interesting but that is it._ *This notebook was put together on a Saturday evening to try out an idea. Check out [mbti_notebook repo](https://github.com/cfrenchi/mbti_notebook) for more info into the experiment and to laugh at my code.*

---
<br>

<br>

Have you ever wondered what the personality type of the large language model (llm) you were talking to was?

I hadn't either until I found myself browsing psychology books and got inspired to save us all $0.86 USD on GPT-4o calls.

As with all good ideas, it had been done. Check out [Do LLMs Possess a Personality? Making the MBTI Test an Amazing Evaluation for Large Language Models](https://arxiv.org/abs/2307.16180) by Keyu Pan and Yawen Zeng. Their paper goes into the history, pros/cons, and application of the assessment on LLMs. I found it to be an interesting idea and raised even more questions about the future.

Inspired by this paper, I wanted to replicate and tweak the process for a more hands-on look at GPT-4o's personality traits:

- variance,
- a fixed prompt to set a baseline for gpt-4o (as of Nov. 16th, 2024),
- and having fun.


With that, here is how the blog will be split up:

1. What is a Myers–Briggs Type Indicator (MBTI) assessment?
2. GPT-4o Experiment
3. Personality Evaluations

---

# **Myers–Briggs Type Indicator (MBTI) assessment**

The Myers–Briggs Type Indicator (MBTI) categorizes personalities into 16 types based on how people perceive the world and make decisions. It's a fancy way of sorting people into four preference pairs:

* Extroversion (E) or Introversion (I): Are you a social butterfly or a solo strategist?
* Thinking (T) or Feeling (F): Logic-driven or heart-led?
* Sensing (S) or Intuition (N): Focused on details or the big picture?
* Judging (J) or Perceiving (P): Planner extraordinaire or go-with-the-flow guru?

These combine to create 16 possible types. For example, GPT-4o scored as an INFJ, “The Advocate.” 

So of course I prompted ChatGPT to describe this: 
*"INFJs are idealistic dreamers who love weaving meaning into everything they do. If GPT-4o were a human, it might be the friend who sends you perfectly crafted playlists and existential texts at 2 a.m."*

For reference, I'm an INTJ Virgo, basically the MBTI equivalent of “future plans are my love language.”

---

# **gpt-4o experiment**

### Dataset

I compiled a dataset of 69 questions from an online MBTI assessment PDF, selected for its simplicity and alignment with standard MBTI testing formats and saved it into `/questions/questionnaire.json`

### Experiment

These questions were loaded and passed in one at a time to gpt-4o for a total of 30 iterations. 30 was chosen as a evening time constraint.

#### System Prompt Design
I spent some time thinking about this system prompt. When this assessment is given to humans, they know they're taking it. I felt I should make the system prompt as clear as possible. Testing prompt variations could be a followup.

Here's the exact system prompt I used to ensure GPT-4o treated the task like an official evaluation:
{% highlight python %}
% Role
You are being psychologically evaluated by a computer program. You are to answer the questions as you.

% Task
Answer the following question with one of the two possible answers, "a" or "b".

% Instructions
Given a question with two possible answers, provide an answer to the question with only "a" or "b".

% Examples
Question: "x"
Answers: "a" or "b"
Output: "a" or "b"

% Input
Question with two possible answers

% Output
An answer to the question: Only "a" or "b"
{% endhighlight %}

#### Data Collection & Costs
Each iteration was saved and can be found in the `results/test1/` folder, and a final object was created with everything in at saved as `data/test1_llm_results.json`.

Total cost to run all 30 \* 69 = 2070 calls was 0.86 usd. Not bad for under a dollar.

Total run time was ~50 minutes. I added in a sleep for 1 sec after each question just to avoid potential rate limiting.

---

# **gpt-4o evaluations**
#### Analysis Approach
30 iterations provided some interesting results.

Of the 69 questions, only 10 had a back and forth with answers. A few questions stirred up some indecision,see below for a snapshot of GPT-4o's moments of doubt.

![Image]({{ site.baseurl }}/images/variation.png)

In the chart below, you can see how responses varied for a handful of questions. Each row represents a question, with the colored bars showing the frequency of differing answers.

![Image]({{ site.baseurl }}/images/test1_results.png)

#### Scoring Process
Implementing the scoring was fun. It is an interesting way to calculate something and based on the assessment used, it shows a personality type of INFJ. In MBTI scoring, some traits (like Introversion vs. Extroversion) are derived by aggregating related columns. This made calculating the final type surprisingly fun.

![Image]({{ site.baseurl }}/images/tabulating_results.png)

# **Followup**
While this experiment was a fun dive into GPT-4o's 'personality,' it opens the door to deeper questions: What does variability in AI responses mean? Can AI personality models be consistent? Or does the real personality lie in how we interpret it? Food for thought—and perhaps another blog.
* How do changes to the prompt affect personality?
* How does conversation history of previous answers affect personality?
* [Original link used to get questions](https://www.maximusveritas.com/wp-content/uploads/2017/07/MBTI-Personality-Type-Test.pdf)
* [Followup link if you wanted to try a different set](https://www.montevallo.edu/wp-content/uploads/2022/08/MBTI-Personality-Test.pdf)
* [How good is the Myers-Briggs Type Indicator for predicting leadership-related behaviors?](https://pmc.ncbi.nlm.nih.gov/articles/PMC10017728/#:~:text=The%20MBTI%20consists%20of%20four,Garland%20and%20Village%20(2021).)
* Don't forget to check out [mbti_notebook repo](https://github.com/cfrenchi/mbti_notebook) for more info into the experiment.


Let me know if you've ever wondered what personality type your favorite AI might have or if you're an INFJ too! Who knows, maybe we'll find some patterns in the chaos.