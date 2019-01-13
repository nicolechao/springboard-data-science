# Take Home Challenge Exercise


## Problem: User Engagement Data Analysis
Given a user table with data on 12,000 users who signed up for the product in the last two years and usage summary table that user logged-in hitstory, defining an "adopted user" as a user who has logged into the product on three separate days in at least one sevenday period, identify which factors predict future user adoption.


## Data
1. A user table ( "takehome\_users" ) with the following columns:
  * name: the user's name
  * object_id: the user's id
  * email: email address
  * creation_source: how their account was created. This takes on one of 5 values:
     * PERSONAL_PROJECTS: invited to join another user's personal workspace
     * GUEST_INVITE: invited to an organization as a guest (limited permissions)
     * ORG_INVITE: invited to an organization (as a full member)
     * SIGNUP: signed up via the website
     * SIGNUP\_GOOGLE\_AUTH: signed up using Google Authentication (using a Google email account for their login id)
  * creation_time: when they created their account
  * last_session_creation_time: unix timestamp of last login
  * opted_in_to_mailing_list: whether they have opted into receiving marketing emails
  * enabled_for_marketing_drip: whether they are on the regular marketing email drip
 * org_id: the organization (group of users) they belong to
 * invited\_by\_user_id: which user invited them to join (if applicable).
2. A usage summary table ( "takehome\_user\_engagement" ) that has a row for each day that a user logged into the product.


## Approach
1. Apply data wrangling to fix data types and fill missing values and fix outliers if applicable.
2. Define adopted user using time series analysis techniques.
3. Analyze features predict future user adoption using logistic regression.


## Conclusion
Based on the logistic regression results, we can conclud that creation source seems to be the best feature for predicting future user adoption.

Business-wise, we can analyze more on this feature. For example, there are total 5 different values of it now, which are 'GUEST_INVITE', 'ORG_INVITE', 'PERSONAL_PROJECTS', 'SIGNUP' & 'SIGNUP_GOOGLE_AUTH'. We can further analyze which of them has the best user adoption and see if there are similar organization/user that can potentially be future users.

In conclusion, the model can be useful to identify features to predict future user / organization adoption.


## Deliverables
1. Data wrangling, exploratory data analysis & modeling code in Python notebook.
