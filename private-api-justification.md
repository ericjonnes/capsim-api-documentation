# Private API Justification

These endpoints are private because they are only intended to be called by trusted backend services, not directly by the student or faculty clients.

## POST /internal/grading/calculate-response

- Prevents students from triggering or manipulating internal grading operations.

## POST /internal/grading/calculate-report

- Final grade calculations should only be performed through trusted backend processing.

## POST /internal/branching/resolve-next-scenario

- Prevents students from directly controlling or bypassing scenario progression.

## POST /internal/messages/release

- Message-release rules should be enforced by the backend to prevent students from accessing future scenarios early.

## POST /internal/projects/{projectId}/initialize

- Initializes internal simulation data and student progression records, which should not be directly controlled by ordinary users.

## POST /internal/reports/generate

- Report generation should be handled internally to control access to student grades and protected information.
