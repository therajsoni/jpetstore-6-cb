Perfect 👍 issue samajh aa gaya.

Tum 2 problems face kar rahe ho:

1. `<<EOF` syntax galat paste hua (isliye `deb command not found`)
2. Ubuntu 24.04 (noble) pe old Kubernetes repo (`kubernetes-xenial`) kaam nahi karega

---

# 🚨 Problem 1 — EOF Syntax Error

Tumne paste kiya:

```
sudo tee /etc/apt/sources.list.d/kubernetes.list &lt;&lt;EOF
```

⚠️ `&lt;&lt;` HTML escape hai.
Correct command hota hai:

```
<<EOF
```

Isliye bash error de raha tha:

```
bash: syntax error near unexpected token `;&'
```

---

# 🚨 Problem 2 — Ubuntu 24.04 (Noble)

Tumhare logs me aa raha hai:

```
noble InRelease
```

Matlab tum Ubuntu 24.04 use kar rahe ho.

Old repo:

```
deb https://apt.kubernetes.io/ kubernetes-xenial main
```

Ab deprecated hai.

---

# ✅ ✅ ✅ Correct Way To Install Kubernetes (2026 Working Method)

Kubernetes ne new repo system introduce kiya hai.

Run these commands exactly:

---

## STEP 1 — Required Packages

```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gpg
```

---

## STEP 2 — Add Kubernetes GPG Key (NEW METHOD)

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

---

## STEP 3 — Add Repository (Correct for Noble)

```bash
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

---

## STEP 4 — Install Kubernetes

```bash
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
```

---

## STEP 5 — Hold Versions (Important)

```bash
sudo apt-mark hold kubelet kubeadm kubectl
```

---

# ❌ DO NOT INSTALL

```
sudo snap install kube-apiserver
```

Ye galat hai.

`kube-apiserver` snap se install nahi karte.

Kubernetes cluster me `kubeadm` automatically apiserver setup karta hai.

---

# 🔥 If This Is Master Node

Next command:

```bash
sudo kubeadm init
```

---

# 🔥 If Worker Node

Use join command jo master se milega.

---

# 🎯 Why Tumhara Pehle Fail Hua?

1. HTML paste issue (`&lt;&lt;`)
2. Old kubernetes-xenial repo
3. apt-key deprecated
4. Snap method wrong

---

Ab ye new method run karo.

Agar error aaye to full output bhejna.

Next step me hum:

* containerd install
* swap disable
* kubeadm init

karne wale hain 🔥
