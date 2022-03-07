# Challenge 8 - Integrating quality and security checks

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other Azure credentials.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

At the completion of Challenge 7, you implemented workflow(s) to perform unit testing, continuous integration, Blue/Green deployments, and basic security features to protect your code from secrets leaking. In addition, you performed essential gating to verify that the staging environment was online before performing the Blue/Green swap. However, there are always opportunities to improve automated quality and security gates.

Depending upon the business need, it is common to perform one or more of the following in your workflows:

- **DevSecOps**

    - **Dependency Scanning** - Open source components are used in the majority of modern applications. This greatly accelerates development but can also introduce vulnerability or license issues. Dependency scanning can check for issues as part of your code commit or during CI/CD workflows.
    - **Static Application Security Testing (SAST)** - Computers are useful in identifying patterns, including patterns in code that may be vulnerable, difficult to maintain, perform poorly or are otherwise buggy. Static Code Analysis can identify "code smells" and improve the value of your code reviews.
    - **Dynamic Application Security Testing (DAST)** - Dynamic analysis focuses on the "outside" of the application and runs simulated attacks against the frontend, like an attacker would. DAST tools are able to automatically perform most common attacks (like SQL injection) and then look at test results and identify potential vulnerabilities in the application.
    - **Variant Analysis** - Like Static Code Analysis, Variant Analysis can identify "code smells" and improve the value of your code reviews. However, Variant Analysis can also reduce false positives and otherwise provide more meaningful insights to your code. As a result, variant Analysis has proven extremely useful in security analysis scenarios.

- **Code Quality**

    - **Manual Approvals** - Although manual intervention is against some of the core tenants of automation, it is still required in some scenarios. In this case, moving from a pre-production environment to production requires the approval of a specific individual or team.
    - **Code Coverage** - Unit Tests can provide a safety net and indicator of code quality. However, unit tests require ongoing maintenance and can give a false sense of security. Code Coverage helps you understand how much your code is being tested and monitor whether testing declines as code changes.
    - **Integration Testing** - After deployment to a pre-production environment, automated tests can run against an integrated system, verifying "units" of code and the completely integrated system.

## Challenge

In this challenge you will plan and improve your workflow to support **_one or more_** quality and security checks. You must complete the implementation of **_one of these enhancements from each category below_** (DevSecOps + Code Quality). Challenges in each section has been arranged in increasing degrees of complexity.

### DevSecOps Enhancements

- _Dependency Scanning_ is frequently performed as part of your commit workflow or during PR or CI builds. If you're using GitHub, implement security alerts and automated security updates. For other repositories, integrate [WhiteSource Bolt](https://marketplace.visualstudio.com/items?itemName=whitesource.whiteSource-bolt-v2) or another vulnerability scanner into your PR or CI workflow.
- _Static Application Security Testing_ is generally performed as part of PR or CI builds and reporting is used to support peer reviews. Different computer languages may leverage different tools for static analysis.
- _Dynamic Application Security Testing_ can be executed when new version of the application is deployed to verify that no "easy" security flaws were introduced. The OWASP Foundation maintains a [list of vulnerability scanning tools](https://owasp.org/www-community/Vulnerability_Scanning_Tools) and also provides the [ZAP (Zed Attack Proxy)](https://owasp.org/www-project-zap/) tool as a flagship project.
- _Variant Analysis_ is more intensive than static analysis an is frequently decoupled from the pipeline. Variant analysis tools like [CodeQL](https://codeql.github.com/docs/) can typically be configured to discover variants of vulnerabilities in your public repositories.

### Code Quality Enhancements

- _Manual Approval_ is very common in enterprise environments, relying on a specific individual or team to review an approve a pre-production deployment before pushing to production.
- _Code Coverage_ is generally performed during unit testing to measure how much of your code is actually tested. Integrate code coverage reporting into your PR or CI workflow. You may also implement a gate such that the workflow fails if the amount of code coverage falls as code is changed.
- _Integration Tests_ are generally run against a pre-production environment to verify your components integrate well across your code base. The technology will be different than unit testing (e.g., Selenium et al) and should be implemented after deployment.

> **NOTE:** Different source repositories and orchestration tools will have other mechanisms to implement these capabilities. Depending upon your tools, some of these may be significantly easier or more difficult to achieve.

## Success Criteria

- Demonstrate one or more of the above enhancements (one for each category DevSecOps + Code Quality). This will frequently require pushing changes through your workflow and showing and explaining the steps. It may also require demonstrating integration with external tools.
- For a different enhancement, explain a design, the specific tools you would leverage, how they fit into your process, and how you would integrate them.

## References

- Dependency Scanning
    -GitHub
      - <a href="https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically" target="_blank">Dependabot - Keeping your dependencies updated automatically</a>
      - <a href="https://docs.github.com/en/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/about-alerts-for-vulnerable-dependencies"  target="_blank">About alerts for vulnerable dependencies</a>
      - <a href="https://docs.github.com/en/code-security/supply-chain-security/managing-vulnerabilities-in-your-projects-dependencies/configuring-dependabot-security-updates" target="_blank">Configuring Dependabot security updates</a>
      - <a href="https://whitesource.atlassian.net/wiki/spaces/WD/pages/556007950/WhiteSource+Bolt+for+GitHub" target="_blank">Whitesource Bolt for GitHub</a>
    -Azure DevOps
    - <a href="https://whitesource.atlassian.net/wiki/spaces/WD/pages/1641644045/WhiteSource+Bolt+for+Azure+Pipelines" target="_blank">Whitesource Bolt for Azure Pipelines</a>
    - <a href="https://marketplace.visualstudio.com/items?itemName=dependency-check.dependencycheck" target="_blank">OWASP Dependency Check</a>
- Static Application Security Testing
    - <a href="https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis" target="_blank">Static Code Analysis tools (Wikipedia)</a>
    - GitHub
        - <a href="https://github.com/marketplace?type=actions&query=lint" target="_blank">Linters in the GitHub Actions marketplace</a>
        - <a href="https://sonarcloud.io/documentation/getting-started/github/" target="_blank">SonarCloud - Getting started with GitHub</a>
        - <a href="https://github.com/marketplace/actions/sonarcloud-scan" target="_blank">SonarCloud for GitHub Actions</a>
    - Azure DevOps
        - <a href="https://sonarcloud.io/documentation/getting-started/azure-devops/" target="_blank">SonarCloud - Getting started with Azure DevOps</a>
        - <a href="https://azuredevopslabs.com/labs/vstsextend/sonarcloud/" target="_blank">Driving continuous quality of your code with SonarCloud</a>
- Dynamic Application Security Testing
    - <a href="https://owasp.org/www-project-zap/" target="_blank">OWASP Zed Attack Proxy (ZAP)</a>
    - GitHub
        - <a href="https://github.com/marketplace/actions/owasp-zap-baseline-scan" target="_blank">GitHub Action - OWASP ZAP Baseline Scan</a>
        - <a href="https://github.com/marketplace/actions/owasp-zap-full-scan" target="_blank">GitHub Action - OWASP ZAP Full Scan</a>
    - Azure DevOps
        - <a href="https://marketplace.visualstudio.com/items?itemName=CSE-DevOps.zap-scanner" target="_blank">OWASP/ZAP Scanning extension for Azure DevOps</a>
- Variant Analysis
    - <a href="https://codeql.github.com/docs/" target="_blank">Variant Analysis with CodeQL</a>
    - <a href="https://lgtm.com/" target="_blank">Continuous security analysis (with GitHub and SEMMLE)</a>
- Integration Testing
    - <a href="https://softwaretestingfundamentals.com/integration-testing/" target="_blank">Integration testing</a>
    - <a href="https://www.guru99.com/unit-test-vs-integration-test.html" target="_blank">Integration tests vs Unit tests</a>
    - <a href="https://docs.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-3.1" target="_blank">Integration testing in .NET Core</a>
    - <a href="https://www.cloudbees.com/blog/testing-in-go" target="_blank">Integration testing in Go</a>
    - <a href="https://www.codementor.io/@olatundegaruba/integration-testing-supertest-mocha-chai-6zbh6sefz" target="_blank">Integration testing with Node.JS</a>
- Code Coverage
    - <a href="https://coveralls.io/" target="_blank">CoverAlls</a>
    - <a href="https://codecov.io/" target="_blank">CodeCov</a>
    - <a href="https://www.jacoco.org/jacoco/" target="_blank">Jacoco</a>
    - GitHub
        - <a href="https://github.com/marketplace/actions/coveralls-github-action" target="_blank">CoverAlls for GitHub Actions</a>
    - Azure DevOps
        - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/ecosystems?view=azure-devops" target="_blank">Azure Pipelines ecosystem (per-language code coverage docs)</a>
- Manual Approvals
    - GitHub
        - <a href="https://docs.github.com/en/actions/managing-workflow-runs/reviewing-deployments" target="_blank">Reviewing deployments</a>
    - Azure DevOps
        - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/release/approvals/?view=azure-devops" target="_blank">Release gates and approvals for Azure Pipelines</a>
        - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/manual-intervention?view=azure-devops" target="_blank">Manual Intervention task for Azure Pipelines</a>
