```
apt update
apt upgrade -y
apt install ca-certificates curl

install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc

tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

apt update
apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

usermod -aG docker ubuntu

apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.35/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.35/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
apt-get update

apt-get install -y kubelet kubeadm kubectl
apt-mark hold kubelet kubeadm kubectl


curl -L https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.21/cri-dockerd_0.3.21.3-0.debian-bookworm_amd64.deb -O
dpkg -i cri-dockerd_0.3.21.3-0.debian-bookworm_amd64.deb 

kubeadm init --cri-socket unix:///var/run/cri-dockerd.sock


curl -O https://raw.githubusercontent.com/projectcalico/calico/v3.28.3/manifests/calico.yaml


kubectl apply -f calico.yml


kubeadm join 172.xxx.xxx.xxx:6443 --cri-socket unix:///var/run/cri-dockerd.sock --token yyyyyyyyyyyyyyyyyy --discovery-token-ca-cert-hash sha256:zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz

kubectl label node ip-172-xxx-xxx-xxx node-role.kubernetes.io/worker=worker


mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config


export KUBECONFIG=/etc/kubernetes/admin.conf


apt install bash-completion

cat >> .bashrc <<EOF
source <(kubectl completion bash)
alias k=kubectl
complete -o default -F __start_kubectl k
EOF


sudo apt-get install curl gpg apt-transport-https --yes
curl -fsSL https://packages.buildkite.com/helm-linux/helm-debian/gpgkey | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/helm.gpg] https://packages.buildkite.com/helm-linux/helm-debian/any/ any main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm


watch 'echo --- PODS && kubectl get pod -o wide && echo \\n--- DEPLOYMENTS && kubectl get deploy -o wide && echo \\n--- STATEFUL SETS && kubectl get statefulset -o wide && echo \\n--- SERVICES && kubectl get svc -o wide && echo \\n--- PERSISTENT VOLUME CLAIMS && kubectl get pvc -o wide && echo \\n--- PERSISTENT VOLUMES && kubectl get pv && echo \\n--- NODES && kubectl get node'
```
