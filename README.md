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
<h2>四、設計前端頁面
  <pre><code>
&lt;!DOCTYPE html&gt;
&lt;html lang="zh-Hant"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8" /&gt;
  &lt;title&gt;學號頁面&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;我的學號&lt;/h1&gt;
  &lt;div class="student-id"&gt;M11307001&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;
  </code></pre>
