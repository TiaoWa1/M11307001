<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>README：安裝 Docker、kubectl 與 Minikube</title>
  <style>
    body {
      font-family: "Segoe UI", sans-serif;
      background-color: #f9f9f9;
      padding: 2rem;
      line-height: 1.6;
    }
    h1, h2 {
      color: #2c3e50;
    }
    pre {
      background-color: #eee;
      padding: 1rem;
      border-radius: 5px;
      overflow-x: auto;
    }
    code {
      color: #c7254e;
    }
  </style>
</head>
<body>
  <h1>Ubuntu 安裝指南：Docker、kubectl 與 Minikube</h1>

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

  <p>安裝完成後，您即可在本機啟動 Kubernetes 環境。</p>
</body>
</html>
