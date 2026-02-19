# Azure Load Balancer Lab

This lab demonstrates how to create **two VMs**, install web servers on them, and configure **Azure Load Balancer** to distribute traffic between them.  

---

## **Lab Steps**

### 1️⃣ Create VMs
- Created **VM1** and **VM2** in Azure.  
- Installed a basic web server (IIS on Windows).  
- Screenshots:screenshots /Webserver-Install.png

---

### 2️⃣ Install Web Server
- VM1: Returned `"VM1"` on homepage  
- VM2: Returned `"VM2"` on homepage  
- Purpose: Easily identify which VM serves a request  

---

### 3️⃣ Configure Azure Load Balancer
**Backend Pool**  
- Added both VM1 and VM2 to the backend pool  
- Screenshot:  
  ![Backend Pool](screenshots/backend-pool.png)  

**Load Balancing Rule**  
- Protocol: TCP  
- Port: 80 (HTTP)  
- Backend pool: VM1 + VM2  
- Health probe: HTTP, port 80, path `/`  
- Screenshot:  
  ![LB Rule](screenshots/lb-rule.png)  

**Inbound NAT Rules** (Optional for RDP/SSH)  
- Forward specific ports to VM1 and VM2 for direct access  
- Screenshot:  
  ![Inbound NAT](screenshots/inbound-nat.png)  

**Outbound SNAT Rules**  
- Ensure VMs can access the internet using the LB's public IP  

---

### 4️⃣ Testing Load Balancer
- From terminal or browser, access the **LB public IP**: `http://<LB_PIP>`  
- Should see `"VM1"` and `"VM2"` alternately if **round-robin** is used.  
- Use `curl` to verify alternation:  
```bash
curl http://<LB_PIP>
curl http://<LB_PIP>
