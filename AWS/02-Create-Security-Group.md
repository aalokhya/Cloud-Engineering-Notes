# 🛡️ AWS EC2 – Create a Security Group

## 🎯 Objective

Create a Security Group named **`xfusion-sg`** in the **default VPC** with the following inbound rules:

| Property | Value |
|----------|-------|
| Name | `xfusion-sg` |
| Description | `Security group for Nautilus App Servers` |
| Region | `us-east-1` |
| HTTP | Port **80** from `0.0.0.0/0` |
| SSH | Port **22** from `0.0.0.0/0` |

## 🤔 Why do we need a Security Group?

A **Security Group** acts as a virtual firewall for an EC2 instance.

It controls **who can access the server** and **which ports are open**. Every EC2 instance must be associated with at least one Security Group.


## 🌐 What is a VPC?

A **Virtual Private Cloud (VPC)** is your own private network in AWS.

Security Groups are created inside a VPC and are used to protect resources such as EC2 instances.



## 📥 What is Inbound Traffic?

Inbound traffic refers to **requests coming into the EC2 instance**.

Examples:

- 🌐 HTTP (Port 80) → Users accessing a website.
- 🔐 SSH (Port 22) → Administrators connecting to the server.



## 📤 What is Outbound Traffic?

Outbound traffic refers to **requests leaving the EC2 instance**, such as:

- Accessing the internet.
- Connecting to a database.
- Calling another application or API.

By default, AWS allows all outbound traffic.



## 📝 AWS Console Steps

1. Log in to the AWS Console.
2. Select the **us-east-1** region.
3. Open **EC2 Dashboard**.
4. Navigate to **Network & Security → Security Groups**.
5. Click **Create Security Group**.
6. Enter:
   - Name: `xfusion-sg`
   - Description: `Security group for Nautilus App Servers`
   - VPC: **Default VPC**
7. Add the following inbound rules:
   - HTTP → Port **80** → Source: `0.0.0.0/0`
   - SSH → Port **22** → Source: `0.0.0.0/0`
8. Click **Create Security Group**.



## 📸 Screenshots

### Step 1 – Create Security Group

![Create Security Group](screenshots/1-security%20group.png)



### Step 2 – Configure the Security Group

![Security Group Configuration](screenshots/2-security%20group.png)



### Step 3 – Verify the Security Group

![Security Group Created](screenshots/3-security%20group.png)



## 💻 AWS CLI

### Create the Security Group

```bash
aws ec2 create-security-group \
--group-name xfusion-sg \
--description "Security group for Nautilus App Servers" \
--vpc-id <default-vpc-id>
```

### Allow HTTP (Port 80)

```bash
aws ec2 authorize-security-group-ingress \
--group-name xfusion-sg \
--protocol tcp \
--port 80 \
--cidr 0.0.0.0/0
```

### Allow SSH (Port 22)

```bash
aws ec2 authorize-security-group-ingress \
--group-name xfusion-sg \
--protocol tcp \
--port 22 \
--cidr 0.0.0.0/0
```



## 🌍 Real-World Example

Imagine a company hosts its website on an EC2 instance.

- Customers need access to the website, so **HTTP (Port 80)** is open.
- System administrators need to manage the server remotely, so **SSH (Port 22)** is open.

In production, SSH access is usually restricted to trusted IP addresses instead of being open to everyone.



## 📚 Key Takeaways

- ✅ Security Groups act as virtual firewalls.
- ✅ Every EC2 instance belongs to a VPC.
- ✅ Inbound rules control incoming traffic.
- ✅ Outbound rules control outgoing traffic.
- ✅ HTTP uses Port **80**.
- ✅ SSH uses Port **22**.
- ✅ `0.0.0.0/0` allows access from any IPv4 address.
