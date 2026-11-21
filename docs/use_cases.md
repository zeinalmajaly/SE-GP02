
## Actors

| Actor | What they can do |
| --- | --- |
| Advisor | Review student records and dashboard analytics, request and review outcome estimates, override or dismiss estimates, and manage follow-ups. |
| Administrator | Review student records, dashboard analytics, prediction history, and follow-up history. View and export cohort reports, manage user accounts and roles, and review the audit log. |

Both actors sign in to access protected features. They can view model limitations and sign out to end their session.

The Data/ML Engineer is a development time actor shown in the C4 architecture. The Engineer loads the dataset and creates synthetic identities (FR-04), then trains, evaluates, and publishes a versioned model (FR-11 and FR-12). These activities take place outside the dashboard.
## Sign In

**Primary actors:** Advisor and Administrator.

**Precondition:** The user has an active account.

1. The user enters and submits their credentials.
2. The system verifies the credentials and starts a session with the user's assigned role.
3. The system opens the dashboard.

**Postcondition:** The user is signed in and can access the features allowed for their role.

**Alternate flow:** If the credentials are invalid or the account is inactive, the system displays an error and the user remains signed out.

## Review Student Records and Dashboard Analytics

1. The Advisor or Administrator opens the dashboard to view summary statistics and charts.
2. The actor searches or filters the student list and opens a student profile.
3. The actor reviews the profile, prediction history and explanations, and follow-up history.

## Request an Outcome Estimate

**Precondition:** The Advisor is signed in and has selected a student profile.

1. The Advisor requests an estimate for the selected student.
2. The Application API checks the Advisor's permissions and validates the required student data.
3. The Prediction Service uses the published model to estimate Dropout, Enrolled, or Graduate and returns probabilities and explanation data.
4. The API saves the result, model version, and generation time. The system logs the prediction request.
5. The Dashboard displays the outcome, all three class probabilities, the contributing factors, the model version, the generation time, and the decision-support notice.

**Postcondition:** The estimate is saved in the student's prediction history and displayed on the dashboard.

**Alternate flows:** If access is denied, the required data is missing or invalid, or the model is unavailable, the dashboard displays an error and shows no new estimate.

## Override or Dismiss an Estimate

**Precondition:** The Advisor is signed in and has selected an existing estimate.

1. The Advisor chooses to override or dismiss the estimate.
2. The Advisor enters a reason.
3. The system saves the decision, retains the original estimate, and logs the action.

**Postcondition:** The decision is saved, the original estimate is retained, and an audit entry is recorded.

**Alternate flow:** If the reason is missing, the system asks for one and leaves the estimate unchanged.

## Manage Advisor Follow-Up

**Precondition:** The Advisor is signed in and has opened a student profile. To update a follow-up, the Advisor selects an existing action.

1. The Advisor reviews the student profile and decides whether a follow-up is needed.
2. The Advisor enters the action type, note, assignee, and date. Linking a prediction is optional.
3. The system saves the action as Open and records an audit event.
4. The Advisor can add notes or request a status change. The normal progression is Open → In progress → Resolved → Closed.
5. The system validates the change and saves and audits valid updates.
6. Both roles can view the follow-up's current status and history.

**Postcondition:** A new follow-up is saved as Open. Valid updates appear in the follow-up history. Creation and updates are recorded in the audit log.

**Alternate flows:** If the Advisor decides no follow-up is needed, the review ends without creating an action. If required details are missing, the system asks for them before saving. If a status transition is invalid, the system displays an error and keeps the current status.


## Review and Export Cohort Reports

1. The Administrator reviews cohort summaries of predicted outcomes.
2. The Administrator can filter the reports by course and risk level.
3. The Administrator can export permitted report data as CSV. The system logs the export.

## Manage Accounts and Review the Audit Log

1. The Administrator can create or deactivate user accounts and assign roles.
2. The system records account and role changes in the audit log.
3. The Administrator can review audit events.

## Review Model Information

1. Either actor can review the model's intended use, performance, known limitations, and decision-support notice.
2. The system provides a summary of the features that are most important to the model overall.
