CONTRACT RUN SUMMARY
====================

Result: The todos_crud run failed on the first step because the create request returned 401 instead of the expected 201.

Root cause: Authentication/authorization was rejected on the POST create step, causing the status assertion to fail.

State reached: create_failed

Next step for you: Fix the auth setup for the POST /create path and rerun the test to confirm it returns 201.


WHAT HAPPENED
-------------

The test run "todos_crud" in the dev environment executed one step: create (POST). That step failed after 1378 ms with HTTP 401, so the workflow stopped immediately. The only assertion, create status, also failed because it expected 201 but got 401. No later CRUD steps were reached.

WHY IT HAPPENED
---------------

The failure occurred at the first step, matching summary.failure_reason and summary.first_failure_step: "test \"todos_crud\" failed at step \"create\"". The step-level status_code was 401, which directly violated assertion s1 with expression "= 201" and error_message "expected status 201, got 401". This indicates the request was unauthorized rather than successfully creating a resource.

WORKFLOW STATE
--------------

Status: create_failed

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Verify the create request includes valid authentication/authorization credentials for the dev environment so POST returns 201 instead of 401.
2. Confirm the create endpoint’s security requirements and rerun the test to validate the create status assertion passes before proceeding to downstream CRUD steps.