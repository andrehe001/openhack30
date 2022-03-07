# DevOps OpenHack - Changelog

## Purpose

This document aims to highlight significant changes to the OpenHack over time.
Add a section with the release date/version for each significant content refresh and summarize the fundamental changes as a bulleted list.

## v3.0.0 [Feb 14th, 2022]

### General

Challenges contain GitHub naming convention, e.g., workflow instead of pipeline. This is to give the impression that GitHub is the 1st choice platform (aligned with the current Microsoft Sales & Marketing strategy).

### Lab environment provisioning / BYOS

Any resources pre-provisioning and environment pre-configuration have been deprecated. Instead, teams during the OpenHack are responsible for setting the initial setup configuration based on the BYOS deployment guide and scripts. BYOS deployment scripts and guide contains GitHub and Azure DevOps configuration.

### YAML approach

The classic UI approach for building Azure DevOps Pipelines has been deprecated. Instead, YAML is the only choice for building GitHub Workflows and Azure DevOps Pipelines.

### Jenkins

Jenkins is no longer available for pickup as a learning path. Only GitHub and Azure DevOps learning paths are available.

### Challenge 1: Establish your plan

Challenge 1 has been enhanced and added a hands-on experience for basic task board custom configuration.

### Challenge 2: Setting up the Development Workflow

Challenge 2 has adjusted to the common approach available on both platforms. For example, "linked work item enforcement" is not currently available on GitHub, so the challenge success criteria were confusing for attendees and not achievable in the standard approach. This point has been replaced with "flat history" in the PR.

### Challenge 3: Deploy Cloud Infrastructure with Infrastructure as Code (IaC)

It is a new Challenge to introduce the Infrastructure as Code (IaC) concept. The challenge contains two options for choosing based on the team's learning needs - Terraform and Bicep.

### Challenge 4: Implement Continuous Integration (CI) with Testing

This is old Challenge 3, a bit adjusted and refreshed without big changes. Added feature to show how to automatically report custom comments to the PR/Issue based on workflow behavior.

### Challenge 5: Implement Continuous Deployment (CD)

This is old Challenge 4, slightly adjusted and refreshed without big changes. Added optional extended challenge for GitHub learning path - GitHub Packages as Container Registry instead of Azure Container Registry.

### Challenge 6: Implement a Blue/Green deployment strategy

This is old Challenge 5. The concept remains the same, but the approach for health checks has changed from custom code to platform-native solutions.

### Challenge 7: DevSecOps basics – get rid of secrets

It is a new Challenge to introduce DevSecOps basics. The goal is to use secret scanning tools to discover hardcoded secrets in the source code. Then, remediate it by implementing secure storage to pull secrets (Key Vault) and next remove them from the source code.

The challenge contains an optional extended challenge to implement a secret rotation strategy for Azure SQL Server.

### Challenge 8: Integrating quality and security checks

This is old Challenge 7, slightly adjusted and refreshed without big changes. Load Testing moved to Challenge 9.

### Challenge 9: Implement a Load Testing & Monitoring solution with alerting

This is old Challenge 6. There are no significant changes in the Monitoring area. Added Azure Load Test service for the load testing scenario.

### Challenge 10: Implement phased rollout with rollback

This is old Challenge 8. There are no significant changes.

## v2.0.0

- Kubernetes has been deprecated and replaced by App Service for the application hosting platform.
- Added GitHub as 3rd option (not fully supported yet)

## v1.0.1

- Use of a container to provision the infrastructure used during the OpenHack
- Helm charts refactored to enable the use of helm package for the API. [@mathieu-benoit](https://github.com/mathieu-benoit)
- Helm charts refactored to include B/G support using labels/selectors.
- Replaced monitoring infrastructure with polling scripts to be run by the attendees (powershell and bash).
- Emphasise the use of YAML for pipelines in the challenge resources.

## v1.0.0

- Initial release as of December 2018
