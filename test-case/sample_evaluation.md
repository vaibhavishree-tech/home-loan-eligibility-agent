# Sample Evaluation & Test Case

This document outlines the test case used to evaluate the `HomeLoan_Eligibility` autonomous agent during debugging.

---

### Test Case 1: Standard Eligibility (Experience > 5 Years, Non-Manager)
**Objective:** Verify standard 60% rule application for mid-level permanent employees.

**Input Data:**
* **EmployeeName:** Rahul Sharma
* **Designation:** Senior Software Engineer
* **Salary:** 85000 
* **Experience:** 6 
* **EmploymentType:** Permanent

**Agent Output (`LoanEligibilityReport`):**

Based on the company HR Home Loan Policy, Rahul Sharma is eligible for a corporate home loan. The policy states that only permanent employees are eligible, and Rahul is a permanent employee. Additionally, employees must have at least 3 years of experience to qualify; Rahul has 6 years of experience, which meets this criterion.

For employees with more than 5 years of experience, the maximum loan amount allowed is up to 60% of their annual salary. Rahul's monthly salary is ₹85,000, so his annual salary is ₹85,000 x 12 = ₹10,20,000. Sixty percent of this amount is ₹6,12,000.

Since Rahul's designation is Senior Software Engineer, which is below the manager level, the 60% rule applies rather than the 70% rule for managers and above.

The maximum loan limit as per policy is ₹50,00,000, but Rahul's calculated eligible amount based on salary and experience is ₹6,12,000, which is well within this limit.

Summary:
- Eligibility: Eligible
- Maximum Loan Amount: ₹6,12,000
- Reasoning: Permanent employee with more than 5 years of experience, eligible for up to 60% of annual salary.
- Explanation: Rahul meets all eligibility criteria and the loan amount is calculated based on company policy percentages applied to his annual salary.