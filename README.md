Part 1:
Given the attached app.py, please do the following:
1. Write a Dockerfile to package this flask Application as a container.
2. Write the necessary Kubernetes manifests to deploy this container as a web application.
3. Incorporate a dummy URL this application would respond on.
Requirements:
    - Treat this as introducing a new application into an already existing Kubernetes cluster that already has a number of other web applications deployed. The Kubernetes files should be designed with Production quality, High Availability, and Scalability in mind.
    - Do not affix the Application Pod to a static port on the host.
    - Reproducibility. Use the most efficient cloud costs management approach when creating your manifests in case the company decides to create 20 additional similar applications.

Part 2:
1. In a few words, describe how you provision cloud infrastructure from scratch to host this application with High Availability in mind. (Output should not be code, but a description in your own words). Some topics you might want to include:
  - Cloud of choice
  - Infrastructure design and components
  - Automation and deployment Tools
2. In a few words, describe how you would create a continuous delivery pipeline to automatically build and deploy this application to dev --> int --> uat --> prod environments with every Git push. (Output should not be code, but a description in your own words). Some topics you might want to include:
  - CI/CD tool of choice and setup
  - Procedural build steps
  - Procedural deployment steps
The output of this test would be a zip containing a Dockerfile, a set of yaml files, and text files as appropriate.




###
First of all, I'm going to use Terraform for provisioning the Cloud Infrastructure. So, basically if I'm going to use the containers, I'm going to need a container orchestration tool. So, I'm going to build an EKS Cluster and its good because AWS is going to be responsible for updating my Master Nodes, and I'm going to be responsible for updating the Worker Nodes.

 For the automation & deployment, I'm going to use Jenkins.  I'm going to build a CI/CD pipeline. I will configure GitHub Webhook so if I am going to do any changes to my repo it will trigger a job and build new Docker image. So after new image with new version of application is build, my pipeline will deliver that image to Nexus Artifactory and then second pipeline will take image from Nexus and make deployment on Kubernetes.