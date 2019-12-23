
Github Action to update a Lambda function.

# How to use

Takes 
This file can be created in a step or job prior to this action.

Required parameters:
  * `package`: A ZIP file with the code of your Lambda.

  * `function-name`
  * `AWS_REGION`
  * `AWS_SECRET_ID`
  * `AWS_SECRET_KEY`

```
name: Update Lambda
on:
  push
jobs:
  lambda:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - run: echo "THIS IS A TEST PACKAGE" > file.txt
      - run: zip lambda.zip file.txt
      - uses: stcalica/update-lambda
        with:
          package: lambda.zip
          function-name: TEST-FUNCTION
          AWS_REGION: ${{ secrets.AWS_REGION }}
          AWS_SECRET_ID: ${{ secrets.AWS_SECRET_ID }}
          AWS_SECRET_KEY: ${{ secrets.AWS_SECRET_KEY }}
```
