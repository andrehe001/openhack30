# Challenge 5 - Implement Continuous Deployment (CD)

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other Azure credentials.
- Common references for DevOps tools can be found under the **Cheat sheet** section.

---

Now that you have successfully implemented Continuous Integration (CI), it is time to show that you can deploy a container image for at least one of the four APIs to Azure App Service.

## Challenge

Earlier, each API of the MyDriving application was built and deployed to an Azure Container Registry using the Terraform/Bicep scripts in the `iac` directory. Mixing the infrastructure code with the application is not recommended. Your team has to separate the deployment of the application from IaC code and create a dedicated workflow for at least one API.

Using the tooling that you have implemented so far, you must build & push the images of each of the four APIs to a Container Registry and deploy each of them to your existing Azure App Service using Continuous Delivery (CD). Configuration steps will differ depending on whether your team decides to use Azure Container Registry or GitHub Packages to store your images.

Ensure proper naming of your images. The tag format was already decided by your organization, so you should look for already deployed images in your subscription and replicate the naming convention.

### Hint

- The image tag format looks like `<Azure Container Registry URI>/<ACR repository name>:<Revision Number>`.

### Extended challenge (optional)

> **NOTE:** This extended, optional challenge is only for the teams who have chosen GitHub as their DevOps tool and want to explore GitHub Packages as Container Registry.

By design, Azure Container Registry is the default registry for the MyDriving application. Container Registry is part of infrastructure architecture design. To make a change to GitHub Packages, your team has to leverage changes into the IaC part to set a new configuration per each APIs to use GitHub Packages.

#### Hints

- The image tag should take the format of `ghcr.io/<Owner>/<Repository name>/<Image Name>:<Revision Number>` where image name follows the naming convention `devopsoh/<Image Name>:<tag>`.
- IaC code accepts optional parameters like:
    - Terraform: `docker_registry_server_url`, `docker_registry_server_username`, `docker_registry_server_password`
    - Bicep: `dockerRegistryServerUrl`, `dockerRegistryServerUsername`, `dockerRegistryServerPassword`

## Success Criteria

Demonstrate the following to your coach for **at least one** API:

- The container images (one per API) are published to the Container Registry (only when pushing to `main` branch, but not on PRs).

  > **NOTE:** Your publish process should not overwrite the existing image tag, so consider how you will ensure unique values for image tags.

- The API(s) code is deployed to the `staging` slot of the Azure App Service every time code is pushed to `main` (if the code compiles and all tests pass on PRs before).
  > **NOTE:** Your branch/pull request policy can be used to enforce workflow and gates between CI and CD activities.

## References

Continuous Delivery

- <a href="https://docs.microsoft.com/en-us/devops/deliver/what-is-continuous-delivery" target="_blank">What is Continuous Delivery?</a>
- <a href="https://continuousdelivery.com/#why-continuous-delivery" target="_blank">Why Continuous Delivery?</a>

Azure App Service

- <a href="https://docs.microsoft.com/en-us/azure/app-service/configure-custom-container?pivots=container-linux" target="_blank">Configure a custom container for Azure App Service</a>
- <a href="https://docs.microsoft.com/en-us/azure/app-service/tutorial-custom-container?pivots=container-linux" target="_blank">Migrate custom software to Azure App Service using a custom container</a>

GitHub

- <a href="https://docs.microsoft.com/en-us/azure/app-service/deploy-container-github-action?tabs=service-principal" target="_blank">Deploy a custom container to App Service using GitHub Actions</a>
- <a href="https://github.com/marketplace/actions/azure-cli-action" target="_blank">GitHub Actions - Azure CLI Action</a>
- <a href="https://github.com/marketplace/actions/build-and-push-docker-images" target="_blank">GitHub Actions - Build and push Docker images</a>
- <a href="https://github.com/marketplace/actions/azure-webapp" target="_blank">GitHub Actions - Azure WebApp</a>
- <a href="https://github.com/marketplace/actions/azure-app-service-settings" target="_blank">GitHub Actions - Azure App Service Settings</a>

Azure DevOps

- <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/targets/webapp-on-container-linux?view=azure-devops&tabs=yaml" target="_blank">Deploy an Azure App custom container</a>
- <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/build/docker?view=azure-devops" target="_blank">Azure Pipelines - Docker task</a>
- <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-deployment?view=azure-devops" target="_blank">Azure Pipelines - Azure App Service Deploy task</a>
- <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-containers?view=azure-devops" target="_blank">Azure Pipelines - Azure Web App for Container task</a>
- <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-app-service-manage?view=azure-devops" target="_blank">Azure Pipelines - Azure App Service Manage task</a>

Container Registries

- <a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-tutorial-quick-task" target="_blank">Build and deploy container images in the cloud with Azure Container Registry Tasks</a>
- <a href="https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-docker-cli?tabs=azure-cli" target="_blank">Push your first image to your Azure container registry using the Docker CLI</a>
- <a href="https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry" target="_blank">GitHub Packages - Working with the Container registry</a>
- <a href="https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions" target="_blank">GitHub Packages - Publishing and installing a package with GitHub Actions</a>
