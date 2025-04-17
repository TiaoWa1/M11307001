  <h2>一、安裝 Docker</h2>
  <pre><code>sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl
sudo apt install -y docker.io
sudo usermod -aG docker $USER
newgrp docker
</code></pre>

  <h2>二、安裝 kubectl</h2>
  <pre><code>curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client --output=yaml
</code></pre>

  <h2>三、安裝 Minikube</h2>
  <pre><code>curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
minikube version
minikube start --driver=docker
</code></pre>
<h2>四、前端頁面與Dockerfile</h2>
  <pre><code>FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
  </code></pre>

<h2>五、建立映像與上傳至 Docker Hub</h2>
<p>使用下列指令將前端頁面包成映像檔並推送到 Docker Hub：</p>
<pre><code>docker build -t tiaowa8165/id-app .
docker tag tiaowa8165/id-app tiaowa8165/id-app:latest
docker push tiaowa8165/id-app:latest
</code></pre>

