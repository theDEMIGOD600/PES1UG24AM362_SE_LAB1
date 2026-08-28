# Lab 1 — Requirements and Use-Cases
**Problem Statement #02 — Automated Rubric Assignment Evaluator**
**Actors:** Student, Faculty Evaluator, Peer Reviewer

## 1. Requirements Table

| Req ID | Type | Description | Priority | Acceptance Criteria | Rationale |
| :--- | :--- | :--- | :--- | :--- | :--- |
| FR-001 | Functional | The system shall automatically queue uploaded student project zip files, execute pre-configured unit test suites, and generate an itemized rubric score breakdown. | High | Pass: Rubric breakdown is rendered with test results within 10 seconds of submission. Fail: File queue stalls or invalid rubric tally. | Automates the core grading pipeline so evaluators are not manually running tests per submission. (Given) |
| FR-002 | Functional | The system shall automatically assign each graded submission to exactly two peer reviewers, excluding the submission's own author. | Medium | Pass: Every submission has exactly 2 reviewers assigned within 5 seconds of scoring completion, with no self-assignment. Fail: A submission has fewer than 2 reviewers or is assigned to its own author. | Distributes peer-review workload evenly and prevents biased self-review. |
| FR-003 | Functional | The system shall allow a faculty evaluator to manually override or adjust an automatically generated rubric score, with the change logged. | High | Pass: Override is saved and an audit entry records original score, new score, evaluator ID, and timestamp. Fail: Override is not persisted or no audit entry is created. | Automated scoring can misjudge edge cases; faculty need final authority and a traceable record. |
| FR-004 | Functional | The system shall notify a student via email and dashboard once their submission's test execution and rubric scoring are complete. | Medium | Pass: Notification is sent within 30 seconds of scoring completion. Fail: Notification is delayed beyond 30 seconds or not sent. | Keeps students informed of grading status without needing to poll the portal. |
| FR-005 | Functional | The system shall flag any submission whose automated rubric score falls within a low-confidence variance threshold for mandatory manual faculty review. | Medium | Pass: All submissions above the configured variance threshold appear in the faculty 'Needs Review' queue. Fail: A flagged submission is missing from the queue. | Ensures ambiguous or borderline automated grades receive human verification before being finalized. |
| NFR-001 | Nonfunctional | The system shall handle up to 100 concurrent project submissions without dropping queue items or exceeding 1.5 GB memory footprint. | High | Pass: Benchmarking tests confirm target latency and stable memory use under simulated peak load. | Ensures the platform stays responsive during deadline-driven submission spikes. (Given) |
| NFR-002 | Nonfunctional | The system shall store all submitted code, test results, and scores in an encrypted data store, accessible only to the submitting student and authorized faculty. | High | Pass: Storage audit confirms encryption at rest; access-control tests show unauthorized read/write attempts are denied. Fail: Data is stored unencrypted or an unauthorized access attempt succeeds. | Protects student academic records and satisfies institutional data-privacy requirements. |

## 2. Use-Case Diagram Elements
**System:** Automated Rubric Assignment Evaluator (System)

**Actors & Use Cases:**
*   **Student**
    *   UC-01: Upload Project Submission
*   **Peer Reviewer**
    *   UC-04: Assign Peer Review
    *   UC-05: Submit Peer Review Feedback
*   **Faculty Evaluator**
    *   UC-03: Generate Rubric Score Breakdown (Supporting Actor)
    *   UC-06: Flag Submission for Manual Review (via extension)
    *   UC-07: View Rubric Report

**Use Case Relationships:**
*   **UC-01 (Upload Project Submission)** `<<include>>` **UC-02 (Execute Automated Test Suite)**
*   **UC-02 (Execute Automated Test Suite)** `<<include>>` **UC-03 (Generate Rubric Score Breakdown)**
*   **UC-06 (Flag Submission for Manual Review)** `<<extend>>` **UC-03 (Generate Rubric Score Breakdown)**

## 3. Use-Case Flow

**Use Case: UC-03 — Generate Rubric Score Breakdown**
*   **Primary Actor:** Student (triggers via submission)
*   **Supporting Actor:** Faculty Evaluator

**Preconditions**
*   Student has an active account and a valid assignment is open for submission.
*   The pre-configured unit test suite and rubric weighting for the assignment exist in the system.

**Postconditions**
*   An itemized rubric score breakdown is generated and stored against the submission.
*   The student and faculty evaluator can view the report; peer-review assignment (UC-04) becomes eligible to run.

**Main Success Scenario**
1. Student selects "Upload Submission" and uploads a zipped project file (includes UC-01).
2. System validates the file structure and confirms it meets the assignment's submission format.
3. System automatically queues the submission and executes the pre-configured unit test suite (includes UC-02).
4. System collects the test results (pass/fail per test case, coverage, syntax check output).
5. System applies the assignment's rubric weighting rules to the test results.
6. System generates an itemized rubric score breakdown (per-criterion scores and a total).
7. System stores the report and notifies the student and faculty evaluator that scoring is complete.
8. Use case ends successfully.

**Alternate Flow — A1: Low-Confidence Score (extends to UC-06)**
*Trigger: at Step 6, the computed rubric score falls within the configured low-confidence variance threshold.*
1. System flags the submission and adds it to the faculty "Needs Review" queue (UC-06 — extend).
2. Faculty Evaluator manually inspects the test output and rubric breakdown.
3. Faculty Evaluator confirms or overrides the automated score (UC-03 / FR-003).
4. Flow resumes at Step 7 of the main success scenario with the faculty-confirmed score.

**Alternate Flow — A2: Invalid or Corrupted Submission File**
*Trigger: at Step 2, the uploaded file cannot be unzipped or is missing required project structure.*
1. System rejects the file and marks the submission status as "Failed — Invalid Format."
2. System notifies the student with the specific validation error.
3. Student corrects the submission and re-uploads, returning to Step 1.
