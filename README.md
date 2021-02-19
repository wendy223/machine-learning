# machine-learning
predict material properties by their structures

Hi everyone,

I am Wendy and I like soup noodle. 

This is my course homework & project written in Jupyter Notebook.

If you have any issue about opening these jupyter notebook, please try below:
1. Open "https://nbviewer.jupyter.org/"

2. paste the github linkage into the opened nbviewer


# Requirements
## 1. When the app is started, the user is presented with the main menu, which allows the user to (1) enter or edit current job details, (2) enter job offers, (3) adjust the comparison settings, or (4) compare job offers (disabled if no job offers were entered yet).  

**A class “User” is added to execute these four actions in the main menu. I added four attributes for each user. The “name” and “userID” are used to identify the user. The “hasCurrentJob” is boolean to record whether this user has a current job or not.** 

**I added four operators (“editCurrentJob”, “enterJobOffer”, “adjustComparisonSetting”, “compareJobOffers”) for the user to meet the requirement. These four operators stand for the capacity of the user to navigate inside this app.**

**The attribute “numberOfJob”, including current job and job offers, is used to count the total number of jobs the user has. If it’s equal or greater than two, it will enable the “compareJobOffers” operators/button.** 


## 2. When choosing to enter current job details, a user will:

### 2.1. Be shown a user interface to enter (if it is the first time) or edit all of the details of their current job.

**When the user clicks the edit current job, it will first check the attribute(“hasCurrentJob”) of “User”. If it’s false, it will provide a user interface for the user to enter the current job. If it’s true, it will load the current job to the UI for use to edit. The loading is invoked by the “getCurrentJob” operator.**
 
**To edit the current job, I added a class “CurrentJob”, which is a subclass of “Job”. “CurrentJob” will inherit these attributes from the superclass “Job”.** 

### 2.2. Be able to either save the job details or cancel and exit without saving, returning in both cases to the main menu.

**To achieve this requirement, two operators are evoked. “saveJob” is to save the job details, similar to the “setValue” in Java. This operator is connected with the “save” button in the UI. If “saveJob” is executed, the attribute “hasCurrentJob” in “CurrentJob” class will be updated to be True.**

**If the user doesn’t want to save it, the operator “cancelJob” can be used to discard the change. After clicking either the save or cancel button on the UI, it will return to the main menu.**

## 3. When choosing to enter job offers, a user will:

### 3.1 Be shown a user interface to enter all of the details of the offer, which are the same ones listed above for the current job.

**To enter the details of the job offer, I added a class “JobOffers”, which is a subclass of “Job”. “JobOffers” will inherit all attributes from the superclass “Job”. If “saveJob” is executed, the attribute “hasJobOffer” in “JobOffers” class will be updated to be True.**

### 3.2 Be able to either save the job offer details or cancel.

**To achieve this requirement, two operators are evoked. “saveJob” and “cancelJob” are inherited from the superclass “Job”.**


### 3.3 Be able to (1) enter another offer, (2) return to the main menu, or (3) compare the offer (if they saved it) with the current job details (if present).

**“Enther another offer” and “return to the main menu” are not shown here in my design. These two functions can be achieved with the UI implementation. Entering another offer is just to initiate a new JobOffer class. Returning to the main menu is just a button back to the main menu.** 

**“Compare offers” is to compare the current job offer (if saved) with the current job details(if present). Thus, we need to compare two classes. I added the operator “compareWithCurrentJob” to achieve this comparison. If both “hasCurrentJob” and “hasJobOffer” are true, it will start to compare them. This operator will invoke “CurrentJob”, “JobOffer”, and “Comparison’.**

		
## 4. When adjusting the comparison settings, the user can assign integer weights to:

Yearly salary
Yearly bonus
Allowed weekly telework days
Retirement benefits
Leave time
If no weights are assigned, all factors are considered equal. 

**A class “ComparisonSetting” is added. Five attributes are added to record these five weights. If no weights are assigned, to make all factors equal, I initiate each weight using 1. The operator “saveSetting” here is to save the user's adjustment.**

## 5. When choosing to compare job offers, a user will:

### 5.1 Be shown a list of job offers, displayed as Title and Company, ranked from best to worst (see below for details), and including the current job (if present), clearly indicated.

**To achieve this, a class “Comparison” is added. For each user, collect the user's current job and job offering information and calculate the score for each job by operator “calculateScoreForEachJob”. Then, rank each job based on their score by the operator “rankAllJobs” and display it with title and company and score in descending order. If a current job is present, indicate it; this can be achieved by knowing the attribute “hasCurrentJob”.**
		
**The class “ComparisonSetting” is used to calculate the score.**

### 5.2 Select two jobs to compare and trigger the comparison.

**After the user selects any of two jobs and clicks the button “compare”, this can be achieved by operator “compareTwoJobs”. The input can be any of two jobs (either job offer or current job).** 

### 5.3 Be shown a table comparing the two jobs, displaying, for each job:
Title
Company
Location
Yearly salary adjusted for cost of living
Yearly bonus adjusted for cost of living
Allowed weekly telework days
Retirement benefits (as percentage matched)
Leave time

**This can be achieved by operator “compareTwoJobs”. The input can be any of two jobs (either job offer or current job). The operator can return these values of interest to display. The display format can be handled by the UI.** 


### 5.4 Be offered to perform another comparison or go back to the main menu.

**Buttons “Perform another comparison” and “Back to main menu” can handle this part.** 


## 6 When ranking jobs, a job’s score is computed as the weighted sum of:

AYS + AYB + (RBP * AYS) + (LT * AYS / 260) - ((260 - 52 * RWT) * (AYS / 260) / 8)

where:
AYS = yearly salary adjusted for cost of living
AYB = yearly bonus adjusted for cost of living
RBP = retirement benefits percentage
LT = leave time
RWT = telework days per week
The rationale for the RWT subformula is:
value of an employee hour = (AYS / 260) / 8
commute hours per year (assuming a 1-hour/day commute) =
1 * (260 - 52 * RWT)
therefore travel-time cost = (260 - 52 * RWT) * (AYS / 260) / 8

For example, if the weights are 2 for the yearly salary, 2 for the retirement benefits, and 1 for all other factors, the score would be computed as:


2/7 * AYS + 1/7 * AYB + 2/7 * (RBP * AYS) + 1/7 * (LT * AYS / 260) - 1/7 * ((260 - 52 * RWT) * (AYS / 260) / 8)

**The score is calculated for each job by operator “calculateScoreForEachJob”. The formula shown here can be written into this operator. The class “ComparisonSetting” is required here to initiate the weight for each variable.**


## 7. The user interface must be intuitive and responsive.

**it will be handled by UI implementation.**

## 8. For simplicity, you may assume there is a single system running the app (no communication or saving between devices is necessary).

**it will be handled by UI implementation.**
