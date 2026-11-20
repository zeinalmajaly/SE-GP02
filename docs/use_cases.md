# Use Cases

## Actors
- Advisor: Reviews student records, requests outcome estimates, and manages follow-up actions.
- Administrator: Reviews student records, prediction history, and follow-up history, and views cohort reports.

## Request Outcome Estimate
1. The signed-in Advisor opens a student profile and requests an estimate.
2. The system checks the Advisor's permissions and validates the student data.
3. The prediction service returns an estimated outcome, explanation, and model version.
4. The system saves the result and displays it with a decision-support notice.
5. If the input is invalid or the model is unavailable, the system displays an error.

## Manage Advisor Follow-Up
1. The Advisor reviews the student record and decides whether to record a follow-up.
2. The Advisor enters the action type, note, assignee, and date. Linking a prediction is optional.
3. The system saves the follow-up as Open and logs the action.
4. The Advisor adds notes or updates the status through In progress, Resolved, and Closed.
5. The system rejects invalid status changes and logs valid updates.
