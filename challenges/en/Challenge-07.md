# Challenge 7 - DevSecOps basics – get rid of secrets

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other Azure credentials.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

## Background

Securely managing secrets (user accounts, passwords, connection strings, certificates, etc.) is essential to running secure applications in the cloud. As teams move to agile development with frequent deployments/releases, exposing secrets in code can be easy to overlook. When it comes to secrets, managing where the secrets are stored and how they are injected into code is only half of the problem. It is also crucial to make sure that secrets are updated routinely.

## Challenge

The application team of the fictitious insurance company is concerned that they might have leaked some information in the application that could expose the site to hackers. In this challenge, you will use the API repo provided to you.
There are secrets exposed in the current codebase. This challenge will have you update your CI pipelines to catch leaked secrets and prevent a Pull Request that fails validation to be merged. Once detected, you will mitigate the issues by securely storing secrets across environments and removing them from any source code.

### Scan for secrets

The first part of this challenge will have you add credential scanning to your CI workflow. Your workflow should fail if the credential scanning has a positive outcome. Inevitably you will discover that false positives are possible with credential scanning. Ensure that your credential scanning has filters that suppress any false positives that you discover.

### Hints

In most cases, secret scanning tools are available on the market based on the patterns for common secrets like connection strings, access tokens, etc. However, if your codebase contains not commonly used secrets, the scanner may fail and not detect your secret. Therefore, it is not a "magic" solution that will solve your secret's problem - the most important thing is to raise awareness and avoid sensitive data in your code. Most tools allow you to extend and define your own rules/patterns. Below are some examples that may be helpful in this Challenge.

#### Gitleaks

Gitleaks custom rule for detecting common passwords based on keyword detection.

```toml
[[rules]]
id = "common-passwords"
description = "Common Passwords"
regex = '''(?i)1q2w3e|abc123|admin@123|admin123|alpha123|asdf|asdfgh|bienvenue|bienvenue123|changeme123|demopass|dragon|iloveyou|letmein|letmein!|letmein_apr|letmein_aug|letmein_dec|letmein_feb|letmein_jan|letmein_jul|letmein_jun|letmein_mar|letmein_may|letmein_nov|letmein_oct|letmein_sep|l0ve|m0t2pass|m0t2passe|mot2pass|mot2passe|mustang|n0tallowed|n0tallowed123|notallowed123|oliver|p@55w0rd|p@55w0rd123|p@55word|p@55word123|p@5sw0rd|p@5sw0rd123|p@5sword|p@5sword123|p@s5w0rd|p@s5w0rd123|p@s5word|p@s5word123|p@55w0rd|p@ssw0rd|p@ssw0rd123|p4ssw0rd|password1|password123|qwert|qwerty|qwerty123|secret1|simplepass|support123|test123|tigger|trustno1|virus|welc0me123|welcome123'''
```

#### GitHub Advanced Security -

GitHub Advanced Security secret scanning custom pattern for detecting common passwords based on keyword detection.

```plaintext
(?i)1q2w3e|abc123|admin@123|admin123|alpha123|asdf|asdfgh|bienvenue|bienvenue123|changeme123|demopass|dragon|iloveyou|letmein|letmein!|letmein_apr|letmein_aug|letmein_dec|letmein_feb|letmein_jan|letmein_jul|letmein_jun|letmein_mar|letmein_may|letmein_nov|letmein_oct|letmein_sep|l0ve|m0t2pass|m0t2passe|mot2pass|mot2passe|mustang|n0tallowed|n0tallowed123|notallowed123|oliver|p@55w0rd|p@55w0rd123|p@55word|p@55word123|p@5sw0rd|p@5sw0rd123|p@5sword|p@5sword123|p@s5w0rd|p@s5w0rd123|p@s5word|p@s5word123|p@55w0rd|p@ssw0rd|p@ssw0rd123|p4ssw0rd|password1|password123|qwert|qwerty|qwerty123|secret1|simplepass|support123|test123|tigger|trustno1|virus|welc0me123|welcome123
```

### Move secrets to Azure Key Vault

The second part of the challenge you will move your secrets to Azure Key Vault. Included in your repos are Infrastructure as Code (IaC) samples you can use to complete this step.

> **NOTE:** If you can't see the secrets in Key Vault (which you won't be able to), you can add an Access Policy to the Key Vault manually to give users in the Team access. However, be aware that any IaC run will reset the policies, which will need to be done again.

### Remove secrets from the source code

In this step you will remove all secrets from your application code and configure your application code to read securely form Azure Key Vault. Once this is complete validate that the scanning no longer has any true positive results.

## Success Criteria

- Demonstrate that your branch policy for `main` branch detects exposed secrets in code and fails the build
- Demonstrate that the App Service with your APIs are configured to read secrets from Azure Key Vault
- IaC code is updated to new configuration for security requirements
- All exposed secrets have been identified and removed from code

## Extended Challenge (optional)

> **NOTE:** This extended, optional challenge is only for the teams who want to explore key rotation of secrets in Azure Key Vault.

Secret Rotation is a key feature that strengthens your overall security posture. This feature provides a backstop, should a secret be compromised, by limiting the lifetime that secrets are valid. In this part of the challenge you will implement a key rotation automation process using Azure Key Vault as the secret store. While there are passwordless solutions for .NET and Azure SQL the polyglot nature of the applications services mean the team must stay with traditional password implementations for connections to the data store. In this challenge you will implement a password rotation pipeline to rotate the passwords using automation.

### Hints

IaC and workflow for <a href="https://docs.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation" target="_blank">Automate the rotation of a secret for resources that use one set of authentication credentials</a> you can find under your team's repo (see `support/sqlsecretrotation` path).

## Extended Challenge Success Criteria

- An automated secret rotation solution for the Azure SQL Server is implemented, the code can use the new key and the old keys are deprecated.

## References

### Secret Scanning

- <a href="https://docs.microsoft.com/en-us/azure/app-service/app-service-key-vault-references" target="_blank">Use Key Vault references for App Service and Azure Functions</a>

- **Azure DevOps**

    - <a href="https://docs.microsoft.com/en-us/azure/devops/repos/git/branch-policies?view=azure-devops&tabs=browser" target="_blank">Improve code quality with branch policies</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups?view=azure-devops&tabs=yaml#link-secrets-from-an-azure-key-vault" target="_blank">Key Vault in Azure DevOps variable groups</a>
    - <a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-key-vault?view=azure-devops" target="_blank">Azure Key Vault task</a>
    - <a href="https://marketplace.visualstudio.com/items?itemName=sariftools.scans" target="_blank">SARIF SAST Scans Tab</a>
    - **CredScan (part of Secure Development Tools aka Guardian)** (only for Microsoft employees)
        - <a href="https://marketplace.visualstudio.com/items?itemName=securedevelopmentteam.vss-secure-development-tools " target="_blank">Secure Development Tools (Guardian)</a>
        - <a href="https://aka.ms/CredScan " target="_blank">CredScan</a>
        - <a href="https://eng.ms/docs/cloud-ai-platform/developer-services/one-engineering-system-1es/1es-docs/credscan/credscan-overview#v2---official-release-v2117---recommended" target="_blank">CredScan recommended version</a>
        - <a href="https://secdevtools.azurewebsites.net/helpPostAnalysis.html" target="_blank">Getting started with the Post-Analysis (Build Break)</a>
        - <a href="https://strikecommunity.azurewebsites.net/articles/8148/credscan-false-positives-and-suppressions.html" target="_blank">CredScan False Positives and Suppressions</a>
        - <a href="https://strikecommunity.azurewebsites.net/articles/8148/credscan-false-positives-and-suppressions.html" target="_blank">Local Suppression</a>
    - **Gitleaks**
        - <a href="https://github.com/zricethezav/gitleaks" target="_blank">Gitleaks scanning tool</a>
        - <a href="https://marketplace.visualstudio.com/items?itemName=Foxholenl.Gitleaks" target="_blank">Azure DevOps task for Gitleaks</a>
        - <a href="https://github.com/zricethezav/gitleaks#configuration" target="_blank">Your own secret detection rules for Gitleaks</a>
        - <a href="https://github.com/zricethezav/gitleaks#configuration" target="_blank">Gitleaks suppressing false positives with allow patterns</a>

- **GitHub**
    - <a href="https://github.com/marketplace/actions/azure-key-vault-get-secrets" target="_blank">GitHub Action for Azure Key Vault</a>
    - **GitHub Advanced Security (GHAS)**
        - <a href="https://docs.github.com/en/code-security/secret-scanning" target="_blank">GitHub Advanced Security Secret Scanning</a>
        - <a href="https://docs.github.com/en/enterprise-cloud@latest/code-security/secret-scanning/defining-custom-patterns-for-secret-scanning" target="_blank">Defining custom patterns for secret scanning</a>
    - **Gitleaks**
        - <a href="https://github.com/zricethezav/gitleaks" target="_blank">Gitleaks scanning tool</a>
        - <a href="https://github.com/marketplace/actions/gitleaks-scanner" target="_blank">GitHub Action for Gitleaks</a>
        - <a href="https://github.com/zricethezav/gitleaks#configuration" target="_blank">Your own secret detection rules for Gitleaks</a>
        - <a href="https://github.com/zricethezav/gitleaks#configuration" target="_blank">Gitleaks suppressing false positives with allow patterns</a>
        - <a href="https://docs.github.com/en/code-security/code-scanning/integrating-with-code-scanning/uploading-a-sarif-file-to-github" target="_blank">Uploading a SARIF file to GitHub</a>

### Secret Rotation

- <a href="https://docs.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation" target="_blank">Automate the rotation of a secret for resources that use one set of authentication credentials</a>
- <a href="https://docs.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation-dual?tabs=azure-cli" target="_blank">Automate the rotation of a secret for resources that have two sets of authentication credentials</a>

### DevSecOps (takeaways after the event)

- <a href="https://azure.microsoft.com/en-us/resources/6-tips-to-integrate-security-into-your-devops-practices/" target="_blank">6 tips to integrate security into your DevOps practices</a>
- <a href="https://resources.github.com/downloads/GitHub-eBook-Built-in-Security-Demo-Day-Promo.pdf" target="_blank">GitHub e-Book DevSecOps</a>
