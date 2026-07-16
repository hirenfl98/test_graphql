CONTRACT RUN SUMMARY
====================

Result: auth_login completed successfully with 1 step and all 4 assertions passing.

Root cause: All steps and assertions passed.

State reached: login_verified

Next step for you: Confirm the login endpoint continues returning 200 with a bearer access_token and the expected user email in dev.


WHAT HAPPENED
-------------

The workflow executed a single step named "login" using POST and it returned HTTP 200. That step passed in 1172 ms. All four assertions on the login response also passed, including the access token, token type, and user email checks.

WHY IT HAPPENED
---------------

This run succeeded because the only step completed with status 200 and no failures were recorded. The assertion = 200 passed for login status, and the response validations login.response.body.access_token != null, login.response.body.token_type == 'bearer', and login.response.body.user.email == 'test@example.com' all evaluated true. There were no failed assertions or step errors to explain.

WORKFLOW STATE
--------------

Status: login_verified

No tracked IDs were left in scope at the end of this run.

RECOMMENDED NEXT STEPS
----------------------

1. Confirm the POST login endpoint still returns HTTP 200 in dev.
2. Confirm the login response still includes a non-null access_token, token_type='bearer', and user.email='test@example.com'.

