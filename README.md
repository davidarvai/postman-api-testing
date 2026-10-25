# Postman-api-testing
# Postman API Testing – JSONPlaceholder

Automated API tests built with Postman for the public [JSONPlaceholder](https://jsonplaceholder.typicode.com) REST API. The collection covers CRUD operations, filtering, a negative scenario and a persistence check, with assertions written as Postman test scripts.

## What is tested

| Request | Method | Checks |
|---------|--------|--------|
| R1 – Get all posts | GET | status 200, JSON content type, response time, 100 items |
| R2 – Get single post | GET | status 200, correct id, required fields |
| R3 – Filter posts by user | GET | status 200, all posts belong to the user, expected count |
| R4 – Create post | POST | status 201, response matches request, id returned |
| R5 – Update post | PUT | status 200, updated title returned |
| R6 – Delete post | DELETE | status 200 |
| R7 – Non-existent post | GET | status 404 |
| R8 – Created post persistence | GET | documents that writes are not persisted |

## Results

The full collection run passes. Details, observations and next steps are in [TEST_REPORT.md](TEST_REPORT.md).

![Collection run results](screenshots/collection-run.png)

## How to run

1. Install [Postman](https://www.postman.com/downloads/).
2. Download `JSONPlaceholder_API_Tests.postman_collection.json` from this repository.
3. In Postman: **Import** → select the file.
4. Open the collection → **Variables** and check that `baseUrl` is set to `https://jsonplaceholder.typicode.com`.
5. Right-click the collection → **Run collection** → **Start run**.

## Tools

Postman, JavaScript (Postman test scripts / Chai assertions), Markdown.

## Key finding

JSONPlaceholder fakes write operations: `POST /posts` returns `201` with a new id, but fetching that id afterwards returns `404`. On a real API I would verify every create, update and delete with a follow-up GET request. See the report for details.

## Next steps

- JSON schema validation
- Run the collection with Newman from the command line
- Run the tests automatically with GitHub Actions
