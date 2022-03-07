# Challenge 2 - Setting up the Development Workflow

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other credentials you may use to access Azure resources.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

## Challenge

Configure and implement the mechanisms that will form the basis of the development workflow. You will need to set up the mechanism to prevent people from directly changing the code in your `main` branch without peer-reviewing (including code owners to establish mandatory reviewers). In addition, you would like to have clean commits history in your `main` branch and prevent people from merging their commits from the development phase.

You are expected to implement a policy to enforce that code changes submitted must go through a peer review and formal approval process. Since the repository contains four APIs and IaC, code ownership should be defined per API and IaC. It should be mandatory to review the code by owner(s). The second policy must enforce that the commit history from your feature branch has not been visible in the `main` branch after the PR merging operation.

> **NOTE:** You are expected to work on all the APIs of the MyDriving application and Infrastructure as Code part as well.
>
> **NOTE:** You are not expected to automate the build process yet. However, this will be required in the following challenges.
>
> **NOTE:** Discuss Git merging strategies with your Coach if you are unfamiliar with different merging opinions. The _flat history_ might not always be the best strategy.

## Success Criteria

- Demonstrate to your coach that you have implemented a branch protection policy to prevent any code changes from being committed to the `main` branch without being reviewed. The policy must require at least two reviewers and including a code owner(s) review.
- Demonstrate to your coach that you have defined code owner(s) for each of the services.
- Demonstrate to your coach that you have implemented a branch protection policy to prevent development phase commits from being committed to the `main` branch.

## References

- **GitHub**

    - <a href="https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches" target="_blank">About protected Branches</a>
    - <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners" target="_blank">About code owners</a>
    - <a href="https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-linear-history" target="_blank">About protected branches - require linear history</a>
    - <a href="https://docs.github.com/en/github/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges#squash-and-merge-your-pull-request-commits" target="_blank">Squash and merge your pull request commits</a>

- **Azure DevOps**

    - <a href="https://docs.microsoft.com/en-us/azure/devops/repos/git/branch-policies?view=azure-devops" target="_blank">Improve code quality with branch policies</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/repos/git/branch-policies?view=azure-devops#automatically-include-code-reviewers" target="_blank">Automatically include code reviewers</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/repos/git/merging-with-squash?view=azure-devops" target="_blank">Squash merge pull requests</a>
