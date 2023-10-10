

What is vulnerability
What is maven global server?
What is Maven local repository.


What is Maven?
  It is product of apache.

All the open source communities  like  Jenkins, tomcat, mysql etc upload their updated API's into maven global server ( search.maven.org )



Developers  connect to  the maven global server, download those
 API  that are necessary for the project development and store them in  Maven local repository.


All  developers connect   to  maven local repository and perform the development activity.


In this way, the code is preserved in github

This will help in protecting the code from any threats/viruses that might be present in the  API's.

Maven  is also a build tool. Where it can compile the programs and create a artifact.

+++++++++++++++++++++++++++++

Build tools

Java	- Maven
Dotnet	- MS Build
Python 	- PY Builder

+++++++++++++++++++++

+++++++++++++++++++
Configure Maven



In google  --  jdk 18 download
Download  and Install

Where jdk is installed?




C:\Program Files\Java\jdk-18.0.2.1



Copy the path of jdk


This PC --> properties -- Advanced system settings --> advanced tab---> Environment variables --> system variables -- new



Variable name - JAVA_HOME
Variable value - C:\Program Files\Java\jdk-18.0.2.1

Ok 





+++++++++++++++





Now, go to "path" variable --- Edit  -- click on new button
C:\Program Files\Java\jdk-18.0.2.1\bin

Ok  



++++++++++++

Download apache  Maven
In files section
download  bin.zip  version  and extract

C:\Users\ADMIN\Downloads\apache-maven-3.8.6-bin\apache-maven-3.8.6



++++++++++++++++++
Again, create new environment variable

Variable name - M2_HOME
Variable value - C:\Users\dell 7490\Downloads\apache-maven-3.9.0-bin\apache-maven-3.9.0

Ok 

Now, go to "path" variable --- Edit  -- click on new button
C:\Users\ADMIN\Downloads\apache-maven-3.8.6-bin\apache-maven-3.8.6\bin




Ok  --> Ok



How to check maven is configured or not?
Open command prompt
>  mvn  --version

++++++++++++++
