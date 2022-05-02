# User Roles

### **Roles** refer to _different kinds of users_ who can do different things (i.e. have specific "permissions")

## Primary Roles

### **Staff** can:

* create accounts for other **Staff**, **Reviewers**, and **Applicants** (rare)
* deactivate other user accounts
* modify roles for other users
* set up applications (this means creating Forms, Funds, and Rounds&#x20;
* see applications/submissions
* give other users (e.g. Reviewers or other Staff) access to applications/submissions
* review applications/submissions
* process determinations/decisions (_if they have **Approver** role_)
* communicate with Applicants
* disburse funds(?)

> ℹ️ _Account created during deployment_

### A **Reviewer** can:

* look at the application(s) to which they have been assigned
* complete Review Forms for application(s)
* communicate with applicants (?)

> ℹ️ _Account created by **Staff** & assigned to either "Fund" or specific application(s)_

### An **Applicant** can:

* create, edit, and submit own applications
* contact fund staff regarding own application
* submit invoice/request for fund dispersal

> ℹ️ _Account created automatically when user applies to specific fund/round_

### **Finance** (under development) can:

* access projects, invoices, & reports
* _additional capabilities to be added_

> ℹ️ _Account created by **Staff**_

***

## Secondary Roles

### **Partner**:

* Can see, edit, and communicate about a specific application
* Used when two or more people are working together on an application; one applicant gets **Applicant** role, and additional applicants get this role

> ℹ️ _This role is created by Staff and associated with a specific application_

### **Approver**

* If assigned with **Staff** role, can approve applications
* If assigned with **Finance** role, can approve invoices/contracts

> ℹ️ _This role is an add-on that allows users additional capabilities_

## Additional Roles

### New roles can be created and permissions (capabilities) for these roles can be set in Wagtail by the person deploying Hypha for your organization.



_For example, current Hypha whitelabel includes the following roles, which were created for different Hypha adopters:_

* **Community Reviewer**
* **Team Admin**
