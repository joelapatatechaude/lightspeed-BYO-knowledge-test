# OpenShift usage policy

# Summary

This document lists all internal policy when interacting with the OpenShift cluster. Those policy should be followed. Any policy violation will be blocked by a Kyverno or ACM policy.

# CIS-Docker-4.6 \- Ensure HEALTHCHECK instruction has been added to container

Description: CIS Docker Benchmark 4.6: Ensure HEALTHCHECK instruction has been added to container image.  
Rationale: Health checks help ensure containers are running properly and enable automated recovery.  
Remediation: Add HEALTHCHECK instruction to Dockerfiles to monitor container health.

# CIS-K8s-5.7.2 \- Ensure that default service accounts are not actively used

Description: CIS Kubernetes Benchmark 5.7.2: Ensure default service accounts are  not actively used.  
Rationale: Default service accounts have broad permissions and should not be used by applications.  
Remediation: Create dedicated service accounts for applications with minimal required permissions.

# Deployments should have at least one ingress Network Policy

Description: Alerts if deployments are missing an ingress Network Policy.  
Rationale: Pods that lack ingress Network Policies have unrestricted reachability on the network and may be exposed to attacks  
Remediation: Create and apply an appropriate Network Policy of type ingress to all Deployments.

# Latest tag

Description: Alert on deployments with images using tag 'latest'  
Rationale: Using latest tag can result in running heterogeneous versions of code. Many Docker hosts cache the Docker images, which means newer versions of the latest tag will not be picked up.  
Remediation: Consider moving to semantic versioning based on code releases (semver.org) or using the first 12 characters of the source control SHA. This will allow you to tie the Docker image to the code.

# Required Annotation: Email

Description: Alert on deployments missing the 'email' annotation.  
Rationale: The 'email' annotation should always be specified so that issues with the deployment can quickly be routed to the proper party.  
Remediation: Redeploy your service and set the 'email' annotation as your email or your team's email.

# Require Annotations

Define and use annotations that identify semantic attributes of your application or Deployment. A common set of annotations allows tools to work collaboratively, describing objects in a common manner that all tools can understand. The recommended annotations describe applications in a way that can be queried. This policy validates that the annotation \`corp.org/department\` is specified with some value.

# Enforce Istio Sidecar Injection

In order for Istio to inject sidecars to workloads deployed into Namespaces, the label \`istio-injection\` must be set to \`enabled\`. This policy ensures that all new Namespaces set \`istio-inject\` to \`enabled\`.

# Disallow Secrets from Env Vars

Secrets used as environment variables containing sensitive information may, if not carefully controlled, be printed in log output which could be visible to unauthorized people and captured in forwarding applications. This policy disallows using Secrets as environment variables.

# Require TLS routes in OpenShift

HTTP traffic is not encrypted and hence insecure. This policy prevents configuration of OpenShift HTTP routes.

# Require NetworkPolicy

NetworkPolicy is used to control Pod-to-Pod communication and is a good practice to ensure only authorized Pods can send/receive traffic. This policy checks incoming Deployments to ensure they have a matching, preexisting NetworkPolicy.

