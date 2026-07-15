# 🔑 AWS EC2 – Create a Key Pair

## 🎯 Objective

Create an RSA Key Pair named **`devops-kp`** in the **us-east-1** region.

## 🤔 Why do we need a Key Pair?

AWS EC2 instances are usually accessed using **SSH key pairs** instead of passwords.

A key pair consists of:

- 🔓 **Public Key** – Stored on the EC2 instance by AWS.
- 🔐 **Private Key** – Downloaded to my computer and kept secure.

When I connect to an EC2 instance, AWS verifies that my private key matches the public key before allowing access.

> **Never share or lose your private key.**


## 💻 What is EC2?

**EC2 (Elastic Compute Cloud)** is AWS's virtual server service.

It allows me to launch Linux or Windows servers in the cloud without owning physical hardware.

Common uses:
- 🌐 Host websites
- ⚙️ Run applications
- 🗄️ Host databases
- 🐳 Run Docker containers


## 🔑 Why RSA?

AWS supports multiple key types.

For this lab, I used **RSA**, which is widely supported and commonly used for SSH authentication.


## 📝 Lab Details

| Property | Value |
|----------|-------|
| Name | `devops-kp` |
| Type | RSA |
| Region | `us-east-1` |


# 🖥️ AWS Console Steps

1. Login to AWS Console.
2. Select **us-east-1** region.
3. Open **EC2 Dashboard**.
4. Go to **Network & Security → Key Pairs**.
5. Click **Create Key Pair**.
6. Enter:
   - Name: `devops-kp`
   - Type: **RSA**
   - Format: **.pem**
7. Click **Create Key Pair**.
8. The private key (`devops-kp.pem`) downloads automatically.


# 💻 AWS CLI

```bash
aws ec2 create-key-pair \
--key-name devops-kp \
--key-type rsa \
--region us-east-1 \
--query 'KeyMaterial' \
--output text > devops-kp.pem
```

### 📌 Command Breakdown

- `aws` → AWS CLI
- `ec2` → EC2 service
- `create-key-pair` → Creates a new key pair
- `--key-name` → Specifies the key pair name
- `--key-type rsa` → Creates an RSA key
- `--query 'KeyMaterial'` → Returns only the private key
- `> devops-kp.pem` → Saves the key to a `.pem` file

## 🌍 Real-World Use

Companies use key pairs to securely access Linux servers. Instead of sharing passwords, each engineer can have their own SSH key, making access more secure and easier to manage.

## 📚 Key Takeaways

- ✅ EC2 is a virtual server.
- ✅ Key Pairs provide secure SSH access.
- ✅ AWS stores the **public key**; I keep the **private key**.
- ✅ RSA is a common key type for SSH.
- ✅ Keep the `.pem` file safe and never share it.
