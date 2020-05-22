## Data Inventory

Our app collects information from a state's citizens and shares the contact information of doctors who have partnered with us.

| name                           | data store | public |
| ------------------------------ | ---------- | ------ |
| citizen emails                 | s3 bucket  | false  |
| citizen names                  | s3 bucket  | false  |
| citizen social security number | AWS RDS    | false  |
| doctor names                   | AWS RDS    | true   |
| doctor emails                  | AWS RDS    | true   |
