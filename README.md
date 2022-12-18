# Timetable Constraint Solver on AWS Lambda

> This project is a modified version of the source code for a timetable solver from OptaPlanner's quickstart: https://github.com/kiegroup/optaplanner-quickstarts

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