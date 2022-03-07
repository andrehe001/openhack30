# Challenge 3 - Deploy Cloud Infrastructure with Infrastructure as Code (IaC)

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other credentials you may use to access Azure resources.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

Infrastructure as Code (IaC) is the management of infrastructure (networks, virtual machines, load balancers, and connection topology) in a descriptive model, using the same versioning as DevOps team uses for source code. Like the principle that the same source code generates the same binary, an IaC model generates the same environment every time it is applied. IaC is a key DevOps practice and is used in conjunction with continuous delivery.

Teams that implement IaC can rapidly deliver stable environments at scale, avoid manual configuration of environments, and enforce consistency by representing the desired state of their environments via code.

## Challenge

Your Team just started preparing the official launch of the MyDriving solution. Currently, nothing is deployed to Azure. Your Team now needs to to deploy all the infrastructure resources required by the MyDriving application.

You don't have to write the IaC code yourself, because one of the developers responsible for provisioning the Azure infrastructure prepared complete code to deploy all required resources in both [Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview) and [Terraform](https://www.terraform.io/intro/index.html) with similar functionality.

To build the pipelines/workflows, you can draw inspiration from a bash script named `deploy.sh`, which contains all the steps required to run an end-to-end Bicep or Terraform deployment. Your task is to replicate these steps in a pipeline, while also respecting requirements described further.

**Decision time!** Explore IaC code in your repository (you can find it under `iac` path) and select only the IaC tooling that best fits your team's skills or learning plans (Terraform or Bicep). The chosen technology will stay with you until the end of the OpenHack.

> **NOTE:** Discuss Bicep vs. Terraform differences with your coach, like Stateless vs. Stateful deployment, ARM vs. API driven deployment, local/remote custom scripts execution inside IaC code.

Your team's job is to leverage the IaC code selected and design a DevOps workflow to deploy the infrastructure needed by the MyDriving solution to Azure Cloud.

The company's lead engineer wants to review proposed deployment changes of the infrastructure and provide a pre-deployment approval before these are pushed into production as this infrastructure is a critical part of your project and any small and incorrect change may cause a problem for the whole solution. However you are not expected to touch or change the existing IaC code in this challenge!

Furthermore, the lead of the project requires high-quality IaC code as well. Your team has to design a workflow to validate the quality of the IaC code and configuration of any potential changes before the new code will be merged with the `main` branch. Only linted code and no faulty configuration should be pushed to the `main` branch.

> **NOTES:**
>
> - The IaC contains a full deployment of cloud infrastructure and application layer as well. Of course, this is a bad practice, but this approach has been implemented only for OpenHack purposes for overall event flow simplification. The good practice is always to separate infrastructure and application parts.
>
> - Terraform requires remote state configuration for a production workload. A Resource Group and Storage Account is already provisioned for this purpose on your Azure Subscription. Look for resources with _state_ in the name. If your team has no experience with remote states, start a discussion with your coach about this concept. Terraform configures remote state during the init operation. This part requires information to connect to the remote state see next note.
>
> - The IaC code needs parameter values to be provided as input. All required details are set inside Repository Secrets (GitHub) or Variable Groups (Azure DevOps). More information can be found in the sections below.

### GitHub

If your team selected GitHub then basic input data for your workflows is already provisioned inside Repository Secrets. Explore it first, and then try to use them inside your workflow.

#### Hints

- IaC code during deployment requires RESOURCES_PREFIX. This variable is the name of your team and repository. You can hardcode this name or make your workflow more dynamic and generic with the following code:

  ```yaml
  jobs:
    job1:
      name: "Job 1"
      outputs:
        # Set output for next job
        RESOURCES_PREFIX: ${{ steps.resources_prefix.outputs.result }}
      steps:
        # Get RESOURCES_PREFIX based on the repo name
        - name: Get repo name
          uses: actions/github-script@v5
          id: resources_prefix
          with:
            result-encoding: string
            script: return context.repo.repo.toLowerCase()

      # Usage for current job: ${{ steps.resources_prefix.outputs.result }}

    job2:
      name: "Job 2"
      steps:
      # Usage for next job: ${{ needs.job1.outputs.RESOURCES_PREFIX }}
  ```

### Azure DevOps

If your team selected Azure DevOps then basic parameter values for your pipelines is already provisioned inside Variable Groups. Explore it first, and then try to use them inside your workflow.

## Success Criteria

- Demonstrate that the validation workflow is triggered only for proposed IaC code changes via a Pull Request.
- Demonstrate that the validation workflow checks lint for the IaC.
- Demonstrate that the validation workflow validates IaC configuration.
- Demonstrate that the deployment workflow is triggered for a selected IaC only when changes to the IaC code are pushed to the `main` branch.
- Demonstrate that the deployment workflow shows a preview for deployment or configuration changes.
- Demonstrate that the deployment workflow has a manual approval process to see a preview of the changes before deploying into the **production** environment.

## References

- <a href="https://docs.microsoft.com/en-us/devops/deliver/what-is-infrastructure-as-code" target="_blank">What is Infrastructure as Code?</a>

- **Bicep**

    - <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview" target="_blank">What is Bicep?</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/linter#use-in-bicep-cli" target="_blank">Use Bicep linter</a>
    - <a href="https://docs.microsoft.com/en-us/cli/azure/deployment/sub?view=azure-cli-latest#az_deployment_sub_validate" target="_blank">Bicep sub-level deployment validate</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/deploy-what-if?tabs=azure-cli%2CCLI" target="_blank">Bicep deployment what-if operation</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/deploy-cli" target="_blank">How to deploy resources with Bicep and Azure CLI</a>

- **Terraform**

    - <a href="https://www.terraform.io/intro/index.html" target="_blank">Introduction to Terraform</a>
    - <a href="https://www.terraform.io/docs/language/state/remote.html" target="_blank">Terraform Remote State</a>
    - <a href="https://www.terraform.io/docs/cli/commands/fmt.html" target="_blank">terraform fmt</a>
    - <a href="https://www.terraform.io/docs/cli/commands/validate.html" target="_blank">terraform validate</a>
    - <a href="https://www.terraform.io/docs/cli/commands/plan.html" target="_blank">terraform plan</a>
    - <a href="https://www.terraform.io/docs/cli/commands/apply.html" target="_blank">terraform apply</a>
    - <a href="https://www.terraform.io/docs/cli/commands/output.html" target="_blank">terraform output</a>

- **GitHub**

    - <a href="https://docs.github.com/en/actions/security-guides/encrypted-secrets#using-encrypted-secrets-in-a-workflow" target="_blank">Using encrypted secrets in a workflow</a>
    - <a href="https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobs" target="_blank">Workflow Job</a>
    - <a href="https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idneeds" target="_blank">Workflow Requiring dependent job</a>
    - <a href="https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idoutputs" target="_blank">Workflow Job outputs</a>
    - <a href="https://docs.github.com/en/actions/deployment/using-environments-for-deployment" target="_blank">Using environments for deployment</a>
    - <a href="https://github.com/marketplace/actions/hashicorp-setup-terraform" target="_blank">GitHub Actions - Terraform</a>
    - <a href="https://github.com/marketplace/actions/azure-login" target="_blank">GitHub Actions - Azure Login</a>
    - <a href="https://github.com/marketplace/actions/azure-cli-action" target="_blank">GitHub Actions - Azure CLI</a>
    - <a href="https://github.com/marketplace/actions/bicep-build-output" target="_blank">GitHub Actions - Bicep Build</a>
    - <a href="https://github.com/marketplace/actions/deployment-what-if" target="_blank">GitHub Actions - Azure Deployment What-If Action</a>
    - <a href="https://github.com/marketplace/actions/deploy-azure-resource-manager-arm-template" target="_blank">GitHub Actions - Azure Resource Manager (ARM) deployment</a>

- **Azure DevOps**

    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups?view=azure-devops&tabs=yaml#use-a-variable-group" target="_blank">Use a variable group</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/scripts/cli/pipeline-variable-group-secret-nonsecret-variables?view=azure-devops" target="_blank">Use a variable group's secret and nonsecret variables in an Azure Pipeline</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/stages?view=azure-devops&tabs=yaml" target="_blank">Azure Pipelines Stages</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/phases?view=azure-devops&tabs=yaml" target="_blank">Azure Pipelines Jobs</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/deployment-jobs?view=azure-devops" target="_blank">Azure Pipelines Deployment jobs</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch#use-output-variables-from-tasks" target="_blank">Use output variables from tasks</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch#set-variables-in-scripts" target="_blank">Set variables in scripts</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch#set-variables-by-using-expressions" target="_blank">Set variables by using expressions</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/environments?view=azure-devops#approvals" target="_blank">Environment Approvals</a>
    - <a href="https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform" target="_blank">Azure Pipelines Task - Terraform</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-cli?view=azure-devops" target="_blank">Azure Pipelines Task - Azure CLI</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment?view=azure-devops" target="_blank">Azure Pipelines Task - Azure Resource Group Deployment</a>
