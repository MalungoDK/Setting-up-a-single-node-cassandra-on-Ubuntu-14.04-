

**1. Installing Java**

In order to install cassandra I needed to install Java 7 or 8, but I used Java 7 instead.

**sudo apt-get update**

**sudo apt-get install openjdk-7-jdk**

**2. Add DataStax community repository**

After installing Java 7, I then added DataStax Community repository to the source files 

**echo "deb http://debian.datastax.com/community stable main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list**

After adding the repository, I had to add the DataStax repository key to my aptitude trusted key. However, Because I was working in a network under a proxy server, I had to do some extra effort which is explained bellow.

**3. Edit the /etc/apt/apt.conf**

**sudo vi /etc/apt/apt.conf**

The content of this file should be the following

Acquire::http::proxy "http://username:password@ProxyIPAddress:Port/";

For example the file should look like:

Acquire::http::proxy "http://samba:1234@10.2.2.3:8080/";

Save and quit this file. 

**4. Export HTTP proxy**

Again, I had to replace the fields on the commands with my details. After exporting the HTTP proxy, I was then able to add the DataStax Community repositoty key to my aptitude trusted key. Before I figured this out, I was getting connection timeout when trying to add the key.

**export http_proxy="http://username:password@ProxyIPAddress:Port"**

**5. Add DataStax Community key to aptitude trusted key**

**curl -L http://debian.datastax.com/debian/repo_key | sudo apt-key add -**

After adding the key I was finally able to install cassandra

**6. Install Cassandra**

**sudo apt-get update**

**sudo apt-get install cassandra**

Before running cassandra,I had to make small configuration change as mentioned in the tutorial that I used. Open /etc/passwd and change:

cassandra:x:***:***:Cassandra database,,,:/var/lib/cassandra:/bin/false

to 

cassandra:x:***:***:Cassandra database,,,:/var/lib/cassandra:/bin/bash

basically I only changed **/false** to **/bash**, otherwise everything else remains the same.

**7. Run Cassandra**

**sudo /usr/sbin/cassandra**

When I got to this point, I had my single node cassandra working.However, because this is only a single node cluster, There was no need to make changes in the cassandra.yaml file.

Thanks, I hope this tutorial will help others working on similar projects as well.
