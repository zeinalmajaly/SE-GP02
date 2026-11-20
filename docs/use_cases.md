
## Actors

| Actor | What they can do |
| --- | --- |
| Advisor | Review student records and dashboard analytics, request and review outcome estimates, override or dismiss estimates, and manage follow-ups. |
| Administrator | Review student records, dashboard analytics, prediction history, and follow-up history. View and export cohort reports, manage user accounts and roles, and review the audit log. |

Both actors sign in to access protected features. They can view model limitations and sign out to end their session.

## Review Student Records and Dashboard Analytics

1. The Advisor or Administrator opens the dashboard to view summary statistics and charts.
2. The actor searches or filters the student list and opens a student profile.
3. The actor reviews the profile, prediction history and explanations, and follow-up history.

## Request an Outcome Estimate

1. The signed-in Advisor opens a student profile and requests an estimate.
2. The Application API checks the Advisor's permissions and validates the required student data.
3. The Prediction Service uses the published model to estimate Dropout, Enrolled, or Graduate and returns probabilities and explanation data.
4. The API saves the result, model version, and generation time. The system records the prediction request in the audit log.
5. The Dashboard displays the estimated outcome, all three class probabilities, the contributing factors, the model version, the generation time, and the decision-support notice.
6. If access is denied, the data is invalid, or the model is unavailable, the Dashboard shows an error. No new estimate is displayed.

## Override or Dismiss an Estimate

1. The Advisor reviews an estimate and chooses to override or dismiss it.
2. The Advisor enters a reason.
3. The system records the decision, retains the original estimate, and logs the action.

## Manage Advisor Follow-Up

1. The Advisor reviews the student profile and decides whether a follow-up is needed.
2. The Advisor enters the action type, note, assignee, and date. Linking a prediction is optional.
3. The system saves the action as Open and records an audit event.
4. The Advisor can add notes or request a status change. The normal progression is Open → In progress → Resolved → Closed.
5. The system rejects invalid status transitions and saves and audits valid updates.
6. Both roles can view the follow-up's current status and history.

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
