# OidcAwsGithub

## Goal
The primary aim of this project is to facilitate secure authentication of GitHub actions within AWS using OIDC (OpenID Connect). This enables seamless integration into various workflows, such as continuous integration, with services like S3 buckets.

## Description

### Context
OIDC federation eliminates the need for custom sign-in code or managing user identities separately. Instead, it leverages OIDC-compatible Identity Providers (IdPs), such as GitHub Actions, to authenticate with AWS. Users receive a JSON Web Token (JWT) upon authentication, which is then exchanged for temporary security credentials within AWS. These credentials are associated with an IAM role, granting permissions to access specific AWS resources. Utilizing an IdP enhances AWS account security by eliminating the need to embed and distribute long-term security credentials with applications.

For further details, refer to [AWS Blog - Use IAM Roles to Connect GitHub Actions to AWS](https://aws.amazon.com/fr/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/).

## Implementation

### AWS GitHub OIDC Workflow

![Design sans titre(6)](https://github.com/gkounga/OidcAwsGithub/assets/99138607/3c1b2eb6-286e-45ec-8d32-32ce37041608)


1. **OIDC Trust Setup**: Establish an OIDC trust between your AWS IAM role and GitHub workflow(s) requiring access to AWS services.

2. **Token Generation**: Each time a job is executed, GitHub's OIDC Provider automatically generates an OIDC token. This token contains multiple claims that establish a secure and verifiable identity for the associated workflow.

3. **Token Retrieval**: Incorporate a step or action in your job to fetch this token from GitHub's OIDC provider and present it to AWS.

4. **Token Validation**: AWS validates the claims within the token and issues short-lived cloud access credentials, granting access to specified resources for the duration of the job.

### Use of OIDC in Github Actions

![Design sans titre(9)](https://github.com/gkounga/OidcAwsGithub/assets/99138607/e255396b-2cfd-4bfc-a591-1fde75600f65)
