# Reflection: Challenges in Translating Requirements to Use Cases and Tests
## RPL (Recognition of Prior Learning) Application System

**Author:** Boniface Kabaso
**Date:** March 2026
**Assignment:** Assignment 5

---

Translating the stakeholder concerns and system requirements defined in Assignment 4 into concrete use cases and test cases was a more demanding process than I initially anticipated. While the requirements provided a solid foundation, moving from "what the system must do" to "how users interact with it step by step" and "how we prove it works" exposed a number of significant challenges.

**From Requirements to Interactions: Finding the Right Level of Detail**

The first challenge I encountered was determining the right level of granularity for use cases. Requirements like FR-02 ("The system shall allow students to submit an RPL application") are clear statements of capability, but they do not specify the exact sequence of steps, what the user sees at each point, or how the system responds. Writing the basic flow for UC2 (Submit RPL Application) required me to think through the entire user journey — navigating to the form, selecting a module, completing fields, uploading documents, reviewing, and confirming — and then decide which of these steps were important enough to capture and which could be grouped together. Going too granular risks creating use cases that are more like screen-by-screen UI specifications, while staying too abstract defeats the purpose of the modelling exercise. Finding the right balance took several iterations.

**Handling the Relationships Between Use Cases**

One of the more intellectually demanding parts of this assignment was correctly identifying and representing the relationships between use cases — particularly the difference between «include» and «extend». For example, UC14 (Prevent Duplicate Applications) is always triggered as part of UC2 (Submit RPL Application), making it an «include» relationship. By contrast, the notification behaviour in UC5 extends UC4 (Track Application Status) because it is a conditional, automatic behaviour rather than a mandatory sub-step. Getting these distinctions right required me to go back to the requirements and ask: "Is this behaviour always triggered, or only under certain conditions?" This was not always obvious from the requirement statements alone and required careful reasoning about system behaviour.

**Writing Alternative Flows: Thinking Like an Adversary**

Defining alternative flows — the error paths and exception scenarios — was one of the most valuable but also most time-consuming parts of the use case specifications. It was relatively straightforward to describe the happy path (a student successfully submits an application), but thinking through what could go wrong required a different mindset. I had to consider network failures during document uploads, students attempting to bypass the duplicate check, assessors trying to access applications they are not assigned to, and edge cases like a student reapplying after a rejection. Each of these scenarios had to be traced back to a specific stakeholder concern or functional requirement to ensure the alternative flows were not arbitrary but grounded in real risk. This process deepened my understanding of the system significantly.

**Translating Requirements into Testable Conditions**

Writing test cases presented its own distinct challenge: every test case must have a clear, measurable expected result. Several requirements from Assignment 4 were well-suited for this — for example, NFR-P01 specifies that pages must load within 2 seconds, which translates directly into a performance test with a concrete pass/fail condition. However, other requirements were harder to test directly. FR-10 (Audit Trail and Activity Logging) required me to think about how to verify that logs are tamper-proof, not just that they exist. I addressed this by including a verification step that confirms log entries cannot be edited or deleted after creation, but I recognise that a thorough security test of tamper-proofing would require more sophisticated tooling than a simple functional test.

**Balancing Coverage with Practicality**

Finally, there was the challenge of scope. With 12 functional requirements and multiple non-functional requirements from Assignment 4, a fully exhaustive test suite would contain dozens of test cases. I had to make deliberate choices about which requirements to prioritise, focusing on the core user journey (registration, submission, duplicate prevention, review, decision) and the highest-risk non-functional areas (performance under load, HTTPS encryption, and role-based access control). This reflects a real-world constraint that requirements engineers and testers face constantly: there is never enough time or resource to test everything, and risk-based prioritisation is an essential professional skill.

Overall, this assignment reinforced that use case modelling and test case development are not mechanical exercises — they require creative thinking, a thorough understanding of stakeholder needs, and the ability to anticipate failure. The RPL system's core challenge of replacing a manual, error-prone process means that getting these specifications right is directly tied to the real-world value the system will deliver to students and institutions.

---

*Reflection prepared for Assignment 5 — RPL Application System*
*Author: Boniface Kabaso | March 2026*
*(Word count: approximately 640 words)*
