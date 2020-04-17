# Kubernetes
in progress

# Skaffold

## Developers' Problem

Kubernetes manage containers; containers run code. It takes complicated workflow for code to arrive into a container in Kubernetes cluster.

Typically, developers and devops
1. Write code
2. Run build
3. Compose container image, such as docker image
4. Publish image to resigstry
5. Create Kubernetes artifacts
6. "Apply" Kubernetes artifacts

Above tedious heavy duty workflow, drastically reduces developers' productivity.

Alternatively, developers can maintain local dev configuration, integration/qa, and production configuration. This solves productivity problem, but it also raise risks of environment disparities.

Skaffold is the rescue. Below are demo/sample Kubernetes projects with step by step instruction with Skaffold.

[Spring Boot Java Application](./skaffold/K8sSpringBootandSkaffoldJiB.md)

[NodeJS Web Application](./skaffold/K8sNodeJSandSkaffold.md)

## Beyond Developers' Problem

Skaffold is a tool for providing portability for CI integrations with different build system, image registry and deployment. It comes with basic capability for generating manifests. Skaffold is also extendible and lets user pick tools for use in each of the steps in building and deploying applications.

## References

https://kubernetes.io/blog/2018/05/01/developing-on-kubernetes/
