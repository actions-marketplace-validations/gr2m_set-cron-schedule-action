# iterate-cron-action

> Updates the current GitHub Action workflow's cron trigger based on a list of cron expressions

[![Build Status](https://github.com/gr2m/iterate-cron-action/workflows/Test/badge.svg)](https://github.com/gr2m/iterate-cron-action/actions)

[cron expressions](https://en.wikipedia.org/wiki/Cron#CRON_expression) are powerful, but if you want to run a task on Tuesday morning at 10am and Thursday afternoon at 3pm each week, you are out of luck. This action persmits you to set a list of cron expressions, by iterating through a provided list each time the workflow is run and updating the workflow file itself

## Usage

Notify users only when a release was published. The [repository dispatch event type](https://docs.github.com/en/free-pro-team@latest/rest/reference/repos#create-a-repository-dispatch-event) is set to `[current repositories full name] release` (e.g. `gr2m/release-notifire action`)

```yml
name: Do the thing
on:
  schedule:
    cron: "0 10 * * 2"

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - run: do-the-thing.sh
      - uses: gr2m/iterate-cron-action@v1
      - with:
          crons: |
            0 10 * * 2
            0 15 * * 4
          # optional: Defaults to "ci($WORKFLOW_NAME): update cron expression to $CRON_EXPRESSION".
          #           $WORKFLOW_NAME and $CRON_EXPRESSION will be replaced.
          message: "update cron for next reminder to do the thing"
```

## License

[ISC](LICENSE)