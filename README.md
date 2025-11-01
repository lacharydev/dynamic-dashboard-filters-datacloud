# Dynamic Dashboard Filters in CRM Analytics + Data Cloud
Secure, personalized dashboards using Interaction (Binding) filters.

## Overview
This repo accompanies my LinkedIn article:
[Dynamic Dashboard Filters in CRM Analytics + Data Cloud](<add-your-linkedin-post-url>)

It demonstrates how to filter Data Cloud direct queries by the logged-in user.

## Prerequisites
- Salesforce org with CRM Analytics + Data Cloud enabled
- Access to Opportunity, Account, and User DMOs
- Permissions to create dashboards in Analytics Studio

## Steps
1. **Create “Logged_In_User” query**
   ```sql
   SELECT Id, Name, Country
   FROM User
   WHERE Id = '!{User.Id}'
   LIMIT 1

2. **Create Data Cloud Query**
- Choose Opportunity DMO, join Account and User.
- Add filter on User Id.

3. **Add Interaction**
- Open Advanced Interaction Editor.
- Replace filter value with:
```javascript
cell(Logged_In_User.result, 0, "Id").asString()
```
4. **Optional Country filter**
```javascript
cell(Logged_In_User.result, 0, "Country").asString()
```
## Demo Assets
- **dashboard/dynamic_dashboard.json** – ready-to-import dashboard
- **data/** – small sample CSVs for testing
- **images/** – architecture diagram + demo GIF

## Expected Result
Each user who opens the dashboard automatically sees only their own opportunities, derived from Data Cloud DMOs in real time.

## Next Steps
- Extend this to regional filters or role hierarchies.
- Integrate with Data Spaces for native row-level security when available.
- Fork and share your own use case variants!
