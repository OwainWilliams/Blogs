# Create a readme file automatically

This job runs on the 0th, 6th, 12th, 18th hour of the day e.g. midnight, 6am, midday 6pm.  
To run it on the hour, every hour, just change the value to `/1`

```text
name: Update README

on:
  push:
  schedule:
    - cron: "0 */6 * * *"

jobs:
  markscribe:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master

      - uses: muesli/readme-scribe@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITBOOK_TOKEN }}
        with:
          template: "templates/README.md.tpl"
          writeTo: "README.md"

      - uses: actions/upload-artifact@v1
        with:
          name: README.md
          path: README.md

      - uses: stefanzweifel/git-auto-commit-action@v4
        env:
          GITHUB_TOKEN: ${{ secrets.GITBOOK_TOKEN }}
        with:
          commit_message: Update generated README
          branch: master
          commit_user_name: readme-scribe 🤖
          commit_user_email: actions@github.com
          commit_author: readme-scribe 🤖 <actions@github.com>
```

Created a GITBOOK\_TOKEN which lives in my 'secrets' section of github and was generated from the developer settings under my profile. It must be prefixed with `secrets.` in the action. It doesn't work if you just try and use `GITBOOK_TOKEN` or whatever you decide to call your secret. 



