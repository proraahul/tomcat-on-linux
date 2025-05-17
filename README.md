
# Apache Tomcat Installation on Linux

Apache Tomcat is a popular open-source web server and servlet container for running Java applications.

By default, Tomcat listens on **port 8080**, so we need to ensure this port is open in your firewall or network settings.

---

## Step-by-Step Installation Guide

### 1. Update the System and Install Java

```
sudo apt update
sudo apt install default-jre -y
```

This ensures the Java Runtime Environment is installed, which is required to run Tomcat.

---

### 2. Create a Directory for Tomcat

```
mkdir -p /home/cloudadmin/tomcat/tomcat1
chmod 755 /home/cloudadmin/tomcat/tomcat1
cd /home/cloudadmin/tomcat/tomcat1
```

We create a directory structure and assign the proper permissions.

---

### 3. Download and Extract Tomcat

```
wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.24/bin/apache-tomcat-8.5.24.tar.gz
tar -zxvf apache-tomcat-8.5.24.tar.gz
```

This downloads and extracts Apache Tomcat version 8.5.24.

---

### 4. Change Ownership

```
chown -R cloudadmin:cloudadmin /home/cloudadmin/tomcat/tomcat1/apache-tomcat-8.5.24
```

Gives ownership to the `cloudadmin` user.

---

### 5. Configure Tomcat

#### Copy Configuration Files

```
cp tomcat-users.xml /home/cloudadmin/tomcat/tomcat1/apache-tomcat-8.5.24/conf/tomcat-users.xml
cp context.xml /home/cloudadmin/tomcat/tomcat1/apache-tomcat-8.5.24/webapps/manager/META-INF/context.xml
```

These files manage access control and user roles.

---

### 6. Start Tomcat

```
sh /home/cloudadmin/tomcat/tomcat1/apache-tomcat-8.5.24/bin/startup.sh
```

Tomcat should now be running and accessible at: `http://<your-server-ip>:8080`

---

### Optional: Stop Tomcat

```
sh /home/cloudadmin/tomcat/tomcat1/apache-tomcat-8.5.24/bin/shutdown.sh
```

---

## Example `tomcat-users.xml`

```
<tomcat-users>
  <role rolename="manager-gui"/>
  <role rolename="admin-gui"/>
  <user username="admin" password="admin123" roles="manager-gui,admin-gui"/>
</tomcat-users>
```

---

## Example `context.xml`

```
<Context antiResourceLocking="false" privileged="true" >
  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|<your-server-ip>" />
</Context>
```

Replace `<your-server-ip>` with the actual IP address you wish to allow.

---

## Notes

- Update the Tomcat version as needed.
- Use strong credentials in a production environment.
- Restrict admin access based on IP.
