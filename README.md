# IDS_Configuration_Suricata
## Overview
**Intrusion Detection System (IDS)**
**Definition:**
An IDS is a monitoring system designed to detect suspicious activities or policy violations within a network or system. It does not take direct action to stop threats but instead alerts administrators to potential security incidents.
**Key Features:**
- **Passive Monitoring:** IDS operates by analyzing network traffic or system logs for malicious patterns.
- **Alerting:** It generates alerts when suspicious activities are detected, enabling administrators to investigate further.
  
**Pros:**
- Provides detailed logs for forensic analysis.
- Can detect a wide range of attacks, including zero-day exploits (with proper rule updates).
  
**Cons:**
- No real-time prevention; relies on manual or external intervention.
- Can produce false positives or negatives.
  
**Use Case:** Ideal for environments that prioritize monitoring over automatic threat mitigation, such as research labs or environments requiring in-depth analysis.


**Configuration**

Open the following directory:
```
cd /etc/suricata/
```


Edit the config file:

```
sudo nano suricata.yaml
```


You need to find default **"rule-path:"** section and add the following:

default-rule-path: 
/var/lib/suricata/rules

rule-files:
  - suricata.rules
  - local.rules



Change the path to suricata rules directory:
```
cd /var/lib/suricata/rules
```

Create rule file named local.rules:
```
touch local.rules
```

Edit local.rules:
```
sudo nano local.rules
```

Paste the rules present in the [local.txt](https://github.com/raghu2301/IDS_Configuration_Suricata/blob/main/local.txt) file into your local.rules file:


Run a config change success test:
```
sudo suricata -T -c /etc/suricata/suricata.yaml
```
if you get any error check the suricata.yaml or local.rules for errors



**Start Monitoring**
```
sudo systemctl start suricata 
```

Select interface to monitor:
```
sudo suricata -c /etc/suricata/suricata.yaml -i <interface_name>
```
If you dont know the interface name you can find it by the following command:
```
ifconfig
```

To View Alert:
```
cd /var/log/suricata
```
```
sudo nano eve.json
```
```
sudo nano fast.log
```
