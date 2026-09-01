# Lab 2: Agile Backlog Creation & Sprint Simulation
**Project Scenario:** Automated Rubric Assignment Evaluator  
**Target Stakeholders / Actors:** Student, Faculty Evaluator  

---

## 1. Epics & User Stories Breakdown

### Epic 1: Batch Submission & Automated Test Execution
* **Description:** Enable students to submit code packages, queue submissions, and run automated syntax checks and test suites.

| Story ID | User Story Title | User Story Description (Agile Format) | Priority | Story Points | Sprint |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **STORY-1.1** | Zip File Submission Queue | **As a** Student,<br>**I want to** upload my project as a ZIP file,<br>**So that** it is queued for automated test execution. | High | **3** | Sprint 1 |
| **STORY-1.2** | Automated Test Suite Execution | **As a** Faculty Evaluator,<br>**I want the system to** execute pre-configured unit test suites on queued submissions within 10 seconds,<br>**So that** code correctness is objectively verified. | High | **8** | Sprint 1 |

---

### Epic 2: Rubric-Based Scoring & Evaluation Breakdown
* **Description:** Generate itemized rubric score breakdowns automatically and allow faculty members to review and adjust final grades.

| Story ID | User Story Title | User Story Description (Agile Format) | Priority | Story Points | Sprint |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **STORY-2.1** | Itemized Rubric Score Breakdown | **As a** Faculty Evaluator,<br>**I want to** view an itemized rubric breakdown rendered with test results,<br>**So that** I can see exact score deductions and pass/fail statuses. | High | **5** | Sprint 1 |
| **STORY-2.2** | Manual Score Override | **As a** Faculty Evaluator,<br>**I want to** manually override automated rubric scores with custom feedback comments,<br>**So that** edge cases and partial credit are fairly addressed. | Medium | **3** | Sprint 2 |

---

### Epic 3: Peer Review Assignment & Workflow
* **Description:** Automatically distribute anonymized student code to peers for review without manual administrative effort.

| Story ID | User Story Title | User Story Description (Agile Format) | Priority | Story Points | Sprint |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **STORY-3.1** | Automated Peer Review Distribution | **As a** Faculty Evaluator,<br>**I want the system to** automatically assign 3 peer reviews per student submission,<br>**So that** manual distribution overhead is eliminated. | Medium | **5** | Sprint 2 |
| **STORY-3.2** | Peer Feedback Submission | **As a** Student,<br>**I want to** submit structured feedback and scores for assigned peer code,<br>**So that** I can fulfill my peer review requirement. | Medium | **3** | Sprint 2 |

---

## 2. Sprint Allocation Plan

* **Sprint 1 (Commitment: 16 Points)**
  * `STORY-1.1` (3 pts) - Zip File Submission Queue
  * `STORY-1.2` (8 pts) - Automated Test Suite Execution
  * `STORY-2.1` (5 pts) - Itemized Rubric Score Breakdown
  * *Sprint Goal:* Deliver an end-to-end automated testing and rubric scoring pipeline for student code submissions.

* **Sprint 2 (Commitment: 11 Points)**
  * `STORY-2.2` (3 pts) - Manual Score Override
  * `STORY-3.1` (5 pts) - Automated Peer Review Distribution
  * `STORY-3.2` (3 pts) - Peer Feedback Submission
  * *Sprint Goal:* Implement peer review distribution and enable faculty score adjustments.

---

## 3. Reflection Questions & Answers

### Question 1: Did your estimations reflect the actual effort?
> **Answer:**  
> Yes, the story point assignments using the Fibonacci sequence accurately captured relative complexity and uncertainty. High-complexity stories such as `STORY-1.2` (Automated Test Suite Execution, 8 points) required significantly more effort due to sandboxed environment setup, process isolation, and 10-second timeout constraints. In contrast, standard UI tasks like `STORY-1.1` (ZIP File Submission Queue, 3 points) had low uncertainty and straightforward implementation effort.

### Question 2: Was your backlog well-prioritized?
> **Answer:**  
> Yes, the backlog was prioritized using business value and technical dependencies. High-priority functional requirements (ZIP submission upload, test execution, and rubric generation) were placed in Sprint 1 to establish the core MVP (Minimum Viable Product). Secondary features such as manual score overrides and peer review distribution were assigned Medium priority and scheduled for Sprint 2, ensuring core value was delivered early.

### Question 3: How did your simulated sprint align with your plan?
> **Answer:**  
> The simulated sprint aligned closely with our initial velocity expectations. Sprint 1 focused on completing the core execution engine (16 points), progressing smoothly from `To Do` → `In Progress` → `Done`. Minor bottlenecks occurred during `STORY-1.2` due to test runner integration, but moving items sequentially prevented work-in-progress (WIP) bloat. Sprint 2 successfully delivered the peer review features.

### Question 4: What insights did the burndown chart give about your team’s capacity?
> **Answer:**  
> The burndown chart illustrated steady progress against the ideal linear trendline. Early in Sprint 1, the remaining points line stayed horizontal while complex setup tasks were underway, followed by a sharp downward trend as test suite stories were completed. This confirmed that our team capacity of ~14-16 story points per 1-week sprint is realistic, and warned us against over-committing in future sprint planning meetings.
