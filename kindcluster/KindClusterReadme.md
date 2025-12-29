Installing and Using Kind Cluster
This repository provides documentation and scripts to install and use a Kind (Kubernetes in Docker) cluster for local development and testing.

📘 Installation Steps
1. Create Installation Script
vim install_kind.sh
	• Opens a new file install_kind.sh in Vim editor.
	• Script typically contains commands to install Kind and kubectl.
2. Make Script Executable
chmod +x install_kind.sh
⚠️ Best practice: use chmod +x instead of 777 for security.
3. Run Installation Script
./install_kind.sh
Executes the script to install Kind and kubectl.
4–8. Install Docker
sudo apt-get update
sudo apt-get install docker.io
	• Updates package lists and installs Docker.
	• Docker is required because Kind runs Kubernetes nodes as Docker containers.
9. Verify Docker
docker ps
Lists running containers. If Docker is installed correctly, this should work without errors.
10–11. Add User to Docker Group
sudo usermod -aG docker $USER && newgrp docker
	• Adds your user to the docker group so you can run Docker without sudo.
	• newgrp docker refreshes group membership immediately.
12–13. Verify Docker Installation
docker ps
docker --version
Confirms Docker is installed and running.
14–16. Verify kubectl Installation
kubectl --version
kubectl version
Ensures kubectl is installed and can talk to clusters.
17–18. Verify Kind Installation
kind --version
Confirms Kind is installed.
19–21. Prepare Cluster Config
mkdir kindcluster
cd kindcluster/
vim config.yml
Creates a directory for cluster configs. config.yml defines cluster settings (e.g., number of nodes, roles).
Example config.yml:
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
22–25. Create Cluster
kind create cluster --config config.yml --name tws-kind-cluster
Creates a Kind cluster named tws-kind-cluster using the config file. Each node is a Docker container.
26–28. Interact with Cluster
kubectl cluster-info --context kind-tws-kind-cluster
kubectl get nodes
kubectl cluster-info
	• cluster-info: Shows API server and DNS details.
	• get nodes: Lists all nodes (control-plane + workers).
	• Confirms cluster is running.
29. Delete Cluster
kind delete cluster --name my-kind-cluster
Deletes the specified Kind cluster. Useful for cleanup.
30. View Command History
history
Displays all commands executed in the session.

🚀 Workflow Summary
	1. Install Docker → verify.
	2. Install kubectl & Kind → verify.
	3. Create config → launch cluster.
	4. Use kubectl to interact with cluster.
	5. Delete cluster when done.

✅ Best Practices
	• Use non-root permissions for Docker (usermod -aG docker).
	• Keep cluster configs modular (separate YAML files for dev/test).
	• Automate with scripts for CI/CD pipelines.
	• Always clean up clusters to free resources.

This README provides a complete guide to installing and using Kind clusters for local Kubernetes development.

