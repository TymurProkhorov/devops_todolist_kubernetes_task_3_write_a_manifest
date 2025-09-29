## Deployment instruction forTodoapp.

### 1. Docker image Build and push.
    - go to project folder with Dockerfile
    - build docker image:
        docker build . -t {your_name}/todoapp:3.0.0
    - login in docker hub:
        docker login
    - push the image to docker hub:
        docker push {your_name}/todoapp:3.0.0
### 2. K8s namespaces creating.
    - K8s namespaces creating:
        kubectl apply -f .infrastructure/namespace.yml
    - check if namespace was created:
        kubectl get ns
### 3. Deployment of test-pod.
    - Deployment of test-pod:
        kubectl apply .infrastructure/busybox.yml
    - check if test pod was created:
        kubectl get pods -n todoapp
### 4. Deployment of app pod.
    - Deployment of app pod:
        kubectl apply -f .infrastructure/todoapp-pod.yml
### 5. Todo app test.
    - port-forwarding:
        kubectl port-forward pod/todoapp 8081:8080 -n todoapp
    - via curl:
        kubectl exec -it busybox -n todoapp -- sh
        curl http://todoapp:8080/api/liveness/
        curl http://todoapp:8080/api/readiness/
    
    - to exit from busybox:
        exit
