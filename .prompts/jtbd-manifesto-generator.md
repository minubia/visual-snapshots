# JTBD Manifesto Generator - Universal Prompt

## Multi-Source Manifesto Generation

This prompt works with ANY of these inputs:
- 🔗 GitHub repository URL
- 📄 Customer proposal document
- 💼 Product requirements doc (PRD)
- 🏗️ Existing codebase (local path)
- 💬 Interview-style Q&A
- 📊 Support ticket analysis
- 🚨 Production incident reports

---

## Universal Prompt (Copy This)

```
You are a Jobs-to-be-Done (JTBD) expert creating a comprehensive quality manifesto.

## YOUR TASK:
Analyze the provided source and create a JTBD Manifesto that defines non-negotiable quality standards.

## SOURCE PROVIDED:
[Choose ONE and specify details]

Option A - GitHub Repository:
- Repository URL: [paste URL]
- Branch: [branch name, default: main]
- Focus areas: [e.g., "payment processing module", "entire system", "API endpoints"]

Option B - Customer Proposal:
- Document: [paste proposal text or path to file]
- Customer context: [industry, company size, pain points]

Option C - Product Requirements:
- PRD/Spec: [paste or provide path]
- Target launch date: [date]
- Known constraints: [technical, business, regulatory]

Option D - Existing Codebase:
- Path: [local path to code]
- Language/Framework: [e.g., PHP/Zend, Node/Express, Python/Django]
- Problem statement: [what needs documenting]

Option E - Interview Mode:
- I will answer your questions about:
  - Who uses this system
  - What problems it solves
  - What workflows must work
  - What failures have occurred

Option F - Incident Analysis:
- Incident reports: [paste logs, error messages, timeline]
- Support tickets: [common issues]
- User complaints: [what breaks, what frustrates users]

## STEP 1: DISCOVERY (You do this first)

Based on the source type, perform analysis:

### If GitHub Repository:
1. Clone and read README, documentation
2. Analyze code structure (controllers, models, services)
3. Find test files (what's being tested tells you what's critical)
4. Check commit history (what breaks often?)
5. Review issues/PRs (what are users reporting?)
6. Identify API endpoints and data models
7. Look for error handling patterns

**Output:** Summary of:
- What this system does (in job terms)
- Who uses it (user types)
- Critical workflows (from API routes, tests)
- Known issues (from git history, TODO comments)

### If Customer Proposal:
1. Extract the "pain points" or "challenges" section
2. Identify stated goals and success metrics
3. Find the "must-haves" vs "nice-to-haves"
4. Note compliance/regulatory requirements
5. Identify integration points with existing systems

**Output:** Summary of:
- Jobs customer is hiring this solution for
- What they're firing (current broken process)
- Success criteria they specified
- Constraints and requirements

### If Product Requirements:
1. Extract user stories or use cases
2. Identify acceptance criteria
3. Note performance requirements
4. Find security/compliance requirements
5. List integration dependencies

**Output:** Summary of:
- User personas and their jobs
- Functional requirements (as jobs)
- Non-functional requirements (as standards)
- Edge cases and error scenarios

### If Existing Codebase:
1. Map out main workflows (follow the code paths)
2. Find validation logic (tells you what can go wrong)
3. Identify calculation/business logic (money, dates, quantities)
4. Check error handling and logging
5. Look for TODO/FIXME/HACK comments

**Output:** Summary of:
- Critical business logic (what must be correct)
- Data flow (what must not be lost)
- Integration points (what must stay connected)
- Technical debt (what's at risk)

### If Interview Mode:
Ask me these questions in order:

**About Users:**
1. Who are the primary users of this system?
2. What's their role/job title?
3. What are they trying to accomplish?
4. What happens if this system is unavailable?

**About Pain Points:**
5. What broken/manual process does this replace?
6. What's the cost of the current way of doing things?
7. What frustrated users about the old way?

**About Critical Workflows:**
8. Walk me through the most important use case.
9. What data absolutely cannot be lost?
10. What calculations must be 100% accurate?
11. What integrations must always work?

**About Failures:**
12. What's broken in the past?
13. What do users complain about?
14. What keeps you up at night about this system?

**About Success:**
15. How do users measure if this is working?
16. What's the minimum acceptable performance?
17. What would cause users to abandon this system?

### If Incident Analysis:
1. Parse incident timeline (what broke, when)
2. Identify root causes (code, data, infrastructure)
3. Calculate blast radius (how many users affected)
4. Note detection time (how long until noticed)
5. Review resolution steps (what fixed it)

**Output:** Summary of:
- What standards were violated
- What tests were missing
- What monitoring was lacking
- What needs to be non-negotiable going forward

## STEP 2: VALIDATE UNDERSTANDING

After discovery, show me:
```
## Discovery Summary

**System:** [Name]
**Primary Users:** [List]
**Core Value Proposition:** [One sentence]

**Critical Jobs (Ranked by Impact):**
1. [Job name] - [Why critical]
2. [Job name] - [Why critical]
3. [Job name] - [Why critical]
...

**Known Failure Modes:**
- [What breaks]
- [What goes wrong]
- [What users complain about]

**Integration Points:**
- [System 1] - [What it does]
- [System 2] - [What it does]

**Performance Requirements:**
- [Metric 1]
- [Metric 2]

Does this accurately capture the system? Any corrections or additions?
```

Wait for my confirmation before proceeding.

## STEP 3: GENERATE MANIFESTO

Once I confirm, generate the manifesto with this structure:

### Part 1: Our Purpose
**When** [user type] hire [system name], they fire [old way]. This manifesto defines the jobs customers hire us to do and the non-negotiable quality standards we commit to maintaining.

### Part 2: Primary Job
**When** [situation],
**They want to** [motivation],
**So they can** [expected outcome].

**Success looks like:**
- [Measurable outcome 1]
- [Measurable outcome 2]
- [Measurable outcome 3]
- [Measurable outcome 4]
- [Measurable outcome 5]

### Part 3: Critical Jobs (5-10 Non-Negotiables)

For each critical job:

#### Critical Job #X: [Job Name]

**What customers are really trying to do:**
[Underlying motivation, not surface feature request]

**Why this matters:**
[Business impact if this fails - money, trust, time, safety]

**Non-Negotiable Quality Standards:**

| Standard | Measurement | Current Status |
|----------|-------------|----------------|
| [What must be true] | [How we verify it] | [✅❌⚠️🔄] |
| [What must be true] | [How we verify it] | [✅❌⚠️🔄] |
| [What must be true] | [How we verify it] | [✅❌⚠️🔄] |

Status Legend:
- ✅ PASSING - Tested and working
- ❌ BROKEN - Known failure with evidence
- ⚠️ AT RISK - Works but fragile
- 🔄 NEEDS MONITORING - Untested or no data

**Test Requirements:**
- `[TYPE]-[AREA]-[NUM]`: [Specific test scenario]
  - Test types: UT (unit), IT (integration), E2E (end-to-end), REGRESSION, LOAD
  - Example: `IT-ORDER-001`: Submit valid order → expect HTTP 201 + order ID

**Real-World Evidence:**
```
[Show actual data, errors, incidents that prove importance]
- Order numbers
- Error messages
- Timestamps
- Customer quotes
- Support ticket IDs
```

### Part 4: Quality Standards Contract

Comprehensive checklist:

#### Functional Correctness
- [ ] [Standard related to business logic]
- [ ] [Standard related to validation]
- [ ] [Standard related to calculations]

#### Performance
- [ ] [Response time requirement]
- [ ] [Throughput requirement]
- [ ] [Scalability requirement]

#### Reliability
- [ ] [Logging requirement]
- [ ] [Error handling requirement]
- [ ] [Retry logic requirement]

#### Data Integrity
- [ ] [Consistency requirement]
- [ ] [Immutability requirement]
- [ ] [Audit trail requirement]

#### User Experience
- [ ] [Error message requirement]
- [ ] [Feedback requirement]
- [ ] [Validation requirement]

### Part 5: Test Strategy

```
Test Pyramid:
           ┌─────────────────┐
           │   Manual E2E    │  5%
           └─────────────────┘
         ┌───────────────────────┐
         │  Automated E2E Tests  │  15%
         └───────────────────────┘
       ┌─────────────────────────────┐
       │  Integration Tests          │  30%
       └─────────────────────────────┘
    ┌────────────────────────────────────┐
    │   Unit Tests                       │  50%
    └────────────────────────────────────┘
```

**Critical Test Scenarios (Pre-Deploy):**

*Smoke Test (5 min):*
1. [Most critical happy path]
2. [Most common error case]
3. [Integration point check]

*Regression Test (30 min):*
1. [Known bug that was fixed - prevent reoccurrence]
2. [Edge case that broke before]
3. [Performance degradation check]

*Integration Test (45 min):*
See `.tests/[feature]-testplan.md` for 50+ detailed cases

### Part 6: Failure Conditions

We have failed the customer when:

**Silent Failures:**
- ❌ [What fails without visibility]

**Wrong Answers:**
- ❌ [What calculates incorrectly]

**Lost Data:**
- ❌ [What data gets lost]

**Broken Promises:**
- ❌ [What commitment we violate]

### Part 7: Real-World Evidence

*[If incidents exist, create this section. If new system, mark as "No incidents yet - will update when they occur"]*

**[Date] - [Incident Name]**

| Time | Event | Impact |
|------|-------|--------|
| [timestamp] | [what happened] | [who affected] |

**Customer Impact:**
- [Business consequence 1]
- [Business consequence 2]

**Root Causes:**
1. [Technical cause]
2. [Process cause]

**What This Taught Us:**
[Lesson learned that informs standards]

### Part 8: Our Commitment

We commit to:
1. Test every change against these standards before deployment
2. Monitor production for violations 24/7
3. Fix violations immediately (not "next sprint")
4. Update this manifesto after incidents
5. Reject changes that violate standards

**Change Evaluation Framework:**

| Question | Action Required |
|----------|-----------------|
| Could this break [critical job]? | CRITICAL test required |
| Could this cause wrong [calculation]? | CRITICAL test required |
| Could this lose customer data? | CRITICAL test required |
| Could this fail silently? | Add comprehensive logging |
| Could this affect [integration]? | Integration test required |

**When to Break the Rules:**
NEVER. These are non-negotiable. If a requirement conflicts with these standards, the requirement is wrong.

### Part 9: Living Document

**This manifesto evolves when:**
- Production incident occurs → Update within 24 hours
- New critical job discovered → Add within sprint
- Standard becomes obsolete → Remove with team approval
- Test coverage gaps found → Add test requirements

**Maintenance:**
- Last Updated: [Date]
- Next Review: [Date]
- Maintained By: Engineering, Product, QA, Support
- Approved By: All who deploy code

### Part 10: Appendix - JTBD Framework

**The JTBD Statement:**
**When** [situation], **I want to** [motivation], **So I can** [outcome].

**Why This Matters for Testing:**

❌ Feature thinking: "Test the discount calculation method"
✅ Job thinking: "Ensure customers trust discounts won't cost them money"

The second approach leads to:
- Testing with real customer data
- Testing full workflow (not just one function)
- Testing edge cases users encounter
- Monitoring production for violations

**This manifesto is our contract with customers.**

---

## CRITICAL REQUIREMENTS (You must follow):

### 1. Use Concrete Measurements
❌ "System should be fast"
✅ "Order submission must respond in <2 seconds at 95th percentile"

### 2. Include Real Data
- Actual order numbers, error messages, timestamps
- Reference specific files and line numbers
- Show before/after with real values

### 3. Honest Status Assessment
- Don't mark everything ✅ PASSING
- Use ❌ BROKEN when there's evidence
- Use 🔄 NEEDS MONITORING when untested
- Use ⚠️ AT RISK when fragile

### 4. Specific Test IDs
Format: `[TYPE]-[AREA]-[NUMBER]`
- UT-CALC-001: Test discount calculation with 100% discount
- IT-API-005: Test order submission with invalid customer ID
- E2E-FLOW-003: Complete checkout flow from cart to confirmation

### 5. Prioritize by Impact
Order critical jobs by:
1. Money (calculations, pricing, payments)
2. Data integrity (never lose orders, maintain consistency)
3. Trust (security, privacy, audit trail)
4. Experience (speed, feedback, error messages)

### 6. Clear, Direct Language
- No corporate jargon
- No vague terms ("robust", "scalable", "enterprise-grade")
- Focus on customer outcomes, not technical implementation
- Use "we" and "our" (this is OUR contract)

### 7. Actionable Standards
Each standard must be:
- Testable (can write automated test)
- Measurable (has specific metric)
- Verifiable (can check production)
- Achievable (technically feasible)

---

## OUTPUT FORMAT

**Markdown file with:**
- Clear heading hierarchy (##, ###, ####)
- Horizontal rules (---) between major sections
- Tables for standards, measurements, incidents
- Code blocks for examples and logs
- Status emojis: ✅❌⚠️🔄
- Bold for key terms on first use
- ASCII diagrams where helpful

**File naming:**
- System-wide: `jtbd_manifesto.md`
- Feature-specific: `[feature-name]-jtbd-manifesto.md`
- Example: `cbbc-pricing-jtbd-manifesto.md`

---

## VALIDATION BEFORE FINISHING

Ask yourself:
- [ ] Can an engineer read this and know what to test?
- [ ] Can a product manager read this and understand customer value?
- [ ] Can QA read this and build test plans?
- [ ] Can an executive read this and understand business risk?
- [ ] Does every critical job have measurable standards?
- [ ] Does every standard have test requirements?
- [ ] Are all status assessments honest?
- [ ] Is there real evidence supporting importance?
- [ ] Is the language clear and direct?
- [ ] Would this document prevent the last production incident?

If any answer is "no", revise before finalizing.

---

## EXAMPLES OF GOOD DISCOVERY

### Example 1: From GitHub Repo
```
Analyzing: github.com/company/payment-service

Discovery:
- API endpoints: 12 routes in routes/payments.js
- Critical paths: charge, refund, dispute
- Test coverage: 45% (payment_test.go shows what's critical)
- Recent issues: 3 about failed refunds, 2 about duplicate charges
- Integration points: Stripe API, internal ledger service

Critical jobs identified:
1. Never charge customer twice (idempotency)
2. Always process refunds within SLA
3. Maintain audit trail for disputes
```

### Example 2: From Customer Proposal
```
Analyzing: "CBBC Pricing Requirements.pdf"

Customer pain points (page 2):
- "Manual price lookups take 5+ minutes per customer"
- "Sales reps don't know which price to charge"
- "Finance discovers unauthorized discounts after invoicing"

Success criteria (page 8):
- "Price displayed instantly when customer selected"
- "100% compliance with customer-specific pricing rules"
- "Zero unauthorized discounts reaching accounting"

Critical jobs identified:
1. Apply correct customer price automatically
2. Enforce pricing rules without manual oversight
3. Maintain pricing audit trail for compliance
```

### Example 3: From Incident Report
```
Analyzing: "Nov 18 Production Incident"

Timeline:
- 09:26 AM: Code deployed
- 08:25 AM: Order 41039 charged 176.7 instead of 0.00
- 17:09 PM: 11 orders failed, no response to users

Root cause:
- property_exists() bug broke discount calculation
- Missing $log initialization prevented error logging

Critical jobs violated:
1. Calculate money correctly (charged wrong amount)
2. Never lose an order (11 orders stuck)
3. Respond to every request (silent failures)

Standards needed:
- Discount calculation must be tested with 100% discount
- Every API call must log request AND response
- All variables must be initialized before use
```

---

## START GENERATION

I'm ready. Please provide:

**What do you want me to analyze?**

Option A: Paste GitHub repository URL
Option B: Paste customer proposal text
Option C: Paste PRD/requirements
Option D: Provide local codebase path
Option E: Start interview mode (I'll ask questions)
Option F: Paste incident reports/logs

[PASTE YOUR INPUT HERE OR SPECIFY OPTION]
```

---

## Quick Examples for Common Scenarios

### Scenario 1: New Feature from Requirements
```
Analyze this and create a JTBD manifesto:

[PASTE REQUIREMENTS DOC OR PRD]

The feature launches on [DATE].
Target users are [USER TYPES].
It integrates with [SYSTEMS].
```

### Scenario 2: Existing System Needing Documentation
```
Option D: Existing Codebase

Path: /Users/rignacio/Documents/mierp/application/modules/api/controllers/OrderController.php
Language: PHP/Zend Framework
Problem: This order submission API has had 3 production incidents in the last month. We need to document what MUST work.

Recent incidents:
- Nov 18: Undefined $log variable caused silent failures
- Nov 18: Wrong discount calculation (Order 41039)
- Nov 15: Missing discount validation

Please analyze the code and create a manifesto defining non-negotiable standards.
```

### Scenario 3: From GitHub Repo
```
Option A: GitHub Repository

Repository URL: https://github.com/company/payment-processor
Branch: main
Focus: Payment processing module (specifically charge and refund flows)

Context: We're having reliability issues. Need manifesto to define what "working correctly" means.
```

### Scenario 4: Interview Mode
```
Option E: Interview Mode

I'll answer your questions about our warehouse management system.
Start by asking about users and critical workflows.
```

---

## Tips for Best Results

### 1. Provide Context Upfront
Don't just say "analyze this code". Say:
- Why this matters (business context)
- What's broken (if anything)
- What success looks like
- What constraints exist

### 2. Include Production Data
If available, provide:
- Real error messages
- Actual order numbers
- Support ticket summaries
- Performance metrics
- User quotes

### 3. Be Honest About Current State
Don't hide problems. Say:
- "This has never been tested"
- "We know this breaks under load"
- "Users complain about this weekly"
- "We have no monitoring"

### 4. Think About Money First
The most critical jobs usually involve:
- Financial calculations
- Payment processing
- Order totals
- Pricing rules
- Refunds/credits

### 5. Remember the Audience
Good manifestos serve:
- **Engineers:** Know what to test
- **Product:** Understand customer value
- **QA:** Build test plans
- **Execs:** See business risk
- **Support:** Set customer expectations

---

## Next Steps After Generation

1. **Review with team** (30-60 min)
   - Does this capture the critical jobs?
   - Are measurements realistic?
   - Any missing failure modes?

2. **Update status emojis** (if analyzing existing system)
   - Run tests to determine ✅❌⚠️🔄
   - Don't guess - verify

3. **Create test plan**
   - Every standard → specific test case
   - Reference manifesto in test descriptions
   - Track status in manifesto

4. **Set up monitoring**
   - Add logging for critical paths
   - Create dashboards showing standard compliance
   - Alert on violations

5. **Schedule reviews**
   - After every incident: Update manifesto
   - Monthly: Update status
   - Quarterly: Full review

---

**This prompt works for ANY system. Just provide the source and I'll discover the jobs, then generate the manifesto.**
