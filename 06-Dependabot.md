## Dependabot
Dependabot is a crucial tool in DevSecOps, designed to automatically identify and fix security vulnerabilities in the packages used by your applications.
It constantly monitors your repository's package files (like go.mod, pom.xml, npm packages, make file or Docker-related packages) and compares them against a vulnerability database.
If a vulnerable package version is detected, Dependabot automatically creates a pull request to update the version in your repository, often within minutes of a vulnerability being disclosed. It can even merge these pull requests automatically, ensuring rapid remediation.

This is an example dependabot yaml file from argocd-controller
```yaml
version: 2
updates:
  - package-ecosystem: "gomod"
    directory: "/"
    schedule:
      interval: "daily"
    open-pull-requests-limit: 10

  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"

  - package-ecosystem: "docker"
    directory: "/"
    schedule:
      interval: "daily"

  - package-ecosystem: "docker"
    directory: "/build/"
    schedule:
      interval: "daily"

  - package-ecosystem: "docker"
    directory: "/build/util/"
    schedule:
      interval: "daily"

  - package-ecosystem: "docker"
    directory: "/deploy/registry/"
    schedule:
      interval: "daily"

  - package-ecosystem: "docker"
    directory: "/tests/auxiliary/smtplistener/"
    schedule:
      interval: "daily"
```