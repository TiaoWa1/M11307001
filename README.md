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
<h2>四、將前端頁面與Dockerfile建立完成</h2>
<p>Docker File:</p>
  <pre><code>FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html</code></pre>

<h2>五、建立映像與上傳至 Docker Hub</h2>
<p>使用下列指令將前端頁面包成映像檔並推送到 Docker Hub：</p>
<pre><code>docker build -t tiaowa8165/id-app .
docker tag tiaowa8165/id-app tiaowa8165/id-app:latest
docker push tiaowa8165/id-app:latest</code></pre>

<h2>六、部署應用與建立服務</h2>
<p>透過以下指令，將部署設定 <code>deployment.yaml</code> 和服務設定 <code>service.yaml</code> 套用至 Kubernetes 叢集中：</p>

![image](https://github.com/user-attachments/assets/b91c4543-acbc-4723-bd09-830c3a35372b)

<p>本地測試成功</p>

![image](https://github.com/user-attachments/assets/99b67bbf-8745-4375-bb4e-769388647085)

![image](https://github.com/user-attachments/assets/6d3bf552-0ad2-4875-8c2a-6a2c4c166bcb)

![image](https://github.com/user-attachments/assets/e1b9bae9-22c9-4c69-b8e9-8bb451dac4c3)

![image](https://github.com/user-attachments/assets/261d23f1-05d3-4b36-bccd-8a0c2fba0f03)
