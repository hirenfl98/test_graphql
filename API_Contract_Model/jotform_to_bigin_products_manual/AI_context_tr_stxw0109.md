CONTRACT RUN SUMMARY
====================

Result: The Jotform-to-Bigin products E2E run succeeded with all steps and assertions passing.

Root cause: All steps and assertions passed.

State reached: create_skipped_existing_records

Next step for you: Confirm the upstream CRM deduplication behavior is expected for existing external_id values and keep this workflow monitored for accidental duplicate creation.


WHAT HAPPENED
-------------

The run executed the full jotform_to_bigin_products workflow in dev and completed successfully. Step get_form (GET) returned 200 and passed, followed by fetch (GET) returning 200 and passing its body assertion that fetch.response.body.content.0.id is not null. The create#0 and create#1 branches each performed a search (GET 200) and then skipped record creation because matching CRM records already existed; both skip steps were marked passed.

WHY IT HAPPENED
---------------

The run passed because every HTTP step returned the expected status codes and all assertions succeeded: get_form status = 200, fetch status = 200, and fetch.response.body.content.0.id != null. The create branches did not fail because the workflow detected existing CRM records during create#0:search and create#1:search, triggering SKIP outcomes rather than attempted writes. The skip error_message fields confirm deduplication, with existing crm_record_id values found for external_id 6580956722126513996 and 6579415042126485148. There was no failed assertion expression or error_message indicating an API contract violation.

WORKFLOW STATE
--------------

Status: create_skipped_existing_records

Relevant IDs from this run:

create#1: map[crm_record_id:1297440000000491043 external_id:6579415042126485148]
create#0: map[crm_record_id:1297440000000491041 external_id:6580956722126513996]

RECOMMENDED NEXT STEPS
----------------------

1. Validate that the create#0 and create#1 search-then-skip behavior is the intended idempotent path for existing external_id records.
2. Confirm the upstream mapping and deduplication rules continue to resolve to the same crm_record_id values before enabling broader rollout.