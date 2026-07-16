CONTRACT RUN SUMMARY
====================

Result: The google_forms_to_bigin_contacts workflow succeeded end-to-end with all 8 steps and 3 assertions passing.

Root cause: All steps and assertions passed.

State reached: contacts_upserted_or_verified

Next step for you: Confirm the skip-on-existing-record behavior is intentional for repeated runs and monitor the mapped external_id to crm_record_id links.


WHAT HAPPENED
-------------

The run started in dev and executed the get_form GET step, which returned 200 and passed. It then executed fetch GET, also returning 200, and the fetch.response.body.responses.0.responseId != null assertion passed. The workflow continued through create#0, create#1, and create#2 search GET steps, each returning 200, and each corresponding create step was SKIP with status_code 0 because an existing CRM record was found. Events tied to create#0, create#1, and create#2 confirm the upsert_skip behavior with the matched external_id and crm_record_id values.

WHY IT HAPPENED
---------------

Success was expected because every HTTP step returned the expected 200 status where applicable, and the assertions s1, s2, and v3 all passed. The create path did not fail; instead, each create step was intentionally skipped after the search step found an existing CRM record, which is reflected in the SKIP method, status_code 0, and the error_message on each create step. No assertion failed, and no failure_reason or first_failure_step applies because the run completed successfully.

WORKFLOW STATE
--------------

Status: contacts_upserted_or_verified

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Validate that get_form returned 200 and the form fetch returned 200 with fetch.response.body.responses.0.responseId present.
2. Confirm the create#0, create#1, and create#2 search steps returned 200 and the corresponding create steps correctly skipped due to existing CRM records.
3. Verify the upsert_skip events match the intended deduplication behavior for the reported external_id values.