# Private API

## Internal — Grading

## Internal — Grading

### POST /internal/grading/calculate-response

Calculates the points earned for a submitted student response.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| submissionId | Integer | Student response that needs grading. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| submissionId | Integer | Graded submission identifier. |
| score | Integer | Points awarded for the response. |
| skillScores | Array[Object] | Points awarded to associated skills. |
| skillId | Integer | Skill identifier. |
| points | Integer | Points earned for that skill. |

**Example URL**

- api.example.local/internal/grading/calculate-response

### POST /internal/grading/calculate-report

Calculates the final scores and report for a student.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project being evaluated. |
| studentId | Integer | Student whose final report is calculated. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| reportId | Integer | Generated report identifier. |
| totalScore | Integer | Overall student score. |
| skillScores | Object | Calculated scores for each evaluated skill. |
| success | Boolean | Whether report calculation succeeded. |

**Example URL**

- api.example.local/internal/grading/calculate-report

## Internal — Branching and Message Release

### POST /internal/branching/resolve-next-scenario

Determines which scenario follows a selected response.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| scenarioId | Integer | Scenario the student just answered. |
| optionId | Integer | Response selected by the student. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| nextScenarioId | Integer or Null | Identifier of the next scenario, or null if no scenario follows. |
| isComplete | Boolean | Whether the scenario sequence has ended. |

**Example URL**

- api.example.local/internal/branching/resolve-next-scenario

### POST /internal/messages/release

Releases messages that have become available to a student.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project containing the messages. |
| studentId | Integer | Student whose available messages are being updated. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| releasedMessageIds | Array[Integer] | IDs of messages newly made available. |
| releasedCount | Integer | Number of messages released. |
| success | Boolean | Whether the release operation succeeded. |

**Example URL**

- api.example.local/internal/messages/release

## Internal — Project Initialization and Reports

### POST /internal/projects/{projectId}/initialize

Initializes a project and its student simulation records.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project being initialized. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Initialized project identifier. |
| initializedCount | Integer | Number of student simulation records initialized. |
| success | Boolean | Whether initialization succeeded. |

**Example URL**

- api.example.local/internal/projects/12/initialize

### POST /internal/reports/generate

Generates an internal grade report file.

**Input:**

| Name | Type | Description |
| --- | --- | --- |
| projectId | Integer | Project requiring a grade report. |
| format | Enum (pdf, xlsx) | Requested file format. |

**Output:**

| Name | Type | Description |
| --- | --- | --- |
| reportId | Integer | Generated report identifier. |
| fileLocation | String | Internal storage location of the generated report. |
| success | Boolean | Whether report generation succeeded. |

**Example URL**

- api.example.local/internal/reports/generate
