## Assignment 5: Convolutional Neural Networks and Transformers
Assignment Date: Monday, November 9, 2026 <br>
Due Date: Sunday, November 15 @ 11:59pm <br>

### Assignment Overview

In this assignment you will explore a couple of key aspects of convolutional neural networks such as self-attention and feature encoding as well as explore a pre-trained convolutional neural network for gene expression prediction. For this assignment, we will provide a Jupyter notebook with code for you to use and complete your assignment in. 

For this assignment, you will create the environment as follows:

`mamba create -n asn5 python=3.10 scikit-learn pytorch matplotlib pandas numpy jupyter seaborn kipoiseq logomaker`

If installation fails due to "warning: libmamba - Problem type not implemented SOLVER_RULE_STRICT_REPO_PRIORITY", try running the following and then attempt the above command again:

`conda config --set channel_priority flexible`

Then activate the environment and install the following package using pip:

`mamba activate asn5`

`pip install enformer-pytorch`

If you have issues with creating the environment and installing the required packages, you can use [Google Colab](https://colab.research.google.com/)

You will need to add the following cells to the top of the notebook in Google Colab to install the dependencies:

```
!pip install kipoiseq==0.5.2
!pip install logomaker
!pip install enformer-pytorch
```

Because of the way Google Colab works, you will need to install these every time you reopen the notebook. 

As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/).

See the notebook here: [Assignment5.ipynb](Assignment5.ipynb)


### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and all relevant code, text, and figures (as needed). If you use ChatGPT for any of the code, also record the prompts used. Submit your solutions by uploading the PDF to [GradeScope](https://www.gradescope.com/courses/1370921), and remember to select where in your submission each question/subquestion is.  

If you submit after this time, you will use your late days. Remember, you are only allowed 4 late days for the entire semester!


### Resources

* Jupyter notebooks: [https://jupyter.org/](https://jupyter.org/)
* scikit-learn: [https://scikit-learn.org/stable/](https://scikit-learn.org/stable/) 
* pytorch: [https://pytorch.org/](https://pytorch.org/)
* pytorch tutorial: [https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html)
