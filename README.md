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
    
## How to use the API

Barry's Flightgear Connect API uses the HTTP service of Flightgear to read and write properties. Make sure that you activated the 
HTTP service on Flightgear before you try using the API. In the following examples we assume that Flightgear is running on the same 
machine ```localhost``` on port ```5500```.

### Example: Initializing the property service

     ServerConfig config = new ServerConfig("localhost", 5500);
     PropertyService service = new HttpPropertyServiceImpl(config);


### Example: Reading a single property from Flightgear
    
    Double value = propertyService.readProperty("/velocities/groundspeed-kt");

### Example: Reading multiple properties at once

        String root = "/autopilot/route-manager";
        Map<String,Object> p = service.readProperties(
                root + "/departure/airport",
                root + "/destination/airport",
                root + "/total-distance",
                root + "/distance-remaining-nm",
                root + "/flight-time",
                root + "/ete" );
        
        String departure = (String) p.get(root + "/departure/airport");
        String destination = (String) p.get(root + "/destination/airport");
        Double totalDistance = (Double) p.get(root + "/total-distance");
        Double distanceRemaining = (Double) p.get(root + "/distance-remaining-nm");
        Double flightTime = (Double) p.get(root + "/flight-time");
        Double estimatedTimeToDestination = (Double) p.get(root + "/ete");

### Example: Write properties to Flightgear

The following example will relocate your plane in flightgear.
        
     Map<String, Object> position = new HashMap<>();
     position.put("/position/latitude-deg", 52.31835581);
     position.put("/position/longitude-deg", 4.796849554);
     position.put("/position/altitude-ft",34.3224337705);
     position.put("/orientation/heading-deg", 266.888);
     
     service.writeProperties(position);
