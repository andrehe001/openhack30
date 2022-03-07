# Challenge 6 - Implement a Blue/Green deployment strategy

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other credentials you may use to access Azure resources.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

Classic deployment mechanisms require downtime, and if something goes wrong, you need to rollback or otherwise remediate the broken deployment.

A blue/green deployment strategy involves having two environments and shifting traffic between them. Blue or green can be your current version with the other being the proposed next version. This allows you to 'instantaneously' shift between versions without downtime. In addition, if there is an issue with the new version, rolling back simply requires reverting traffic to the previous deployment.

In the previous challenges, your team implemented workflow(s) for Continuous Integration, testing, and deployment to a Container Registry and to production Azure App Service. You also verified that updated container image was deployed and running in each API's respective web application. Unfortunately, during the deployment your team had interruptions in API(s) operation and availability. In this challenge you'll extend that capability to perform a Blue/Green deployment into your existing Azure App Service to minimize downtime during new version deployment.

> **NOTE:** Blue/Green deployment is different from flighting, canary testing and progressive exposure - those are covered in in another challenge.

## Challenge

Leveraging your selected orchestration tool, update your existing workflow(s) to automatically perform Blue/Green deployments into Azure App Service.

Think about your strategy as a team before you start developing your solution.

### Hint

Before swapping the Blue and Green environments, ensure that the destination environment is online and available. Additional gates (e.g., health check) may be desired before switching. Health check endpoint is implemented for each of the APIs and you can use HTTP calls to check the response code during the deployment process (or choose a prebuilt extension from the Marketplace, but be ready to explain your reasoning).

## Success Criteria

To successfully complete the challenge, implement Blue/Green deployments for each of the APIs.

- Demonstrate that a code change in an API is deployed initially to a staging environment and automatically to production with "zero downtime".
- Explain to your coach the logic that you are using for blue/green deployment and address the following points:
- Describe the mechanism that validates that the container and web app is ready and reasons for choosing a particular approach
- Demonstrate what triggers or constraints are used to determine when/whether it is safe to swap to the new version
- Demonstrate the CI code that determines the version of the container in production (green) and version of the container in staging (blue)

## References

- <a href="https://martinfowler.com/bliki/BlueGreenDeployment.html" target="_blank">Blue/Green deployment</a>
- <a href="https://docs.microsoft.com/en-us/azure/app-service/deploy-staging-slots">Set up staging environments in Azure App Service</a>
- <a href="https://medium.com/@sangeetavsunchu/azure-slot-deployment-with-blue-green-deployment-model-b52cd5ffaf07" target="_blank">Azure Slot Deployment with Blue-Green Deployment Model</a>

- **GitHub**

    - <a href="https://github.com/marketplace/actions/url-health-check" target="_blank">GitHub Actions - URL Health Check</a>
    - <a href="https://docs.microsoft.com/en-us/cli/azure/webapp/deployment/slot?view=azure-cli-latest#az_webapp_deployment_slot_swap" target="_blank">az webapp deployment slot swap</a>

- **Azure DevOps**

    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/environments?view=azure-devops#approvals" target="_blank">Environment Approvals</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/process/approvals?view=azure-devops&tabs=check-pass#invoke-rest-api" target="_blank">Define approvals and checks - Invoke REST API</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-app-service-manage?view=azure-devops" target="_blank">Azure Pipelines - Azure App Service Manage task</a>
