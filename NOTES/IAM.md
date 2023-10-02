# Identity Access Management

---

## GuideLines & Principles

Main

- Grant Least Privilege Access (prohibit all, then allow some)
- Dont use Root Account, except for AWS setup

User Accounts

- One physical user = One AWS user
- Assign user to groups, then put privilege on groups
- Group only contains users not other groups

Behavior & Common Sense

- Use MFA (Multifactor Authentication)
- Enforce strong password usage
- Use Access keys for programmatic access, not user one
- never share IAM & Access Keys

Admin Related

- Audit privilege access by using Access advisor

---

## User, User Groups, and Roles

### User

Entity that is created in AWS
IAM User represents a human or a workload (backend,frontend or any service) that interact with AWS
consists of **name** & **credential**
User with Administrator role is _not the same_ with Root Account

Amazon Resource Name is a unique identifier of user accross all AWS
example:
`arn:aws:iam::account-ID-without-hyphens:user/Richard`

### User Group

A group that contains users

## Policies

is a list of privilege granted, for users or groups
can be stored in JSON format

Policy:
| **Field name** | **Info**                                               |
| -------------- | ------------------------------------------------------ |
| Version        |                                                        |
| Id             | form of UUID, to state an ID for the policy            |
| Statement      | Can be applied as list singular (check component below |

Statement Components:
| **Field name** | **Type**                                      |
| -------------- | --------------------------------------------- |
| Sid            |                                               |
| Princial       | **Only applicable** for Resource-based policy |
| Effect         | `Allow` `Deny`                                |
| Action         |                                               |
| Resource       | **Optional** for Resource-based policy        |
| Condition      | Specify the circumstances of the rules        |

---

## Roles

an Authorization entity
We can add user account to give the role's granted permissions
Used to EC2 instances or AWS Services 

---

### Access Keys
 by using access account & a secret key or CLS using this method

---

## IAM Tools

### Credential Report

report that list all user accounts and their status

### Access Advisor

shows service permission granted of to a user when last accessed
use this to review privilege granted

---