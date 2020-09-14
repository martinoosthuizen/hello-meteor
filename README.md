# hello-meteor

Docker image for a meteor test app (ie on Kubernetes).

This is a minimal MeteorJS app, built on the geoffreybooth/meteor-base image.
It's useful as a typical "Hello World" app for testing docker or kubernetes deployments.

Docker run example:
`docker run -e ROOT_URL=http://localhost -e PORT=3000 goodworxsmooth/hello-meteor`

YAML Example:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: meteor-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: meteor-app
  template:
    metadata:
      labels:
        app: meteor-app
    spec:
      containers:
        - name: meteor
          image: goodworxsmooth/hello-meteor
          ports:
            - containerPort: 3000
              protocol: TCP
          env:
            - name: PORT
              value: "3000"
            - name: ROOT_URL
              value: https://YOURURLHERE
      imagePullSecrets:
        - name: regcred
```
