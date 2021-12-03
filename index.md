# ML Rapid Text Labeling

## Capstone Project for Master of Applied Data Science

## University of Michigan School of Information

### Contributors:
https://github.com/Tak-Man
https://github.com/michp-ai

December 2021

## ML Rapid Text Labeling - High Level Scenario
The amount of natural language text that is stored is growing rapidly and there is an ever-increasing demand to extract information from that text. Many supervised learning applications exist for Natural Language Processing (NLP). Supervised learning requires labels to be attached to the text. Many texts do not have labels currently and there are many cases where it would be beneficial to add labels to text. Labeling can be slow, laborious and prone to error. There are many questions about labeling such as, how many labels is enough? Is it better to aim for more labels, or to aim for fewer labels of higher quality? What is an efficient way of labeling texts? In this Capstone project we build a web app that illustrates a user-friendly way of doing rapid text labeling. It gives a real-time indicator to the labeling user that can act as a reasonable guide about how many labels are enough. The web app implements multiple Data Science and Machine Learning techniques to enable the labeling user to progress through the labeling of a text corpus making decisions along the way about the trade-off between accuracy and speed. The final project submission consists of two repositories.


### Purpose

This notebook investigates how well a classifier can predict the **event type (i.e. 'earthquake', 'fire', 'flood', 'hurricane)** of the Tweets in the [Disaster tweets dataset](https://crisisnlp.qcri.org/humaid_dataset.html#).

This classifier is to be used as a baseline of classification performance. Two things are investigated:
- Is it possible to build a reasonable 'good' classifier of these tweets at all
- If it is possible to build a classifier how well does the classifier perform using all of the labels from the training data

If it is possible to build a classifier using all of the labels in the training dataset then it should be possible to implement a method for rapidly labeling the corpus of texts in the dataset. Here we think of rapid labeling as any process that does not require the user to label each text in the corpus, one at a time.

To measure the performance of the classifier we use a metric called the Area Under the Curve (AUC). This metric was used because we believe it is a good metric for the preliminary work in this project. If a specific goal emerges later that requires a different metric, then the appropriate metric can be used at that time. The consequence of false positives (texts classified as having a certain label, but are not that label) and false negatives should be considered. For example, a metric like precision can be used to minimize false positives. The AUC metric provides a value between zero and one, with a higher number indicating better classification performance.




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
