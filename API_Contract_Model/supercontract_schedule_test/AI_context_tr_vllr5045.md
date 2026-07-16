CONTRACT RUN SUMMARY
====================

Result: google_forms_to_zoho_leads completed successfully; all 6 steps and 3 assertions passed.

Root cause: All steps and assertions passed.

State reached: records_checked_and_skipped

Next step for you: Confirm the duplicate-detection/upsert-skip behavior remains intentional for existing Zoho CRM leads.


WHAT HAPPENED
-------------

The workflow ran in dev on the scheduler trigger for google_forms_to_zoho_leads and completed in 2503 ms. Step get_form (GET) returned 200 and passed, followed by fetch (GET) returning 200 and passing. Two record-processing branches then executed: create#0:search (GET) returned 200 and create#0 was SKIP with status_code 0 because an existing CRM record was found; create#1:search (GET) returned 200 and create#1 was also SKIP for the same reason.

WHY IT HAPPENED
---------------

The run succeeded because every HTTP step returned the expected 200 status where applicable, and both skip steps were treated as passing control-flow outcomes with status_code 0. All assertions passed, including get_form status = 200, fetch status = 200, and fetch.response.body.responses.0.responseId != null, indicating the fetch step produced a response entry with a responseId. The events confirm the create#0 and create#1 branches hit upsert_skip due to existing CRM records, with the specific external_id and crm_record_id values recorded in the step error_message fields.

WORKFLOW STATE
--------------

Status: records_checked_and_skipped

Relevant IDs from this run:

create#0: map[crm_record_id:1261847000000647001 external_id:ACYDBNilGSNzMDovHNF5uHime8yiujbRb7t1DkomNcq1ZKrQWFm9eeMTI5exHznArkJ7k8M]
create#1: map[crm_record_id:1261847000000648001 external_id:ACYDBNhmKBIWgozTgClPKiXgIMakphksWT3IQSK4o4VUvLKxHiFiGsaVazEqH0MS9aL3ehQ]

RECOMMENDED NEXT STEPS
----------------------

1. Validate that get_form (GET 200) and fetch (GET 200) continue to return successful responses with the expected responseId assertion passing.
2. Confirm the create#0 and create#1 branches continue to skip duplicates intentionally when CRM search finds existing records, as indicated by the upsert_skip events and SKIP step outcomes.

