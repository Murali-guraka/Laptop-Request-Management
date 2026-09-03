# Laptop Request Management – ServiceNow

## 1. Project Overview

Laptop Request Management is a ServiceNow scoped application designed to manage employee laptop requests in an organization.

The application allows employees to submit laptop requests, routes requests to managers for approval, prevents duplicate requests, and provides role-based access to employees and IT managers.

The project demonstrates the use of ServiceNow application development, tables, fields, Record Producers, Service Catalog, ACLs, Business Rules, Flow Designer, approval workflows, and Update Sets.

---

## 2. Application Details

**Application Name:** Project Application

**Application Purpose:** Laptop Request Management

**Application Type:** ServiceNow Scoped Application

**Main Table:** Laptop Request Form

The application is designed to provide a controlled and automated process for requesting and approving laptops.

---

## 3. Main Features

The application provides the following features:

- Employee laptop request submission
- Laptop request form
- Employee and manager information
- Laptop type selection
- Request status tracking
- Manager approval workflow
- Duplicate request prevention
- Role-based access control
- ACL-based security
- Record Producer
- Service Catalog integration
- Flow Designer automation
- Approval tracking
- Email notifications
- Update Set deployment
- XML export for application migration

---

## 4. Laptop Request Form

The main table used by the application is:

**Laptop Request Form**

Important fields include:

| Field | Description |
|---|---|
| Number | Unique request number |
| Requester | Employee submitting the request |
| Employee Email | Employee email address |
| Date | Request date |
| Short Description | Brief description of the request |
| Manager | Employee's manager |
| Type of Laptop | Requested laptop type |
| Status | Current request status |
| Reason | Reason for requesting the laptop |

---

## 5. Request Workflow

The laptop request follows this process:

```text
Employee
   |
   v
Submit Laptop Request
   |
   v
Validate Request
   |
   v
Check Duplicate Request
   |
   +---- Duplicate Found ----> Reject / Stop Request
   |
   v
Send Request for Manager Approval
   |
   +---- Rejected ----> Update Status + Email
   |
   v
Approved
   |
   v
Update Request Status
   |
   v
Send Notification
```
## 6. Roles

Two custom roles were created for the application.

### IT Employee

**Role:** `x_1959161_projec_0.it_employee`

Purpose:

- Create laptop requests
- Manage laptop requests
- Access employee-related request functionality

### IT Manager

**Role:** `x_1959161_projec_0.it_manager`

Purpose:

- View laptop requests
- Review requests
- Approve or reject requests

---

## 7. Groups

The application uses groups to organize users according to their responsibilities.

### IT Employees

The IT Employees group is used for users who create and manage laptop requests.

The group is associated with the `it_employee` role.

### IT Managers

The IT Managers group is used for users who review and approve laptop requests.

The group is associated with the `it_manager` role.

---

## 8. Access Control Lists

ACLs were implemented to control access to the Laptop Request Form table.

### Employee Create ACL

**Operation:** Create

**Role:** `x_1959161_projec_0.it_employee`

This allows authorized IT employees to create laptop requests.

### Manager Read ACL

**Operation:** Read

**Role:** `x_1959161_projec_0.it_manager`

This allows IT managers to view laptop requests.

ACLs were tested to verify that access is controlled according to user roles.

---

## 9. Business Rule

### Laptop Request BR

A Business Rule was created on the Laptop Request Form table to prevent duplicate laptop requests from the same employee in the same year.

If an employee has already submitted a laptop request during the current year, another request is blocked.

The user receives the following message:

> You have already submitted a laptop request this year.

The Business Rule uses:

`setAbortAction(true)`

to stop the duplicate request from being inserted.

This improves data quality and prevents unnecessary duplicate requests.

---

## 10. Approval Relationship

An approval relationship was configured between the Laptop Request Form table and the Approval table.

**Relationship Name:** Laptop request

**Applies to:** Laptop Request Form

**Queries from:** Approval `[sysapproval_approver]`

The relationship allows approval records associated with a laptop request to be displayed and tracked.

The approval record contains information such as:

- Approver
- Approval state
- Related laptop request
- Approval reason

---

## 11. Record Producer

A Record Producer named **Laptop Request** was created for the **Laptop Request Form** table.

The Record Producer provides a simple interface for employees to submit laptop requests.

When an employee submits the form, a corresponding record is created in the Laptop Request Form table.

---

## 12. Service Catalog

A Service Catalog item named **Employee Service Catalog** was configured under:

**Category:** Services

**Catalog:** Service Catalog

The catalog provides employees with a convenient way to access the laptop request service.

The Service Catalog integrates the request process into the employee service experience.

---

## 13. Flow Designer

Flow Designer was used to automate the laptop request process.

### Flow 1 – Laptop Request Manager Approval

The flow is triggered when a Laptop Request Form record is created.

The manager specified in the request is added as the approver.

The manager can:

- Approve the request
- Reject the request

### Flow 2 – Laptop Request Approval and Execution

This flow handles the complete request process.

The flow:

1. Triggers when a laptop request is created.
2. Checks for duplicate requests.
3. Handles duplicate requests.
4. Updates the request record.
5. Sends the request for approval.
6. Handles approved requests.
7. Handles rejected requests.
8. Updates the request status.
9. Sends email notifications.

Flow Designer reduces manual processing and provides an automated approval workflow.

---

## 14. Approval Process

When an employee submits a valid laptop request:

1. The request is created.
2. The manager receives an approval request.
3. The approval state becomes **Requested**.
4. The manager reviews the request.
5. The manager approves or rejects the request.
6. The approval record is updated.
7. The main request record is updated.
8. Email notifications are sent.

Example approval states include:

- Requested
- Approved
- Rejected

---

## 15. Duplicate Request Handling

The application prevents employees from submitting multiple laptop requests within the same year.

The process is:

```text
First Request
     |
     v
Request Accepted
     |
     v
Employee submits another request
     |
     v
Business Rule checks existing request
     |
     v
Duplicate Found
     |
     v
Request Blocked
```
## 16. Update Set and Deployment

The completed application configuration was published to a ServiceNow Update Set.

The Update Set contains application configuration changes, including:

- Custom application
- Tables and fields
- Record Producer
- Business Rules
- ACLs
- Roles
- Flow Designer configuration
- Approval configuration
- Service Catalog configuration

The Update Set was:

1. Published
2. Scanned
3. Verified successfully
4. Exported as XML

The exported XML file is available in the `update-set/` folder of this repository.

The XML can be used to transfer the application configuration to another ServiceNow instance.

---

## 17. Testing

The application was tested for the following scenarios.

### Employee Access

- Employee can create a laptop request.
- Employee access is controlled through the IT Employee role.

### Manager Access

- Manager can view laptop requests.
- Manager can review requests.
- Manager can approve or reject requests.

### Duplicate Request

- First request is accepted.
- Duplicate request in the same year is blocked.
- The appropriate error message is displayed.

### Approval

- Manager receives an approval request.
- Approval state initially becomes **Requested**.
- Approval state changes after manager action.
- The request workflow continues according to the approval result.

### Security

- ACLs were tested for required operations.
- Role-based access was verified.

---

## 18. Project Structure

```text
Laptop-Request-Management/
│
├── README.md
│
├── update-set/
│   └── ServiceNow Update Set XML
│
├── screenshots/
│   ├── Project-application.png
│   ├── laptop-request-form.png
│   ├── employee-request.png
│   ├── it-employee-role.png
│   ├── it-manager-role.png
│   ├── acl-create-employee.png
│   ├── acl-read-manager.png
│   ├── approval-relationship.png
│   ├── business-rule-duplicate-request.png
│   ├── duplicate-request-blocked.png
│   ├── record-producer.png
│   ├── employee-service-catalog.png
│   ├── manager-approval.png
│   ├── approval-result.png
│   └── flow-designer.png
│
└── docs/
    └── project-documentation.md
```
## 19. Technologies Used

The following ServiceNow technologies and features were used:

- ServiceNow
- Scoped Applications
- Custom Tables
- Custom Fields
- Flow Designer
- Service Catalog
- Record Producer
- ACLs
- Roles
- Groups
- Business Rules
- Approval Workflows
- Email Notifications
- Update Sets
- XML

---

## 20. Project Outcome

The Laptop Request Management application provides a structured and secure solution for managing employee laptop requests.

The project demonstrates how ServiceNow can be used to automate business processes while maintaining security through roles and ACLs.

The application integrates:

- Request creation
- Duplicate validation
- Manager approval
- Workflow automation
- Email notifications
- Role-based security
- Service Catalog
- Update Set deployment

The result is a centralized and automated laptop request management process.

---

## 21. Future Enhancements

The application can be further enhanced by adding:

- IT inventory integration
- Automatic laptop assignment
- SLA tracking
- Request dashboards
- Reports and analytics
- Multi-level approval
- Automated approval reminders
- Laptop availability checking
- Asset Management integration
- Automated request status tracking

These enhancements could further improve automation, reporting, and overall user experience.

---

## 22. Conclusion

The Laptop Request Management project demonstrates the development of a complete ServiceNow scoped application for managing employee laptop requests.

The application provides employees with an easy way to submit laptop requests while allowing managers to review and approve requests through an automated workflow.

The implementation of Business Rules, ACLs, roles, groups, Record Producers, Service Catalog, Flow Designer, approval relationships, and Update Sets makes the application secure, automated, and deployable.

Overall, the project demonstrates practical knowledge of ServiceNow application development, workflow automation, security, approval management, and application deployment.
```
