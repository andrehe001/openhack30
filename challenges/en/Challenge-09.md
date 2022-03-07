# Challenge 9 - Implement a Load Testing & Monitoring solution with alerting

**Reminders:**

- Use an **InPrivate/Incognito** window in your browser to avoid any confusion with any other Azure credentials.
- Common references for your DevOps tool you can find under the **Cheat sheet** section.

---

## Challenge

Your challenge is to define and implement a Load Testing & Monitorin strategy for your APIs. First, carefully select the monitoring tool(s) you want to use.

You are expected to achieve the following goals:

- Implement a solution that performs Load Testing of your APIs.
- Implement a solution that monitors the health and performance of your APIs. You will have to collect data regarding the performance of your web applications and the APIs hosted in each web application.
- Define the performance baseline for the APIs running in Azure and implement a mechanism that will automatically raise an alert and create an incident in your work item tracking system if performance degradation is observed.
- Build a dashboard that will allow you to visualize the global health of your environment.

> **NOTE:**
>
> It is recommended to discuss the capabilities of the tools that you have selected with your team. Keep in mind that your coach is here to help you make an educated decision.
>
> A sample JMX (JMeter XML) file is provided in the resources section on the teams repo.

## Success Criteria

Show your coach Load testing solution and the aggregated view of your application and infrastructure that includes the following:

- Web application monitoring that displays the CPU utilization for each production web application
- The average response time is over 1 minute for each production web application
- A work item is created when API performance degradation is observed
- The top 10 queries by duration over the last 24 hours for the **mydrivingDB** database
- The percentage of DTU utilized on the **mydrivingDB** database

Show your coach that an incident is automatically created when an alert is raised.

## References

### Azure resources

- **Azure Load Testing**

    - <a href="https://docs.microsoft.com/en-us/azure/load-testing/overview-what-is-azure-load-testing" target="blank">What is Azure Load Testing?</a>
    - <a href="https://docs.microsoft.com/en-us/azure/load-testing/quickstart-create-and-run-load-test" target="blank">Create and run a load test with Azure Load Testing</a>
    - <a href="https://docs.microsoft.com/en-us/azure/load-testing/how-to-parameterize-load-tests" target="blank">Conduct configurable load tests with secrets and environment variables</a>
    - <a href="https://jmeter.apache.org/download_jmeter.cgi" target="blank">Apache JMeter</a>
    - <a href="https://docs.microsoft.com/en-us/azure/load-testing/tutorial-identify-bottlenecks-azure-portal" target="blank">Run a load test to identify performance bottlenecks in a web app</a>
    - <a href="https://docs.microsoft.com/en-us/azure/load-testing/tutorial-cicd-github-actions" target="blank">Identify performance regressions with Azure Load Testing and GitHub Actions</a>
    - <a href="https://docs.microsoft.com/en-us/azure/load-testing/tutorial-cicd-azure-pipelines" target="blank">Identify performance regressions with Azure Load Testing and Azure Pipelines</a>

- **Azure Monitor**

    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/overview" target="blank">Azure Monitor overview</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial" target="_blank">Log Analytics tutorial</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/monitor-azure-resource" target="_blank">Monitor Azure resources with Azure Monitor</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/app/azure-web-apps" target="_blank">Application Monitoring for Azure App Service</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/insights/azure-sql" target="_blank">Monitor Azure SQL Database using Azure SQL Analytics</a>
    - <a href="https://docs.microsoft.com/en-us/Azure/app-service/web-sites-monitor" target="_blank">Monitor apps in Azure App Service</a>
    - <a href="https://docs.microsoft.com/en-us/azure/app-service/faq-availability-performance-application-issues" target="_blank">Application performance FAQs for Web Apps in Azure</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings" target="_blank">Create diagnostic settings to send Azure Monitor platform logs and metrics to different destinations</a>
    - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-overview" target="_blank">Overview of alerts in Microsoft Azure</a>
    - <a href="hhttps://docs.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-log" target="_blank">Create, view, and manage log alerts using Azure Monitor</a>

- **Azure Logic Apps**

      - <a href="https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview" target="_blank">What is Azure Logic Apps?</a>
      - <a href="https://docs.microsoft.com/en-us/connectors/visualstudioteamservices/" target="_blank">Azure DevOps connector for Azure Logic Apps</a>
      - <a href="https://docs.microsoft.com/en-us/connectors/github/" target="_blank">GitHub connector for Azure Logic Apps</a>

- **Kusto documentation and references**:

      - The solutions in Azure will evolve to use <a href="https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/" target="_blank">Azure Data Explorer query language</a> (also know as <a href="https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/" target="_blank">Kusto Query Language (KQL)</a>)
      - Syntax for regular expressions supported by <a href="https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/re2" target="_blank">Azure Data Explorer</a>

- **Regular Expressions**

      - You can test your regular expression on this site: <a href="https://regexr.com/" target="_blank">RegExr: Learn, Build, & Test RegEx</a>
      - You can use regular expressions in the `extract()` function in Kusto. For example, this code will extract and convert to a double the response time from the container output showed above:

      ```sh
          todouble(extract(@"CreateTripPoint ([0-9.]*)ms", 1, LogEntry))
      ```

- **Application availability and responsiveness**
      - <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/app/monitor-web-app-availability#alerts" target="_blank">Availability alerts of any web site</a>
