# Develop A NodeJS Web Application with Skaffold

## Steps

1. Create app.js with following code

```
const http = require('http');
const os = require('os');

const hostname = os.hostname() || '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, undefined, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

Note: have to use undefined for hostname argument in server.listen(), otherwise empty result will be returned from K8S deployment.

2. Create package.json with "npm init", then update it like following content

```
{
  "name": "nodejsskaffold",
  "version": "1.0.0",
  "description": "nodejs skaffold demo",
  "main": "app.js",
  "scripts": {
    "production": "node app.js",
    "development": "node app.js"
  },
  "dependencies": {
    "express": "^4.16.4"
  },
  "devDependencies": {
    "nodemon": "^1.18.4"
  },
  "keywords": [
    "nodejs",
    "skaffold"
  ],
  "author": "charles.xu@sap.com",
  "license": "ISC"
}
```

3. Create package-lock.json, with content like this [example](./package-lock.json)

4. Test locally with commands "node app.js" and "watch curl localhost:3000"

5. Add Dockerfile with following content

```
FROM node:12.16.0-alpine3.10

USER node
RUN mkdir /home/node/app
WORKDIR /home/node/app

EXPOSE 3000
ARG ENV=production
ENV NODE_ENV $ENV
CMD npm run $NODE_ENV

COPY --chown=node:node package* ./
RUN npm ci
COPY --chown=node:node . .
```

6. Run "docker build -t node/nodejsskaffold ." to create docker image

7. Run docker image with "docker run -p 3000:3000 node/nodejsskaffold:latest", this does followings
- run docker container with above image
- proxy local port 3000 to container's port 3000 so that you can test it out from you desktop

8. Test the docker image with running "watch curl localhost:3000". The result is something like "Hello World". Remember to shutdown, i.e. "crtl + c", docker container to release port used.

9. Run "skaffold init" to create skaffold.yaml

10. Add following to skaffold.yaml for port forwarding. Avoid using "kubectl port-forward". "kubectl port-forward <yourpod> 8080:8080" has to re-started after every change since pod name changes for every code change (this is k8s behavior).

```
portForward:
  - resourceType: service
    resourceName: nodejsskaffold
    port: 3000
    localPort: 3000
```

11. Create k8s folder and add a yaml with content similar to followings

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodejsskaffold
spec:
  selector:
    matchLabels:
      app: nodejsskaffold
  template:
    metadata:
      labels:
        app: nodejsskaffold
    spec:
      containers:
      - name: nodejsskaffold
        image: nnodejsskaffoldimg
        ports:
        - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: nodejsskaffold
spec:
  ports:
  - port: 3000
    targetPort: 3000
  type: LoadBalancer
  selector:
    app: nodejsskaffold
```

12. make sure "image" used in skaffold.yaml and yaml in k8s folder are the same

13. Run "skaffold dev --port-forward". This will
- push you project to K8S
- watch changes of your code and update deployment

After K8S deployment is ready, "watch curl localhost:3000" shows "Hello World" again.

14. Edit app.js to make change to return "Hello World from Skafold" like following

```
......

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World from Skafold');
});

......
```

Right after saving changes, Kubernetes deployment should be updated very quickly

15. Verify "watch curl localhost:3000" returns "Hello World from Skaffold."
Note: with port forwarding, request to localhost:3000 is proxied to K8S deployment.


Reference:
https://github.com/GoogleContainerTools/skaffold/tree/master/examples/nodejs
https://skaffold.dev/docs/quickstart/
