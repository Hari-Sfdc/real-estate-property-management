# 🏢 Real Estate Property Management System (Salesforce)

## 📌 Project Overview
A Salesforce-based Real Estate Property Management System designed to manage properties, tenants, lease agreements, vendors, and maintenance requests with automation, reporting, and scalability in mind.

This application demonstrates real-world Salesforce best practices including:
- Scalable data model
- Server-side pagination
- Declarative and programmatic automation
- Bulk-safe Apex
- Test-driven development
- Dashboard-driven insights

---

## 🧩 Features Implemented (Progressive)
- [x] Property Management (Core)
- [ ] Tenant Management
- [ ] Lease Agreement Management
- [ ] Vendor Management
- [ ] Maintenance Request Automation
- [ ] Reporting & Dashboards
- [ ] Security & Access Control
- [ ] Unit Testing (80%+ Coverage)

---

## 🗂️ Data Model Overview
(Will be updated as objects are added)

---

## 🏠 Property Management

### 📌 Objective
Manage real estate properties with complete details, enforce mandatory data, and prepare the foundation for leasing, maintenance, and reporting.

---

### 🧱 Object: Property__c

The `Property__c` object represents a real estate unit (Residential or Commercial).

#### 🔹 Key Fields

| Field Label | API Name | Type | Mandatory |
|------------|---------|------|-----------|
| Property Name | Name | Text | ✅ |
| Address | Address__c | Text Area | ✅ |
| City | City__c | Text | ✅ |
| State | State__c | Text | ✅ |
| Postal Code | Postal_Code__c | Text | ✅ |
| Country | Country__c | Picklist | ✅ |
| Type | Type__c | Picklist (Residential / Commercial) | ✅ |
| Furnishing Status | Furnishing_Status__c | Picklist | ❌ |
| Status | Status__c | Picklist (Available / Occupied) | ✅ |
| Rent | Rent__c | Currency | ✅ |
| Description | Description__c | Long Text Area | ✅ |

---

### 🖼 Property Images

- Property images are managed using **Salesforce Files**
- Multiple images can be uploaded per property
- Attachments are not used (deprecated)

#### 🔒 Validation Rule
A validation rule ensures that **a property cannot be created without at least one image**.

**Rule Logic:**
- Triggered only during record creation
- Uses `HASRELATEDRECORD(ContentDocumentLink)`

**User Message:**
> “Please upload at least one image before saving the Property.”

---

### 🧠 Design Considerations & Best Practices

- Files are used instead of attachments for scalability and preview support
- Picklists are used for status and type to support filtering and reporting
- Validation is enforced at the database level to prevent bad data
- Object is activity-enabled to support tasks and follow-ups

---

### ✅ Current Status
- Property object created
- Mandatory fields enforced
- Image upload enforced
- Page layout optimized

## 🧑 Tenant Management

### 📌 Objective
Manage tenants and associate them with one or more properties using a scalable data model.

---

### 🧱 Object: Tenant__c

Represents a tenant renting one or more properties.

#### Fields
- Tenant Name (Text, Required)
- Phone Number (Phone)
- Email (Email)

---

### 🔗 Many-to-Many Relationship

To support tenants renting multiple properties, a junction object `Property_Tenant__c` is used.

#### Object: Property_Tenant__c
- Property (Lookup → Property__c)
- Tenant (Lookup → Tenant__c)

Both lookups are mandatory, ensuring valid assignments.

---

### 🧠 Design Rationale
- Junction object enables scalability
- Avoids data duplication
- Supports future enhancements like rent sharing and occupancy tracking

### 📄 Property-Tenant Assignment

The `Property_Tenant__c` object represents the occupancy relationship between a tenant and a property.

#### Key Fields
- Tenant Role (Primary / Co-Tenant)
- Occupancy Status (Active / Vacated)
- Move-in Date
- Move-out Date

This design allows tracking of current and historical occupancies without data duplication.

## 📄 Lease Agreement Management
(To be implemented)

---

## 🛠 Vendor & Maintenance Management
(To be implemented)

---

## 📊 Reports & Dashboards
(To be implemented)

---

## ⚙️ Technical Architecture
(To be updated)

---

## 🧪 Testing Strategy
(To be updated)

---

## 🚀 Deployment & Setup
(To be updated)

---

## 📁 Version Control
- All changes are tracked using Git
- Feature-based commits
