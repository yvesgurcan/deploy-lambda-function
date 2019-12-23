
Github Action to deploy/update a Lambda function from a ZIP file.

## Required parameters

  * `package`: A ZIP file with the code of your Lambda. This file can be created in a step or job prior to this action.
  * `function-name`
  * `AWS_REGION`
  * `AWS_SECRET_ID`
  * `AWS_SECRET_KEY`

## Example

```
name: Deploy Lambda

on:
  pull_request:
    types: [closed]
      branches:
        - master

jobs:
  deploy-lambda:
    if: github.event.pull_request.merged
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - run: echo "THIS IS A TEST PACKAGE" > file.txt
      - run: zip lambda.zip file.txt
      - uses: yvesgurcan/update-lambda-function
        with:
          package: lambda.zip
          function-name: TEST-FUNCTION
          AWS_REGION: ${{ secrets.AWS_REGION }}
          AWS_SECRET_ID: ${{ secrets.AWS_SECRET_ID }}
          AWS_SECRET_KEY: ${{ secrets.AWS_SECRET_KEY }}
```
