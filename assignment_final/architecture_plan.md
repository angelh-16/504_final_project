# Architecture & Implementation Plan

## Server mapping

   | Layer          | Service (Cloud)                              | Role in Solution                                           | Related Assignment/Module |
   |----------------|----------------------------------------------|------------------------------------------------------------|---------------------------|
   | Storage        | e.g., GCP Cloud Storage / Azure Blob Storage | Store raw uploaded CSV files                               | Assignment/Module X       |
   | Compute        | e.g., Cloud Run / Azure Container Apps       | Run containerized Flask API                                | Assignment/Module X       |
   | Database/SQL   | e.g., Cloud SQL / Azure SQL / BigQuery       | Store cleaned/aggregated tables for reporting              | Assignment/Module X       |
   | Analytics/AI   | e.g., Vertex AI Notebook / Azure ML Notebook | Run simple analytics or a pre-trained model (optional)     | Assignment/Module X       |