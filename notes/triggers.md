## Triggers

on: defines the events. it can be an array

Options:

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
- schedule: minimum frequency of 5 min. crontab notation: [https://crontab.guru/](https://crontab.guru/)
- repository_dispatch: triggered from external
  - POST to [https://github.com/karlambsilva/github-actions-course/dispatches](https://github.com/karlambsilva/github-actions-course/dispatches) with event name on the body
  - can also pass attributes in the payload — github.event.client_payload.
  - [example in postman](https://personal-studies-kmbs.postman.co/workspace/MB.io~67e57702-9144-474b-ba64-90b361ba0c21/request/2445161-ec927cff-1b75-4a2c-b84a-17f63ba25da0)
