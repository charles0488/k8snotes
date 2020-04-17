# Develop A K8S Spring Boot Java Application with Skaffold and Jib

## Why Skaffold and Jib

Jib replaces heavy steps of building, packaging, image composing, and deploying Java application onto Kubernetes with "shortcut", therefore improves developers' productivity.

## Steps
1. Use https://start.spring.io to create spring boot project (at least with web dependency)
and add demo controller code, like following

```
package com.sap.mobile.skaffolddemo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class SkaffoldController {

    @GetMapping("/")
    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
        return String.format("Hello %s!", name);
    }
}
```

2. Edit pom.xml to add jib dependency

	in plugins section
  ```
			<plugin>
          		<groupId>com.google.cloud.tools</groupId>
          		<artifactId>jib-maven-plugin</artifactId>
          		<version>${jib.maven-plugin-version}</version>
        	</plugin>
```
    in properties section
```
    	<jib.maven-plugin-version>2.1.0</jib.maven-plugin-version>
```

3. Create k8s folder and add a yaml with content similar to followings

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: skaffolddemo
spec:
  selector:
    matchLabels:
      app: skaffolddemo
  template:
    metadata:
      labels:
        app: skaffolddemo
    spec:
      containers:
      - name: skaffolddemo
        image: skaffolddemo-jib
        ports:
          - containerPort: 8080
```
4. Run "skaffold init --XXenableJibInit" in project folder to generate skaffold.yaml

5. Add following to skaffold.yaml for port forwarding. This works like "kubectl port-forward <yourpod> 8080:8080"; Avoid using "kubectl port-forward" because every change results a new pod, therefore "kubectl port-forward" had to be started again

```
portForward:
  - resourceType: deployment
    resourceName: skaffolddemo
    port: 8080
    localPort: 8080
```

6. Make sure "image" used in skaffold.yaml and yaml in k8s folder are the same

7. Run "skaffold dev --trigger notify --port-forward". This performs
- push initial deployment to K8S
- watch changes of code and updates K8S deployment
- forward testing requests to K8S deployment

8. Run "watch curl localhost:8080" for testing; "Hello World" should be returned

9. Edit SkaffoldController.java like following
```
...
@RestController
public class SkaffoldController {

    @GetMapping("/")
    public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
        return String.format("Hello %s from Skaffold.", name);
    }
}
```
Right after saving changes, Kubernetes deployment should be updated very quickly

10. Verify "watch curl localhost:8080" should return something like "Hello World from Skaffold."
Note: with port forwarding, request to localhost:8080 is proxied to K8S deployment.

Additionally, "docker build" is not required for building docker image. Skaffold provides more efficient tool, i.e. jib. The build command is "mvn compile jib:dockerBuild"

## References:
https://medium.com/flant-com/skaffold-kubernetes-development-tool-2897d6903e02
https://skaffold.dev/docs/quickstart/
