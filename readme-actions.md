### Setting an environment variable
https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-an-environment-variable

echo "{environment_variable_name}={value}" >> $GITHUB_ENV

env:
    DAY_OF_WEEK: Monday

run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"

if: ${{ env.DAY_OF_WEEK == 'Monday' }}

### Contexts
github
env
secrets


- name: Dump GitHub context
  id: github_context_step
  run: echo '${{ toJSON(github) }}'

steps:
- uses: actions/labeler@v4
  with:
      repo-token: ${{ secrets.GITHUB_TOKEN }}