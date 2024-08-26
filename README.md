# github-actions-terraform

https://github.com/hashicorp/setup-terraform


This workflow installs the latest version of Terraform CLI and configures the Terraform CLI configuration file with an API token for Terraform Cloud (app.terraform.io). On pull request events, this workflow will run `terraform init`, `terraform fmt`, and `terraform plan` (speculative plan via Terraform Cloud). On push events
to the "main" branch, `terraform apply` will be executed.

Documentation for `hashicorp/setup-terraform` is located here: https://github.com/hashicorp/setup-terraform

## To use this workflow, you will need to complete the following setup steps.

    terraform {
        backend "remote" {

            # The name of your Terraform Cloud organization.
            organization = "example-organization"

        # The name of the Terraform Cloud workspace to store Terraform state files in.
        workspaces {
            name = "example-workspace"
            }
        }
    }

# An example resource that does nothing.

    resource "null_resource" "example" {
        triggers = {
            value = "A example resource that does nothing!"
        }
    }

## Generate a Terraform Cloud user API token and store it as a GitHub secret (e.g. TF_API_TOKEN) on this repository.

Documentation:
    - https://www.terraform.io/docs/cloud/users-teams-organizations/api-tokens.html
    - https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets

## Reference the GitHub secret in step using the `hashicorp/setup-terraform` GitHub Action.
    
    - name: Setup Terraform
      uses: hashicorp/setup-terraform@v1
      with:
        cli_config_credentials_token: ${{ secrets.TF_API_TOKEN }}
