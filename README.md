# Barry`s Flightgear Connect API

This API contains a service to communicate with the Flightgear Open Source Flight Simulator
from any Java application via HTTP properties protocol.

## How to use as maven dependency

Barry's Flightgear Connect API has been deployed to Barry's Maven Repository. To use it in your own project you need to add the 
following repository to your project ```pom.xml```:

    <repositories>
      <repository>
        <id>barry-ballantines-releases</id>
        <url>https://raw.github.com/barryballantines/mvn-repository/releases/</url>
      </repository>
    </repositories>
    
The API itself is available dependency:

    <dependency>
      <groupId>ballantines.avionics</groupId>
      <artifactId>flightgear-connect-api</artifactId>
      <version>1.0</version>
    </dependency>
    
