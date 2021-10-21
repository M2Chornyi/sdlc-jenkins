# Development Lifecycle
- Utilize our sample application (th3-server.py inside [th3.zip](https://volskayaindustries.com/th3.zip)) and create a simple `blue/green` 
deployment strategy using the method/technology of your choosing. It is not required to have any 
endpoints exposed for us to examine but we would love to see your code and documentation in your 
Github repo. _Feel free to use local resources_ (VMs, Minikube, etc.) to `test` and `demonstrate` your work. 
Using public cloud technology under their free tier is also fine!
    - Start v1 of the application
    - Write a simple test client to call {service_base_url}/version repeatedly
    - Update the version of the sample application
    - Utilize your deployment strategy to execute a blue/green deploy of test application v2
    - Capture the output of your test client to show that no requests failed and the version being returned from
      the sample application changed
 
## TASKS:
Setup `blue/green` deployment.

---
Requirements:
- Kubernetes cluster
- Jenkins
  - Node requirement:
    - Kubernetes access
    - Helm installed
    - Docker installed
---
WORKFLOW:
1. Build docker image
2. Create customer facing service
3. Provision resources using kubernetes+docker image
4. Test resources 
5. Flip if needed

    
