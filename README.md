##### OVERVIEW

Tampere Open Trip Planner with estimation of bus connection chance is built on OpenTripPlanner (OTP) https://github.com/opentripplanner, an open source multi-modal trip planner. It depends on open data in open standard file formats (GTFS and OpenStreetMap), and includes a REST API for journey planning as well as several map-based Javascript clients. For more information, see the project website: http://opentripplanner.org


##### INSTALL

Installation instructions are available on the website: http://opentripplanner.org/wiki/

##### FILES

OpenTripPlanner is a multi-module Maven project. It contains the following sub-modules:

* `otp-core/`              - Core routing algorithms, data structures, libraries, and stand-alone server.
* `otp-analyst-client/`    - A Javascript client focusing on OTP analyst web service visualizations.
* `otp-geocoder/`          - A servlet that converts addresses to geographic locations using web services.
* `otp-leaflet-client/`    - The newer Javascript client providing a map-based UI for trip planning.
* `otp-municoder/`         - A servlet that determines which administrative area a coordinate falls within. 
* `otp-openlayers-client/` - The original Javascript client providing a map-based UI for trip planning.
* `otp-rest-servlet/`      - A servlet that provides the OTP REST API within a servlet container.
* `otp-thrift-api/`        - A Thrift API supporting lower-level queries than the REST API.
* `otp-admin-client/`      - A client for administration.

OTP also includes the following subprojects which must be built separately:

* `otp-datastore/`         - A Play-based backend for logging OTP queries.
* `otp-gvsig/`             - An OpenTripPlanner-based extension to GVSIG.

##### CHANGES

The function of estimation of bus connection chance has been implemented in the stable version of OTP 0.11. The bus movements data being collected and processed daily to calculate distribution parameters of vehicles' arrivals at bus stops daily during the last 60 days in a separate system. The summarized data as a list of trip_id, bus stop and distribution parameters are loaded to the planning graph of OTP. The changes of OTP involved the following modules: 

* `otp-leaflet-client/src/main/webapp/js/otp/config.js` - Description of the project and initial focus of the map
* `otp-leaflet-client/src/main/webapp/js/otp/modules/Itinerary.js` and `otp-leaflet-client/src/main/webapp/js/otp/modules/ItinerariesWidget.js` - Adding connection chance information to the trip summary in the Itineraries widget
* `otp-core/src/java/org/opentripplanner/routing/impl/GraphServiceFileImpl.java` and `otp-core/src/java/org/opentripplanner/routing/graph/Graph.java` - Adding a new property "distribution" to the graph
* `otp-core/src/java/org/opentripplanner/api/model/Itinerary.java` - Setting default value for risk
* `otp-core/src/java/org/opentripplanner/api/resource/PlanGenerator.java` - Calculating chance of connection

##### DEVELOPMENT

OpenTripPlanner is a collaborative project incorporating code, translation, and documentation from contributors around the world. We welcome new contributions and prefer to format our code according to GeoTools-based formatting guidelines; an Eclipse autoformatter can be found at the root of this project (https://raw.github.com/openplans/OpenTripPlanner/master/formatter.xml). Further development guidelines can be found on the project wiki (https://github.com/openplans/OpenTripPlanner/wiki/DevelopersGuide).

The OpenTripPlanner project was launched by Portland, Oregon's transport agency TriMet (http://trimet.org/), and began in July of 2009 with a kick-off conference bringing together transit agencies and the authors of the major open source transit passenger information software of the day: David Emory of FivePoints, Brian Ferris of OneBusAway, and Brandon Martin-Anderson of GraphServer. From 2008 through 2012, development was coordinated by New York nonprofit OpenPlans (http://openplans.org/). By early 2013, OpenTripPlanner had become the primary trip planning software used by TriMet in the Portland regional trip planner (http://ride.trimet.org/) and was backing several popular mobile applications. Public-facing OpenTripPlanner instances were available in ten countries throughout the world. At this point the OpenPlans transportation software team became the independent consultancy Conveyal (http://www.conveyal.com/). The original OpenTripPlanner development team from OpenPlans still actively participates in programming, design, and community coordination via the mailing list and their roles on the OTP Project Leadership Committee.

As of Summer 2013, the OpenTripPlanner project has been accepted for membership in the Software Freedom Conservancy (SFC). SFC handles the legal and financial details common to many open source projects, providing a formal framework for OTP and allowing contributors to concentrate on the code. For more information, see the SFC website at http://sfconservancy.org/.
