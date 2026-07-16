CONTRACT RUN SUMMARY
====================

Result: The google_forms_to_zoho_leads workflow completed successfully with all 6 steps and all 5 assertions passing.

Root cause: All steps and assertions passed.

State reached: lead_created

Next step for you: Keep the current integration path intact and verify the duplicate-check/search behavior remains returning 204 before each create call.


WHAT HAPPENED
-------------

The run executed 6 steps in dev for test_name google_forms_to_zoho_leads. Step get_form used GET and passed with status 200, followed by fetch using GET and passing with status 200. The create#0:search step used GET and passed with status 204, then create#0 used POST and passed with status 201; the same pattern repeated for create#1:search (GET, 204) and create#1 (POST, 201).

WHY IT HAPPENED
---------------

This was a success because every HTTP status matched the assertions: get_form status = 200, fetch status = 200, create#0 status = 201, create#1 status = 201, and fetch verify confirmed fetch.response.body.responses.0.responseId != null. There were no failed assertions or failed steps, so no contract mismatch or API error surfaced. The 204 statuses on create#0:search and create#1:search indicate the search/pre-check did not find an existing record before creation, which is consistent with the successful 201 POST results.

WORKFLOW STATE
--------------

Status: lead_created

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Confirm get_form (GET 200) and fetch (GET 200) continue to satisfy their status assertions in dev.
2. Confirm each create pre-check search step returns 204 before POST creation, and each create call returns 201 as expected.
3. Confirm fetch.response.body.responses.0.responseId remains non-null so the downstream Zoho lead linkage stays valid.