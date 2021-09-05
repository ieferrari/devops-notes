# DevSecOps
You cant implement the security audit at the end of the deploy cycle, because it often generates bottleneck in the production schedule.

The solution is to implement best security practices at every step of the CI/CD process:

* Security policies
  * training for best practices in develop and operation
  * check vulnerabilities for the used libraries
* automation tools for detecting security issues

 ¿ Backups?

* pre commit hooks
* source composition analysis (SCA)
* Static App Security Testing (SAST)
* Dynamic App Security Testing (DAST)
* Securtiy in infrastructure as Code
* Secret Management

## Security as Code

* automated security vulnerability and configuration scanning
* application security testing for custom code
* version control and tight management of infrastructure automation tools


## Blue/green Deployment

Using **infrastructure as code** you can implement some kind of A/B test with the new  changes, if something goes wrong you can go back to the previous state of code and architecture


## Chaos

"The best way to avoid failure is to fail constantly" Netflix
Netflix uses Simian Army

Chaos Monkey, randomly disconnects services in production to test the infrastructure resilience.
