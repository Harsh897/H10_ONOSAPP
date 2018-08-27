# H10_ONOSAPP
 ONOS Implementation
Install Git:
build:~$ sudo apt-get install git-core
Install Karaf, Maven:
Create two directories called ~/Downloads and ~/Applications. Download the Karaf 3.0.5 and Maven 3.3.9 binaries (the tar.gz versions of both) into ~/Downloads and extract it to ~/Applications. Keep the tar archives in ~/Downloads; we'll need that later.
Code :-
build:~$ cd; mkdir Downloads Applications
build:~$ cd Downloads
build:~$ wget http://archive.apache.org/dist/karaf/3.0.5/apache-karaf-3.0.5.tar.gz
build:~$ wget http://archive.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
build:~$ tar -zxvf apache-karaf-3.0.5.tar.gz -C ../Applications/
build:~$ tar -zxvf apache-maven-3.3.9-bin.tar.gz -C ../Applications/

Next, install Oracle Java 8:

build:~$ sudo apt-get install software-properties-common -y
build:~$ sudo add-apt-repository ppa:webupd8team/java -y
build:~$ sudo apt-get update
build:~$ sudo apt-get install oracle-java8-installer oracle-java8-set-default -y
It will ask you to acknowledge the license; do so when prompted.
The second step above may prompt for the installation of python-software-properties. If prompted, do so.
Clone the ONOS source:
Now let’s copy a repository into a new onos directory under the home directory on the build machine.
navigate to the home directory by issuing this command:
build:~$ cd ~
build:~$ git clone https://gerrit.onosproject.org/onos 
This will create a directory called onos, with the source code in it.
4. Set up your build environment
On the build VM, Edit the .bashrc file (by typing the command below)
sdn@build:~$ nano ~/.bashrc
Add the line below at the end of the file:
. ~/onos/tools/dev/bash_profile
Press Ctrl-X to exit and Yes to save changes.
Once the line is added, source the file you just modified (or just log out and log back in): or run this command:
Building ONOS
Edit  ~/Applications/apache-karaf-3.0.5/etc/org.apache.karaf.features.cfg file by appending the following line to featuresRepositories:
build:~$ nano ~/Applications/apache-karaf-3.0.5/etc/org.apache.karaf.features.cfg
locate the featuresRepositories and append this line (will need a comma before appending the text to separate from the previous value)
mvn:org.onosproject/onos-features/1.5.0-SNAPSHOT/xml/features
Save and close the file. Now we are ready to build ONOS with Maven:
build:~$ cd ~/onos
build:~$ mvn clean install  # or use the alias 'mci'
Now we are ready to start customizing, creating, and installing ONOS packages.



4. Package and Deploy ONOS
Creating the package
To create an ONOS binary, run onos-package (or op, for short):
build:~$ onos-package
-rw-rw-r--  1 onosuser  onosuser  33395409 Dec  4 16:12 
/tmp/onos-1.5.1.onosuser.tar.gz
This creates a tar archive in /tmp .
Deploying the package
We can now deploy it to our VM:
build:~$ onos-install -f $OC1
onos start/running, process 2028
Once onos-install returns with the last message in the code block above, we can try logging on from our build machine: 
