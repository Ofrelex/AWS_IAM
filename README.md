# Introduction to Cloud Computing – Security &amp; Identity Management (IAM) for "Zappy e-Bank"
#
## Phase 1: Foundation – Understanding the Basics
### Step 1: Review Cloud Computing & AWS Basics
* Understand the core benefits of cloud computing: scalability, elasticity, pay-as-you-go, global reach.
* Review AWS services broadly (compute, storage, networking, databases).
* Read up on AWS Identity and Access Management (IAM) [via AWS Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html).
#
## Phase 2: Project Setup for Zappy e-Bank
### Step 2: Sign in to AWS
* Visit: [https://aws.amazon.com/](https://aws.amazon.com/)
* Log in using your “root or admin user” credentials.
#
### Step 3: Navigate to the IAM Dashboard
* Go to **Services > Security, Identity, & Compliance > IAM.
* You’ll land on the IAM “Dashboard”.
#
## Phase 3: IAM Core Implementation for Zappy e-Bank
### Step 4: Create IAM Groups
Zappy e-Bank departments may include:
* Developers
* Finance
* Operations
* Security/Admins
#
### To create groups:
1. In IAM Dashboard > Groups > Create New Group
2. Name it (e.g., `Zappy-Developers`)
3. Skip policy attachment for now (will attach custom later)
4. Repeat for other groups
#
### Step 5: Create IAM Users and Assign Them to Groups
### Create users like:
* `alice.dev@zappy.com` (Developer)
* `bob.finance@zappy.com` (Finance)
* `carol.ops@zappy.com` (Operations)
* `dave.admin@zappy.com` (Admin/Security)
#
### To create users:
1. IAM > Users > Add users
2. Enter username (e.g., `alice.dev`)
3. Enable “programmatic access” and/or “Console access”
4. Set a custom password and enforce password reset
5. Assign user to the appropriate group (e.g., `Zappy-Developers`)
#
### Step 6: Create and Attach IAM Policies
Now define what each group/user can do.
Example custom policy for Developers:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:*",
        "s3:*"
      ],
      "Resource": "*"
    }
  ]
}
```
#
### To create custom policies:
1. IAM > Policies > Create policy
2. Use “JSON editor” to paste policy
3. Review and name (e.g., `Zappy-Dev-FullAccess`)
4. Attach the policy to the appropriate group
Repeat for other departments:
* Finance: S3 (read-only), billing permissions
* Ops: EC2 & CloudWatch access
* Admins: Full access (use AWS managed `AdministratorAccess` policy)
#
### Step 7: Enable Multi-Factor Authentication (MFA)
Enhance user security with MFA:
1. IAM > Users
2. Click on user > Security credentials
3. Set up “MFA” using “virtual MFA device” (Google Authenticator or Authy)
4. Scan QR code and enter codes to complete setup
#
## Phase 4: Role-Based Access and Cross-Service Permissions
### Step 8: Create IAM Roles for Services
Example: Allow EC2 instance to access S3
1. IAM > Roles > Create role
2. Choose AWS Service > EC2
3. Attach a policy like `AmazonS3ReadOnlyAccess`
4. Name the role (e.g., `EC2-S3Access`)
5. Launch or attach role to EC2 instances via EC2 console
#
### Step 9: Implement Temporary Access via IAM Roles
* Create a role for “external auditors” or “temporary consultants”
* Use “Trust relationships” in role policy to allow only specific AWS accounts to assume the role
* Use “STS (Security Token Service)” to manage session duration
#
## Phase 5: Secure Access Management & Monitoring
### Step 10: Apply Password Policy
Set secure password requirements:
1. IAM > Account Settings
2. Edit Password policy:
   * Require at least one upper/lowercase, symbol, number
   * Minimum length: 12 characters
   * Enable password expiration & reuse prevention
#
### Step 11: Monitor IAM Activities
1. Enable “AWS CloudTrail” to track all IAM and AWS account activities
2. Review “IAM Access Analyzer” for over-permissive policies
3. Set up “CloudWatch Alarms” for suspicious login attempts or failed authentication
#
## Phase 6: Final Documentation & Review
### Step 12: Document IAM Strategy for Zappy e-Bank
Include:
* Group structure and rationale
* Policies created and attached
* MFA configurations
* Roles and temporary access mechanisms
* Security monitoring setup
#
### Step 13: Perform an IAM Review
* Verify least privilege principles are applied
* Remove unused users and roles
* Rotate access keys and passwords regularly
#
## Learning Outcomes Recap
By completing this project, you have:
* Practically managed users, groups, roles, and permissions in AWS IAM
* Designed a secure IAM framework tailored for a fintech company
* Applied strong security practices such as MFA and least privilege
* Understood how IAM contributes to compliance and data protection.