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
- 
### Defining outputs for jobs
https://docs.github.com/en/enterprise-server@3.4/actions/using-jobs/defining-outputs-for-jobs


Example: Defining outputs for a job

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    # Map a step output to a job output
    outputs:
      output1: ${{ steps.step1.outputs.test }}
      output2: ${{ steps.step2.outputs.test }}
    steps:
      - id: step1
        run: echo "::set-output name=test::hello"
      - id: step2
        run: echo "::set-output name=test::world"
  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - run: echo ${{needs.job1.outputs.output1}} ${{needs.job1.outputs.output2}}
```


Job outputs are strings

Write-Output "::set-output name=GREET::$output"