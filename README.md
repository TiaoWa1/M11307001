<a href="https://hub.docker.com/r/tiaowa8165/id-app/tags" target="_blank">🐳 映像檔</a>


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

<h2>七、EC2 上設置 iptables 讓外網連得進來</h2>
<pre><code>
  
# 1. 將外部 port 80 導向 Minikube VM
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.49.2:30007

# 2. 讓回傳封包能順利出去
sudo iptables -t nat -A POSTROUTING -j MASQUERADE

# 3. 放行封包穿越主機
sudo iptables -A FORWARD -p tcp -d 192.168.49.2 --dport 30007 -j ACCEPT

# 4. 新增傳入規則
![image](https://github.com/user-attachments/assets/e1b9bae9-22c9-4c69-b8e9-8bb451dac4c3)

# 5. 連線http://<EC2公有ip>
![image](https://github.com/user-attachments/assets/9dad7bdb-514e-4504-a946-2a209a2968da)

</code></pre>

兩個複本

![image](https://github.com/user-attachments/assets/334c13ed-e090-44cc-9868-de967859f764)

![image](https://github.com/user-attachments/assets/7c6d74c5-1c5f-46ec-b80e-5a96a2f826d4)
