CONTRACT RUN SUMMARY
====================

Result: The workflow got through Google Forms retrieval and search, but both deal creation attempts failed with HTTP 400 instead of the expected 201.

Root cause: Test "google_forms_to_hubspot_deals" failed at step "create" because the create requests returned 400 and did not satisfy the expected status 201 assertions.

State reached: create_started

Next step for you: Inspect the HubSpot deal creation request payload and validation rules for create#0 and create#1, then fix the fields causing the 400 responses.


WHAT HAPPENED
-------------

Step get_form (GET) passed with status 200, and step fetch (GET) also passed with status 200. The two search prechecks, create#0:search (POST) and create#1:search (POST), both passed with status 200. The actual creation steps create#0 (POST) and create#1 (POST) both failed with status 400.

WHY IT HAPPENED
---------------

The assertions for get_form status and fetch status passed, each matching the expected 200. The assertions for create#0 status and create#1 status failed because they expected 201 but the API returned 400, which is consistent with the step-level error_message "expected status 201, got 400". The first failure occurred at step create#0, and the run summary confirms the failure_reason as test "google_forms_to_hubspot_deals" failed at step "create". Since both create attempts failed the same way, the issue is likely a request validation problem rather than a transient one-off.

WORKFLOW STATE
--------------

Status: create_started

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Verify the HubSpot create payload used by create#0 and create#1 against the API's required fields and formatting rules, since both POSTs returned 400.
2. Confirm the upstream search/mapping data feeding create#0:search and create#1:search produces valid create requests before retrying the workflow.