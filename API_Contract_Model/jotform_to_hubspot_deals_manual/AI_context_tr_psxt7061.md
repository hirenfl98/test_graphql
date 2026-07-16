CONTRACT RUN SUMMARY
====================

Result: The Jotform to HubSpot deals workflow completed successfully with all 4 steps and 4 assertions passing.

Root cause: All steps and assertions passed.

State reached: deal_created

Next step for you: Keep the current integration behavior and add/maintain regression checks around the create#0 response and downstream ID mapping.


WHAT HAPPENED
-------------

The run started in dev on the manually triggered test_name jotform_to_hubspot_deals. Step get_form used GET and passed with HTTP 200. Step fetch used GET and passed with HTTP 200. Step create#0:search used POST and passed with HTTP 200, then step create#0 used POST and passed with HTTP 201, completing the deal creation flow.

WHY IT HAPPENED
---------------

This was a success case because every HTTP step returned the expected status code: get_form = 200, fetch = 200, create#0:search = 200, and create#0 = 201. All assertions passed, including s1 for get_form status, s2 for fetch status, s1 for create#0 status, and v4 verifying fetch.response.body.content.0.id != null. No failed assertion expressions or error_message values were present, so there is no evidence of contract or mapping breakage.

WORKFLOW STATE
--------------

Status: deal_created

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Confirm the get_form GET contract continues to return HTTP 200 in dev.
2. Confirm the fetch GET contract continues to return HTTP 200 and exposes a non-null fetch.response.body.content.0.id.
3. Confirm create#0:search POST remains HTTP 200 and create#0 POST remains HTTP 201 for deal creation.