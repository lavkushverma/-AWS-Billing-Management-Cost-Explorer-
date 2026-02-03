# 💰 AWS Billing Management & Cost Explorer - Complete Guide

![AWS](https://img.shields.io/badge/AWS-Billing-orange?logo=amazon-aws)
![Cost](https://img.shields.io/badge/Cost-Management-green)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

Complete guide to understanding and managing AWS costs effectively.

---

## 📋 Table of Contents

- [Overview](#overview)
- [AWS Billing Dashboard](#aws-billing-dashboard)
- [AWS Cost Explorer](#aws-cost-explorer)
- [AWS Budgets](#aws-budgets)
- [Cost Allocation Tags](#cost-allocation-tags)
- [AWS Cost and Usage Reports](#aws-cost-and-usage-reports)
- [Savings Plans](#savings-plans)
- [Reserved Instances](#reserved-instances)
- [Spot Instances](#spot-instances)
- [Cost Optimization Strategies](#cost-optimization-strategies)
- [Billing Alarms with CloudWatch](#billing-alarms-with-cloudwatch)
- [AWS Organizations Billing](#aws-organizations-billing)
- [Free Tier Monitoring](#free-tier-monitoring)
- [CLI Commands](#cli-commands)
- [Terraform Examples](#terraform-examples)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Overview

### What is AWS Billing Management?

AWS Billing Management helps you:
- ✅ Monitor your AWS spending
- ✅ Set budgets and alerts
- ✅ Analyze cost patterns
- ✅ Optimize resource usage
- ✅ Forecast future costs

### AWS Cost Management Tools

```
┌─────────────────────────────────────────────────────────────┐
│                 AWS COST MANAGEMENT TOOLS                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Billing    │  │    Cost      │  │    AWS       │      │
│  │  Dashboard   │  │   Explorer   │  │   Budgets    │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │    Cost      │  │   Savings    │  │  Reserved    │      │
│  │   Reports    │  │    Plans     │  │  Instances   │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Cost       │  │   Billing    │  │   Pricing    │      │
│  │ Anomaly Det. │  │   Alarms     │  │  Calculator  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 📊 AWS Billing Dashboard

### What is Billing Dashboard?

The **Billing Dashboard** provides a summary of your AWS costs and usage.

### Key Features

```
┌─────────────────────────────────────────────────┐
│           BILLING DASHBOARD                      │
├─────────────────────────────────────────────────┤
│                                                  │
│  Month-to-Date Costs    │  $1,234.56            │
│  Forecasted Month End   │  $2,500.00            │
│  Last Month Total       │  $2,100.45            │
│                                                  │
│  ┌─────────────────────────────────────────┐    │
│  │  TOP SERVICES BY COST                    │    │
│  ├─────────────────────────────────────────┤    │
│  │  EC2           ████████████  45%  $555  │    │
│  │  RDS           ██████        25%  $309  │    │
│  │  S3            ████          15%  $185  │    │
│  │  Lambda        ██            10%  $123  │    │
│  │  Others        █              5%   $62  │    │
│  └─────────────────────────────────────────┘    │
│                                                  │
└─────────────────────────────────────────────────┘
```

### Access Billing Dashboard

**Console:** 
```
AWS Console → Billing → Dashboard
URL: https://console.aws.amazon.com/billing/
```

### Enable IAM Access to Billing

By default, only root account can access billing. To enable IAM users:

```
1. Log in as root user
2. Go to Account Settings
3. IAM User and Role Access to Billing Information
4. Click "Edit"
5. Select "Activate IAM Access"
6. Click "Update"
```

### IAM Policy for Billing Access

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "aws-portal:ViewBilling",
        "aws-portal:ViewAccount",
        "aws-portal:ViewUsage",
        "aws-portal:ViewPaymentMethods",
        "budgets:ViewBudget",
        "ce:GetCostAndUsage",
        "ce:GetCostForecast"
      ],
      "Resource": "*"
    }
  ]
}
```

---

## 📈 AWS Cost Explorer

### What is Cost Explorer?

**AWS Cost Explorer** is a tool that helps you visualize, understand, and manage your AWS costs and usage over time.

### Key Features

| Feature | Description |
|---------|-------------|
| **Cost Analysis** | View costs by service, account, tag |
| **Forecasting** | Predict future costs |
| **Filtering** | Filter by time, service, region |
| **Grouping** | Group costs by various dimensions |
| **Reports** | Save and schedule reports |
| **Recommendations** | Get optimization suggestions |

### Enable Cost Explorer

```bash
# Cost Explorer must be enabled first (takes 24 hours for data)
# Go to: AWS Console → Billing → Cost Explorer → Enable Cost Explorer
```

### Cost Explorer Dashboard

```
┌─────────────────────────────────────────────────────────────────────┐
│                      COST EXPLORER                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Date Range: [Last 6 Months ▼]    Granularity: [Monthly ▼]          │
│  Group By:   [Service ▼]          Filter: [All Services ▼]          │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────┐     │
│  │                                                             │     │
│  │  $3000 │                                           ████    │     │
│  │        │                                    ████   ████    │     │
│  │  $2500 │                             ████   ████   ████    │     │
│  │        │                      ████   ████   ████   ████    │     │
│  │  $2000 │               ████   ████   ████   ████   ████    │     │
│  │        │        ████   ████   ████   ████   ████   ████    │     │
│  │  $1500 │ ████   ████   ████   ████   ████   ████   ████    │     │
│  │        │ ████   ████   ████   ████   ████   ████   ████    │     │
│  │  $1000 │ ████   ████   ████   ████   ████   ████   ████    │     │
│  │        │ ████   ████   ████   ████   ████   ████   ████    │     │
│  │   $500 │ ████   ████   ████   ████   ████   ████   ████    │     │
│  │        │ ████   ████   ████   ████   ████   ████   ████    │     │
│  │     $0 ├──────┬──────┬──────┬──────┬──────┬──────┬──────   │     │
│  │          Jan    Feb    Mar    Apr    May    Jun    Jul     │     │
│  │                                                             │     │
│  │  Legend: ██ EC2  ██ RDS  ██ S3  ██ Lambda  ██ Others       │     │
│  └────────────────────────────────────────────────────────────┘     │
│                                                                      │
│  Total: $15,234.56                  Forecasted: $18,500.00          │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Using Cost Explorer API

#### Get Cost and Usage

```bash
# Get cost for last 30 days
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity MONTHLY \
  --metrics "UnblendedCost" \
  --group-by Type=DIMENSION,Key=SERVICE
```

**Output:**
```json
{
  "ResultsByTime": [
    {
      "TimePeriod": {
        "Start": "2024-01-01",
        "End": "2024-01-31"
      },
      "Groups": [
        {
          "Keys": ["Amazon Elastic Compute Cloud - Compute"],
          "Metrics": {
            "UnblendedCost": {
              "Amount": "555.45",
              "Unit": "USD"
            }
          }
        },
        {
          "Keys": ["Amazon Simple Storage Service"],
          "Metrics": {
            "UnblendedCost": {
              "Amount": "125.30",
              "Unit": "USD"
            }
          }
        }
      ]
    }
  ]
}
```

#### Get Cost by Tag

```bash
# Get cost grouped by tag
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity MONTHLY \
  --metrics "UnblendedCost" \
  --group-by Type=TAG,Key=Environment
```

#### Get Cost Forecast

```bash
# Forecast next 30 days
aws ce get-cost-forecast \
  --time-period Start=2024-02-01,End=2024-02-28 \
  --granularity MONTHLY \
  --metric UNBLENDED_COST
```

**Output:**
```json
{
  "Total": {
    "Amount": "2850.00",
    "Unit": "USD"
  },
  "ForecastResultsByTime": [
    {
      "TimePeriod": {
        "Start": "2024-02-01",
        "End": "2024-02-28"
      },
      "MeanValue": "2850.00",
      "PredictionIntervalLowerBound": "2500.00",
      "PredictionIntervalUpperBound": "3200.00"
    }
  ]
}
```

#### Get Daily Costs for Specific Service

```bash
# Get daily EC2 costs
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity DAILY \
  --metrics "UnblendedCost" \
  --filter '{
    "Dimensions": {
      "Key": "SERVICE",
      "Values": ["Amazon Elastic Compute Cloud - Compute"]
    }
  }'
```

### Python Script for Cost Analysis

```python
#!/usr/bin/env python3
# cost_analysis.py

import boto3
from datetime import datetime, timedelta

def get_monthly_costs():
    """Get cost breakdown by service for current month"""
    
    client = boto3.client('ce', region_name='us-east-1')
    
    # Get date range
    end_date = datetime.now()
    start_date = end_date.replace(day=1)
    
    response = client.get_cost_and_usage(
        TimePeriod={
            'Start': start_date.strftime('%Y-%m-%d'),
            'End': end_date.strftime('%Y-%m-%d')
        },
        Granularity='MONTHLY',
        Metrics=['UnblendedCost'],
        GroupBy=[
            {'Type': 'DIMENSION', 'Key': 'SERVICE'}
        ]
    )
    
    print("\n📊 CURRENT MONTH COSTS BY SERVICE")
    print("=" * 50)
    
    total = 0
    for group in response['ResultsByTime'][0]['Groups']:
        service = group['Keys'][0]
        cost = float(group['Metrics']['UnblendedCost']['Amount'])
        total += cost
        print(f"{service[:40]:<40} ${cost:>10.2f}")
    
    print("=" * 50)
    print(f"{'TOTAL':<40} ${total:>10.2f}")

def get_cost_forecast():
    """Get cost forecast for next month"""
    
    client = boto3.client('ce', region_name='us-east-1')
    
    start_date = datetime.now().replace(day=1) + timedelta(days=32)
    start_date = start_date.replace(day=1)
    end_date = start_date.replace(day=28)
    
    response = client.get_cost_forecast(
        TimePeriod={
            'Start': start_date.strftime('%Y-%m-%d'),
            'End': end_date.strftime('%Y-%m-%d')
        },
        Granularity='MONTHLY',
        Metric='UNBLENDED_COST'
    )
    
    print("\n🔮 COST FORECAST")
    print("=" * 50)
    print(f"Predicted: ${float(response['Total']['Amount']):.2f}")

def get_top_cost_drivers():
    """Identify top cost drivers"""
    
    client = boto3.client('ce', region_name='us-east-1')
    
    end_date = datetime.now()
    start_date = end_date - timedelta(days=7)
    
    response = client.get_cost_and_usage(
        TimePeriod={
            'Start': start_date.strftime('%Y-%m-%d'),
            'End': end_date.strftime('%Y-%m-%d')
        },
        Granularity='DAILY',
        Metrics=['UnblendedCost'],
        GroupBy=[
            {'Type': 'DIMENSION', 'Key': 'SERVICE'}
        ]
    )
    
    # Calculate totals by service
    service_costs = {}
    for time_period in response['ResultsByTime']:
        for group in time_period['Groups']:
            service = group['Keys'][0]
            cost = float(group['Metrics']['UnblendedCost']['Amount'])
            service_costs[service] = service_costs.get(service, 0) + cost
    
    # Sort and show top 5
    sorted_services = sorted(service_costs.items(), key=lambda x: x[1], reverse=True)
    
    print("\n🔝 TOP 5 COST DRIVERS (Last 7 Days)")
    print("=" * 50)
    for service, cost in sorted_services[:5]:
        print(f"{service[:40]:<40} ${cost:>10.2f}")

if __name__ == '__main__':
    get_monthly_costs()
    get_cost_forecast()
    get_top_cost_drivers()
```

---

## 💰 AWS Budgets

### What is AWS Budgets?

**AWS Budgets** allows you to set custom budgets and receive alerts when costs or usage exceed thresholds.

### Budget Types

```
┌─────────────────────────────────────────────────────────────┐
│                   BUDGET TYPES                               │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─────────────────┐    ┌─────────────────┐                 │
│  │   COST BUDGET   │    │  USAGE BUDGET   │                 │
│  │                 │    │                 │                 │
│  │  Track spending │    │  Track resource │                 │
│  │  by service,    │    │  usage (hours,  │                 │
│  │  account, tag   │    │  GB, requests)  │                 │
│  └─────────────────┘    └─────────────────┘                 │
│                                                              │
│  ┌─────────────────┐    ┌─────────────────┐                 │
│  │ RESERVATION     │    │ SAVINGS PLAN    │                 │
│  │    BUDGET       │    │    BUDGET       │                 │
│  │                 │    │                 │                 │
│  │  Track RI       │    │  Track Savings  │                 │
│  │  utilization    │    │  Plan coverage  │                 │
│  │  and coverage   │    │  and usage      │                 │
│  └─────────────────┘    └─────────────────┘                 │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Create Budget via Console

```
1. Go to AWS Console → Billing → Budgets
2. Click "Create budget"
3. Select budget type
4. Configure:
   - Budget name
   - Period (Monthly/Quarterly/Annually)
   - Budget amount
   - Filters (Service, Account, Tag)
5. Set alert thresholds
6. Add email recipients
7. Review and create
```

### Create Budget via CLI

#### Monthly Cost Budget

```bash
# Create budget configuration file
cat > budget.json << 'EOF'
{
  "BudgetName": "Monthly-Cost-Budget",
  "BudgetLimit": {
    "Amount": "1000",
    "Unit": "USD"
  },
  "BudgetType": "COST",
  "CostFilters": {},
  "CostTypes": {
    "IncludeTax": true,
    "IncludeSubscription": true,
    "UseBlended": false,
    "IncludeRefund": false,
    "IncludeCredit": false,
    "IncludeUpfront": true,
    "IncludeRecurring": true,
    "IncludeOtherSubscription": true,
    "IncludeSupport": true,
    "IncludeDiscount": true,
    "UseAmortized": false
  },
  "TimeUnit": "MONTHLY"
}
EOF

# Create notifications file
cat > notifications.json << 'EOF'
[
  {
    "Notification": {
      "NotificationType": "ACTUAL",
      "ComparisonOperator": "GREATER_THAN",
      "Threshold": 80,
      "ThresholdType": "PERCENTAGE"
    },
    "Subscribers": [
      {
        "SubscriptionType": "EMAIL",
        "Address": "alerts@example.com"
      }
    ]
  },
  {
    "Notification": {
      "NotificationType": "FORECASTED",
      "ComparisonOperator": "GREATER_THAN",
      "Threshold": 100,
      "ThresholdType": "PERCENTAGE"
    },
    "Subscribers": [
      {
        "SubscriptionType": "EMAIL",
        "Address": "alerts@example.com"
      }
    ]
  }
]
EOF

# Create budget
aws budgets create-budget \
  --account-id 123456789012 \
  --budget file://budget.json \
  --notifications-with-subscribers file://notifications.json
```

#### Service-Specific Budget

```bash
cat > ec2-budget.json << 'EOF'
{
  "BudgetName": "EC2-Monthly-Budget",
  "BudgetLimit": {
    "Amount": "500",
    "Unit": "USD"
  },
  "BudgetType": "COST",
  "CostFilters": {
    "Service": ["Amazon Elastic Compute Cloud - Compute"]
  },
  "TimeUnit": "MONTHLY"
}
EOF

aws budgets create-budget \
  --account-id 123456789012 \
  --budget file://ec2-budget.json
```

#### Tag-Based Budget

```bash
cat > project-budget.json << 'EOF'
{
  "BudgetName": "Project-Alpha-Budget",
  "BudgetLimit": {
    "Amount": "2000",
    "Unit": "USD"
  },
  "BudgetType": "COST",
  "CostFilters": {
    "TagKeyValue": ["user:Project$Alpha"]
  },
  "TimeUnit": "MONTHLY"
}
EOF

aws budgets create-budget \
  --account-id 123456789012 \
  --budget file://project-budget.json
```

### List Budgets

```bash
# List all budgets
aws budgets describe-budgets --account-id 123456789012

# Get specific budget
aws budgets describe-budget \
  --account-id 123456789012 \
  --budget-name "Monthly-Cost-Budget"
```

### Delete Budget

```bash
aws budgets delete-budget \
  --account-id 123456789012 \
  --budget-name "Monthly-Cost-Budget"
```

### Budget Alert Thresholds

```
┌─────────────────────────────────────────────────────────────┐
│              BUDGET ALERT THRESHOLDS                         │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Budget: $1,000/month                                        │
│                                                              │
│  ├─ 50% ($500)  → Email: "Heads up - 50% used"             │
│  ├─ 80% ($800)  → Email: "Warning - 80% used"               │
│  ├─ 90% ($900)  → Email + SNS: "Critical - 90% used"        │
│  ├─ 100% ($1000) → Email + SNS + Lambda: "Budget exceeded!" │
│  └─ 120% ($1200) → All + Slack notification                 │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Budget Actions (Auto-Remediation)

```bash
# Create budget with automatic action
cat > budget-action.json << 'EOF'
{
  "BudgetName": "Auto-Stop-Budget",
  "BudgetLimit": {
    "Amount": "500",
    "Unit": "USD"
  },
  "BudgetType": "COST",
  "TimeUnit": "MONTHLY"
}
EOF

# Create action to stop EC2 instances when budget exceeded
aws budgets create-budget-action \
  --account-id 123456789012 \
  --budget-name "Auto-Stop-Budget" \
  --notification-type ACTUAL \
  --action-type APPLY_IAM_POLICY \
  --action-threshold ActionThresholdValue=100,ActionThresholdType=PERCENTAGE \
  --definition IamActionDefinition='{PolicyArn=arn:aws:iam::aws:policy/AWSDenyAll,Roles=["EC2Role"]}' \
  --execution-role-arn arn:aws:iam::123456789012:role/BudgetActionRole \
  --approval-model AUTOMATIC
```

---

## 🏷️ Cost Allocation Tags

### What are Cost Allocation Tags?

**Cost Allocation Tags** help you categorize and track AWS costs by project, team, environment, etc.

### Tag Types

```
┌─────────────────────────────────────────────────────────────┐
│                     TAG TYPES                                │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌───────────────────────────────────────────────────────┐  │
│  │         AWS GENERATED TAGS (Automatic)                 │  │
│  │                                                        │  │
│  │  aws:createdBy          → Who created the resource    │  │
│  │  aws:cloudformation:*   → CloudFormation info          │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌───────────────────────────────────────────────────────┐  │
│  │         USER DEFINED TAGS (Custom)                     │  │
│  │                                                        │  │
│  │  Environment    → Production, Development, Testing     │  │
│  │  Project        → ProjectAlpha, ProjectBeta           │  │
│  │  CostCenter     → Marketing, Engineering, Finance     │  │
│  │  Owner          → team-name, email                    │  │
│  │  Application    → WebApp, API, Database               │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Enable Cost Allocation Tags

```
1. Go to AWS Console → Billing → Cost Allocation Tags
2. Select tags to activate
3. Click "Activate"
4. Wait 24 hours for data to appear in reports
```

### Recommended Tagging Strategy

```json
{
  "Tags": [
    {
      "Key": "Environment",
      "Value": "Production"
    },
    {
      "Key": "Project",
      "Value": "WebApplication"
    },
    {
      "Key": "CostCenter",
      "Value": "CC-12345"
    },
    {
      "Key": "Owner",
      "Value": "devops-team"
    },
    {
      "Key": "Application",
      "Value": "CustomerPortal"
    },
    {
      "Key": "CreatedBy",
      "Value": "terraform"
    }
  ]
}
```

### Tag Resources via CLI

```bash
# Tag EC2 instance
aws ec2 create-tags \
  --resources i-1234567890abcdef0 \
  --tags Key=Environment,Value=Production \
         Key=Project,Value=WebApp \
         Key=CostCenter,Value=CC-12345

# Tag S3 bucket
aws s3api put-bucket-tagging \
  --bucket my-bucket \
  --tagging 'TagSet=[{Key=Environment,Value=Production},{Key=Project,Value=WebApp}]'

# Tag RDS instance
aws rds add-tags-to-resource \
  --resource-name arn:aws:rds:us-east-1:123456789012:db:mydb \
  --tags Key=Environment,Value=Production
```

### Enforce Tagging with AWS Config

```json
{
  "ConfigRuleName": "required-tags",
  "Source": {
    "Owner": "AWS",
    "SourceIdentifier": "REQUIRED_TAGS"
  },
  "InputParameters": "{\"tag1Key\":\"Environment\",\"tag2Key\":\"Project\",\"tag3Key\":\"Owner\"}",
  "Scope": {
    "ComplianceResourceTypes": [
      "AWS::EC2::Instance",
      "AWS::S3::Bucket",
      "AWS::RDS::DBInstance"
    ]
  }
}
```

### Tag Policy (AWS Organizations)

```json
{
  "tags": {
    "Environment": {
      "tag_key": {
        "@@assign": "Environment"
      },
      "tag_value": {
        "@@assign": ["Production", "Development", "Testing", "Staging"]
      },
      "enforced_for": {
        "@@assign": ["ec2:instance", "s3:bucket", "rds:db"]
      }
    },
    "CostCenter": {
      "tag_key": {
        "@@assign": "CostCenter"
      },
      "tag_value": {
        "@@assign": ["CC-*"]
      }
    }
  }
}
```

---

## 📑 AWS Cost and Usage Reports

### What is CUR?

**AWS Cost and Usage Report (CUR)** is the most comprehensive cost and usage data available.

### Features

```
┌─────────────────────────────────────────────────────────────┐
│            COST AND USAGE REPORT (CUR)                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ✓ Most detailed billing data                               │
│  ✓ Hourly/Daily/Monthly granularity                         │
│  ✓ Resource-level line items                                │
│  ✓ Cost allocation tags                                     │
│  ✓ Reserved Instance utilization                            │
│  ✓ Savings Plans utilization                                │
│  ✓ Delivered to S3 bucket                                   │
│  ✓ Can be analyzed with Athena, Redshift, QuickSight        │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Create CUR

```
1. Go to AWS Console → Billing → Cost & Usage Reports
2. Click "Create report"
3. Configure:
   - Report name: "my-cost-report"
   - Include resource IDs: ✓
   - Time granularity: Hourly
   - Refresh: Automatically
4. Select S3 bucket
5. Report path prefix: "cur"
6. Compression: GZIP
7. Format: Parquet (for Athena)
8. Create report
```

### Analyze CUR with Athena

#### Create Athena Table

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS cost_reports;

-- Create table (Athena will auto-create from crawler)
CREATE EXTERNAL TABLE IF NOT EXISTS cost_reports.cur_data (
  identity_line_item_id STRING,
  identity_time_interval STRING,
  bill_invoice_id STRING,
  bill_billing_period_start_date STRING,
  bill_billing_period_end_date STRING,
  line_item_usage_account_id STRING,
  line_item_line_item_type STRING,
  line_item_usage_start_date STRING,
  line_item_usage_end_date STRING,
  line_item_product_code STRING,
  line_item_usage_type STRING,
  line_item_operation STRING,
  line_item_availability_zone STRING,
  line_item_resource_id STRING,
  line_item_usage_amount DOUBLE,
  line_item_unblended_rate STRING,
  line_item_unblended_cost DOUBLE,
  line_item_blended_rate STRING,
  line_item_blended_cost DOUBLE,
  product_region STRING,
  resource_tags_user_environment STRING,
  resource_tags_user_project STRING
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe'
STORED AS PARQUET
LOCATION 's3://my-bucket/cur/'
```

#### Common CUR Queries

```sql
-- Total cost by service (current month)
SELECT 
  line_item_product_code AS service,
  SUM(line_item_unblended_cost) AS total_cost
FROM cost_reports.cur_data
WHERE 
  YEAR(line_item_usage_start_date) = 2024
  AND MONTH(line_item_usage_start_date) = 1
GROUP BY line_item_product_code
ORDER BY total_cost DESC
LIMIT 10;

-- Daily costs
SELECT 
  DATE(line_item_usage_start_date) AS date,
  SUM(line_item_unblended_cost) AS daily_cost
FROM cost_reports.cur_data
WHERE MONTH(line_item_usage_start_date) = 1
GROUP BY DATE(line_item_usage_start_date)
ORDER BY date;

-- Cost by tag (Environment)
SELECT 
  resource_tags_user_environment AS environment,
  SUM(line_item_unblended_cost) AS total_cost
FROM cost_reports.cur_data
WHERE MONTH(line_item_usage_start_date) = 1
GROUP BY resource_tags_user_environment
ORDER BY total_cost DESC;

-- Top 10 expensive resources
SELECT 
  line_item_resource_id,
  line_item_product_code,
  SUM(line_item_unblended_cost) AS total_cost
FROM cost_reports.cur_data
WHERE 
  MONTH(line_item_usage_start_date) = 1
  AND line_item_resource_id IS NOT NULL
  AND line_item_resource_id != ''
GROUP BY line_item_resource_id, line_item_product_code
ORDER BY total_cost DESC
LIMIT 10;

-- Reserved Instance coverage
SELECT 
  line_item_product_code,
  SUM(CASE WHEN line_item_line_item_type = 'DiscountedUsage' THEN line_item_usage_amount ELSE 0 END) AS ri_usage,
  SUM(CASE WHEN line_item_line_item_type = 'Usage' THEN line_item_usage_amount ELSE 0 END) AS on_demand_usage,
  SUM(CASE WHEN line_item_line_item_type = 'DiscountedUsage' THEN line_item_usage_amount ELSE 0 END) * 100 /
    NULLIF(SUM(line_item_usage_amount), 0) AS ri_coverage_percentage
FROM cost_reports.cur_data
WHERE MONTH(line_item_usage_start_date) = 1
GROUP BY line_item_product_code;
```

---

## 💵 Savings Plans

### What are Savings Plans?

**Savings Plans** offer flexible pricing models for consistent compute usage.

### Savings Plan Types

```
┌─────────────────────────────────────────────────────────────┐
│                  SAVINGS PLANS                               │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │         COMPUTE SAVINGS PLANS                           │ │
│  │                                                         │ │
│  │  • Most flexible                                        │ │
│  │  • Applies to EC2, Fargate, Lambda                     │ │
│  │  • Any region, instance family, OS                     │ │
│  │  • Up to 66% savings                                   │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │         EC2 INSTANCE SAVINGS PLANS                      │ │
│  │                                                         │ │
│  │  • Instance family specific                            │ │
│  │  • Region specific                                     │ │
│  │  • Any size, OS, tenancy                               │ │
│  │  • Up to 72% savings                                   │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │         SAGEMAKER SAVINGS PLANS                         │ │
│  │                                                         │ │
│  │  • SageMaker ML instances                              │ │
│  │  • Any component, region, size                         │ │
│  │  • Up to 64% savings                                   │ │
│  └────────────────────────────────────────────────────────┘ │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Purchase Savings Plan

```bash
# View Savings Plan offerings
aws savingsplans describe-savings-plans-offerings \
  --product-type EC2 \
  --plan-types COMPUTE_SP \
  --payment-options NO_UPFRONT \
  --durations 31536000

# Create Savings Plan purchase
aws savingsplans create-savings-plan \
  --savings-plan-offering-id offering-id \
  --commitment "100.00" \
  --purchase-time "2024-01-01T00:00:00Z"
```

### View Savings Plan Utilization

```bash
# Get utilization
aws ce get-savings-plans-utilization \
  --time-period Start=2024-01-01,End=2024-01-31

# Get coverage
aws ce get-savings-plans-coverage \
  --time-period Start=2024-01-01,End=2024-01-31
```

### Comparison: Savings Plans vs Reserved Instances

```
┌────────────────────┬─────────────────┬──────────────────┐
│     Feature        │  Savings Plans  │ Reserved Instance│
├────────────────────┼─────────────────┼──────────────────┤
│ Flexibility        │ High            │ Low              │
│ Instance Change    │ Yes             │ Limited          │
│ Region Change      │ Yes (Compute)   │ No               │
│ OS Change          │ Yes             │ No               │
│ Tenancy Change     │ Yes             │ No               │
│ Services           │ EC2,Fargate,    │ EC2, RDS,        │
│                    │ Lambda          │ ElastiCache,etc  │
│ Max Savings        │ Up to 72%       │ Up to 75%        │
│ Commitment         │ $/hour          │ Instance         │
│ Payment Options    │ All Upfront,    │ All Upfront,     │
│                    │ Partial, None   │ Partial, None    │
└────────────────────┴─────────────────┴──────────────────┘
```

---

## 📦 Reserved Instances

### What are Reserved Instances?

**Reserved Instances (RIs)** provide discounts (up to 75%) compared to On-Demand pricing in exchange for a 1 or 3-year commitment.

### RI Types

```
┌─────────────────────────────────────────────────────────────┐
│                RESERVED INSTANCE TYPES                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  STANDARD RIs                                         │   │
│  │  • Up to 75% discount                                │   │
│  │  • Limited flexibility                               │   │
│  │  • Can sell in marketplace                           │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  CONVERTIBLE RIs                                      │   │
│  │  • Up to 54% discount                                │   │
│  │  • Can change instance family, OS, tenancy           │   │
│  │  • Cannot sell in marketplace                        │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Payment Options

```
┌────────────────────────────────────────────────────────────┐
│            PAYMENT OPTIONS                                  │
├────────────────────────────────────────────────────────────┤
│                                                             │
│  All Upfront      → Highest discount (~75%)                │
│  Partial Upfront  → Moderate discount (~60%)               │
│  No Upfront       → Lower discount (~45%)                  │
│                                                             │
└────────────────────────────────────────────────────────────┘
```

### Purchase Reserved Instances

```bash
# Describe available RIs
aws ec2 describe-reserved-instances-offerings \
  --instance-type t3.large \
  --product-description "Linux/UNIX" \
  --instance-tenancy default

# Purchase RI
aws ec2 purchase-reserved-instances-offering \
  --reserved-instances-offering-id offering-id \
  --instance-count 5
```

### View RI Utilization

```bash
# Get RI utilization
aws ce get-reservation-utilization \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --group-by Type=DIMENSION,Key=SERVICE

# Get RI coverage
aws ce get-reservation-coverage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --group-by Type=DIMENSION,Key=SERVICE

# Get RI purchase recommendations
aws ce get-reservation-purchase-recommendation \
  --service "Amazon Elastic Compute Cloud - Compute" \
  --lookback-period-in-days SIXTY_DAYS
```

---

## 🎰 Spot Instances

### What are Spot Instances?

**Spot Instances** let you use unused EC2 capacity at up to 90% discount.

### Key Points

```
✅ Up to 90% discount vs On-Demand
✅ Great for fault-tolerant workloads
✅ Batch processing, big data, CI/CD
❌ Can be interrupted with 2-minute warning
❌ Not for critical, stateful applications
```

### Request Spot Instances

```bash
# Request spot instance
aws ec2 request-spot-instances \
  --instance-count 1 \
  --type "one-time" \
  --launch-specification '{
    "ImageId": "ami-0abcdef1234567890",
    "InstanceType": "t3.large",
    "KeyName": "my-key-pair",
    "SecurityGroupIds": ["sg-12345678"]
  }'

# Check spot price history
aws ec2 describe-spot-price-history \
  --instance-types t3.large \
  --product-descriptions "Linux/UNIX" \
  --start-time $(date -u +"%Y-%m-%dT%H:%M:%SZ" -d '1 day ago') \
  --end-time $(date -u +"%Y-%m-%dT%H:%M:%SZ")
```

### Spot Fleet

```json
{
  "SpotFleetRequestConfig": {
    "IamFleetRole": "arn:aws:iam::123456789012:role/aws-ec2-spot-fleet-role",
    "TargetCapacity": 10,
    "SpotPrice": "0.05",
    "LaunchSpecifications": [
      {
        "ImageId": "ami-0abcdef1234567890",
        "InstanceType": "t3.medium",
        "SubnetId": "subnet-12345678"
      },
      {
        "ImageId": "ami-0abcdef1234567890",
        "InstanceType": "t3.large",
        "SubnetId": "subnet-12345678"
      }
    ],
    "AllocationStrategy": "lowestPrice"
  }
}
```

---

## 🔔 Billing Alarms with CloudWatch

### Create Billing Alarm

```bash
# Step 1: Enable billing alerts
# Go to: Billing → Billing Preferences → Enable "Receive Billing Alerts"

# Step 2: Create SNS topic
aws sns create-topic --name billing-alerts
aws sns subscribe \
  --topic-arn arn:aws:sns:us-east-1:123456789012:billing-alerts \
  --protocol email \
  --notification-endpoint alerts@example.com

# Step 3: Create CloudWatch alarm
aws cloudwatch put-metric-alarm \
  --alarm-name "Monthly-Billing-Alarm" \
  --alarm-description "Alarm when estimated charges exceed $500" \
  --metric-name EstimatedCharges \
  --namespace AWS/Billing \
  --statistic Maximum \
  --period 21600 \
  --threshold 500 \
  --comparison-operator GreaterThanThreshold \
  --dimensions Name=Currency,Value=USD \
  --evaluation-periods 1 \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:billing-alerts \
  --region us-east-1
```

### Multiple Threshold Alarms

```bash
# Warning at $500
aws cloudwatch put-metric-alarm \
  --alarm-name "Billing-Warning-500" \
  --threshold 500 \
  --comparison-operator GreaterThanThreshold \
  --metric-name EstimatedCharges \
  --namespace AWS/Billing \
  --statistic Maximum \
  --period 21600 \
  --evaluation-periods 1 \
  --dimensions Name=Currency,Value=USD \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:billing-alerts \
  --region us-east-1

# Critical at $800
aws cloudwatch put-metric-alarm \
  --alarm-name "Billing-Critical-800" \
  --threshold 800 \
  --comparison-operator GreaterThanThreshold \
  --metric-name EstimatedCharges \
  --namespace AWS/Billing \
  --statistic Maximum \
  --period 21600 \
  --evaluation-periods 1 \
  --dimensions Name=Currency,Value=USD \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:billing-alerts \
  --region us-east-1

# Emergency at $1000
aws cloudwatch put-metric-alarm \
  --alarm-name "Billing-Emergency-1000" \
  --threshold 1000 \
  --comparison-operator GreaterThanThreshold \
  --metric-name EstimatedCharges \
  --namespace AWS/Billing \
  --statistic Maximum \
  --period 21600 \
  --evaluation-periods 1 \
  --dimensions Name=Currency,Value=USD \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:billing-alerts \
  --region us-east-1
```

### Service-Specific Billing Alarm

```bash
# EC2 specific billing alarm
aws cloudwatch put-metric-alarm \
  --alarm-name "EC2-Billing-Alarm" \
  --alarm-description "Alarm when EC2 charges exceed $200" \
  --metric-name EstimatedCharges \
  --namespace AWS/Billing \
  --statistic Maximum \
  --period 21600 \
  --threshold 200 \
  --comparison-operator GreaterThanThreshold \
  --dimensions Name=Currency,Value=USD Name=ServiceName,Value=AmazonEC2 \
  --evaluation-periods 1 \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:billing-alerts \
  --region us-east-1
```

---

## 🏢 AWS Organizations Billing

### Consolidated Billing

```
┌─────────────────────────────────────────────────────────────┐
│                AWS ORGANIZATIONS                             │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Management Account (Payer)                                  │
│  ├── Dev Account ($500)                                     │
│  ├── Staging Account ($800)                                 │
│  ├── Production Account ($2,500)                            │
│  └── Shared Services Account ($700)                         │
│                                                              │
│  Total Bill: $4,500 (paid by Management Account)            │
│                                                              │
│  Benefits:                                                   │
│  ✓ Single bill for all accounts                             │
│  ✓ Volume discounts (combined usage)                        │
│  ✓ Reserved Instance sharing                                │
│  ✓ Savings Plans sharing                                    │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### View Linked Account Costs

```bash
# Get cost by linked account
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity MONTHLY \
  --metrics "UnblendedCost" \
  --group-by Type=DIMENSION,Key=LINKED_ACCOUNT
```

### Service Control Policy for Cost Control

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyExpensiveEC2",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Condition": {
        "ForAnyValue:StringNotLike": {
          "ec2:InstanceType": [
            "t2.*",
            "t3.*",
            "t3a.*"
          ]
        }
      }
    },
    {
      "Sid": "DenyExpensiveRegions",
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": [
            "us-east-1",
            "us-west-2"
          ]
        }
      }
    }
  ]
}
```

---

## 🆓 Free Tier Monitoring

### Free Tier Services

```
┌─────────────────────────────────────────────────────────────┐
│                 AWS FREE TIER                                │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ALWAYS FREE                                                 │
│  ├── Lambda: 1M requests/month                              │
│  ├── DynamoDB: 25 GB storage                                │
│  ├── SNS: 1M publishes                                      │
│  └── CloudWatch: 10 custom metrics                          │
│                                                              │
│  12-MONTHS FREE (New Accounts)                              │
│  ├── EC2: 750 hours t2.micro/month                         │
│  ├── S3: 5 GB storage                                       │
│  ├── RDS: 750 hours db.t2.micro                            │
│  └── CloudFront: 50 GB data transfer                       │
│                                                              │
│  TRIALS                                                      │
│  ├── Amazon Redshift: 2 months                              │
│  ├── Amazon Inspector: 90 days                              │
│  └── Amazon GuardDuty: 30 days                              │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Free Tier Alerts

```
1. Go to AWS Console → Billing → Billing Preferences
2. Enable "Free Tier Usage Alerts"
3. Enter email address
4. Save preferences
```

### View Free Tier Usage

```bash
# Check Free Tier usage
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity MONTHLY \
  --metrics "UsageQuantity" \
  --filter '{
    "Dimensions": {
      "Key": "USAGE_TYPE_GROUP",
      "Values": ["EC2: Running Hours"]
    }
  }'
```

---

## 💡 Cost Optimization Strategies

### 1. **Right Sizing**

```
┌─────────────────────────────────────────────────────────────┐
│                  RIGHT SIZING                                │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Before: t3.xlarge (16 GB RAM) - $0.166/hr                  │
│  Average CPU: 10%                                            │
│  Average Memory: 25%                                         │
│                                                              │
│  After: t3.medium (4 GB RAM) - $0.0416/hr                   │
│  Monthly Savings: $90 (75% reduction)                        │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

```bash
# Get EC2 right-sizing recommendations
aws ce get-rightsizing-recommendation \
  --service "AmazonEC2" \
  --configuration '{
    "RecommendationTarget": "SAME_INSTANCE_FAMILY",
    "BenefitsConsidered": true
  }'
```

### 2. **Delete Unused Resources**

```bash
# Find unattached EBS volumes
aws ec2 describe-volumes \
  --filters Name=status,Values=available \
  --query 'Volumes[*].[VolumeId,Size,CreateTime]' \
  --output table

# Find unused Elastic IPs
aws ec2 describe-addresses \
  --query 'Addresses[?AssociationId==null].[PublicIp,AllocationId]' \
  --output table

# Find old snapshots
aws ec2 describe-snapshots \
  --owner-ids self \
  --query 'Snapshots[?StartTime<=`2023-01-01`].[SnapshotId,VolumeSize,StartTime]' \
  --output table

# Find unused load balancers
aws elbv2 describe-load-balancers \
  --query 'LoadBalancers[*].[LoadBalancerName,State.Code]' \
  --output table
```

### 3. **Use Appropriate Storage Classes (S3)**

```
┌────────────────────────────────────────────────────────────┐
│              S3 STORAGE CLASSES                             │
├────────────────────────────────────────────────────────────┤
│                                                             │
│  S3 Standard            $0.023/GB  → Frequently accessed   │
│  S3 Intelligent-Tier    $0.023/GB  → Unknown access pattern│
│  S3 Standard-IA         $0.0125/GB → Infrequent access     │
│  S3 One Zone-IA         $0.01/GB   → Non-critical data     │
│  S3 Glacier Instant     $0.004/GB  → Archive, instant access│
│  S3 Glacier Flexible    $0.0036/GB → Archive, mins to hours│
│  S3 Glacier Deep Archive $0.00099/GB → Long-term archive   │
│                                                             │
└────────────────────────────────────────────────────────────┘
```

**S3 Lifecycle Policy:**
```json
{
  "Rules": [
    {
      "ID": "Move to IA then Glacier",
      "Status": "Enabled",
      "Filter": {
        "Prefix": "logs/"
      },
      "Transitions": [
        {
          "Days": 30,
          "StorageClass": "STANDARD_IA"
        },
        {
          "Days": 90,
          "StorageClass": "GLACIER"
        }
      ],
      "Expiration": {
        "Days": 365
      }
    }
  ]
}
```

### 4. **Schedule Resources**

```bash
# Start instances on schedule (EventBridge + Lambda)
# Example: Start at 8 AM, Stop at 6 PM

# Lambda to stop instances
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2')
    
    # Get instances with Schedule tag
    response = ec2.describe_instances(
        Filters=[
            {'Name': 'tag:Schedule', 'Values': ['office-hours']},
            {'Name': 'instance-state-name', 'Values': ['running']}
        ]
    )
    
    instance_ids = []
    for reservation in response['Reservations']:
        for instance in reservation['Instances']:
            instance_ids.append(instance['InstanceId'])
    
    if instance_ids:
        ec2.stop_instances(InstanceIds=instance_ids)
        print(f"Stopped instances: {instance_ids}")
```

### 5. **Use Auto Scaling**

```bash
# Create Auto Scaling policy
aws autoscaling put-scaling-policy \
  --auto-scaling-group-name my-asg \
  --policy-name scale-down \
  --policy-type TargetTrackingScaling \
  --target-tracking-configuration '{
    "PredefinedMetricSpecification": {
      "PredefinedMetricType": "ASGAverageCPUUtilization"
    },
    "TargetValue": 50.0
  }'
```

---

## 🔧 Terraform Examples

### Budget with Alert

```hcl
resource "aws_budgets_budget" "monthly_cost" {
  name              = "monthly-cost-budget"
  budget_type       = "COST"
  limit_amount      = "1000"
  limit_unit        = "USD"
  time_unit         = "MONTHLY"

  notification {
    comparison_operator        = "GREATER_THAN"
    threshold                  = 80
    threshold_type            = "PERCENTAGE"
    notification_type         = "ACTUAL"
    subscriber_email_addresses = ["alerts@example.com"]
  }

  notification {
    comparison_operator        = "GREATER_THAN"
    threshold                  = 100
    threshold_type            = "PERCENTAGE"
    notification_type         = "FORECASTED"
    subscriber_email_addresses = ["alerts@example.com"]
  }
}
```

### Billing Alarm

```hcl
resource "aws_cloudwatch_metric_alarm" "billing_alarm" {
  alarm_name          = "billing-alarm"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 1
  metric_name         = "EstimatedCharges"
  namespace           = "AWS/Billing"
  period              = 21600
  statistic           = "Maximum"
  threshold           = 500
  alarm_description   = "Billing alarm when charges exceed $500"
  alarm_actions       = [aws_sns_topic.billing_alerts.arn]

  dimensions = {
    Currency = "USD"
  }
}

resource "aws_sns_topic" "billing_alerts" {
  name = "billing-alerts"
}

resource "aws_sns_topic_subscription" "email" {
  topic_arn = aws_sns_topic.billing_alerts.arn
  protocol  = "email"
  endpoint  = "alerts@example.com"
}
```

### Cost Explorer IAM Policy

```hcl
resource "aws_iam_policy" "cost_explorer_access" {
  name        = "cost-explorer-access"
  description = "Policy for Cost Explorer access"

  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect = "Allow"
        Action = [
          "ce:GetCostAndUsage",
          "ce:GetCostForecast",
          "ce:GetReservationCoverage",
          "ce:GetReservationUtilization",
          "ce:GetRightsizingRecommendation",
          "ce:GetSavingsPlansCoverage",
          "ce:GetSavingsPlansUtilization"
        ]
        Resource = "*"
      },
      {
        Effect = "Allow"
        Action = [
          "budgets:ViewBudget",
          "budgets:DescribeBudgets"
        ]
        Resource = "*"
      }
    ]
  })
}
```

---

## ✅ Best Practices

### 1. **Set Up Budgets Early**
```
✅ Create budgets before deploying resources
✅ Set multiple thresholds (50%, 80%, 100%)
✅ Enable forecasted alerts
✅ Include all stakeholders in notifications
```

### 2. **Use Tags Consistently**
```
✅ Tag all resources
✅ Use standardized naming (Environment, Project, Owner)
✅ Enable cost allocation tags
✅ Enforce tagging with AWS Config
```

### 3. **Review Costs Regularly**
```
✅ Weekly cost reviews
✅ Monthly optimization meetings
✅ Use Cost Explorer recommendations
✅ Check for unused resources
```

### 4. **Optimize Before Committing**
```
✅ Right-size before buying RIs
✅ Use Compute Savings Plans for flexibility
✅ Start with shorter commitments (1 year)
✅ Review utilization before renewals
```

### 5. **Enable Guardrails**
```
✅ Use SCPs to prevent expensive instance types
✅ Restrict regions to limit data transfer costs
✅ Set up billing alarms
✅ Use Budget Actions for auto-remediation
```

### 6. **Automate Cost Optimization**
```
✅ Schedule non-production resources
✅ Use Auto Scaling
✅ Implement S3 lifecycle policies
✅ Automate cleanup of unused resources
```

---

## 🐛 Troubleshooting

### Issue 1: Can't Access Billing Dashboard

```bash
# Solution: Enable IAM access to billing
# 1. Log in as root user
# 2. Go to Account Settings
# 3. Enable "IAM User and Role Access to Billing Information"
```

### Issue 2: Cost Explorer Shows No Data

```bash
# Solution: Enable Cost Explorer (takes 24 hours)
# Go to: Billing → Cost Explorer → Enable Cost Explorer
```

### Issue 3: Budget Not Creating

```bash
# Check if you have the right permissions
aws budgets create-budget \
  --account-id $(aws sts get-caller-identity --query Account --output text) \
  --budget file://budget.json

# Error: User not authorized
# Solution: Add budgets:CreateBudget permission
```

### Issue 4: Tags Not Showing in Cost Reports

```bash
# Solution:
# 1. Activate cost allocation tags
# 2. Wait 24 hours for data to appear
# 3. Ensure resources are tagged correctly

# Verify tags
aws resourcegroupstaggingapi get-tag-keys
aws resourcegroupstaggingapi get-tag-values --key Environment
```

---

## 📊 Quick Reference

### Cost Explorer API Commands

```bash
# Get current month costs
aws ce get-cost-and-usage \
  --time-period Start=$(date -d "$(date +%Y-%m-01)" +%Y-%m-%d),End=$(date +%Y-%m-%d) \
  --granularity MONTHLY \
  --metrics UnblendedCost

# Get cost by service
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity MONTHLY \
  --metrics UnblendedCost \
  --group-by Type=DIMENSION,Key=SERVICE

# Get cost by region
aws ce get-cost-and-usage \
  --time-period Start=2024-01-01,End=2024-01-31 \
  --granularity MONTHLY \
  --metrics UnblendedCost \
  --group-by Type=DIMENSION,Key=REGION

# Get cost forecast
aws ce get-cost-forecast \
  --time-period Start=$(date -d "+1 day" +%Y-%m-%d),End=$(date -d "+30 days" +%Y-%m-%d) \
  --granularity MONTHLY \
  --metric UNBLENDED_COST
```

### Budget Commands

```bash
# List budgets
aws budgets describe-budgets --account-id $(aws sts get-caller-identity --query Account --output text)

# Create budget
aws budgets create-budget --account-id ACCOUNT_ID --budget file://budget.json

# Delete budget
aws budgets delete-budget --account-id ACCOUNT_ID --budget-name "BudgetName"
```

---

## 📚 Additional Resources

- [AWS Cost Management](https://aws.amazon.com/aws-cost-management/)
- [AWS Pricing Calculator](https://calculator.aws/)
- [AWS Cost Explorer Documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)
- [AWS Well-Architected Framework - Cost Optimization](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html)

---

## 🎓 Summary

```
┌─────────────────────────────────────────────────────────────┐
│              AWS COST MANAGEMENT CHECKLIST                   │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  □ Enable Cost Explorer                                      │
│  □ Set up Budgets with alerts                               │
│  □ Create Billing Alarms                                    │
│  □ Enable Cost Allocation Tags                              │
│  □ Set up Cost and Usage Reports                            │
│  □ Review Right-Sizing Recommendations                      │
│  □ Consider Savings Plans or Reserved Instances             │
│  □ Use Spot Instances for fault-tolerant workloads          │
│  □ Schedule non-production resources                         │
│  □ Implement S3 Lifecycle Policies                          │
│  □ Delete unused resources regularly                        │
│  □ Review costs weekly/monthly                              │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---
**Happy Cost Optimizing!** 💰
