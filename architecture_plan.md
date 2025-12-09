# Architecture & Implementation Plan

## Server mapping

   | Layer          | Service (Cloud)                              | Role in Solution                                           | Related Modules           |
   |----------------|----------------------------------------------|------------------------------------------------------------|---------------------------|
   | Frontemd/API   | Cloud Run                                    | Hosts the patient intake form and receives submissions from browser/app clients | Module 10       |
   | Storage        | GCP Cloud Storage                            | Stores patient/provider uploaded images (ID, insurance cards or attachments) | Module 6      |
   | Compute        | Cloud Function                               | Computes the triage score based on symptoms and inputs and sends to SQL    | Module 5       |
   | Database/SQL   | Cloud SQL                                    | Stores structured intake data, triage results, timestamps, visit status| Module 7 |
   | Analytics/AI   | Python analytics                             | Generates basic reports and insights from intake and triage data     | Module 9       |
   | Network/Access | GCP Network settings, Firewall and IAM            | Secures access to Cloud SQL, Cloud Functions, Cloud Run, and Storage buckets   | Module 4       |


## Data flow narrative
1. Patient uses browser or app to access the intake form
2. Form submission travels through the Internet to GCP
3. Traffic reaches the Flask Web App
4. Flask app stores intake data (JSON) in Cloud SQL, stores uploaded images (JPEG/PNG) in Cloud Storage and sends symptom inputs to the triage function
5. Triage function analyzes patient’s symptoms and returns a triage score (urgent, moderate, routine)
6. Flask sends triage result back to Cloud SQL
7. Staff Dashboard queries Cloud SQL to displays patient info, triage category, waiting status, timestamp
9. Clinicians confirms or modify triage assessment
10. Patient status of appointment is updated by staff

## Security, identity, and governance basics

Security and governance are implemented to ensure HIPPA-aligned practices, such as protecting credentials, enforcing role-based access, and preventing any exposure of PHI in non-secure environments. All application credentials, such as database passwords, service account keys, and API tokens, are stored in GCP Secret Manager. Identity and Access Management (IAM) assigns least-privilege roles to Cloud Run, Cloud SQL, and Cloud Functions through service accounts to ensure each component can only access the resources it needs. The staff dashboard is restricted to authenticated clinic personnel, with role-based read/write permissions controlling who can view, edit, or update patient and triage data. Network security is enforced through a private VPC and firewall rules that block public access to Cloud SQL and other internal services, preventing it from being leaked into the public. Inbound and outbound traffic is restricted to essential services, and all communication between clients, APIs, and backend services is encrypted using HTTPS. Cloud AUdit Logs will track system activity and Cloud Monitoring will provide performance tracking and error alerts. These combined controls ensure that only authorized users access patient information and that protected data remains isolated, encrypted, and compliant with HIPAA requirements.

## Cost and operational considerations
From a cost perspective, the architecture uses serverless and managed services to reduce ongoing expenses. Cloud Run and Cloud Functions scale to zero when not in use, making them cost-effective for intermittent clinical traffic. Cloud Storage provides low-cost storage for uploaded images, while Cloud SQL is the largest cost component, using a small instance type keeps it within a student budget. Analytics workloads are lightweight and require minimal compute resources. Operationally, the architecture requires little maintenance, with automatic scaling, managed security, and built-in monitoring features. These all make the solution efficient, affordable, and suitable for real clinical environments handling digital intake and triage.