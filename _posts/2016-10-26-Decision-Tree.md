---
title: "Machine Learning Part 8: Decision Tree"
header:
  teaser: tutorials/decision-tree/graph.png
categories:
  - Tutorial
tags:
  - machine-learning
  - decision-tree
  - classification
  - essential
---
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
Hello guys, I'm here with you again! So we have made it to the 8th post of the Machine Learning tutorial series. The topic of today's post is about **Decision Tree**, an algorithm that is widely used in classification problems (and sometimes in regression problems, too). *Decision Tree* is well-known not only for its great performance on classification, but also for its easy-to-understand algorithm.

As we have already seen up to now, in [Linear Regression](https://chunml.github.io/ChunML.github.io/tutorial/Linear-Regression/) and [Logistic Regression](https://chunml.github.io/ChunML.github.io/tutorial/Logistic-Regression/) tutorials, understanding how a learning algorithm works is somehow irritated. We got to go through boring theories, boring mathematical explanations and so on. Although I tried my best to make the explanation as simple as I can, but you know, functions is still functions, matrices are still matrices, there is no other way to get rid of those terms. But you won't have to go through that pain today. *Decision Tree* can totally be explained using human-understandable natural language. So keep reading, okay?

And before we get started, it's great to know that we have made it to the 8th post of the Machine Learning tutorial series. If you take a look back, I'm quite sure you will be surprised by how much you have progressed. We have learned two learning algorithms: *Linear Regression* and *Logistic Regression* respectively. We have worked on some simple dataset and visualized how your Model performed. At the moment, I'm quite sure that you are now familiar with Machine Learning. So in this post, we will use a more complicated set of data and see how our learning algorithms handle it.

So, let's talk about *Decision Tree*. You are somehow a real Model of Decision Tree algorithm yourself! In your daily life, you make many decisions exactly the same way *Decision Tree* does, subconsciously (of course). For example, your friend Joe invited you to his party. You may asked him back: "Any girls tonight?". He said yes. You asked him again: "Will Miley join too?". "Of course, homie!", he replied. And you accepted his invitation. The example I have just showed you is one of many situations that you may face everyday, in which you have to make your own decision on something. For that example, I can express it using the graph below:

![graph](images/tutorials/decision-tree/graph.png)

Simply enough, right? You may be wondering: Is this real that such simple algorithm can solve complicated classification problem? The answer is: Yes! To make it more clear to you, let's consider a bigger one:

|Weather|Temperature|Humidity|Injure|Mood|RUN|
|-------|-----------|--------|------|----|---|
|clear|<10|<70|slightly|happy|NO|
|shower|20~30|>80|fit|stressed|YES|
|storm|10~20|>80|fit|happy|NO|
|shower|10~20|>80|slightly|stressed|YES|
|clear|>30|70~80|fit|lazy|YES|
|storm|20~30|>80|fit|stressed|NO|
|clear|>30|70~80|severe|happy|NO|
|clear|10~20|<70|severe|stressed|NO|
|shower|10~20|70~80|slightly|happy|NO|
|shower|>30|>80|fit|happy|YES|
|storm|20~30|70~80|slightly|happy|NO|
|clear|10~20|<70|slightly|happy|?|

Let's see what we have here. Here's the dataset I created for demonstration. I actually created based on my running experience, but some examples may sound weird to you, please ignore them for now, lol. 

Let's say we want to predict whether I am gonna go for a run, based on some factors such as Weather, Temperature or even my Mood! And as you has learned so far, Weathers, Temperature, Humidity, Injure, Mood are just the features, and the YES or NO in the RUN column is the targets (or labels).

Before going further into an appropriate explanation on how the algorithm works, I will first show you how we can solve the problem using the approach above.

First, let's randomly pick one feature from the features above. We will use that feature as the first condition, exactly the same way you asked "Any girls tonight?" above. To make it easy, let's pick the first one, Weather. As you can see, Weather can be either *clear* or *shower* or even *storm*. We will then split our data into three groups according to the Weather feature. In terms of Decision Tree, each time we use a feature to split the data, we create one **node**, and each group is called one **subset**. Let's first see how the *clear* Weather subset looks like:

|Weather|Temperature|Humidity|Injure|Mood|RUN|
|-------|-----------|--------|------|----|---|
|*clear*|<10|<70|slightly|happy|NO|
|*clear*|>30|70~80|fit|lazy|YES|
|*clear*|>30|70~80|severe|happy|NO|
|*clear*|10~20|<70|severe|stressed|NO|

Let's take a look at the RUN column. Obviously, just knowing the Weather is clear is not enough to decide whether to make a run or not. Just like the example above, you didn't make your decision after just one question, right? So we will have to look for another feature, hoping it will help us decide. Let's pick the *Temperature* feature. Now we can omit the Weather column (because it contains only *clear*), and just like what we did, we see that the Temperature feature can be either *<10* or *10~20* or *> 30*, so we will now have three more subsets, let's say, subsets of the subset above (where Weather is *clear*):

|Temperature|Humidity|Injure|Mood|RUN|
|-----------|--------|------|----|---|
|*<10*|<70|slightly|happy|NO|

|Temperature|Humidity|Injure|Mood|RUN|
|-----------|--------|------|----|---|
|*10~20*|<70|severe|stressed|NO|

|Temperature|Humidity|Injure|Mood|RUN|
|-----------|--------|------|----|---|
|*>30*|70~80|fit|lazy|YES|
|*>30*|70~80|severe|happy|NO|

Let's take a look at three new subsets above. The first two subsets are already clear, because the RUN column in each subset contains only one value. In terms of Decision Tree, we call the result in those subsets **Leaf Nodes**, and when they are now **pure**, which means that the output contains only one value. Meanwhile, the third subset still requires some further work. But it's quite easy now. Let's go ahead and use the *Injure* feature to create two new subsets:

|Humidity|Injure|Mood|RUN|
|--------|------|----|---|
|70~80|*fit*|lazy|YES|

|Humidity|Injure|Mood|RUN|
|--------|------|----|---|
|70~80|*severe*|happy|NO|

Up to now, all the nodes in the *clear* Weather subset are clear, since there's no any node in which the RUN column contains more than one value. We can now move on to the rest two subsets: the *shower* Weather subset and the *storm* Weather subset. By doing exactly the same way, we will get a result in the end, where all the subsets are clear. I have created a another graph for a better visualization:

![run_graph](images/tutorials/decision-tree/run_graph.png)

Using the graph above, we can now predict the value of the RUN column for our last row above:

![run_graph_pred](images/tutorials/decision-tree/run_graph_pred.png)

So, it's likely that I'm gonna stay at home with my PlayStation 4 that night, lol.

So that's it. Just easy to understand like I said earlier, right? Of course, we have some kind of mathematical explanation for how Decision Tree actually does. For example, choosing which Feature to split in the beginning is not done randomly, but depends on some considerations. And each time we need to create new subsets from the parent subset, the process is repeated again. Why do we have to make things such complicated, you may ask. Technically say, Decision Tree is a greedy algorithm, which means that it's likely to fall into local-minimum rather than the desired global-minimum, which means we may get an ugly result if we run out of luck. I will give you a simple explanation for Decision Tree algorithm below for ones who concern. You can skip it to jump directly to the Python Implementation because the explanation is just optional.

###Decision Tree Python

As I mentioned in the previous tutorials, the **scikit-learn** library comes bundled with everything you need to implement Machine Learning algorithms with ease. Furthermore, the library provides us many methods to generate data for learning purpose. And today I will use one of them to create a more complicated dataset, just to see how well Decision Tree can handle that.

First, let's import necessary modules as usual:

{% highlight python %} 
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import make_classification
from sklearn.tree import DecisionTreeClassifier
from sklearn.cross_validation import cross_val_score
{% endhighlight %}

If you went through my last tutorial, you may now know a proper way to evaluate the performance of a Machine Learning Model using the *cross_val_score* method. And if you didn't, you can always give it a look here: [Cross Validation](https://chunml.github.io/ChunML.github.io/tutorial/Cross-Validation/).

Next, let's using *make_classification*, a method provided by scikit-learn library to generate data for classification problems.

{% highlight python %} 
X, y = make_classification(n_samples=100, n_features=2, 
	n_redundant=0, n_classes=2, n_clusters_per_class=1)
{% endhighlight %}

Let's plot the data we created to see what it looks like:

{% highlight python %} 
X1_min, X1_max = X[:, 0].min() - 0.1, X[:, 0].max() + 0.1
X2_min, X2_max = X[:, 1].min() - 0.1, X[:, 1].max() + 0.1

plt.scatter(X[:, 0], X[:, 1], c=y, cmap='rainbow')
axes = plt.gca()
axes.set_xlabel('X1')
axes.set_ylabel('X2')
axes.set_xlim([X1_min, X1_max])
axes.set_ylim([X2_min, X2_max])
plt.show()
{% endhighlight %}

In my case, the data looks like below. Note that your graph may be way different, since the *make_classification* method generates data in some unpredictable way.

![data](images/tutorials/decision-tree/data.png)

As you might notice, I also included Logistic Regression. That is because I want to compare the performance of the two classification algorithms that we have known so far. From now on, you will learn some more algorithms, and it's always a good practice to compare between them, to see what algorithm work best for a particular problem.

Let's train our Model using one algorithm at a time, and print out the mean accuracy of each algorithm respectively. We will, of course, use the *cross_val_score* method for evaluation:

{% highlight python %} 
clf = DecisionTreeClassifier()
score = np.mean(cross_val_score(clf, X, y, cv=5))
print('Decision Tree: {}'.format(score))

clf = LogisticRegression()
score = np.mean(cross_val_score(clf, X, y, cv=5))
print('Logistic Regression: {}'.format(score))
{% endhighlight %}

So let's run our code a few times and see how the two algorithms perform. Note that you have to run the *make_classification* too, or you will likely get the same results!

Here's my results:
{% highlight python %} 
Decision Tree: 0.97999
Logistic Regression: 0.99

Decision Tree: 0.98999
Logistic Regression: 0.99487

Decision Tree: 0.91
Logistic Regression: 0.935
{% endhighlight %}

