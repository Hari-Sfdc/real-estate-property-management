# 🏢 Real Estate Property Management System (Salesforce)

## 📌 Project Overview

A Salesforce-based **Real Estate Property Management System** designed to manage properties, tenants, lease agreements, vendors, and maintenance requests.

This project is built incrementally with a focus on **real-world Salesforce best practices**, platform limitations, and scalable architecture rather than just feature completion.

Key goals of this project:
- Correct Salesforce data modeling
- Declarative-first automation
- Clear separation of responsibilities between objects
- Honest documentation of what is implemented vs in progress

---

## 🧩 Overall Implementation Status

### ✅ Completed
- Core data model (Property, Tenant, Junction, Lease, Vendor, Maintenance)
- Property creation with **mandatory image upload via Screen Flow**
- Tenant management
- Property–Tenant assignment (junction object)
- Automatic **Task creation** on property assignment

### 🟡 In Progress
- Lease expiry reminder email (Scheduled Flow – logic designed, doubts being resolved)
- Property image enforcement refinements & documentation

### ⏳ Pending
- Maintenance request vendor auto-assignment
- Property list UI (pagination & filters using LWC)
- Reports & Dashboards
- Security & access control
- Apex unit testing (80%+ coverage)

---

## 🗂️ Data Model Status

| Object | Purpose | Status |
|------|--------|--------|
| Property__c | Stores property details | ✅ Done |
| Tenant__c | Stores tenant details | ✅ Done |
| Property_Tenant__c | Junction between Property & Tenant | ✅ Done |
| Lease_Agreement__c | Lease contract management | ✅ Done |
| Vendor__c | Maintenance vendors | ✅ Done |
| Maintenance_Request__c | Property maintenance tracking | ✅ Done (Automation pending) |

---

## 🏠 Property Management

### 📌 Objective
Manage real estate properties and ensure **no property can be created without at least one image**, respecting Salesforce platform constraints.

---

### 🧱 Object: Property__c

Represents a residential or commercial property.

#### Key Fields

| Field | Type | Required |
|-----|------|----------|
| Property Name | Text | ✅ |
| Address | Text Area | ✅ |
| City | Text | ✅ |
| State | Text | ✅ |
| Postal Code | Text | ✅ |
| Country | Picklist | ✅ |
| Type (Residential / Commercial) | Picklist | ✅ |
| Furnishing Status | Picklist | ❌ |
| Status (Available / Occupied) | Picklist | ✅ |
| Rent | Currency | ✅ |
| Description | Long Text Area | ✅ |
| Has_Image__c | Checkbox | System-controlled |

---

### 🖼 Property Image Enforcement (Important)

#### ⚠️ Salesforce Platform Limitation
Salesforce validation rules **cannot validate Files** (`ContentDocumentLink`) because files are saved **after record commit**.

#### ✅ Implemented Solution
- A **Screen Flow** (`Create Property with Image`) is used instead of the standard New button
- Flow sequence:
  1. Capture property details
  2. Create Property record
  3. Force image upload using File Upload component
  4. Update `Has_Image__c = true`

This ensures:
- No property is created without an image
- No unsupported validation logic is used

**Status:** 🟡 Refinements in progress, core enforcement working

---

## 🧑 Tenant Management

### 📌 Objective
Allow tenants to rent **multiple properties** without data duplication.

---

### 🧱 Object: Tenant__c

Fields:
- Tenant Name (Required)
- Phone Number
- Email

**Status:** ✅ Done

---

## 🔗 Property–Tenant Assignment (Junction Object)

### 🧱 Object: Property_Tenant__c

Represents the occupancy relationship.

#### Key Fields
- Property (Lookup → Property__c)
- Tenant (Lookup → Tenant__c)
- Tenant Role (Primary / Co-Tenant)
- Occupancy Status (Active / Vacated)
- Move-in Date
- Move-out Date

**Status:** ✅ Done

---

### ⚙️ Automation: Lease Preparation Task

- When a `Property_Tenant__c` record is created,
- A **Task** is automatically generated to prepare the lease agreement

**Status:** ✅ Working perfectly

---

## 📄 Lease Agreement Management

### 📌 Objective
Manage lease contracts independently from occupancy assignments.

---

### 🧱 Object: Lease_Agreement__c

Fields:
- Lease Number (Auto Number)
- Property (Lookup)
- Tenant (Lookup)
- Terms
- Agreed Monthly Rent
- Start Date
- End Date
- Status (Active / Expired / Terminated)

**Status:** ✅ Data model complete

---

### ⏰ Lease Expiry Reminder Email

- Designed using **Scheduled Flow**
- Runs daily
- Targets leases expiring in 30 days
- Sends reminder email to tenant

**Status:** 🟡 In progress (logic designed, implementation doubts being resolved)

---

## 🛠 Vendor & Maintenance Management

### Vendor__c
Stores vendor details.

**Status:** ✅ Done

---

### Maintenance_Request__c
Tracks maintenance issues.

Fields:
- Property
- Vendor
- Status
- Description

**Status:** 🟡 Automation pending  
(Vendor auto-assignment based on workload to be implemented)

---

## 🧠 Key Design Decisions

- Files enforced via **Screen Flow**, not validation rules
- Junction object used instead of overloading Lease Agreement
- Clear separation of:
  - Occupancy (`Property_Tenant__c`)
  - Contract (`Lease_Agreement__c`)
- Declarative-first approach
- No unsupported Salesforce hacks used

---

## 📁 Version Control

- Git used for version control
- Feature-based commits
- README updated incrementally with actual progress

---

## 🚀 Upcoming Work

- LWC-based Property List
  - Server-side pagination (25 records/page)
  - Filters: Price, Status, Furnishing
- Vendor workload-based assignment (Apex)
- Reports & Dashboards
- Apex unit tests (80%+ coverage)

---

## 📌 Note

This project intentionally documents **what is implemented vs in progress** to reflect real-world Salesforce development practices rather than demo-only implementations.
