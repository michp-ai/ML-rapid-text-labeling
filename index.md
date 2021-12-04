# ML Rapid Text Labeling

## Capstone Project for Master of Applied Data Science

## University of Michigan School of Information

### Contributors:
* https://github.com/Tak-Man
* https://github.com/michp-ai

December 2021

## ML Rapid Text Labeling - High Level Scenario
The amount of natural language text that is stored is growing rapidly and there is an ever-increasing demand to extract information from that text. Many supervised learning applications exist for Natural Language Processing (NLP). Supervised learning requires labels to be attached to the text. Many texts do not have labels currently and there are many cases where it would be beneficial to add labels to text. Labeling can be slow, laborious and prone to error. There are many questions about labeling such as, how many labels is enough? Is it better to aim for more labels, or to aim for fewer labels of higher quality? What is an efficient way of labeling texts? In this Capstone project we build a web app that illustrates a user-friendly way of doing rapid text labeling. It gives a real-time indicator to the labeling user that can act as a reasonable guide about how many labels are enough. The web app implements multiple Data Science and Machine Learning techniques to enable the labeling user to progress through the labeling of a text corpus making decisions along the way about the trade-off between accuracy and speed. The final project submission consists of two repositories.
1. https://github.com/Tak-Man/ML-rapid-text-labeling-app This is the web app itself
2. https://github.com/Tak-Man/ML-rapid-text-labeling This repo is used to analyse the dataset selected for this project and evaluate the performance of the web-app in terms of speed and accuracy.

The web app itself is intended to be available on a live url for users and readers to interact with and ideally to allow users to label their own corpus of text.

_insert short demo video of the web app_

The web app is designed to allow unlabeled datasets to be labeled. However, in the project itself, we used a labeled dataset but then in the app treated it as unlabeled. We did this because it allowed us to measure certain benchmarks in terms of accuracy and to see how well the web app performed against those benchmarks. If we had started with a completely unlabeled dataset we would not have been able to have that baseline comparison. Using a pre-labeled dataset also had some further advantages in terms of evaluating the product. These will be explained later in more detail. At a high level though we evaluated the product partially through manually interacting with the web app, partly through web automation to simulate multiple potential paths that a user could reasonably take given the dataset and the functionality available in the web app, and partly by doing NLP on the underlying dataset directly to establish the benchmarks themselves.


### Dataset
The main dataset used in this project is the [Disaster tweets dataset](https://crisisnlp.qcri.org/humaid_dataset.html#). This dataset was pre-approved for the Capstone project and meant that the project could focus on steps 1, 3 and 4 of the Data Science Project lifecycle namely Project Design, Analysis and Modeling and finally deployment and presentation of results. Step 2 data collection and cleaning was effectively done by the providers of this dataset. In the Milestone projects I spent a lot of time and effort on data collection through automated web-scraping and for this project it was more beneficial to focus on the other areas mentioned which was made possible by the use of a pre-existing dataset. The dataset contains fifty-three thousand labeled training examples. Another advantage of this datset is that it actually contains 2 separate types of labels. There is an event type which is one of "Earthquake", "Fire", "Flood" or "Hurricane". This is the label type used in the web app. 

There is also a class type which classifies the event not so much in terms of the type of disaster but more in terms of the consequences of the event and human responses. The figure below illustrates the class type of labels with the dataset along with their value counts.

![alt_labels_df](https://user-images.githubusercontent.com/48130648/144719083-23410271-6b13-401b-959a-9424f6ed2546.JPG)

_insert image of the dataset in pandas_

## How we Built the Web App
### Development with Flask
_Tak-Man to update this section, images and videos welcome_

### Deployment with Heroku
_Tak-Man to update this section, images and videos welcome_

### How did we think about Speed?
We thought about speed mainly from the user's point of view. We thought about it as the number of labeling actions, and the length of time each labeling action took. This meant that we had to use Data Science techniques that ran fast enough that someone using a website would find acceptable. It is important to repeat that there is a trade-off between speed and accuracy in any labeling process. Although we wanted the web app to be fast we also wanted to achieve reasonable accuracy. This is not the same as optimal accuracy that could be achieved by individually labeling each of the 53,000 examples and then attempting a Kaggle style optimisation of the accuracy against the test set by running multiple different sophisticated models and ensembling the results together. Instead we were looking for a reasonable level of accuracy that could be acceptable in a real-world scenario. A motivating example for this came from a workplace setting where one of the team had to manually label thousands of customer emails with the department they should be sent to for further investigation. The process of labeling was very slow and the list of emails was gorwing as the labeling was done. Potentially this could have been a never ending task! A tool to speed up the process would have been very useful so that beyond that supervised learning techniques could then start learning and automatically identifying which emails should go to which department. However, we believe that although the app grew out of this one example, there are many other potential use cases in NLP where rapid labeling of text would be very useful. Obviously in each case the user wil have to decide based on the dataset and the purpose of the labeling how they want to handle the trade-off between accuracy and speed. During that process they should consider speed of labeling itself, speed of model training and speed of inference or making predictions. The way we built the web app itself allowed for speed of user interaction which included model training and in some cases prediction as well for the automated labeling options. In the evaluation we timed both how long the models would take when running with the app and how long those models would take to train and predict outside the app.

### Benchmarking using Existing Labels
The labeling process is always a trade off between speed and accuracy. As a starting point we trained the model on different sized subsets of the training data and used the trained model to predict against the test set provided with the data. We then plotted a curve to see the accuracy achieved against the test set with differing amounts of training data. We repeated this for three different fast machine learning models available in scikit-learn. Another important variable that impacts speed and accuracy is the maximum number of features output by the vectorizer. We experimented setting this to 100, 200, 300, 500, 800 and leaving it blank i.e. to take the full output of the vectorizer without constraining the number of features. We produced several charts of our benchmark runs. These visualizations helped us to compare the results in terms of speed and accuracy across the various settings of our grid search on the parameters of model type, max number of vectorizer features, and, number of training examples. _insert example viz_

### What we learned through using the App Ourselves
Using the app ourselves a few things became obvious. The functionality to label single texts worked in a timely fashion and could allow labeling an entire corpus, however, it would be extremely slow. As in the example of an initial labeling of emails, only in the case where extreme accuracy was needed would it make sense to label 53,000 individually. The functionality to select a single text then locate similar texts by cosine similarity also worked well and enabled a batch labeling of those other texts with the same label. It also allowed each of the batch of tweets to be inspected before the user decided to batch label, and it allowed the user to adjust the size of the batch. Perhaps the user is happy with the top 10 most similar texts that they do share the same label but in the top 50 most similar they may notice a few that should not share the same label so they can choose to just label the 10 most similar. This will still be quicker than individual labeling. The user doesn’t have to manually check the similar texts, but the option is available. Once some labels of all types are available the functionality to learn from existing labels to generate new labels is available. Just like the similar texts functionality the user can inspect the texts that the app is proposing to label and can control the size of the batch to achieve their desired trade-off between speed and accuracy. The ability to search for texts and have exclude words in the search worked well. This was not constrained to the size of the batch so in some cases we saw that in one action we were able to label more than 30,000 of the 50,000 texts just by finding texts that matched one of the keywords. The processing time to label 30,000 tweets was a little longer than labeling 1 or 100 at a time but it was not unacceptably slow. Using the app made us realise that we had effectively allowed the user to have a large degree of control over the speed vs accuracy trade off. Another tool that worked well was the difficult texts section. This highlighted the texts that the supervised model was confident about labeling. This allowed the user to home in on those ones and provide the true label.
The Web App did report an overall quality score which is simply entropy calculated on predictions of the model. We didn’t really refer much to this or know how to interpret the results and as a result we did some more work on this in our evaluation. Through using the app we also realised that a save function would be very useful and this was implemented around half way through the project.



### Feedback we got from User Demos


### What we Learned from Automated Evaluation


### Software Development Approach and Lessons Learned




This classifier is to be used as a baseline of classification performance. Two things are investigated:
- Is it possible to build a reasonable 'good' classifier of these tweets at all
- If it is possible to build a classifier how well does the classifier perform using all of the labels from the training data

If it is possible to build a classifier using all of the labels in the training dataset then it should be possible to implement a method for rapidly labeling the corpus of texts in the dataset. Here we think of rapid labeling as any process that does not require the user to label each text in the corpus, one at a time.

To measure the performance of the classifier we use a metric called the Area Under the Curve (AUC). This metric was used because we believe it is a good metric for the preliminary work in this project. If a specific goal emerges later that requires a different metric, then the appropriate metric can be used at that time. The consequence of false positives (texts classified as having a certain label, but are not that label) and false negatives should be considered. For example, a metric like precision can be used to minimize false positives. The AUC metric provides a value between zero and one, with a higher number indicating better classification performance.






# Original Markdown Notes

You can use the [editor on GitHub](https://github.com/michp-ai/ML-rapid-text-labeling/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/michp-ai/ML-rapid-text-labeling/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
