
```mermaid
graph TD;
    A[Blockchain Data APIs (Etherscan, CoinGecko)] --> B[AWS Lambda (API Call)];
    B --> C{Data Storage};
    C --> D1[AWS S3 (Data Lake)];
    C --> D2[AWS RDS (PostgreSQL/MySQL)];
    C --> D3[AWS DynamoDB];
    
    D1 --> E[AWS Glue (ETL Pipeline)];
    E --> D2;
    E --> D3;
    
    D1 --> F1[AWS Athena (Query S3 Data)];
    D2 --> F2[SQL Queries (RDS Data)];
    D3 --> F3[DynamoDB Queries];

    F1 --> G1[Open-Source Visualization (Grafana, Metabase)];
    F2 --> G1;
    F3 --> G1;

    H[Source Control (GitHub or CodeCommit)] --> I[CI/CD Pipeline (CodePipeline, CodeBuild, CodeDeploy)];
    I --> B;
    I --> E;
