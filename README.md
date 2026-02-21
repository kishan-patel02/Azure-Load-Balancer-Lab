# Azure Load Balancer Lab

This lab demonstrates how to create **two VMs**, install web servers on them, and configure **Azure Load Balancer** to distribute traffic between them.  

---

## **Lab Steps**

### 1️⃣ Create VMs
- Created **VM1** and **VM2** in Azure.  
- Installed a basic web server (IIS on Windows).  
- Screenshots:
[Azure-Load-Balancer-Lab/screenshots
/Webserver-Install.png](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/93e824a3a77c383e090a9fbcdae8eb634fa684f6/screenshots%20/Webserver-Install.png)

---

### 2️⃣ Install Web Server
- VM1: Returned `"VM1"` on homepage  
- VM2: Returned `"VM2"` on homepage  
- Purpose: Easily identify which VM serves a request  

---

### 3️⃣ Configure Azure Load Balancer
**Backend Pool**  
- Added both VM1 and VM2 to the backend pool    

**Load Balancing Rule**  
- Protocol: TCP  
- Port: 80 (HTTP)  
- Backend pool: VM1 + VM2  
- Health probe: HTTP, port 80, path `/`  

**Inbound NAT Rules** (Optional for RDP/SSH)  
- Forward specific ports to VM1 and VM2 for direct access    

**Outbound SNAT Rules**  
- Ensure VMs can access the internet using the LB's public IP  

---

### 4️⃣ Testing Load Balancer
- From terminal or browser, access the **LB public IP**: `http://<LB_PIP>`  
- Should see `"VM1"` and `"VM2"` alternately if **round-robin** is used.  
- Screenshots:[Azure-Load-Balancer-Lab/screenshots
/Load-Balancing-Vm2.png](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/33d2cb78f00d755a16b4d906563805781834019b/screenshots%20/Load-Balancing-Vm1.png)
- Screenshots: [Azure-Load-Balancer-Lab/screenshots
/Load-Balancing-Vm1.png](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/33d2cb78f00d755a16b4d906563805781834019b/screenshots%20/Load-Balancing-Vm2.png)



5️⃣ Configure Azure Application Gateway (Layer 7 Load Balancing)

In this section, we configure an Azure Application Gateway instead of a Load Balancer to handle HTTP traffic at Layer 7 with intelligent routing.

Create Application Gateway

Selected existing VNet

Chose dedicated subnet for Application Gateway

Assigned Public IP

SKU: Standard_v2

Enabled HTTP listener on port 80

Screenshot:[Azure-Load-Balancer-Lab/screenshots
/ApplicationGW-Creation.png](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/5eb420eb085240966dbd7dbf6bb8291b89e16734/screenshots%20/ApplicationGW-Creation.png)


Backend Pool Configuration

Added VM1 and VM2 private IP addresses to backend pool
Backend Settings (HTTP Settings)

Protocol: HTTP

Port: 80

Cookie-based affinity: Disabled

Health probe: Default or custom probe /



Routing Rule Configuration

Created Basic routing rule

Listener: HTTP (Port 80)

Target backend pool: VM1 + VM2

Associated HTTP settings

Screenshot:[Azure-Load-Balancer-Lab/screenshots
/ApplicationGW-RoutingRule.png
](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/5eb420eb085240966dbd7dbf6bb8291b89e16734/screenshots%20/ApplicationGW-RoutingRule.png)


Testing Application Gateway

Access the Application Gateway Public IP:
http://<AppGW_PIP>

You should see responses alternating between "VM1" and "VM2".

Screenshot:[Azure-Load-Balancer-Lab/screenshots
/Application-Gateway-Webserver1.png](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/5eb420eb085240966dbd7dbf6bb8291b89e16734/screenshots%20/Application-Gateway-Webserver1.png)

Screenshot:[Azure-Load-Balancer-Lab/screenshots
/Aaplication-Gateway-Webserver2.png
](https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/5eb420eb085240966dbd7dbf6bb8291b89e16734/screenshots%20/Aaplication-Gateway-Webserver2.png)
