# Gitub Workflow

## Purpose

The recommended Github work flow here is for developers to submit code and documentation contributions to MOSIP open source repositories.

## Setup

1. Fork MOSIP repository of interest from [https://github.com/mosip/](https://github.com/mosip/)
2. Clone the fork to your local machine. Eg:

   ```text
    $ git clone https://github.com/<your_github_id>/commons.git
   ```

3. Set upstream project as the original from where you forked. Eg:

   ```text
    $ cd commons
    $ git remote add upstream https://github.com/mosip/commons.git
   ```

4. Make sure you never directly push to upstream.

   ```text
    $ git remote set-url --push upstream no_push
   ```

5. Confirm the origin and upstream.

   ```text
    $ git remote -v
   ```

## Code changes

1. Create a new issue in [MOSIP Jira](https://mosip.atlassian.net/).
2. You may work on `master`, switch to a branch \(like Release branch\) or create a new branch.
3. Make sure you are up-to-date with upstream repo.

   ```text
    $ git pull upstream <branch>
   ```

4. Once you are done with the work, commit your changes referring to Jira number in the commit message. Eg:

   ```text
    $ git commit -m "[MOS-2346] Adding new upload feature in Pre registration module for POA documents"
   ```

5. Once again ensure that you are up-to-date with upstream repo as it may have moved forward.

   ```text
    $ git pull upstream <branch>
   ```

6. Build and test your code. Make sure it follows the coding guidelines.
7. Push to your forked repo \(origin\).

   ```text
    $ git push
   ```

8. Create a pull-request on your forked repo. Direct the pull-request to `master` or any specific branch on upstream \(like a Release branch\).
9. Make sure the automatic tests on Github for your pull-request pass.
10. The pull-request shall be reviewed by reviewers.

