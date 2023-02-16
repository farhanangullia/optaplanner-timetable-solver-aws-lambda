# Timetable Constraint Solver on AWS Lambda

> This project is a modified version of the source code for a timetable solver from OptaPlanner's quickstart: https://github.com/kiegroup/optaplanner-quickstarts 
> 
> You may find the blog post for this here: [Running a serverless Java constraint solver on AWS](https://medium.com/@farhanangullia/running-a-serverjava-constraint-solver-serverless-on-aws-c497a69a309c) 

A sample serverless project for deploying a Java constraint solver by OptaPlanner as a container on AWS Lambda.

## Compile

```
mvn compile dependency:copy-dependencies -DincludeScope=runtime
```

## Build image

```
docker build -t opta-time-table-solver-lambda . --platform=amd64
```

## Run locally

```
docker run -p 9000:8080 opta-time-table-solver-lambda
```

In a separate terminal:
```
curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'
```
## Deploy

### Set env vars

```
export AWS_ACCOUNT_ID=<YOUR AWS ACCOUNT ID>
export AWS_REGION=<YOUR AWS REGION>
```

### Setup ECR

```
aws ecr create-repository --repository-name opta-time-table-solver-lambda
```

### Push to ECR

```
aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
docker tag opta-time-table-solver-lambda:latest $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/opta-time-table-solver-lambda:latest
docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/opta-time-table-solver-lambda:latest
```

### Serverless deploy

```
sls deploy
```
