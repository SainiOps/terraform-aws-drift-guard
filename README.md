# terraform-aws-drift-guard

Deploys a scheduled AWS Lambda (container image) that runs TF Drift Guard
checks against a live AWS account and posts violations to Slack.

Companion project: https://github.com/SainiOps/tf-drift-guard

## Usage
```hcl
module "drift_guard" {
  source            = "SainiOps/drift-guard/aws"
  version           = "1.0.0"
  region            = "us-east-1"
  required_tags     = "owner,environment"
  slack_webhook_url = var.slack_webhook_url
  lambda_image_uri  = "<your-ecr-repo>:latest"
}
```

## Inputs
| Name | Description | Default |
|---|---|---|
| schedule_expression | EventBridge schedule | rate(6 hours) |
| required_tags | Comma-separated required tag keys | owner,environment |
| slack_webhook_url | Slack incoming webhook URL | "" |
| region | AWS region | us-east-1 |
| lambda_image_uri | ECR image URI for the scan container | (required) |

## Outputs
| Name | Description |
|---|---|
| lambda_function_name | Name of the deployed Lambda function |
