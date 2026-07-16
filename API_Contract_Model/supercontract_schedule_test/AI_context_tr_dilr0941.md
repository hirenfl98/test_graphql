CONTRACT RUN SUMMARY
====================

Result: The google_forms_to_zoho_leads E2E run succeeded with all 6 steps and 3 assertions passing.

Root cause: All steps and assertions passed.

State reached: create_verified

Next step for you: Confirm the skip-on-existing-record behavior remains intentional for both create#0 and create#1 paths.


WHAT HAPPENED
-------------

The run executed in dev for google_forms_to_zoho_leads and completed successfully in 2199 ms. Step get_form (GET) returned 200 and passed, followed by fetch (GET) returning 200 and passing its response assertion. The workflow then processed create#0 and create#1: each search substep returned 200, and each create step was skipped because a CRM record already existed.

WHY IT HAPPENED
---------------

The run passed because every HTTP step returned the expected status code and every assertion succeeded. The assertions s1 and s2 both validated status 200, and v3 confirmed fetch.response.body.responses.0.responseId was not null. The two create skips were expected, with step-level error_message values indicating existing CRM records and events upsert_skip tying both skips to create#0 and create#1.

WORKFLOW STATE
--------------

Status: create_verified

Relevant IDs from this run:

create#0: crm_record_id=1261847000000648004
create#1: crm_record_id=1261847000000654001

RECOMMENDED NEXT STEPS
----------------------

1. Confirm get_form returned 200 and remained stable for the current dev environment.
2. Confirm fetch returned 200 and fetch.response.body.responses.0.responseId was populated as expected.
3. Confirm create#0 and create#1 correctly skip when crm search finds an existing external_id and that the recorded crm_record_id values are acceptable.