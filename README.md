* Navigate to Openshift Cluster using below link:
  https://developers.redhat.com/courses/openshift/playground-openshift

* Login to cluster as developer,create a project and navigate into the project using below commands:
  oc login -u developer -p developer
  oc new-project <projectname>
  oc project myproject
  
* Run below command for root access in the pod:
  oc adm policy add-scc-to-user anyuid -z default -n myproject --as system:admin 

* Create a secret for accessing private image:
  oc create secret docker-registry secret --docker-server=https://index.docker.io/v1/ --docker-username=<username> --docker-password=<password> --docker-email=ihub448@gmail.com

* Navigate to helm chart directory and run below command to deploy backend pods on openshift
  helm install <name> <Backend-chart>
  
* Check the pod, service and route details using below command:
  oc get pods
  oc get service
  oc get route

* Navigate to frontend chart directory and add backend endpoints in data section of frontend-configmap.yaml file [Path: (frontend/templates/frontend-configmap.yaml)]. 
  Example: 

  data:
  search-uri: "http://backend-myproject.2886795305-80-kota02.environments.katacoda.com/"
  system-uri: "http://system-myproject.2886795305-80-kota02.environments.katacoda.com/"
  qna-uri: "http://demo-test-myproject.2886795305-80-kota02.environments.katacoda.com/prepare-qa?personal-number="
  question-uri: "http://demo-test-myproject.2886795305-80-kota02.environments.katacoda.com/questionnaire?"
  
* Deploy frontend pod using frontend chart. 
  helm install <name> <Frontend-chart>

* Then navigate to frontend route to view the application
