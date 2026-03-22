# Lab M7.10 - FinOps Automation and Reporting

**Repository:** https://github.com/MaryaAhmadi/ce-lab-finops-automation-reporting.git

**Activity Type:** Individual  
**Estimated Time:** 45-60 minutes

** Overview
This lab implements an automated FinOps workflow using AWS services. The solution eliminates manual cost reporting and proactively identifies idle resources that contribute to unnecessary cloud spending.
The system leverages AWS Lambda, EventBridge, SNS, Cost Explorer, and EC2 APIs to generate daily and weekly cost insights and deliver them via email.

**Objectives

Automate daily AWS cost reporting
Detect idle resources (waste) in the environment
Generate a unified weekly FinOps digest
Deliver reports via SNS email notifications
Replace manual cost analysis with automated workflows

** Architecture

EventBridge (Schedule)
        ↓
   AWS Lambda
        ↓
   SNS Topic
        ↓
     Email

** Workflows
* Daily Cost Report
EventBridge → Lambda (daily-cost-report) → SNS → Email
Runs daily at 08:00 UTC
* Idle Resource Check
EventBridge → Lambda (idle-resource-checker) → SNS → Email
Runs weekly on Mondays at 09:00 UTC
* Weekly FinOps Digest
EventBridge → Lambda (finops-weekly-digest) → SNS → Email
Runs weekly on Mondays at 10:00 UTC

**Components
1. Daily Cost Report Lambda

** Purpose:
Fetch daily AWS costs and provide a breakdown by service.

** Key Features:
Retrieves cost data from AWS Cost Explorer

** Calculates:
Daily total spend
Month-to-date (MTD) spend
Day-over-day percentage change
Displays top 5 services by cost
Sends formatted report via SNS
2. Idle Resource Checker Lambda
Purpose:
Identify unused or underutilized AWS resources.
Detects:
Unattached EBS volumes
Stopped EC2 instances
Unused Elastic IP addresses
Outputs:
Detailed list of idle resources
Estimated monthly waste based on resource type
Actionable insights for cleanup
3. Weekly FinOps Digest Lambda
Purpose:
Combine cost insights and idle resource findings into a single report.
Includes:
Weekly total spend
Average daily cost
Month-to-date spend
Daily cost trend (ASCII bar chart)
Top 5 services (MTD)
Idle resource summary
Recommended actions
AWS Services Used
AWS Lambda
Amazon EventBridge
Amazon SNS
AWS Cost Explorer API
Amazon EC2 API
AWS IAM
IAM Permissions
The Lambda execution role includes permissions for:
ce:GetCostAndUsage
ce:GetCostForecast
ec2:DescribeVolumes
ec2:DescribeInstances
ec2:DescribeAddresses
sns:Publish
CloudWatch Logs (via AWS managed policy)
Key Findings
Replace the placeholders below with your actual results
Daily average spend: $X.XX
Top cost driver: <Service Name>
Idle resources detected:
X unattached EBS volumes
X stopped EC2 instances
X unused Elastic IPs
Estimated monthly waste: $X.XX
Sample Outputs
Daily Cost Report
Daily total cost
Month-to-date cost
Day-over-day change
Top 5 AWS services by spend
Idle Resource Report
List of unused resources
Resource details (ID, type, size)
Estimated waste
Weekly Digest
Weekly cost summary
Daily cost trend visualization
Top services
Idle resource findings
Recommended actions
Screenshots
Screenshots of email reports are available in the /screenshots directory:
Daily Cost Report
Idle Resource Report
Weekly FinOps Digest
Lessons Learned
Automating FinOps workflows reduces manual effort and human error
Cost visibility improves significantly with daily reporting
Idle resources can silently accumulate and increase costs
Event-driven architectures are ideal for periodic financial monitoring
Combining cost and utilization data provides better optimization insights
Future Improvements
Integrate with Slack or Microsoft Teams instead of email
Add tagging-based cost breakdown (e.g., by project or environment)
Enhance idle detection with age thresholds (e.g., stopped > 7 days)
Store reports in S3 for historical analysis
Add dashboards using QuickSight or Grafana
Repository Structure
lambda/
  ├── daily-cost-report/
  ├── idle-resource-checker/
  └── weekly-digest/

screenshots/
README.md

## Verification Checklist

- [ ] Completed all required steps
- [ ] Documented findings
- [ ] Captured screenshots
- [ ] Submitted to GitHub

## Additional Resources

Refer to Module 7 Day 5 lessons and AWS documentation.

**Good luck! 🚀**
