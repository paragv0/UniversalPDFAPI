# Serverless PDF Generator (AWS Lambda + SQS)

A cloud-native, asynchronous microservice that generates PDF documents on demand. Built using Python, AWS Lambda, and Event-Driven Architecture.

# Live Demo
**Base URL:** `https://xfno7odld6hxji7kchsbpqo7za0jqtix.lambda-url.us-east-1.on.aws`
**Interactive Docs:** [Click here to try the API](https://xfno7odld6hxji7kchsbpqo7za0jqtix.lambda-url.us-east-1.on.aws/docs)

---

# Architecture
This system uses a **decoupled, event-driven architecture** to handle high loads without crashing.



* **Frontend/Client:** Sends JSON request via HTTP POST.
* **API Gateway (Lambda URL):** Acts as the entry point; validates request and pushes a job to the queue.
* **Message Queue (Amazon SQS):** Buffers requests asynchronously, decoupling the API from the heavy processing.
* **Worker (AWS Lambda):** Polls the queue, generates the PDF using `fpdf2`, and uploads to storage.
* **Storage (Amazon S3):** Stores the generated PDFs with a **1-day lifecycle policy** for automatic cleanup.

*(Add a screenshot of your AWS Diagram here)*
<img width="4335" height="1293" alt="image" src="https://github.com/user-attachments/assets/f0233552-8190-406d-befb-9d36a85efa04" />


# API Usage

### 1. Submit a Job
**POST** `/generate-pdf`
```json
{
  "client_id": "PortfolioDemo",
  "template_type": "invoice",
  "data": { "Item": "Cloud Service", "Cost": "Free Tier" }
}
```

### 2. Check Status
**GET** `/download/{job_id}` Returns a secure, pre-signed S3 download link when ready.



# Technologies Used
* **Compute:** AWS Lambda (Serverless Python)

* **Integration:** Amazon SQS (Simple Queue Service)

* **Storage:** Amazon S3 (Simple Storage Service)

* **Framework:** FastAPI & Mangum

* **Language:** Python 3.13

# Working Page
<img width="2932" height="1070" alt="image" src="https://github.com/user-attachments/assets/6b3dc9a0-ec64-40cb-90fa-8542ef611187" />
