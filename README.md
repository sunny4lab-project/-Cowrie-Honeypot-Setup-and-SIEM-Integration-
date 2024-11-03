# 🔐 Cowrie Honeypot Setup and SIEM Integration 🚀
Cowrie is a powerful, open-source honeypot solution designed to emulate an SSH (and optionally, Telnet) environment. It allows cybersecurity professionals and enthusiasts to capture and analyze brute-force attempts, credential guessing, and even more sophisticated intrusion techniques — all in a controlled, safe environment. 🛡️

- 🌟 Key Features of Cowrie
- 🔒 SSH and Telnet Emulation: Cowrie mimics an SSH/Telnet server, interacting with attackers and capturing their actions in real-time.

- 📜 Logging and Recording: Records all sessions, including commands entered, file downloads, and login attempts, enabling in-depth analysis.

- 💾 Fake File System: Simulates a Linux environment with common commands, tricking attackers into believing they’re on a real system.

- ⚙️ Scriptable Responses: Allows for custom responses, making the honeypot appear as realistic as possible to attackers.
#

**🛠️ Setting Up Cowrie on Ubuntu**

Follow these steps to install and configure Cowrie on your Ubuntu machine, ready to capture those attacker interactions! 👩‍💻👨‍💻


**Step 1: 🔄 Update and Install Dependencies**

First, update your system and install the necessary packages:
```bash
sudo apt update
sudo apt install python3 python3-venv python3-pip
```

Step 2: 📥 Download Cowrie

Clone the Cowrie repository from GitHub:
```bash
git clone https://github.com/cowrie/cowrie.git
cd cowrie
```
<img width="480" alt="Screenshot 2024-11-02 185651" src="https://github.com/user-attachments/assets/1703ff19-677f-47ff-8c16-b968ae24548a">

Step 3: 🧪 Set Up a Virtual Environment

Creating a virtual environment helps isolate Cowrie’s dependencies from the rest of your system:
```bash
python3 -m venv cowrie-env
source cowrie-env/bin/activate
```
<img width="486" alt="Screenshot 2024-11-02 190152" src="https://github.com/user-attachments/assets/be53514c-fd7f-4370-85f5-473d4a0b3b99">


Step 4: 📦 Install Cowrie Requirements
Use pip to install all the required Python packages:
```bash
pip install -r requirements.txt
```

<img width="483" alt="Screenshot 2024-11-02 190826" src="https://github.com/user-attachments/assets/622bc952-f632-4cc0-8dde-f47fb74c4498">


Step 5: 📝 Configure Cowrie
Copy the default configuration file and modify it as needed:
```bash
cd cowrie
cd /etc
cp cowrie.cfg.dist cowrie.cfg
nano cowrie.cfg
```
<img width="481" alt="Screenshot 2024-11-02 191038" src="https://github.com/user-attachments/assets/de268750-f09c-409b-be4c-f2ec82acf1d8">


In the configuration file, you can:

Adjust SSH settings
Configure logging options
Specify the port Cowrie listens on (default is 2222 to avoid conflicts with your regular SSH port)

Step 6: ▶️ Run Cowrie
Start Cowrie in the background to begin capturing brute-force attempts:
```bash
bin/cowrie start
To stop Cowrie, use:
```
Step 7: 🔍 Analyze Captured Data

Cowrie logs all activity, including login attempts, commands executed, and any files the attacker tries to upload. These logs are stored in the log directory within Cowrie’s main folder, with session logs saved in JSON format for easy parsing and analysis.


🔗 Integrating Cowrie with SIEM Tools (Elasticsearch, Splunk)

Captured logs can be sent to SIEM solutions like Elasticsearch or Splunk for deeper analysis. Cowrie also supports Syslog forwarding, making it easy to integrate with existing logging infrastructure. 🌐

🚀 Sending Logs to Elasticsearch
To send logs directly to Elasticsearch, enable and configure the Elasticsearch output in cowrie.cfg:
```bash
[output_elasticsearch]
enabled = true
host = localhost
port = 9200
index = cowrie-logs-%Y-%m-%d
```
<img width="278" alt="Screenshot 2024-11-02 191235" src="https://github.com/user-attachments/assets/f3f56921-dae7-4e9d-b8c3-a5fce83ffa7f">


After making these changes, restart Cowrie:

```bash
bin/cowrie stop
bin/cowrie start
```
Now, Cowrie logs will be sent to Elasticsearch, where you can use Kibana to visualize and query the data, identifying patterns in attacker behavior. 📊
#
📈 Benefits of Deploying Cowrie Honeypot
Deploying Cowrie in a controlled environment provides valuable insights into:

📊 Brute-force attack patterns: Analyze common usernames and passwords attackers use.
🔍 Attacker behavior: Observe the commands executed by attackers to understand their objectives.
🧠 Actionable Intelligence: Use these insights to improve your defenses, like adjusting account lockout policies or fine-tuning alert rules in SIEM tools.
With Cowrie, you’re not just tracking attacks — you’re learning from them and building a stronger security posture. 💪
#

🧠 Conclusion:

By setting up Cowrie and integrating it with Elasticsearch or Splunk, you’ll have a powerful, interactive tool for capturing and analyzing attacks in a safe environment. Happy hunting, and stay secure! 🔐🚀



