## General

- **Github Actions**: let you automate your workflows (automated process to build, test, package, deploy… etc. Can be scheduled or based on events).

- Individual tasks = actions. Combined = workflow (can be composed by multiple jobs).

- Runner: any machine with GitHub Actions runner installed. Can be hosted by GitHub (cannot control hardware) or by yourself. Runs the job and give the feedback.

Workflow file needs to…

- Be on .github/workflows folder
- Be a .yml file
- File content:
  - name: defines the name of the workflow

## Job

Jobs will run in parallel on their virtual machine.

They need a name, object containing the runs-on and step (ubuntu by the default uses bash commands).

- Bash, python: supported on all platforms.
- Powershell: Default Windows.

Can have dependency between each other - add tag **needs**

- [Workflow syntax for GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idstepsshell)

Strategy key should be under the job.

- on the matriz, the jobs runs in parallel. Using the max-parallel, you can limit, the number of parallel jobs at once.
- has exclude / include (creates a new variable that only exists on that execution)
- refer a matrix value: ${{ matrix.NAME }}
- fail-fast: true // means that if one job in the matrix fails, the other ones will stop

## Steps

- If one fails, the next ones are skipped. Unless always () is added.
- You can also use continue-on-error:true to all next steps run even if that one failed

## Actions

Actions: some code that does some specific tasks and can be used on the steps

- can be from the same repository. Needs to point the path
- can be from public repositories. for example: https://github.com/actions/hello-world-javascript-action
  - after the @, can be a branch, version or commit
  - to pass parameters, use _with_
- The output of actions can be collected accessing the steps (using the id)
- There are some variables that github already provides. for example, GITHUB_SHA, GITHUB_REPOSITORY, ETC
- Actions Marketplace: created by people, organizations and so on.
  - Checkout commit can take some inputs: [https://github.com/actions/checkout#usage](https://github.com/actions/checkout#usage)
- [GitHub Marketplace: actions to improve your workflow](https://github.com/marketplace?type=actions)

## Variables

You can create custom variables for your workflow.

- They can be created at the workflow level, job level, or at the step level (pay attention to the scope).
- Variables available from github: [https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables)
- Variables can be encrypted:
  - Settings > Secrets
  - secrets.GITHUB_TOKEN is available
    - with this token, you can create issue, commit and push from the virtual machine. more details: [https://docs.github.com/en/actions/security-guides/automatic-token-authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)

## Functions

- Documentation: https://docs.github.com/en/actions/learn-github-actions/expressions#functions
- Ready for use: contains, startwith, endsWith
- Job state functions: https://docs.github.com/en/actions/learn-github-actions/expressions#status-check-functions

## IF

- can be used in jobs or steps
- does not need the curly brackets because github threats anything in if as an expression already
-

## GitHub UI

- On GitHub > actions, the first and the last steps are created by default.

- Sidemenu: workflow and jobs (for each job we have the artifacts )

- Secrets that can help when debuging:
  - ACTIONS_RUNNER_DEBUG > true
  - ACTIONS_STEP_DEBUG > true

## Extras

${{ what is written inside }} - it’s an expression - needs to be evaluated.

timeout-minutes can be added to job or step

CLI tool to encrypt and decrypt - gpg
