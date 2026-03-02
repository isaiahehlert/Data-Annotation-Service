# Data Annotation Management Service

A production-style REST API for managing data annotation workflows.

Built with FastAPI, SQLAlchemy, and SQLite.  
Fully containerized with Docker.  
Tested with PyTest and integrated with GitHub Actions CI.

Repository:  
https://github.com/isaiahehlert/data-annotation-service

---

## Overview

This service allows teams to:

- Create annotation projects
- Load and manage annotation tasks
- Submit annotations
- Track task completion
- Aggregate statistics by annotator

The system models a realistic annotation lifecycle and demonstrates:

- Relational database modeling
- REST API design
- Input validation and error handling
- Aggregation queries
- Containerized deployment
- CI-based test execution

---

## Tech Stack

- Python 3.11
- FastAPI
- SQLAlchemy ORM
- SQLite
- Docker
- PyTest
- GitHub Actions

---

## Architecture

Project → Task → Annotation

- A Project contains multiple Tasks.
- A Task can receive multiple Annotations.
- When an Annotation is submitted, the Task status transitions to "done".
- Project statistics are computed using SQL aggregation queries.

---

## API Endpoints

### Projects

POST /projects  
Create a new project (unique name required)

GET /projects  
List all projects

GET /projects/{project_id}  
Retrieve project details and task counts

---

### Tasks

POST /projects/{project_id}/tasks  
Create multiple tasks under a project

GET /projects/{project_id}/tasks  
List tasks (optional status filter)

---

### Annotations

POST /tasks/{task_id}/annotations  
Submit annotation and mark task as complete

GET /tasks/{task_id}/annotations  
List all annotations for a task

---

### Statistics

GET /projects/{project_id}/stats  

Returns:

- total_tasks
- annotated_tasks
- by_annotator (aggregation)

---

## Running Locally

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
