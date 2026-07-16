CONTRACT RUN SUMMARY
====================

Result: auth_login completed successfully with 1/1 steps and 4/4 assertions passing.

Root cause: All steps and assertions passed.

State reached: login_verified

Next step for you: Confirm the login endpoint continues returning a 200 response with a bearer access token for test@example.com.


WHAT HAPPENED
-------------

The run executed a single step, login, using POST and it passed with HTTP 200 in 1117 ms. All four assertions against the login response succeeded, including access token presence, token_type, and the expected user email. No failure events were present.

WHY IT HAPPENED
---------------

The login step returned the expected 200 status, so the status assertion '= 200' passed. The response contract checks also passed: login.response.body.access_token was not null, login.response.body.token_type matched 'bearer', and login.response.body.user.email matched 'test@example.com'. Since there were no failed assertions or step failures, the workflow completed successfully.

WORKFLOW STATE
--------------

Status: login_verified

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Verify the login endpoint still returns HTTP 200 for valid credentials.
2. Confirm login.response.body.access_token is present and non-null.
3. Confirm login.response.body.token_type remains 'bearer' and login.response.body.user.email matches the expected account.