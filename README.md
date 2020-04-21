# Kubernetes

### Kubernetes vs. Cloud Foundry

["Organizations that are planning to deploy across multiple CSPs will need PCF."](https://techolution.com/kubernetes-vs-pcf/)

["However, PCF also comes at a higher cost and technical challenges."](https://techolution.com/kubernetes-vs-pcf/)

["It’s not as easy finding people skilled in PCF compared to Kubernetes."](https://techolution.com/kubernetes-vs-pcf/)

["Kubernetes requires fewer resources than PCF to run."](https://techolution.com/kubernetes-vs-pcf/)

["CSPs, such as Google Cloud Platform (GCP), the CSP will typically offer its own Kubernetes services out-of-the-box."](https://techolution.com/kubernetes-vs-pcf/)

["Interestingly, even Pivotal is offering Kubernetes."](https://techolution.com/kubernetes-vs-pcf/)

[Almost all CF sponsors supports Kubernetes.](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257)

<a href="https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257">
Similarity:
<li>Both solutions use the idea of containers to isolate your application from the rest of the system.</li>
<li>Both Cloud Foundry and Kubernetes are designed to let you run either on public cloud infrastructure (AWS, Azure, GCP etc.), or on-prem using solutions such as VMWare vSphere.</li>
<li>Both solutions offer the ability to run in hybrid/multi-cloud environments, allowing you to spread your availability among different cloud providers and even split the workload between on-prem and public cloud.</li>
<li>Starting with the latest release of Pivotal Cloud Foundry, both solutions support Kubernetes as a generic container runtime.</li>
<br/>
</a>

["Both platforms support the ability to deploy applications with zero downtime, however this is one area where Kubernetes wins in my opinion, since it provides a built-in mechanism for zero downtime deployments with rollback."](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257)

["With Kubernetes, you can make load-balanced http calls to any Kubernetes service that exposes pods, regardless of the implementation of the client or the server."](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257)

["Kubernetes does not offer a marketplace out of the box. There is a service catalog extension that allows for a similar service catalog, however it is still in beta."](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257)

["In Kubernetes, you can still run a config server as a container, but that would probably become an unneeded operational overhead since you already have built-in support for ConfigMaps. "](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257)

["A big differentiator of Kubernetes is the ability to attach a storage volume to your container."](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers-perspective-6d40a911f257)

["Getting started with Kubernetes was not easy."](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers)

["Game of cloud technologies: Kubernetes vs. Cloud Foundry"](https://blog.overops.com/pivotal-cloud-foundry-vs-kubernetes-choosing-the-right-cloud-native-application-deployment-platform/)

["Kubernetes is a lower-level abstraction in the PaaS world meaning greater flexibility to implement customizations and build your containers to run how you want them to run. Unfortunately, this also means more work for your engineering teams and decreased productivity."](https://medium.com/@odedia/comparing-kubernetes-to-pivotal-cloud-foundry-a-developers)

["Today, Kubernetes is the natural choice for running software in the Cloud."](https://kubernetes.io/blog/2018/05/17/gardener/)


![Interests in Cloud Foundry vs. Kubernetes](https://i.stack.imgur.com/wUjyt.png)


### References

https://blog.overops.com/pivotal-cloud-foundry-vs-kubernetes-choosing-the-right-cloud-native-application-deployment-platform/
https://developer.ibm.com/technologies/containers/blogs/game-of-cloud-technologies-kubernetes-vs-cloud-foundry/


# Skaffold

### Developers' Problem

Kubernetes manage containers; containers run code. It takes complicated workflow for code to arrive into a container in Kubernetes cluster.

Typically, developers and devops
1. Write code
2. Run build
3. Compose container image, such as docker image
4. Publish image to registry
5. Create Kubernetes artifacts
6. "Apply" Kubernetes artifacts

Above tedious heavy duty workflow, drastically reduces developers' productivity.

Alternatively, developers can maintain local dev configuration, integration/qa, and production configuration. This solves productivity problem, but it also raise risks of environment disparities.

Skaffold is the rescue. Below are demo/sample Kubernetes projects with step by step instruction with Skaffold.

[Spring Boot Java Application](./skaffold/K8sSpringBootandSkaffoldJiB.md)

[NodeJS Web Application](./skaffold/K8sNodeJSandSkaffold.md)

### Beyond Developers' Problem

Skaffold is a tool for providing portability for CI integrations with different build system, image registry and deployment. It comes with basic capability for generating manifests. Skaffold is also extendible and lets user pick tools for use in each of the steps in building and deploying applications.

### References

https://kubernetes.io/blog/2018/05/01/developing-on-kubernetes/


# Gardener

["The more clusters you need the harder it becomes to operate, monitor, manage, and keep all of them alive and up-to-date."](https://kubernetes.io/blog/2018/05/17/gardener/)

["At SAP, we face this heterogeneous multi-cloud & on-premise challenge not only in our own platform, but also encounter the same demand at all our larger and smaller customers implementing Kubernetes & Cloud Native."](https://kubernetes.io/blog/2018/05/17/gardener/)

[Gardener provides a central dashboard for comfortable interaction comparing with kubectl, which is CLI for Kubernetes.](https://www.youtube.com/watch?v=1IvTJwtKq-I&t=570s)

[Gardener runs as a dedicated Kubernetes cluster (called "garden" cluster) for creating and managing users' Kubernetes clusters (called shoot cluster).](https://www.youtube.com/watch?v=1IvTJwtKq-I&t=570s)

### References

https://kubernetes.io/blog/2018/05/17/gardener/
