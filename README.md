# 📊 Organization Database Schema

This document provides an overview of the relational database schema designed for managing various aspects of an organization, including departments, employees, projects, policies, teams, events, and associated resources.

---

## 🧱 Entity Overview

### 🔹 Department
- **Fields:** ID, Name, Description, Budget, LeadedID, ChannelID
- **Relationships:**
  - Has many **Projects**, **Policies**, and **Teams**
  - Uses **Channels**

---

### 🔹 Employee
- **Fields:** ID, Name, DateOfBirth, Gender, Address (Street, City, Pincode), Email (Work, Personal), Availability, FeedbackID, ContactInfo, LeadBy, ReportsTo
- **Relationships:**
  - Works on multiple **Projects**
  - Gives and receives **Feedback**
  - Has one **Resume**
  - Leads and Contacts other employees

---

### 🔹 Project
- **Fields:** ID, Name, StartDate, DueDate, Status, Budget, Objective, DepartmentID
- **Relationships:**
  - Tracked by **Employees**
  - Includes **Feedback**
  - Troubleshoots using **Resources**

---

### 🔹 Feedback
- **Fields:** ID, Title, Description, Tags
- **Relationships:** Linked to **Employees** and **Projects**

---

### 🔹 Team
- **Fields:** ID, AreaOfWorking, PointOfContactID, Email, LeadedID, ChannelID, DepartmentID
- **Relationships:**
  - Belongs to a **Department**
  - Uses **Channels**
  - Involves **Employees**

---

### 🔹 Channel
- **Fields:** ID, Type, CreatedAt, ProjectID
- **Relationships:**
  - Communicates with **Teams**
  - Used by **Departments**

---

### 🔹 Policy
- **Fields:** ID, Title, Description, EffectiveDate, EndDate, RevisionDate, ApprovalStatus, Documents, DepartmentID
- **Relationships:** Belongs to a **Department**

---

### 🔹 Event
- **Fields:** ID, Name, Date, Time, Location (Address, City, PIN), Link, Agenda, Recurrence
- **Relationships:** Accessible by **Teams**, may be **Internal** or **External**

#### Event Subtypes:
- **Conference**
  - Fields: Description
- **Product Launch**
  - Fields: Launch Date, Related Product(s)

---

### 🔹 Resource
- **Composite Primary Key:** ID, ProjectID
- **Fields:** Name
- **Relationships:**
  - Categorized into:
    - **Software** (Size)
    - **PDF** (Pages)
    - **Code** (Language, Description, Comments)
    - **GitHubRepo** (Repo File)
  - Troubleshoots **Projects**

---

### 🔹 Reference
- **Fields:** ID, Name, Description, Category, Author, Keywords, Link, Related
- **Purpose:** General linking entity for documentation or citations

---

### 🔹 Resume
- **Fields:** EmployeeID, EducationHistory, WorkExperience, Skills
- **Relationships:** One-to-one with **Employee**

---

### 🔹 Invoice
- **Fields:** ID, EmployeeID, Status, DueDate, Timestamp (auto), PaymentMethod, Notes
- **Relationships:** Issued for an **Employee**

---

## 🔁 Key Relationships Summary

- 🔄 One-to-many:
  - Department → Projects, Teams, Policies
  - Project → Feedback
- 🔁 Many-to-many:
  - Employee ↔ Projects (via tracking)
- 🔗 One-to-one:
  - Employee → Resume
- 🧩 Composite relationships:
  - Resource → Project (via composite PK)

---

## 💡 Use Cases

This schema supports:
- Department and team organization
- Employee assignments and hierarchy
- Resource/document management
- Project tracking and feedback loops
- Policy and event communication
- Invoice generation and HR processes

---

## ✅ Future Improvements

- Add audit fields (`created_at`, `updated_at`)
- Normalize address and contact structures
- Define role-based access controls
- API-ready endpoints per entity (REST or GraphQL)

---
