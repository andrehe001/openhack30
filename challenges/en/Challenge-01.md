# Challenge 1 - Establish your plan

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other credentials you may use to access Azure resources.
- The credentials you need to access the Azure subscription assigned to your team are available on the **OPEN HACK ENVIRONMENT** tab.
- **GitHub path only!** Once you have configured your Git repository, you may see **security alerts** if you are an administrator in your GitHub organization. Do not be alarmed. These are intentional, and you will be required to resolve security issues in a later challenge.

---

To have a successful DevOps strategy, your team needs to have a plan.

Establishing a common plan for communication and collaboration is one of the main aspects of any collective work.

Task boards are used to manage tasks better, prevent omissions, and provide project visibility to team members and management. The task board is a centralized information hub that provides a complete picture of your project. A task can be tracked from inception to completion.

**Resist the initial temptation to rush to the keyboard! Now is the time to pause and think as a team about the end-to-end deployment process that you would implement in this company.**

## Challenge

Your challenge is to organize your team and establish a high-level view of the workflow you will implement during this event to achieve zero-downtime deployment.

Based on your knowledge of the design architecture, your team must establish the fundamental processes needed to go from code to production. Focus only on a fundamental integration and deployment mechanism that considers the architecture of the infrastructure and application.

Get familiar with the basic building blocks of a successful DevOps workflow, and be aware that your current plan may change throughout the event.

Think about the following aspects:

- Each part of API and infrastructure will potentially have a different life cycle.
- Your process should aim at minimizing the time it takes to deploy a feature into production.
- You want to be able to prioritize your tasks.
- Small changes are easier to deploy.

Your Organization requires visibility into your project cycle. Design and implement a task board that meets the following organizational requirements:

- All new issues need to be triaged
- Once the issue has been triaged, it has to be moved into the Backlog
- Issues identified during Sprint planning will be shifted to the Sprint Backlog
- Issues that the Dev Team is actively working on should be moved into In Progress
- Issues with Pull Requests that need to be reviewed should be placed in Review In Progress
- Issues with PRs that have received approval and are ready to be merge have to be moved into the Review Approved
- Closed Issues and PRs where no further action required should be moved into Done

## Success Criteria

- Explain to your coach your DevOps workflow. Then, be ready to answer the following questions:

    - What aspects of DevOps are you implementing?
    - How are you splitting work amongst the team (who is going to be responsible for what)?
    - How will you communicate amongst the team (Teams, Slack, verbal, ...)?

- Demonstrate to your coach that you have implemented a basic task board to track work in progress that meets the organizational requirements.

> NOTE
>
> To manage a project efficiently, you should consider implementing not only a task board, but other features like board automation, milestones/sprints, etc. However, this is not a part of the Challenge.

## GitHub Hints

GitHub introduces new Projects experience (currently in Beta). Unfortunately, this is not supported for this OpenHack - please use the classic approach instead.

## References

- <a href="https://docs.microsoft.com/en-us/devops/what-is-devops" target="_blank">What is DevOps?</a>
- <a href="https://developer-tech.com/news/2016/jan/29/devops-bridging-gap-between-business-and-development/" target="_blank">Bridging the gap between business and development</a>
- <a href="https://docs.microsoft.com/en-us/devops/plan/what-is-kanban" target="_blank">What is Kanban?</a>
- <a href="https://github.com/scgbear/kanban-template/blob/main/docs/EngineeringPractices.md" target="_blank">Kanban Management Best Practices</a>
- <a href="https://docs.microsoft.com/en-us/devops/plan/planning-efficient-workloads-with-devops" target="_blank">Planning efficient workloads with DevOps</a>

- **GitHub**

    - <a href="https://docs.github.com/en/issues/organizing-your-work-with-project-boards/managing-project-boards/about-project-boards/" target="_blank">Managing GitHub Project Boards</a>
    - <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues" target="_blank">Managing work with GitHub Issues</a>
    - <a href="https://docs.github.com/en/issues/organizing-your-work-with-project-boards/tracking-work-with-project-boards/adding-issues-and-pull-requests-to-a-project-board" target="_blank">Adding issues and pull requests to a project board</a>
    - <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue" target="_blank">Linking a pull request to an issue</a>

- **Azure DevOps**

    - <a href="https://docs.microsoft.com/en-us/azure/devops/organizations/settings/work/change-process-basic-to-agile?view=azure-devops" target="_blank">Change a project process from Basic to Agile</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/boards/get-started/customize-boards?view=azure-devops&tabs=basic-process" target="_blank">Customize your Boards</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/boards/work-items/workflow-and-state-categories?view=azure-devops&tabs=basic-process" target="_blank">How workflow states and state categories are used in Azure DevOps Backlogs and Boards</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/boards/work-items/view-add-work-items?view=azure-devops" target="_blank">View and add work items using the Work Items page</a>
