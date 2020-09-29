


# Assignment



Simple spring boot app with an actuator endpoint which returns the health of the app with supporting code to run this on kubernetes. 

### App
- Basic spring boot app with inbuilt actuator endpoints exposed.
- Accept all requests under a context, example `hello`


### Project Structure
*Files / Folders*
 - deployment- All deployment related manifests
 - hello- Consists of spring boot source code
 - hello/Dockerfile - Dockerfile used for the build
 - hello/start.sh - Shell script used to run the app, along with conditional environmental variables to support debugging. Quirks to support graceful shutdown in a docker env.


### Build
- Docker build to package the app, [Dockerfile](https://github.com/nithindv/assignment-1/blob/master/hello/Dockerfile)
- Multistage docker build
- Cache maven dependencies in builder image; light alpine JRE for runtime

      cd hello
      docker build -t nithindv/hello:v1 .
      docker push nithindv/hello:v1



### Deploy
- Details available [here](https://github.com/nithindv/assignment-1/blob/master/deployment/README.MD) 
 
      cd deployment/hello
      helm dep update && helm template --set image.tag=v1 --set global.domain=abc.com . > tmp,yaml
      kubectl apply -f tmp.yaml


## Dependencies


- Docker

- Helm

- Kubectl

