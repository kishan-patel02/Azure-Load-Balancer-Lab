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
- Use `curl` to verify alternation:  
```bash
- Screenshots:https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/33d2cb78f00d755a16b4d906563805781834019b/screenshots%20/Load-Balancing-Vm1.png
- Screenshots:https://github.com/kishan-patel02/Azure-Load-Balancer-Lab/blob/33d2cb78f00d755a16b4d906563805781834019b/screenshots%20/Load-Balancing-Vm2.png

