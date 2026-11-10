# Customer Accounts: user stories (copy each into a new issue using the User Story template)

Backlog order (highest priority first), labels, story points and sprint:

1. Setup the development environment - label: technical debt - 5 (M) - Sprint 1 - Product backlog
2. Read an account from the service - label: enhancement - 3 (S) - Sprint 1 - Product backlog
3. Update an account in the service - label: enhancement - 5 (M) - Sprint 1 - Product backlog
4. Delete an account from the service - label: enhancement - 3 (S) - Sprint 1 - Product backlog
5. List all accounts in the service - label: enhancement - 5 (M) - Sprint 1 - Product backlog
6. Containerize your microservice using Docker - label: technical debt - 8 (L) - Icebox
7. Deploy your Docker image to Kubernetes - label: technical debt - 13 (XL) - Icebox

Scale: 3, 5, 8, 13 = S, M, L, XL.

---

## 1. Title: Setup the development environment

**As a** developer  
**I need** a working development environment for the accounts service  
**So that** I can write and test code using TDD

### Details and Assumptions
* The starter code from the template repository is available
* The environment is ephemeral, so all work must be pushed to GitHub
* Python, Flask, nosetests and coverage tools are required

### Acceptance Criteria
```gherkin
Given the repository has been cloned into the environment
When I install the dependencies and run nosetests
Then the existing tests pass and the coverage report is displayed
```

---

## 2. Title: Read an account from the service

**As a** customer account manager  
**I need** an endpoint to read a single account  
**So that** other services can retrieve customer details

### Details and Assumptions
* Endpoint: GET /accounts/{id}
* The account model already exists
* A missing account must return 404

### Acceptance Criteria
```gherkin
Given an account exists in the database
When I call GET /accounts/{id} with its id
Then I receive the account data and HTTP 200

Given no account exists with the requested id
When I call GET /accounts/{id}
Then I receive HTTP 404
```

---

## 3. Title: Update an account in the service

**As a** customer account manager  
**I need** an endpoint to update an account  
**So that** customer names and addresses stay current

### Details and Assumptions
* Endpoint: PUT /accounts/{id}
* The request body contains the new account data
* A missing account must return 404

### Acceptance Criteria
```gherkin
Given an account exists in the database
When I call PUT /accounts/{id} with changed data
Then the account is updated and I receive HTTP 200 with the new data

Given no account exists with the requested id
When I call PUT /accounts/{id}
Then I receive HTTP 404
```

---

## 4. Title: Delete an account from the service

**As a** customer account manager  
**I need** an endpoint to delete an account  
**So that** customers who leave can be removed

### Details and Assumptions
* Endpoint: DELETE /accounts/{id}
* Deleting an account that does not exist is not an error

### Acceptance Criteria
```gherkin
Given an account exists in the database
When I call DELETE /accounts/{id}
Then the account is removed and I receive HTTP 204

Given the account has been deleted
When I call GET /accounts/{id}
Then I receive HTTP 404
```

---

## 5. Title: List all accounts in the service

**As a** customer account manager  
**I need** an endpoint to list all accounts  
**So that** I can see every customer in the system

### Details and Assumptions
* Endpoint: GET /accounts
* An empty database returns an empty list, not an error

### Acceptance Criteria
```gherkin
Given several accounts exist in the database
When I call GET /accounts
Then I receive a list containing all accounts and HTTP 200

Given no accounts exist in the database
When I call GET /accounts
Then I receive an empty list and HTTP 200
```

---

## 6. Title: Containerize your microservice using Docker

**As a** developer  
**I need** a Docker image of the accounts service  
**So that** it can run the same way in any environment

### Details and Assumptions
* A Dockerfile is added to the repository root
* The image is pushed to the container registry
* Planned for a later sprint

### Acceptance Criteria
```gherkin
Given a Dockerfile exists in the repository
When I build the image and run a container from it
Then the service starts and responds to requests
```

---

## 7. Title: Deploy your Docker image to Kubernetes

**As a** DevOps engineer  
**I need** the service deployed to a Kubernetes cluster  
**So that** it runs reliably and can be scaled

### Details and Assumptions
* Deployment and Service YAML manifests are required
* The database runs as a separate service in the cluster
* Planned for a later sprint

### Acceptance Criteria
```gherkin
Given the Docker image is available in the registry
When I apply the Kubernetes manifests
Then the pods are running and the service responds through the cluster
```
