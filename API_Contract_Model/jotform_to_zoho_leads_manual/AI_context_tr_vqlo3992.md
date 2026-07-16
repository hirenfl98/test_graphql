CONTRACT RUN SUMMARY
====================

Result: The Jotform-to-Zoho Leads E2E run passed successfully with all 6 steps and 4 assertions green.

Root cause: All steps and assertions passed.

State reached: lead_created

Next step for you: Keep the current flow, and confirm the create/search idempotency behavior remains stable in dev.


WHAT HAPPENED
-------------

The workflow started with get_form as a GET request and passed with HTTP 200. The fetch step also passed with HTTP 200, then create#0:search passed with HTTP 200 and create#0 was skipped because an existing CRM record was found for external_id 6580950412128342598 and crm_record_id 1261847000000630009. The next idempotency check create#1:search passed with HTTP 204, and create#1 completed successfully as a POST with HTTP 201.

WHY IT HAPPENED
---------------

This run succeeded because every HTTP step returned the expected status codes: 200 for get_form, fetch, and create#0:search; 204 for create#1:search; and 201 for create#1. The assertions all passed, including get_form status (= 200), fetch status (= 200), create#1 status (= 201), and fetch.response.body.content.0.id != null. The skipped create#0 step was still treated as passed because the CRM search detected an existing record and intentionally avoided a duplicate create. No failing assertion expressions or error messages were present.

WORKFLOW STATE
--------------

Status: lead_created

Relevant IDs from this run:

external_id: 6580950412128342598
crm_record_id: 1261847000000630009

RECOMMENDED NEXT STEPS
----------------------

1. Confirm get_form and fetch continue returning HTTP 200 with passing status assertions.
2. Confirm create#0 remains idempotent by skipping when a CRM record already exists for the external_id.
3. Confirm create#1 search returns HTTP 204 and create#1 returns HTTP 201 for a successful lead creation path.