# AWS Database Savings Plans Pricing Data

Comprehensive pricing data for AWS Database Savings Plans across all available regions and eligible database services.

## Overview

AWS Database Savings Plans offer up to 35% savings on database costs in exchange for a 1-year hourly commitment. This dataset provides the Savings Plan rates for all eligible instance types, serverless configurations, and capacity units across all supported AWS regions.

## Data Source

Data is extracted from the [AWS Price List Bulk API](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/using-the-aws-price-list-bulk-api.html) using the `DatabaseSavingsPlans` service code.

**Last Updated:** December 2024

## File Description

| File | Description |
|------|-------------|
| `database_savings_plans.csv` | Complete pricing data for all regions and instance types |

## Column Reference

| Column | Description |
|--------|-------------|
| **Region** | AWS region code (e.g., `us-east-1`, `eu-west-1`) |
| **Instance Type** | Instance type, serverless unit, or capacity unit (e.g., `db.r7g.2xlarge`, `Aurora Serverless v2 ACU`, `DynamoDB Read Request Unit`) |
| **Savings Plan Rate** | Hourly rate when covered by a Database Savings Plan (USD) |
| **Savings over On-Demand** | Estimated percentage savings compared to on-demand pricing |
| **On-Demand Rate** | Estimated on-demand hourly rate (USD) |
| **Database Edition** | Database engine or service (e.g., `Aurora MySQL`, `PostgreSQL`, `DynamoDB`) |
| **License Model** | Licensing type: `Open Source`, `License Included`, `Bring Your Own License`, `AWS Native`, or `N/A` |
| **Service Code** | AWS service code (e.g., `AmazonRDS`, `AmazonDynamoDB`) |
| **Usage Type** | AWS usage type identifier |
| **Operation** | AWS operation code (used to identify database engine for RDS) |
| **Unit** | Billing unit (`Hrs`, `ReadRequestUnits`, `WriteRequestUnits`, `DCU-Hr`, etc.) |

## Eligible Services

Database Savings Plans cover the following AWS services:

| Service | Coverage |
|---------|----------|
| **Amazon Aurora** | All instance families, Serverless v2, DSQL |
| **Amazon RDS** | MySQL, PostgreSQL, MariaDB, Oracle, SQL Server |
| **Amazon DynamoDB** | On-Demand throughput (RRU/WRU), Provisioned capacity (RCU/WCU) |
| **Amazon ElastiCache** | Valkey instances, Valkey Serverless |
| **Amazon DocumentDB** | Instances, Serverless |
| **Amazon Neptune** | Instances, Serverless |
| **Amazon Keyspaces** | On-Demand and Provisioned throughput |
| **Amazon Timestream** | Query compute units |
| **AWS DMS** | Replication instances, Serverless |

## Discount Rates

Savings vary by deployment type:

| Deployment Type | Maximum Savings |
|-----------------|-----------------|
| Serverless (Aurora, ElastiCache, DocumentDB, Neptune, DMS) | Up to 35% |
| Provisioned Instances | Up to 20% |
| DynamoDB/Keyspaces On-Demand Throughput | Up to 18% |
| DynamoDB/Keyspaces Provisioned Capacity | Up to 12% |

## Database Engine Operation Codes

For Amazon RDS entries, the operation code suffix indicates the database engine:

| Code | Engine |
|------|--------|
| 0002 | Aurora PostgreSQL |
| 0014 | Aurora MySQL |
| 0016 | Aurora MySQL (I/O Optimized) |
| 0017 | Aurora PostgreSQL (I/O Optimized) |
| 0018 | MySQL |
| 0019 | Oracle |
| 0020 | SQL Server |
| 0021 | PostgreSQL |
| 0022 | MariaDB |

## Important Notes

- **Term Length:** Database Savings Plans are only available with a 1-year term (no 3-year option)
- **Payment Option:** Only "No Upfront" payment is available
- **Region Flexibility:** A single commitment covers usage across ALL regions automatically
- **Service Flexibility:** A single commitment covers ALL eligible database services
- **Cannot Combine:** Database Savings Plans cannot be combined with RDS Reserved Instances or DynamoDB Reserved Capacity on the same workload

## Usage Examples

### Filter by Region (bash)
```bash
grep "^us-east-1," database_savings_plans.csv
```

### Filter by Database Edition (bash)
```bash
grep "Aurora MySQL" database_savings_plans.csv
```

### Load in Python
```python
import pandas as pd
df = pd.read_csv('database_savings_plans.csv')

# Filter for Aurora MySQL in us-east-1
aurora_mysql = df[(df['Region'] == 'us-east-1') & (df['Database Edition'] == 'Aurora MySQL')]
```

### Load in Excel/Google Sheets
Import the CSV directly and use filters or pivot tables to analyze by region, service, or instance type.

## Disclaimer

This data is provided for informational purposes only. Pricing is subject to change. Always verify current pricing in the [AWS Console](https://console.aws.amazon.com/cost-management/home#/savings-plans) or via the [AWS Price List API](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/price-changes.html) before making purchasing decisions.

## Related Resources

- [AWS Database Savings Plans Announcement](https://aws.amazon.com/blogs/aws/introducing-database-savings-plans-for-aws-databases/)
- [Database Savings Plans Pricing Page](https://aws.amazon.com/savingsplans/database-pricing/)
- [Savings Plans User Guide](https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html)
- [AWS Price List API Documentation](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/using-the-aws-price-list-bulk-api.html)

## License

This pricing data is derived from publicly available AWS APIs. Use at your own discretion.
