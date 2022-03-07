# Challenge 4 - Implement Continuous Integration (CI) with Testing

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other credentials you may use to access Azure resources.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

No matter how well written the code or experienced the dev team, the benefits of continuous integration (CI) automation will increase velocity and quality of your code and prevent unwanted scenarios such as "Well... it works on my machine :)".

## Challenge

In this challenge you will be expected to create workflows that automate the **building and unit testing** of at least one of the APIs of your application. You are not required to publish code coverage reports, just test results. Instead, focus exclusively on building and executing existing unit tests as part of your workflows. Any unit test failure should be highlighted as a comment in the PR. Carefully review the Readme for your chosen API as it may contain additional instructions. You will also need to consider the flow for a build failure and ensure that code for builds that fail doesn't get merged into the main branch.

> **NOTE:** When selecting GitHub Actions or Azure Pipeline tasks, be prudent and select Actions/Tasks that were created by the vendor as a first choice. If you are going to use a third party option make sure that you verify that you are able to satisfy the success criteria with your selection.
>
> **NOTE:** Continuous Integration (CI) uses best practices including automated testing and ideally <a href="https://trunkbaseddevelopment.com/" target="_blank">trunk-based development</a>. Automated testing will be covered later and will extend the CI setup completed here.

## Success Criteria

- With your coach present, execute the automation workflow, explain each step, and show that each step completes successfully.
- Demonstrate that the workflow is triggered for an API on a Pull Request (PR) only when changes are made to code for that API.
- Demonstrate that the workflow(s) complement existing branch protections by performing verifications before a Pull Request (PR) can be merged to your protected branch.
- Demonstrate that your workflow runs, performs all of the required steps, and ultimately prevents the merging of the code when the workflow fails.
- Demonstrate that your workflow can be triggered manually by developers on their feature branches for ad-hoc code validation - if build/test failed, then creates issue/bug in the backlog.
- Demonstrate that your workflow adds a comment to your PR for each failed build during PR validation.

> **NOTE:** You are required to make a change to the code that will result in the failure of a unit test. If you are uncertain, your coach will provide a breaking change to submit through your pipeline.

## Hints

To create well-formatted comments for PRs, you can use Markdown syntax and built-in variables. The code example for GitHub and Azure DevOps is below.

### GitHub

```text
### Unit Test `failure`
<details>
<summary>Workflow details</summary>

Workflow name: `${{ github.workflow }}`
Action: `${{ github.event_name }}`
Job: `${{ github.job }}`
PR: #${{ github.event.number }}
</details>

Test details: [Run #${{ github.run_id }}](${{ github.server_url }}/${{ github.repository }}/actions/runs/${{ github.run_id }})
Pusher: @${{ github.actor }}
```

### Azure DevOps

```text
### Unit Test `failure`
<details>
<summary>Pipeline details</summary>

Pipeline name: `$(Build.DefinitionName)`
Action: `$(Build.Reason)`
Job: `$(System.JobName)`
PR: [$(System.PullRequest.PullRequestId)]($(System.PullRequest.SourceRepositoryURI)/pullrequest/$(System.PullRequest.PullRequestId))
</details>

Test details: [Run #$(Build.BuildId)]($(System.CollectionUri)$(System.TeamProject)/_build/results?buildId=$(Build.BuildId)&view=ms.vss-test-web.build-test-results-tab)
Pusher: @<$(Build.RequestedForId)>
```

## References

- <a href="https://docs.microsoft.com/en-us/devops/develop/what-is-continuous-integration" target="_blank">What is Continuous Integration (CI)?</a>
- <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/apps/cd/azure/cicd-data-overview?view=azure-devops#what-is-cicd" target="_blank">What is CI/CD?</a>
- <a href="https://docs.microsoft.com/en-us/devops/deliver/what-is-continuous-delivery" target="_blank">What is Continuous Delivery?</a>

### Workflow orchestration

- <a href="https://youtu.be/C7NFwlmSAqU" target="_blank">What is Pipeline as Code? | One Dev Question: Abel Wang</a>

- **GitHub**

    - <a href="https://docs.github.com/en/actions/automating-builds-and-tests/about-continuous-integration" target="_blank">About continuous integration (CI) workflows with GitHub Actions</a>
    - <a href="https://docs.github.com/en/actions/advanced-guides/using-github-cli-in-workflows" target="_blank">Using GitHub CLI in workflows</a>
    - <a href="https://cli.github.com/manual/" target="_blank">GitHub CLI manual</a>
    - <a href="https://github.com/marketplace/actions/github-script" target="_blank">GitHub Script Action</a>
    - <a href="https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-net" target="_blank">Building and testing .NET</a>
    - <a href="https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs-or-python" target="_blank">Building and testing Node.js</a>
    - <a href="https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven" target="_blank">Building and testing Java with Maven</a>

- **Azure DevOps**

    - <a href="https://marketplace.visualstudio.com/items?itemName=mspremier.CreateWorkItem" target="_blank">Azure Pipelines Task - Create Work Item</a>
    - <a href="https://marketplace.visualstudio.com/items?itemName=CSE-DevOps.create-pr-comment-task" target="_blank">Azure Pipelines Task - Create Pull Request Comment</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/dotnet-core" target="_blank">Build, test, and deploy .NET Core apps</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/javascript" target="_blank">Build, test, and deploy JavaScript and Node.js apps</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/java" target="_blank">Build Java apps</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/go" target="_blank">Build and test Go projects</a>

### Unit testing

- <a href="http://agiledata.org/essays/tdd.html" target="_blank">Introduction to Test Driven Development (TDD)</a>
- <a href="https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-dotnet-test" target="_blank">Writing and running units test with .NET Core</a>
- <a href="https://blog.risingstack.com/node-hero-node-js-unit-testing-tutorial/" target="_blank">Writing and running unit tests with Node.js</a>
- <a href="https://www.vogella.com/tutorials/Mockito/article.html" target="_blank">Writing and running unit tests with Java</a>
- <a href="https://blog.alexellis.io/golang-writing-unit-tests/" target="_blank">Writing and running unit tests with GoLang</a>
