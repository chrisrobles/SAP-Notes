# Business Technology Platform

> SAP Business Technology Platform (BTP) is used to manage SAP cloud applications by managing accounts, users, instances, and more.

[Trial Account Tutorial](https://developers.sap.com/tutorials/hcp-create-trial-account.html)

[Documentation](https://help.sap.com/docs/btp)

## Accounts

### Global Account

> Manages entitlements and quotas by distributing to directories and subaccounts. Also manages services and spaces.`

> Entitlements define **what** your're allowed to use (i.e. what services and service plans)

> Quotas quantify **how much** you're allowed to use (i.e. how much of a service plan)

Entitlements and quotas can be freed up and reallocated to other subaccounts

**Give Entitlements**:
1. Entitlements > Entity Assignments
2. Choose subaccount(s)
3. Click `Edit` or `Configure Entitlements` above subaccount
4. Change quotas / Add or remove service plans
5. Click `Save`

### Subaccount 

> Smaller part of your global account

Consumes entitlements

### Directories

[Documentation](https://help.sap.com/docs/btp/sap-business-technology-platform/account-model#loioa92721fc75524ec09a7a7255997dbd94)

> Like a folder, groups subaccounts and directories to create a hierarchy

## Services | Instances

Services / Instances are the Entitlements

Each service has one or more service plans available

### Service plans

Service plans are distributed to subaccounts

Service plans are the quotas

> A service plan shows the costs and features for a specific variant of the service

Each service plan has a quota that the subaccount isnt allowed to go over
- Numeric quota: service plan is measured in units that is defined by the service
- "Limited" quota: service plan entitled to subaccount without having ot worry about how much ofi it to distribute

### Spaces
