# Systems Analysis and Design — Practice Exam Questions & Model Answers

**Note:** These are practice questions I've written based on your syllabus, styled to match the "scenario-based application" format described (30 marks, 6 questions). They are **not the actual exam questions** — your real paper may differ — but the *pattern, style, and reasoning approach* are exactly what you should expect. Study how each answer is structured, not just the content.

---

## Question 1 — Systems Analysis & Information Systems (5 marks)

**Scenario:**
*GreenLeaf Grocers is a mid-sized supermarket chain. Currently, cashiers record sales on paper receipts, and at the end of each day, a staff member manually adds up the totals and writes them into a ledger. The owner wants to start making informed decisions about which products to reorder based on sales trends, but currently has no way to see this data quickly.*

**(a)** Identify TWO benefits GreenLeaf Grocers would gain from adopting Systems Analysis and Design to improve their sales recording process. (2 marks)
**(b)** Recommend a suitable type of Information System for GreenLeaf Grocers' daily sales recording, and a separate type for helping the owner make reorder decisions. Justify your choices. (3 marks)

### Model Answer

**(a) Benefits:**
1. **Improved accuracy** – Replacing manual addition with a computerized system eliminates human calculation errors in daily totals.
2. **Better decision-making** – Digitized, organized sales data allows the owner to quickly identify trends instead of relying on handwritten ledgers.
*(Other acceptable answers: cost reduction, faster processing, easier data retrieval.)*

**(b) Recommended systems:**
- For **daily sales recording**, GreenLeaf should implement a **Transaction Processing System (TPS)** — e.g., a Point of Sale (POS) system — because TPS is designed to record routine, day-to-day transactions accurately and instantly at the point of sale, replacing the paper-receipt process.
- For **reorder decision-making**, the owner needs a **Management Information System (MIS)**, which would summarize the TPS's raw sales data into reports (e.g., weekly best-sellers, low-stock items). This directly solves the stated problem — the owner "has no way to see this data quickly" — because an MIS turns transactional data into digestible reports for decision-making.

*(Why not a DSS? A DSS is for more complex "what-if" modelling; at this stage GreenLeaf just needs summarized reporting, so MIS is the better fit unless the scenario specifically described complex forecasting needs.)*

---

## Question 2 — System Design and Testing (5 marks)

**Scenario:**
*A university is launching a new online course registration system. During a pilot run, several students reported that clicking "Submit" sometimes registered them for the wrong course, and a few students were able to register for courses that were already full.*

**(a)** Identify the likely design flaw(s) causing these problems. (2 marks)
**(b)** Recommend which type(s) of testing should have been carried out before launch to catch these issues, and explain why each is relevant. (3 marks)

### Model Answer

**(a) Likely design flaws:**
- Poor **input design/validation** — the form may not correctly bind the student's selection to the correct course ID before submission, causing wrong registrations.
- Missing **business rule enforcement** in the process design — the system isn't checking course capacity in real time before confirming a registration, allowing over-enrollment in full courses.

**(b) Recommended testing:**
- **Unit Testing** should have been performed on the registration module in isolation to confirm that selecting a course correctly maps to that course's ID — this would likely have caught the "wrong course" bug early, before integration.
- **System Testing** should have verified the complete registration workflow, including the capacity-check business rule, to confirm full courses correctly reject new registrations.
- **User Acceptance Testing (UAT)** with real students (as was attempted in the pilot) is valuable, but should happen *after* unit and system testing catch these more basic errors — relying on UAT alone to catch fundamental logic errors is inefficient and risks a poor first impression for users.

**Why testing matters here:** Skipping thorough testing led to real students being registered incorrectly, which could cause administrative errors, unfair access to popular courses, and reputational damage to the university's new system.

---

## Question 3 — Feasibility Study (5 marks)

**Scenario:**
*A small medical clinic wants to replace its paper-based patient record system with a digital Electronic Health Record (EHR) system. The clinic has 4 staff members, none of whom have strong IT skills. The estimated cost is $15,000, and the clinic expects to save on filing staff time and reduce record-retrieval delays. The clinic needs the system running within 2 months, before a new government health data regulation takes effect.*

**Conduct a feasibility study for this scenario by evaluating Technical, Economic, Operational, and Schedule feasibility.** (5 marks — approx. 1.25 marks per category, with an overall conclusion)

### Model Answer

- **Technical Feasibility:** The clinic's staff currently lack strong IT skills, which poses a risk. However, most modern EHR systems are designed with user-friendly interfaces and vendors typically provide training and support. Feasible, *provided* staff training and technical support are budgeted in.

- **Economic Feasibility:** The $15,000 cost must be weighed against long-term savings in filing staff time and faster patient record retrieval (reduced administrative overhead, potentially improved patient satisfaction and throughput). If these savings recur monthly/yearly, the system likely pays for itself within a reasonable period — appears economically feasible, though a formal cost-benefit analysis with real numbers would strengthen this conclusion.

- **Operational Feasibility:** Moving from paper to digital records is a significant change for staff unfamiliar with IT; there is a risk of resistance or slow adoption. This risk can be mitigated with proper training and a phased rollout, but should not be ignored.

- **Schedule Feasibility:** The 2-month deadline (driven by the new regulation) is tight, especially given staff's limited technical background. This is the highest-risk area — the clinic should prioritize a proven, ready-made EHR solution rather than custom-building one, to realistically meet the deadline.

**Conclusion:** The project is feasible overall, but Schedule and Operational feasibility carry the most risk. The clinic should choose a pre-built, easy-to-use EHR product with vendor-provided training to meet both the regulatory deadline and staff skill limitations.

---

## Question 4 — System Development Methodologies (5 marks)

**Scenario:**
*A fintech startup wants to build a mobile banking app. The founders admit that they are not yet fully sure what features customers will want most, and they wish to release a basic working version quickly, gather user feedback, and keep improving it every few weeks.*

**Recommend a suitable system development methodology for this startup. Justify your answer with reference to flexibility, risk handling, and development speed.** (5 marks)

### Model Answer

**Recommendation:** An **Agile (iterative) methodology** is most suitable for this startup, rather than a traditional Waterfall approach.

**Justification:**
- **Flexibility:** The founders explicitly state they are "not yet fully sure what features customers will want." Agile is built for exactly this situation — requirements can evolve between sprints based on real user feedback, whereas Waterfall requires requirements to be fully defined upfront, which would be risky given their uncertainty.
- **Risk Handling:** Agile's iterative sprints allow the startup to identify problems (technical or market-fit issues) early and often, in small increments, rather than discovering major issues only after a long, complete build — which is a common risk with Waterfall.
- **Development Speed:** The founders want to "release a basic working version quickly" — Agile delivers working software in short cycles (e.g., every 2–4 weeks), matching this need directly, whereas Waterfall would only deliver a finished product at the very end of a long single development phase.

**Conclusion:** Given the startup's uncertain requirements and desire for fast, iterative releases with continuous feedback, Agile is clearly the better fit than a traditional methodology.

---

## Question 5 — Process Modelling and Data Modelling (5 marks)

**Scenario:**
*A logistics company processes customer delivery requests through three departments: Sales (takes the order), Warehouse (prepares the package), and Dispatch (arranges delivery). Each department currently keeps its own separate spreadsheet, and staff have noticed that customer address details are sometimes entered differently in each spreadsheet, causing delivery delays. Management also suspects the order sometimes sits for a long time between Sales and Warehouse without anyone noticing.*

**(a)** Recommend a process modelling technique to address the delay between Sales and Warehouse, and explain how it would help. (2 marks)
**(b)** Recommend a data modelling approach to address the address-detail inconsistency, and explain how it would help. (3 marks)

### Model Answer

**(a) Process Modelling:**
A **Data Flow Diagram (DFD)** should be created to map the current flow of an order from Sales through Warehouse to Dispatch. This would visually expose exactly where the process stalls — for instance, if there is no automatic notification from Sales to Warehouse when a new order arrives, the DFD would reveal this manual handoff gap as the **bottleneck**. Once identified, the company can redesign the process (e.g., automatic system alerts) to remove the delay.

**(b) Data Modelling:**
An **Entity-Relationship Diagram (ERD)** should be used to design a single, shared database structure — with one central "Customer" entity holding address details, linked to "Order," "Warehouse Task," and "Dispatch" entities — rather than three separate department spreadsheets. This ensures address data is entered and stored **once**, and referenced (not re-typed) by each department, eliminating the inconsistency and reducing delivery delays caused by mismatched address data.

---

## Question 6 — Requirements Analysis (5 marks)

**Scenario:**
*An online bookstore wants a new e-commerce website. During discussions, the client says: "Customers should be able to search for books by title or author, add books to a cart, and checkout using a credit card. Since we sell internationally, the site absolutely must load fast even in countries with slow internet, and customer payment information must be fully protected."*

**(a)** Identify THREE functional requirements from this scenario. (1.5 marks)
**(b)** Identify TWO non-functional requirements from this scenario. (1.5 marks)
**(c)** Explain why properly documenting these requirements matters for this project. (2 marks)

### Model Answer

**(a) Functional Requirements:**
1. The system shall allow customers to search for books by title or author.
2. The system shall allow customers to add books to a shopping cart.
3. The system shall allow customers to check out using credit card payment.

**(b) Non-Functional Requirements:**
1. **Performance** – The system must load quickly/efficiently even under slow internet connections.
2. **Security** – Customer payment information must be protected (e.g., through encryption).

**(c) Importance of documenting requirements:**
Clearly documenting these requirements ensures the development team builds exactly what the client needs — for example, without explicitly recording the performance requirement, developers might build a feature-rich but heavy website that fails international customers with slow connections. Documentation also provides a clear benchmark for testing (e.g., "does the site load within X seconds?" and "is payment data encrypted?"), and serves as a reference point to prevent scope disputes between the bookstore and the development team later in the project.

---

## The Pattern to Notice

Across all six questions above, the model answers consistently:

1. **Pull specific details directly from the scenario** (never generic textbook answers)
2. **Name the correct concept/term** clearly and early in the answer
3. **Explain briefly *why*** that concept applies, in plain language
4. **Justify the choice**, often by explicitly ruling out an alternative or noting a risk/trade-off
5. Where relevant, end with a **short conclusion** tying it back to solving the business's problem

**Use this same structure on every question in your real exam** — even if you're unsure of the "perfect" textbook term, reasoning clearly from the scenario using this pattern will earn you strong application marks.

### Suggested next step
Try writing your own answers to a new scenario I give you (or one from your tutorials) *without* looking at the model answers first, then compare. Want me to generate a fresh set of scenarios for you to test yourself on?
