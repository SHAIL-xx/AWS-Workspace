# AWS Cloud Engineering Workspace

This repository collects AWS automation examples, local-emulation projects, Terraform
configurations, and learning labs. It is a portfolio and practice workspace; the presence of
an AWS deployment example does not mean it is production-ready.

## Project areas

- `aws-deploy/`: AWS SAM/Lambda examples intended for deployment to AWS. Review each template,
  permissions, account, region, and potential costs before deploying.
- `localstack-dev/`: LocalStack-based service experiments. The Compose file uses LocalStack
  `4.14.0`, requires an auth token, and enables persistence.
- `terraform-infra/`: Reusable Terraform infrastructure examples. The root configuration uses
  a remote S3 state backend; do not initialize, migrate, or apply it without the intended backend
  and state access.
- `lab-practise/`: Learning exercises and service-specific experiments.

## LocalStack quick start

Prerequisites: Docker Compose and a LocalStack auth token.

```bash
cd localstack-dev
export LOCALSTACK_AUTH_TOKEN=your-token
docker compose up -d
```

Keep the token private. The Compose setup mounts the Docker socket and stores persistent data under
`localstack-dev/volume`; use it only on a trusted development machine. Back up or recreate that
data when changing LocalStack versions, and never commit the token, volume data, or Terraform state.

The LocalStack Lambda examples are separate SAM projects with their own runtime and test instructions.
They were not changed as part of the current non-SAM maintenance work.

## Terraform validation

GitHub Actions validates the two example Terraform roots with the backend disabled. This checks
configuration without accessing the remote state backend or applying infrastructure. The
`terraform-infra/terraform` configuration still requires its intended remote S3 backend for any
stateful operation.

Before deploying any example to AWS, review its IAM permissions, endpoint configuration, state
location, resource costs, and cleanup procedure. Treat all examples as learning material until
they have been independently reviewed and tested for the target account.
