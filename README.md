# 1.Funding Successful Projects(Classification Problem)
Funding successful project is a binary classification problem.
# 1. Business Problem
## 1.1 Problem Context

Our client is a large community of tech enthusiasts called Kickstarter.

- This community aids people in bringing out creative projects.
- Till now, more than 3 billion dollars have been contributed by the members in fuelling creative projects.
- It works on All or Nothing basis i.e if a project dosen't meet its goal, the project owner gets nothing.

## 1.2 Problem Statement

- Recently, Kickstarter released its public data repository to allow researchers and enthusiasts like us to help them solve a problem.
- The problem is regarding whether a project will get successfully funded or not.
- If we are able to build such a model that predicts whether a project will be funded as per its requirements, it can help the community to determine beforehand, its successful completion.

## 1.3 Business Objectives and Constraints

-  Deliverable: Trained model file.
-  Ouput Probabilities along with the prediction.
-  Model interprtability is very important
-  No latency constraints.

# 2. Machine Learning Problem

## 2.1 Data Overview
For this project:

1. The train dataset and the test datset has 108129 observations and 63465 obervations respectively.
2. The train data consists of sample projects from the May 2009 to May 2015. The test data consists of projects from June 2015 to March 2017.
3. Each observation in the train and test sets refers to a project's description and status.

**Target Variable**
- 'final_status' - whether the project got successfully funded (target variable – 1,0)

**Features of the data:**

Unique characteristics

* project_id - unique id of project
* name - name of the project
* desc - description of project
* goal - the goal (amount) required for the project
* keywords - keywords which describe project

General project specifications 

* disable communication - whether the project authors has disabled communication option with people donating to the project
* country - country of project author
* currency - currency in which goal (amount) is required
* deadline - till this date the goal must be achieved (in unix timeformat)
* backers_count - no. of people who backed the project

Project state information

* state_changed_at - at this time the project status changed. Status could be successful, failed, suspended, cancelled etc. (in unix timeformat)
* created_at - at this time the project was posted on the website(in unix timeformat)
* launched_at - at this time the project went live on the website(in unix timeformat)
* final_status - 	whether the project got successfully funded (target variable – 1,0)

## 2.2 Mapping business problem to ML problem

### 2.2.1 Type of Machine Learning Problem

It is a binary classification problem, where given the above set of features, we need to predict if a given project will be successfully funded or not.

### 2.2.2 Evaluation Metric (KPI)

Since this is binary classification problem, we use the following metrics:
* **Confusion matrix** - For getting a better clarity of the no of correct/incorrect predictions by the model
* **ROC-AUC** - It considers the rank of the output probabilities and intuitively measures the likelihood that model can distinguish between a positive point and a negative point. (**Note:** ROC-AUC is typically used for binary classification only). We will use AUC to select the best model.

# 3.Feature Engineering 

### 3.1.Features Created:
##### time_to_achieve:
* This features shows time required to complete the project.
* Feature is created using two other features: launched_at and created_at
* The difference between launched_at and created_at gives the time in terms of number of days required to complete the project.
##### completion_before_deadline:
* This features shows how early the project state is changed before the deadline.
* Feature is created using two other features: launched_at and deadline.
* The difference between deadline and launched_at gives how early the project is launched before the deadline.
##### time_to_change_the_status:
* One more feature is created which gives the number of days in which the status of the project changes after it is launched

### 3.2.Features Removed:
* Features such as project_id, description, name, keywords and other unused features are removed.
