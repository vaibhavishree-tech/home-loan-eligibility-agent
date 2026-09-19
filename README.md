# Corporate HR Home Loan Eligibility Agent

An AI-driven UiPath Autonomous Agent that automates the evaluation of employee home loan eligibility by grounding decisions in corporate policy context.

## Problem Statement

Evaluating employee eligibility for corporate financial benefits, such as home loans, is traditionally a manual, repetitive HR process. HR personnel must cross-reference employee details against multi-tiered company policies, calculate salary percentages, and manually verify caps and role-based exemptions. This manual workflow is time-consuming, prone to calculation errors, and creates unnecessary bottlenecks for employees awaiting decisions. Automating this process ensures strict policy compliance, provides instant decisions, and frees HR teams to focus on strategic, human-centric tasks.

## Architecture / How It Works

The project is built entirely within **UiPath Studio Web** utilizing agentic automation to process natural language policies and structured data.

* **Autonomous Agent:** The core logic is driven by the `HomeLoan_Eligibility` agent, which evaluates incoming requests against system constraints.
* **Context Grounding:** Instead of hardcoding rules, the agent is grounded using the `HomeLoanIndex`. This context index reads directly from a provided text file (`Corporate HR Home Loan Policy Context.txt`), allowing HR to update policies dynamically without altering the agent's underlying code.
* **Data Flow:**

  * The agent accepts **5 Input Variables**: `EmployeeName`, `Designation`, `Salary` (Monthly), `Experience` (in years), and `EmploymentType`.
  * It applies the policy rules through the defined System Prompt and User Prompt.
  * It generates **1 Output Variable**: `LoanEligibilityReport`, which contains the final decision, maximum loan amount, and a clear explanation of the reasoning.

## Policy Rules Implemented

The agent autonomously enforces the following multi-tiered HR constraints:

* **Employment Status:** Only permanent employees are eligible.
* **Experience Thresholds:**

  * Less than 3 years of experience: Not eligible.
  * 3 to 5 years of experience: Eligible for up to 40% of their annual salary.
  * More than 5 years of experience: Eligible for up to 60% of their annual salary.
* **Managerial Tier:** Managers and above can apply for up to 70% of their annual salary.
* **Hard Caps:** The maximum allowable loan limit is strictly capped at ₹50,00,000.
* **Standard Terms:** Interest rate is fixed at 7.2% per annum, with a repayment period of up to 15 years.

## Demo

[Watch the Video Demonstration](https://drive.google.com/file/d/1YHT1kFPfLDI6G8P-XGXF2fA1WT6LzCf2/view?usp=drive_link)

## Sample Test Case

**1. Input Data**

| **Variable**       | **Value**                |
| ------------------ | ------------------------ |
| **EmployeeName**   | Rahul Sharma             |
| **Designation**    | Senior Software Engineer |
| **Salary**         | 85000 (Monthly)          |
| **Experience**     | 6 (Years)                |
| **EmploymentType** | Permanent                |

**2. Agent Reasoning Steps**

1. **Status Check:** Verified as a permanent employee.
2. **Experience Check:** 6 years of experience clears the 3-year minimum threshold.
3. **Tier Classification:** Designation is "Senior Software Engineer" (below Manager). Therefore, the >5 years rule (60% cap) applies, bypassing the 70% managerial rule.
4. **Financial Calculation:** Calculates annual salary (₹85,000 × 12 = ₹10,20,000). Calculates 60% of the annual salary (₹6,12,000).
5. **Policy Cap Check:** Confirms ₹6,12,000 is well below the ₹50,00,000 maximum corporate limit.

**3. Final Output (`LoanEligibilityReport`)**

* **Eligibility:** Eligible
* **Maximum Loan Amount:** ₹6,12,000
* **Explanation:** Rahul meets all eligibility criteria. As a permanent employee with over 5 years of experience below the manager level, the loan amount is calculated at 60% of the annual salary.

## Tech Stack

* **Platform:** UiPath Studio Web
* **Core Capabilities:** UiPath Autonomous Agents
* **Knowledge Base:** Context Grounding / Text Indexing (`HomeLoanIndex`)

## Limitations / Future Work

This project is currently structured as a single-agent proof-of-concept designed to demonstrate deterministic rule application via LLM reasoning.

To scale this into a production-ready enterprise solution, future iterations could feature:

* **Live Database Integration:** Automating data ingestion by connecting the agent directly to an Amazon RDS MySQL database to fetch employee records automatically, eliminating manual input.
* **Multi-Agent Architecture:** Transitioning to a distributed framework (leveraging orchestrators or frameworks like Agno) where distinct agents handle initial triage, financial risk assessment, and final HR approval workflows.
* **Edge Case Handling:** Expanding the policy context to handle nuanced scenarios such as contract-to-hire conversions, joint applications, or mid-year salary adjustments.
