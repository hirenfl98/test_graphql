CONTRACT RUN SUMMARY
====================

Result: The Google Forms to Zoho Leads E2E workflow completed successfully with all 3 steps and the single assertion passing.

Root cause: All steps and assertions passed.

State reached: test_sync_verified

Next step for you: No fix required; confirm the sync verification remains stable in dev and rerun after any integration changes.


WHAT HAPPENED
-------------

The run in dev for test_name google_forms_zoho_leads executed 3 internal steps: validate (200, passed), create_config (200, passed), and test_sync (200, passed). The only assertion, test_sync.response.body.success == true, also passed. No failures, retries, or error events were reported.

WHY IT HAPPENED
---------------

Each step returned status_code 200 and passed=true, so the workflow advanced cleanly through validation, configuration creation, and sync testing. The assertion on test_sync.response.body.success == true passed, confirming the sync outcome was successful. Since summary.failed_steps and summary.failed_assertions are both 0, there is no failure signal to diagnose.

WORKFLOW STATE
--------------

Status: test_sync_verified

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Validate that validate returned 200 and passed before configuration work began.
2. Confirm create_config completed with 200 and passed, ensuring the integration config was accepted.
3. Confirm test_sync returned 200 and the assertion test_sync.response.body.success == true passed.