CONTRACT RUN SUMMARY
====================

Result: google_forms_to_zoho_leads completed successfully with all steps and assertions passing.

Root cause: All steps and assertions passed.

State reached: lead_created

Next step for you: Confirm the create API continues returning 201 and a non-null create.response.body.data.0.details.id in future runs.


WHAT HAPPENED
-------------

The workflow executed three steps in dev: get_form (GET) returned 200 and passed, fetch (GET) returned 200 and passed, and create (POST) returned 201 and passed. All five assertions passed, including response code checks and non-null ID validations for fetch.response.body.responses.0.responseId and create.response.body.data.0.details.id. The slowest step was create at 929 ms, but it still completed successfully. The run finished with 3/3 steps and 5/5 assertions passing.

WHY IT HAPPENED
---------------

This was a success because each HTTP call returned the expected status code: get_form = 200, fetch = 200, and create = 201. The verification assertions also passed, confirming fetch.response.body.responses.0.responseId was present and create.response.body.data.0.details.id was present. No failure_reason or first_failure_step applied because there was no failure. The end-to-end contract from Google Forms to Zoho Leads was therefore satisfied.

WORKFLOW STATE
--------------

Status: lead_created

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Confirm get_form continues to return HTTP 200 in dev.
2. Confirm fetch continues to return HTTP 200 and populate fetch.response.body.responses.0.responseId.
3. Confirm create continues to return HTTP 201 and populate create.response.body.data.0.details.id.