CONTRACT RUN SUMMARY
====================

Result: The run failed on the first API call: get_form returned 401 instead of the expected 200.

Root cause: expected status 200, got 401

State reached: get_form_failed

Next step for you: Verify the Google Forms request authentication/authorization for the scheduler environment and fix the credentials or token scope before retrying.


WHAT HAPPENED
-------------

The scheduled test run for google_forms_to_zoho_leads started in the dev environment and executed a single step: get_form. That step used GET and completed in 261 ms, but it failed with HTTP 401. No further workflow steps were executed after this first failure.

WHY IT HAPPENED
---------------

The run failed because the only step expected status 200 but received 401, which indicates unauthorized access rather than a functional response issue. There were no assertions in this run, so the failure is entirely driven by the HTTP status mismatch recorded on steps[0].error_message and summary.failure_reason. Since summary.first_failure_step is get_form, the workflow did not progress beyond form retrieval.

WORKFLOW STATE
--------------

Status: get_form_failed

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Confirm the GET get_form request is sending valid authentication for the dev scheduler run and that the token/key has not expired or been revoked.
2. Validate the configured permissions/scopes for the Google Forms endpoint so it can return 200 instead of 401, then rerun the workflow.

