# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

The sampling in the model occurs in the following stages
1.	Infecting Individuals: Randomly selecting 10% of individuals to be infected.
2.	Primary Contact Tracing: Randomly selecting 20% of infected individuals to be traced.
3.	Secondary Contact Tracing: Selecting events with at least two traced individuals and marking all infected individuals at those events as traced.

Sampling Procedure
A.	Creating Population:
	    Function: simulate_event
	    Sample Size: 1000 
	    Sampling Frame: Consists of all individuals attending weddings or brunches.
	    Procedure: Dataframe ppl is created with 200 wedding and 800 brunch events. This represents the total population.
B.	Infecting Individuals:
	    Function: simulate_event
	    Sample Size: 10% of the total population - 100
	    Procedure: Random selection and marked as infected using np.random.choice. This selection is based on the ATTACK_RATE (0.10).
C.	Primary Contact Tracing:
	    Function: simulate_event
	    Sample Size: 20% of infected individuals - 20
	    Procedure: Randomly selection for tracing using np.random.rand (sum(ppl['infected'])) < TRACE_SUCCESS. This selection is based on the TRACE_SUCCESS rate (0.20).
D.	Secondary Contact Tracing:
	    Function: simulate_event
	    Sampling Frame: Infected individuals traced in the primary stage and those attending events with at least two traced individuals.
	    Procedure: Secondary tracing is performed based on event attendance. If an event has at least two traced individuals (SECONDARY_TRACE_THRESHOLD), all infected individuals 
        attending that event are marked as traced. This is done using the value counts of traced individuals per event and updating the tracing status accordingly.


Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

1.	The script's output shows clear peaks for both the infections from weddings (blue) and the traced to weddings (red). The peaks are close together, and the distributions are relatively narrow. The blog post's graph has a much broader red distribution (observed proportion) that spans almost the entire x-axis. The blue distribution (true proportion) is more sharply peaked, indicating a narrower range of true infection proportions.
2.	In the script Graph the proportions of infections and traces from weddings are centered around 0.15 to 0.25, with fewer cases in the extreme ends while in the original blog post the true proportion is centered around 0.2, but the observed proportion varies widely from 0 to almost 1.
3.	Also, the blog's graph appears to illustrate a more significant bias because the observed proportion is spread over a larger range.



Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Comparison of graphs with 1000 reps and 5000 reps 
1.	Both graphs have a similar overall shape. They both show a peak around the 0.20-0.25 range for both infections from weddings and cases traced to weddings. This suggests that the simulation tends to produce results where around 20-25% of infections come from weddings, and a similar proportion of cases are traced back to them.
2.	With more repetitions the data points are more spread out creating a smoother curve.
3.	Based on the comparison the results seem to be fairly reproducible. The overall shape and trend are similar between the two graphs which means that increasing the number of repetitions has not changed the outcome. However, the increased smoothness and taller bars in the 5000 reps graph indicate that more repetitions provide a clearer and more detailed picture of the results.



Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times


Moved np.random.seed(10) to the beginning of the script just before the simulation function. This way all random operations performed within the function have becom reproducible. All subsequent random operations within the simulation will generate the same sequence of random numbers each time the script is run and so that means the results will be consistent


#

```
Please write your explanation here...

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
