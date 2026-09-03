# Laptop Request Management – ServiceNow

## Project Overview

Laptop Request Management is a custom ServiceNow scoped application designed to manage employee laptop requests through an automated request and approval lifecycle.

The application demonstrates ServiceNow application development, role-based security, backend validation, workflow automation, manager approvals, email notifications, Service Catalog integration, and Update Set deployment.

## Application

- **Application:** Project Application
- **Type:** Scoped Application
- **Version:** 1.0.0
- **Platform:** ServiceNow

## Key Features

- Employee laptop request form
- Employee and IT Manager roles
- Role-based access control using ACLs
- Manager approval workflow
- Approval relationship with `sysapproval_approver`
- Duplicate request validation
- Business Rule enforcement
- Record Producer
- Employee Service Catalog
- Flow Designer automation
- Approval and rejection handling
- Email notifications
- Update Set based deployment

## Request Workflow

```text
Employee submits Laptop Request
             ↓
     Duplicate Request Check
             ↓
       Request Validation
             ↓
       Manager Approval
          ↙       ↘
     Approved     Rejected
```
## Screenshots

### 1. Project Application
![Project Application](Project-application.png)

### 2. Laptop Request Form
![Laptop Request Form](laptop-request-form.png)

### 3. Employee Request
![Employee Request](employee-request.png)

### 4. Employee Role
![Employee Role](it-employee-role.png)

### 5. Manager Role
![Manager Role](it-manager-role.png)

### 6. ACL - Employee Create Access
![ACL Create Employee](acl-create-employee.png)

### 7. ACL - Manager Read Access
![ACL Read Manager](acl-read-manager.png)

### 8. Approval Relationship
![Approval Relationship](approval-relationship.png)

### 9. Business Rule - Duplicate Request
![Business Rule](business-rule-duplicate-request.png)

### 10. Duplicate Request Blocked
![Duplicate Request Blocked](duplicate-request-blocked.png)

### 11. Record Producer
![Record Producer](record-producer.png)

### 12. Employee Service Catalog
![Employee Service Catalog](employee-service-catalog.png)

### 13. Manager Approval
![Manager Approval](manager-approval.png)

### 14. Approval Result
![Approval Result](approval-result.png)

### 15. Flow Designer
![Flow Designer](flow-designer.png)
        ↓            ↓
   Update Status  Update Status
        ↓            ↓
   Email Notice   Email Notice
