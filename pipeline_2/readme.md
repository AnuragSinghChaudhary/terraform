
```mermaid

erDiagram
    API ||--o{ Lambda : Calls
    Lambda ||--o{ EventBridge : "Triggers on Schedule"
    Lambda ||--o{ S3 : "Stores Data"
    Lambda ||--o{ RDS : "Stores Structured Data"
    Lambda ||--o{ DynamoDB : "Stores Unstructured Data"
    
    S3 ||--o{ Glue : "ETL Jobs"
    RDS ||--o{ Glue : "ETL Jobs"
    DynamoDB ||--o{ Glue : "ETL Jobs"
    
    Glue ||--o{ RDS : "Loads Transformed Data"
    Glue ||--o{ DynamoDB : "Loads Transformed Data"
    Glue ||--o{ S3 : "Stores Processed Data"
    
    S3 ||--o{ Athena : "Queries Data"
    RDS ||--o{ Athena : "Queries Data"
    DynamoDB ||--o{ Athena : "Queries Data"
    
    Athena ||--o{ Grafana : "Visualization"
    Athena ||--o{ Metabase : "Visualization"
    RDS ||--o{ Grafana : "Visualization"
    RDS ||--o{ Metabase : "Visualization"
    DynamoDB ||--o{ Grafana : "Visualization"
    DynamoDB ||--o{ Metabase : "Visualization"
    
    GitHub ||--o{ CodePipeline : "Version Control"
    CodePipeline ||--o{ CodeBuild : "Builds Lambda/Glue"
    CodePipeline ||--o{ CodeDeploy : "Deploys Changes"
    CodePipeline ||--o{ Lambda : "Deploys Updates"
    CodePipeline ||--o{ Glue : "Deploys Updates"
