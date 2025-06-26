# Trendytech Healthcare Azure Data Engineering Project

## 🏥 Project Overview

A comprehensive end-to-end Azure data engineering solution for Healthcare Revenue Cycle Management (RCM) that implements a medallion architecture to process healthcare data from multiple sources. The project demonstrates real-world data engineering practices including data ingestion, transformation, quality checks, and analytics-ready data marts.

## 🏗️ Architecture

### Medallion Architecture Implementation
- **Landing Zone**: Raw flat files from external sources (CSV format)
- **Bronze Layer**: Source of truth with data in Parquet format
- **Silver Layer**: Cleaned, validated data with Common Data Model (CDM) and SCD Type 2
- **Gold Layer**: Analytics-ready facts and dimensions for business intelligence

![Screenshot 2025-06-25 220139](https://github.com/user-attachments/assets/cbf0b108-2de0-438b-a7b2-b6646c26e520)

## 📊 Domain: Healthcare Revenue Cycle Management (RCM)

RCM manages the financial aspects of healthcare from patient appointment scheduling to provider payment collection. The project addresses key business challenges:

- **Accounts Receivable Management**: Tracking payment collection efficiency
- **Data Quality**: Ensuring accuracy across multiple hospital systems
- **Historical Tracking**: Maintaining audit trails for regulatory compliance
- **Performance Metrics**: KPIs like collection rates, aging analysis, and payment cycles

## 🔧 Technologies Used

### Core Azure Services
- **Azure Data Factory (ADF)**: Data orchestration and ETL pipelines
- **Azure Databricks**: Data processing, transformations, and analytics
- **Azure SQL Database**: Source system for EMR data
- **Azure Data Lake Storage Gen2 (ADLS)**: Scalable data lake storage
- **Azure Key Vault**: Secure credential management
- **Unity Catalog**: Centralized metadata management

### Development & Integration
- **GitHub**: Version control and CI/CD
- **Delta Lake**: ACID transactions and data versioning
- **Apache Spark**: Distributed data processing
- **SQL**: Data transformations and analytics
- **Python**: Data processing and API integrations
- **REST APIs**: External data source integrations

## 📋 Data Sources

### 1. EMR (Electronic Medical Records) - Azure SQL DB
- **Patients**: Patient demographics and insurance information
- **Providers**: Healthcare provider (doctor) details
- **Departments**: Hospital department classifications
- **Transactions**: Financial transactions and billing records
- **Encounters**: Patient visit records and medical interactions

### 2. Claims Data - Insurance Flat Files
- Monthly insurance claim files in CSV format
- Processed from landing zone to bronze layer

### 3. External API Integrations
- **NPI (National Provider Identifier)**: Provider identification codes
- **ICD Codes**: International Classification of Diseases
- **CPT Codes**: Current Procedural Terminology (via flat files)

## 🚀 Key Features

### 1. Metadata-Driven Pipeline
- Configuration-based data ingestion
- Dynamic parameter passing
- Scalable to new data sources

### 2. Data Quality Framework
- Automated data validation rules
- Quarantine mechanism for bad data
- Quality metrics and monitoring

### 3. Common Data Model (CDM)
- Standardized schema across multiple hospitals
- Conflict resolution for duplicate IDs
- Surrogate key generation

### 4. Slowly Changing Dimension (SCD Type 2)
- Historical data preservation
- Change tracking with effective dates
- Complete audit trail maintenance

### 5. Security & Best Practices
- Azure Key Vault integration
- Secure credential management
- Role-based access control
- Retry mechanisms and error handling

## 📁 Project Structure

```
├── setup/
│   ├── audit_ddl.sql              # Audit table creation
│   ├── adls_mount.py              # Storage mounting scripts
│   └── unity_catalog_setup.py     # Catalog configuration
├── api_extracts/
│   ├── icd_codes.py               # ICD API integration
│   └── npi_codes.py               # NPI API integration
├── silver/
│   ├── patients.py                # Patient data processing (SCD2)
│   ├── providers.py               # Provider data processing
│   ├── departments.py             # Department data processing
│   ├── transactions.py            # Transaction data processing
│   ├── encounters.py              # Encounter data processing
│   ├── claims.py                  # Claims data processing
│   └── cpt_codes.py               # CPT codes processing
├── gold/
│   ├── dim_patients.py            # Patient dimension
│   ├── dim_providers.py           # Provider dimension
│   ├── dim_departments.py         # Department dimension
│   ├── fact_transactions.py       # Transaction fact table
│   └── gold_queries.py            # Business analytics queries
├── adf_pipelines/
│   ├── pl_emr_ingestion.json      # EMR data ingestion pipeline
│   ├── pl_end_to_end.json         # Master orchestration pipeline
│   └── linked_services/           # ADF linked services configuration
└── config/
    └── emr/
        └── load_config.csv        # Pipeline configuration metadata
```

## 🔄 Pipeline Flow

### 1. Bronze Layer Ingestion
- **EMR Data**: Direct ingestion from Azure SQL DB to Bronze (Parquet)
- **Claims Data**: Landing zone to Bronze transformation
- **API Data**: Real-time API calls to Bronze storage
- **Parallel Processing**: Configurable batch processing with retry mechanisms

### 2. Silver Layer Processing
- **Data Cleaning**: Null value handling and validation rules
- **CDM Implementation**: Schema standardization across sources
- **SCD Type 2**: Historical change tracking with effective dating
- **Quality Checks**: Data quarantine for failed validations

### 3. Gold Layer Analytics
- **Dimension Tables**: Patient, Provider, Department dimensions
- **Fact Tables**: Transaction facts with foreign key relationships
- **Business Metrics**: Revenue cycle KPIs and performance indicators

  ![Screenshot 2025-06-25 224350](https://github.com/user-attachments/assets/6492e2db-6d04-48e1-8ad7-41b2f430c388)

  ![Screenshot 2025-06-25 225356](https://github.com/user-attachments/assets/482f32df-2851-44df-9bcf-560a54d1b496)

![Screenshot 2025-06-25 225504](https://github.com/user-attachments/assets/b95b0a74-49ec-4350-a9f2-eb418da5c722)

![Screenshot 2025-06-25 225308](https://github.com/user-attachments/assets/18dfc040-6a6a-4e05-b476-12b8ce219137)



## 📈 Business Value & KPIs

### Key Performance Indicators
- **Accounts Receivable Aging**: Tracks payment collection efficiency
  - 93% collection rate for 30-day aging
  - 85% collection rate for 60-day aging
  - 73% collection rate for 90-day aging

- **Days in AR**: Average collection period monitoring
- **Revenue Cycle Efficiency**: End-to-end process optimization
- **Data Quality Metrics**: Completeness and accuracy reporting


## 🔍 Monitoring & Maintenance

### Pipeline Monitoring
- Azure Data Factory monitoring dashboard
- Databricks job execution logs
- Custom audit logging in Unity Catalog

### Data Quality Monitoring
- Automated validation rules
- Exception handling and alerting
- Quarantine data analysis

### Performance Optimization
- Partition strategy for large datasets
- Incremental loading mechanisms
- Resource scaling recommendations

## 📚 Documentation

- [Architecture Deep Dive](docs/architecture.md)
- [Pipeline Configuration Guide](docs/pipeline-config.md)
- [Data Quality Framework](docs/data-quality.md)
- [Security Implementation](docs/security.md)
- [Troubleshooting Guide](docs/troubleshooting.md)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## 🙏 Acknowledgments

- Trendytech Healthcare for domain expertise
- Azure Data Engineering community
- Open-source contributors



---

*This project demonstrates enterprise-level data engineering practices and serves as a comprehensive example of modern cloud data architecture implementation.*
