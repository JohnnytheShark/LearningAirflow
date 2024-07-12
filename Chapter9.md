# TESTING

Testing may be a bit difficult because Airflow itself is an orchestration system that it itself (often) does not perform any logic. 

## Unit Testing

Small individual units of work (single functions) can be tested with unit tests. 

## Integration Tests
Validate behavior of multiple components together.

## Acceptance Testing 
Evaluating fit with business requirements.

## pytest 
pytest is one of the most popular third-party testing frameworks for various features such as fixtures

## Integrity Testing All DAGS
1. DAG Integrity Test - Check to make sure your DAG does not contain cycles; if the task IDs in the DAG are unique, etc

### Installation of Pytest
pip install pytest

## Testing Conventions: 
Create a tests/ folder at the root of the project that holds all the tests and mirrors the same directory structure as in the rest of the project.

test_ prefix is required.

Tests are read from top to bottom
Top shows you which tests failed. Bottom shows you why the test failed

## CI/CD Pipeline 
CI/CD pipeline is a system that runs predefined scripts when you make a change to your code repository. The continuous integration (CI) denotes checking and validating the changed code to ensure it complies with coding standards and a test suite. For example, upon pushing code, you could check for Flake8, Pylint, and Black and run a series of tests. The CD indicates automatically deploying the code into production systems, completely automated and without human interference. 

The goal is to maximize coding productivity without having to deal with manually validating and deploying it.

Most CI/CD systems start off with a YAML configuration file in which a pipeline is defined: a series of steps to execute upon changing code. Each step should complete successfully to make the pipeline successful. 

We can enforce rules such as "only merge to master with a successful pipeline" 


