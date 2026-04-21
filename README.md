# AI Resume Screening Automation (n8n)

An end-to-end **n8n workflow** designed to automate resume intake, validation, evaluation, and candidate routing. This system leverages **AI-driven decision-making** to shortlist candidates efficiently and reduce manual recruitment effort.

---

## 🚀 Overview

This workflow acts as an automated **Resume Screening Engine**. It processes candidate applications from submission to final decision, ensuring only qualified candidates are shortlisted for further action.

The solution demonstrates:

* Workflow orchestration
* AI integration in business processes
* Data validation and error handling
* Real-world recruitment automation

---

## ✨ Key Features

* **Multi-Stage Validation**: Validates email format and resume availability before processing
* **Duplicate Detection**: Prevents re-processing using PostgreSQL lookup
* **Resume Management**: Uploads resumes to Google Drive and stores `webViewLink` in database
* **AI-Based Evaluation**: Uses LLM to generate score, decision, and justification
* **Structured Decision Logic**: Categorizes candidates into Shortlist / Reject / Review
* **Database Integration**: Inserts and updates candidate lifecycle status
* **Automated Notifications**:

  * Shortlist → Email + Slack
  * Reject → Email
  * Review → Manual queue
* **Error Handling**: Captures failed records and ensures controlled execution

---

## 📋 Workflow Logic

1. **Trigger**: Candidate form submission (Name, Email, Resume)
2. **Validation**: Email and resume validation
3. **Duplicate Check**: PostgreSQL lookup
4. **Resume Handling**:

   * Upload to Google Drive
   * Capture `webViewLink`
   * Download and extract text
5. **Processing**:

   * Extract job description
   * Prepare input for AI
6. **AI Evaluation**:

   * Generate score
   * Provide decision (Shortlist / Reject / Review)
   * Output structured JSON
7. **Database Operations**:

   * Insert candidate (Processing)
   * Update candidate (Post evaluation)
8. **Decision Routing**:

   * Shortlist → Notifications
   * Reject → Email
   * Review → Manual action
9. **Error Handling**:

   * Failed data stored separately

---

## 🔄 Workflow Diagram


```mermaid

A[Form Submission] --> B[Validate Input]

B -->|Invalid| Z[Mark as Invalid]

B -->|Valid| C[Check Duplicate (DB)]
C -->|Duplicate| Y[Stop Processing]

C -->|New| D[Upload Resume to Drive]
D --> E[Capture webViewLink]

E --> F[Download Resume]
F --> G[Extract Resume Text]

G --> H[Process Job Description]
H --> I[AI Resume Evaluation]

I --> J[Insert Candidate (Processing - DB)]
J --> K[Update Candidate (Processed - DB)]

K --> L{Decision}

L -->|Shortlist| M[Send Email + Slack]
L -->|Reject| N[Send Rejection Email]
L -->|Review| O[Manual Review Queue]

B -->|Error| X[Error Handling]
C -->|Error| X
D -->|Error| X
I -->|Error| X

X --> W[Store Failed Candidate]

```

---

## 🛠️ Tech Stack

* **Automation**: n8n
* **Database**: PostgreSQL
* **Storage**: Google Drive
* **AI/LLM**: OpenAI API
* **Notifications**: Slack, Email (SMTP)
* **Processing**: Resume text extraction

---

## 📈 Business Impact

* Reduces manual resume screening effort by **60–70%**
* Improves consistency in candidate evaluation
* Accelerates shortlisting process
* Provides centralized and traceable candidate data
* Enhances recruiter productivity

---

## 🚀 Future Enhancements

* Role-based job description selection
* Advanced scoring model (skills and experience weighting)
* Integration with enterprise HR systems (e.g., SAP SuccessFactors)
* Analytics dashboard (Power BI)
* Candidate ranking and comparison engine
* Automated interview scheduling
* Feedback loop for continuous AI improvement

---

## ⚠️ Error Handling

* Handles invalid input data (email/resume)
* Prevents duplicate processing
* Captures failed executions using error branches
* Ensures data consistency in database updates

---

## ⚙️ Setup Instructions

### 1. Import Workflow

* Import the workflow JSON into n8n

### 2. Configure Credentials

* Google Drive
* PostgreSQL
* OpenAI API
* Slack (optional)
* Email SMTP

### 3. Database Setup

Create table with fields:

* name
* email
* resume_link
* status
* score


---

## 📸 Visualizing the Output

### 1. Workflow Execution

<img width="940" height="471" alt="image" src="https://github.com/user-attachments/assets/27bbd2df-a232-479d-8518-030c35e58fed" />


### 2.File Management

* Resumes are uploaded to Google Drive to facilitate downstream processing

<img width="1530" height="172" alt="image" src="https://github.com/user-attachments/assets/c5594d3e-cf4a-49f8-af46-9f1f42955733" />


### 3. Database Records

* Stores candidate lifecycle with status updates

  <img width="1781" height="382" alt="image" src="https://github.com/user-attachments/assets/24fb5550-505b-4686-9f57-b4ad1522ef71" />


  

###  4. Notifications

* Slack alerts(Hiring Team) for shortlisted candidates
  

  <img width="1393" height="351" alt="image" src="https://github.com/user-attachments/assets/faad1e07-d343-47a5-9194-c5068494fdf9" />



* Email communication for candidates

<img width="1836" height="765" alt="image" src="https://github.com/user-attachments/assets/aaec8959-fc91-4349-b1a2-12dfeb9e2b7d" />



---

## 📌 Conclusion

This project showcases a practical implementation of **AI-driven recruitment automation**, combining workflow orchestration, data processing, and intelligent decision-making into a scalable solution suitable for enterprise use cases.

