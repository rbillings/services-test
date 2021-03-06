services-test
===================================

Description
----------------------

This repo is intended for: testing tools, test manifests and scripts used by the Mozilla Cloud Services team as part of the Mozilla Cloud Services automated test pipeline.

See: [services-qa-jenkins](https://github.com/mozilla-services/services-qa-jenkins) for how these tests are used in Jenkins jobs. This is a private repo that requires permission to view.

Repo Structure
----------------------
To contribute a new automated test to the services-test repo, please adhere to the following guidelines.  This following file structure is required by Jenkins to execute automated tests.

* {__project__}/ (directory)
 * One directory per project.  For example:
   * services-test/absearch
   * services-test/autopush, etc.
* {__project__}/__README.md__ (file)
 * Add README file in project folder with links to: project repo (github), readthedocs, testplan, etc.
* {__project__}/{__test-type__}/ (directory)
 * One project child directory per test-type.  For example:
  * services-test/absearch/e2e-test
  * services-test/absearch/schema-check, etc.
* {__project__}/{__test-type__}/__run__ (file)
 * Add a "run" file in each test-type directory which should install all dependencies and kick off a test of the type indicated by the parent directory
 * example: [example run file](/demo/e2e-test/run)
* {__project__}/{__test-type__}/__manifest.ini__ (file)
 * Add a manifest file in each test-type directory which should specify any environment-specific parameters
  * example: [example manifest.ini](/demo/e2e-test/manifest.ini)
* {__project__}/{__test-type__}/__misc__ (files)
 * Any additional files needed by that test type should be self-contained in that directory.


Test Environments
----------------------
Environments where tests should be run for a given project

 TEST ENV       |    DESCRIPTION
 ---------------|---------------------------------------------------
 stage          | where most testing happens before prod deployment
 stage-loadtest | this is a special env for msisnd where we need a different setup for loadtesting.  In general loadtesting can take place in stage.
 pre-prod       | final verification in an actual prod env (before DNS switch)
 prod           | final verification to make sure prod deploy was successful. Also, continuous prod testing can be executed as a kind of prod "health check"


Test Types
----------------------
Specify what kinds of tests should be run for any given environment

 TEST TYPE     | DESCRIPTION
 ------------- | -------------------------------------------
 stack-check   | verify stack procs, urls, etc. are running
 config-check  | verify application configuration
 e2e-test      | client-side test
 loadtest      | verify application scalability
 schema-check  | API test
 security      | ZAP test (TBD)
 cdn-test      | check existence/delivery of remote files
