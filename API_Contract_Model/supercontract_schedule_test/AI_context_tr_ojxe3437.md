CONTRACT RUN SUMMARY
====================

Result: The run succeeded: Google Forms data was fetched and both Zoho lead create paths were skipped because matching CRM records already existed.

Root cause: All steps and assertions passed.

State reached: fetch_verified

Next step for you: Confirm the idempotency behavior is expected for existing Zoho records, and rerun with a new external_id if you want to validate actual create behavior.


WHAT HAPPENED
-------------

The workflow executed 6 steps in dev for `google_forms_to_zoho_leads`. `get_form` completed with HTTP 200 and passed, followed by `fetch` which also returned HTTP 200 and passed its verification that `fetch.response.body.responses.0.responseId` is not null. The create flow then ran twice: `create#0:search` and `create#1:search` both returned HTTP 200, and each corresponding `create#0` and `create#1` step was marked as SKIP because CRM records already existed. Events confirm both skips were due to `crm search found existing record` for the two external_id values.

WHY IT HAPPENED
---------------

All assertions passed: `s1` and `s2` confirmed HTTP 200 for `get_form` and `fetch`, and `v3` confirmed `fetch.response.body.responses.0.responseId != null`. The create branches did not fail; they intentionally short-circuited after successful search calls with HTTP 200, and the SKIP steps used status code 0 with explicit `error_message` values indicating existing CRM records. Since the run is marked `success: true`, this is an idempotent success case rather than a create failure.

WORKFLOW STATE
--------------

Status: fetch_verified

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Confirm `get_form` and `fetch` continue returning HTTP 200 and the `fetch.response.body.responses.0.responseId` assertion remains valid.
2. Confirm both `create#0:search` and `create#1:search` correctly detect existing CRM records and emit SKIP with the expected `external_id`/`crm_record_id` behavior.
3. If you need to test the actual Zoho create path, rerun with a new `external_id` so the search steps do not resolve to existing records.