[![CircleCI](https://circleci.com/docs/assets/img/docs/svg-passed.png)](https://app.circleci.com/pipelines/github/hatn381/Depops_project4?branch=main)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API.

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:

- Test your project code using linting
- Complete a Dockerfile to containerize this application
- Deploy your containerized application using Docker and make a prediction
- Improve the log statements in the source code for this application
- Configure Kubernetes and create a Kubernetes cluster
- Deploy a container using Kubernetes and make a prediction
- Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

- Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv.

```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host.
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```

- Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone: `python app.py`
2. Run in Docker: `./run_docker.sh`
3. Run in Kubernetes: `./run_kubernetes.sh`

### Kubernetes Steps

1. Setup and Configure Docker locally

   - Set up the stable repository
     $ sudo add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"
   - Install the latest version of Docker CE
     $ sudo apt-get install docker-ce
   - Install hadolint
     $ sudo wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/ hadolint-Linux-x86_64

     $ sudo chmod +x /bin/hadolint

2. Setup and Configure Kubernetes locally

   # MINIKUBE

   - Install Minikube dependencies
     $ sudo apt install -y curl wget apt-transport-https
   - Download Minikube Binary
     $ wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

   - Copy it to the path /usr/local/bin
     $ sudo cp minikube-linux-amd64 /usr/local/bin/minikube
   - Set the executable permissions
     $ sudo chmod +x /usr/local/bin/minikube
   - Verify the minikube version
     $ minikube version

   # Kubectl

   - Download latest version of kubectl
     $ curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
   - Set the executable permissions
     $ chmod +x kubectl
   - Move it to the path /usr/local/bin
     $ sudo mv kubectl /usr/local/bin/
   - Verify the kubectl version
     $ kubectl version -o yaml

3. Create Flask app in Container
   - Update run_docker.sh file
   - Run "./run_docker.sh" to build and start the Flask app container.
   - Run "./make_prediction.sh" to make prediction and copy/paste the logging info at terminal to output_txt_files/docker_out.txt
   - Update upload_docker.sh
   - Run "./upload_docker.sh" to upload the container to docker hub.
4. Run via kubectl

   - Configure Kubernetes to Run Locally
     $ minikube start
   - Check cluster running(certificate-authority and server)
     $ kubectl config view
   - Update run_kubernetes.sh
   - Run "./run_kubernetes.sh"
   - Run "kubectl get pod" to get pod (waiting to status is Running)
   - Update pod into run_kubernetes.sh
   - Run "./run_kubernetes.sh" again
   - Run "./make_prediction.sh" to make predictions and check logs

5. Delete Cluster
   $ minikube delete
