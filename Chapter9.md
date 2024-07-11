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