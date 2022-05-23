## Deep-Learning-Challenge

### Overview

The goal of this deep learning model is to analyze whether a given applicant for funds will ultimately succeed. Two thoughts instantly come to mind:
 
A. This dataset is a solid use-case for deep learning as an application can obviously contain disqualifying information, even from a human perspective (e.g. an outrageous ask amount). As such an unbiased look at the data from the perspective of ML can tell us how predictive a given application can be.

B. That being said, an algorithm which performs TOO well (say, greater than 85%) should be looked at with suspicion as there are many confounding factors to a charity's success. An important figure could experience serious illness, a competing entity could crop up with even more funding at just the wrong time, perhaps your charity was founded in the months before covid.

As such, we should set for ourself a realistic target and the goal of this project, 75%, seems quite realistic and we were able to achieve it.

### Explanation of Model

Our target for this model was simply the "IS_SUCCESFUL" column, which should be self-explanatory.

The remaining columns consisted of a serialized id, name, application type, charity type, affiliation, classification, status, organization, sepcial consideration, income and ask_amt.

We dropped the id column as it has no bearing on success as well as the special considerations and status for containing extremely lopsided distributions of features. Special considerations, for instance, was a binary yes or no column with less than 100 yes entries in tens of thousands of lines.

Our initial performance was about 72.5 percent accuracy.

### Optimization of Model
We initially dropped the name column, but upon further inspection, the applications often came from multiple bodies within the same organization, so it was added back in and binned, along with application type and classification.

The income was originally non-numeric and consisted of a range. I converted that to an average of those two values, as well as converting some shorthand to actual values. For instance 10M-50M was replaced with 35000000 to allow for appropriate and continuous scaling. I also added a column to the dataframe which calculated the income/ask amount which, arguably, is the job of the ML model to pick up on however adding it as it's own column should allow it to more explicitly see that as a feature of the dataset as it is arguably the single most important predictor of an application's success.

Our final model consisted of 1 input layer of 100 nodes and 2 input layers of 40 and 30 nodes. Interestingly, as more nodes and layers were added, the performance actually suffered. These numbers were found by iterating between 10 and 500 nodes, taking the halfway point after every test in the direction that was most successful.

Various optimizations were utilized as well, however had the best performance.

Finally, a significant increase in accuract was found by utilizing a swish activation function as opposed to relu. Swish has extremely similar shape to relu but has the possibility for slight negatives and has a gentler gradient at 0 on the x-axis. It feels to me like another great all-purpose activation function to use in conjunction with relu.

Our final accuracy was 0.7624 so we were able to hit the target.

