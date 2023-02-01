**Github Actions**: let you automate your workflows (automated process to build, test, package, deploy… etc. Can be scheduled or based on events).

Individual tasks = actions. Combined = workflow (can be composed by multiple jobs).

Runner - any machine with GitHub Actions runner installed. Can be hosted by GitHub (cannot control hardware) or by yourself. Runs the job and give the feedback.

Jobs will run in parallel on their virtual machine.

Workflow file needs to…

- Be on .github/workflows folder
- Be a .yml file
- File content:

  - name: defines the name of the workflow
  - on: defines the events. array
    - push
      - branches
        - can filter by name or pattern (exemplo: 'feature/\*\*’)
        - [filter-pattern-cheat-sheet](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet)
        - has branches-ignore (but cannot be used with branches)
      - tags - work the same way as branches
        - also have tags-ignore
      - paths - work the same way as branches
        - also have the paths-ignore
    - pull_request: runs on open, reopen, syncronize. [events-that-trigger-workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
      - can add the branch filter by name (target) or pattern
    - can be scheduled (minimum frequency of 5 min). crontab notation: [https://crontab.guru/](https://crontab.guru/)
    - can be triggered from external - repository_dispatch:
      - POST to [https://github.com/karlambsilva/github-actions-course/dispatches](https://github.com/karlambsilva/github-actions-course/dispatches) with event name on the body
      - can also pass attributes in the payload — github.event.client_payload.
      - [example in postman](https://personal-studies-kmbs.postman.co/workspace/MB.io~67e57702-9144-474b-ba64-90b361ba0c21/request/2445161-ec927cff-1b75-4a2c-b84a-17f63ba25da0)
  - jobs: needs a name, object containing the runs-on and step (name, ubuntu by the default uses bash commands)
    - Bash, python - supported on all platforms. Powershell - Default Windows.
    - Can have dependency between each other - add tag **needs**
      [Workflow syntax for GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idstepsshell)

  On GitHub > actions, the first and the last steps are created by default.

  Sidemenu: workflow and jobs (for each job we have the artifacts )

  Secrets that can help when debuging:

  - ACTIONS_RUNNER_DEBUG > true
  - ACTIONS_STEP_DEBUG > true

  Actions: some code that does some specific tasks and can be used on the steps

  - can be from the same repository. Needs to point the path
  - can be from public repositories. for example: https://github.com/actions/hello-world-javascript-action
    - after the @, can be a branch, version or commit
    - to pass parameters, use _with_
  - The output of actions can be collected accessing the steps (using the id)
  - There are some variables that github already provides. for example, GITHUB_SHA, GITHUB_REPOSITORY, ETC
  - Actions Marketplace: created by people, organizations and so on.
    - Checkout commit can take some inputs: [https://github.com/actions/checkout#usage](https://github.com/actions/checkout#usage)

  [GitHub Marketplace: actions to improve your workflow](https://github.com/marketplace?type=actions)

  ENV : You can create custom variables for your workflow.

  - They can be created at the workflow level, job level, or at the step level (pay attention to the scope).
  - Variables available from github: [https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables)
  - Variables can be encrypted:
    - Settings > Secrets
    - secrets.GITHUB_TOKEN is available
      - with this token, you can create issue, commit and push from the virtual machine. more details: [https://docs.github.com/en/actions/security-guides/automatic-token-authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)

  CLI tool to encrypt and decrypt - gpg

  ${{ what is written inside }} - it’s an expression - needs to be evaluated.

Steps:

- If one fails, the next ones are skipped. Unless always () is added.

Functions:

- Documentation: https://docs.github.com/en/actions/learn-github-actions/expressions#functions
- Ready for use: contains, startwith, endsWith
- Job state functions: https://docs.github.com/en/actions/learn-github-actions/expressions#status-check-functions

if :

- can be used in jobs or steps
- does not need the curly brackets because github threats anything in if as an expression already
-
