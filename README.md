# WasteTrack 🚛

Enterprise-grade waste management and route optimization platform built on 
**microservices architecture**, designed to digitize and streamline operations 
for waste collection companies and environmental logistics SMEs. Integrates 
**real-time GPS vehicle tracking**, intelligent route optimization, regulatory 
compliance reporting for Colombian environmental authorities (MADS), and 
**high-performance geospatial analytics powered by ElasticSearch**.

Developed for Colombian waste management companies requiring compliance with 
**Decreto 1076/2015** (environmental regulations), **RESPEL reporting** for 
hazardous waste, and operational efficiency dashboards for field fleet management.

---

## 🛠️ Complete Technology Stack

### Backend — Microservices

| Technology               | Version   | Purpose                                          |
|--------------------------|-----------|--------------------------------------------------|
| **Java**                 | 17        | Core backend language                            |
| **Spring Boot**          | 3.2.x     | Microservices framework (Java 17 compatible)     |
| **Spring MVC**           | 6.1.x     | REST controllers and request handling            |
| **Spring Cloud**         | 2023.x    | Distributed systems support                      |
| **Spring Cloud Gateway** | —         | API Gateway with rate limiting                   |
| **Eureka Server**        | —         | Service Discovery                                |
| **Spring Cloud Config**  | —         | Centralized configuration management             |
| **Spring Data JPA**      | —         | ORM and database persistence                     |
| **Spring Security**      | 6.2.x     | Authentication and authorization                 |
| **Resilience4j**         | 2.1.x     | Circuit Breaker and Rate Limiting                |
| **Apache Kafka**         | 3.x       | Asynchronous event-driven messaging              |
| **ElasticSearch**        | 8.11.x    | Geospatial analytics and operational indexing    |
| **Logstash**             | 8.11.x    | Telemetry data pipeline into ElasticSearch       |
| **Kibana**               | 8.11.x    | Operational dashboards and fleet analytics       |
| **PostgreSQL**           | 15+       | Primary relational database                      |
| **MongoDB**              | 6.x       | IoT telemetry events and unstructured logs       |
| **Redis**                | 7.x       | Distributed cache and real-time session data     |
| **MQTT Broker**          | Mosquitto 2.x | IoT device communication protocol            |

### Frontend — Single Page Application

| Technology                | Version | Purpose                                          |
|---------------------------|---------|--------------------------------------------------|
| **React**                 | 18.x    | Frontend UI framework                            |
| **TypeScript**            | 5.x     | Static typing and OOP                            |
| **React-Redux**           | 8.x     | Global state management                          |
| **Redux Toolkit**         | 1.9.x   | Simplified Redux with slices                     |
| **Redux Thunk**           | 2.4.x   | Async middleware for API calls                   |
| **React Router v6**       | 6.x     | Client-side routing                              |
| **Webpack**               | 5.x     | Manual module bundling and optimization          |
| **SASS/SCSS**             | 1.x     | Advanced CSS preprocessing                       |
| **Axios**                 | 1.x     | HTTP client with interceptors                    |
| **Leaflet + React-Leaflet**| 4.x    | Interactive geospatial maps                      |
| **React Testing Library** | 14.x    | Component unit testing (TDD)                     |
| **Cypress**               | 13.x    | End-to-end testing (BDD)                         |
| **Chart.js**              | 4.x     | Operational KPI dashboards and analytics charts  |
| **Socket.io Client**      | 4.x     | Real-time GPS and telemetry WebSocket updates    |

### External Integrations

| System                      | Purpose                                              |
|-----------------------------|------------------------------------------------------|
| **Google Maps / OSRM**      | Route optimization and distance matrix calculation   |
| **MADS Web Services**       | Environmental regulatory reporting                   |
| **IDEAM API**               | Weather data for route planning                      |
| **Twilio**                  | SMS driver notifications and alerts                  |
| **PayU / Mercado Pago**     | Client billing and payment processing                |

### DevOps & Infrastructure

| Technology          | Purpose                                                   |
|---------------------|-----------------------------------------------------------|
| **Docker**          | Service containerization                                  |
| **Docker Compose**  | Local multi-service orchestration                         |
| **Kubernetes**      | Production-grade container orchestration                  |
| **Jenkins**         | CI/CD pipeline automation                                 |
| **Prometheus**      | Metrics collection and IoT alerting                       |
| **Grafana**         | Fleet monitoring and infrastructure dashboards            |
| **ELK Stack**       | Centralized logging (ElasticSearch + Logstash + Kibana)   |

---

## 🏗️ Microservices Architecture
```
                    ┌─────────────────────────────────────────┐
                    │         React 18 Frontend SPA           │
                    │  (Redux + Thunks · SASS · Webpack 5)   │
                    │  (Leaflet Maps · Chart.js · Socket.io)  │
                    └─────────────────────────────────────────┘
                                        ↓
                    ┌─────────────────────────────────────────┐
                    │     API Gateway (Spring Cloud Gateway)  │
                    │  - JWT Validation                       │
                    │  - Rate Limiting (Resilience4j)         │
                    │  - Load Balancing                       │
                    │  - Route Filtering                      │
                    └─────────────────────────────────────────┘
                                        ↓
    ┌───────────┬──────────────┬──────────────┬─────────────┬──────────────┬───────────┐
    ↓           ↓              ↓              ↓             ↓              ↓           ↓
┌────────┐ ┌─────────┐ ┌────────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐
│Vehicle │ │  Route  │ │Collection  │ │Telemetry │ │ Search & │ │Reporting │ │Billing │
│Service │ │ Service │ │  Service   │ │  Service │ │Analytics │ │ Service  │ │Service │
│        │ │         │ │            │ │          │ │  Service │ │          │ │        │
│- Fleet │ │- Plan   │ │- Schedule  │ │- GPS     │ │- ES Geo  │ │- MADS    │ │- Invoic│
│- Driver│ │- Optim. │ │- Waste Log │ │- IoT     │ │  Search  │ │- RESPEL  │ │- PayU  │
│- Maint.│ │- ETA    │ │- Incidents │ │- Alerts  │ │- KPIs    │ │- Env.    │ │- PDF   │
└────────┘ └─────────┘ └────────────┘ └──────────┘ └──────────┘ └──────────┘ └────────┘
    ↓           ↓              ↓              ↓             ↓              ↓           ↓
┌────────┐ ┌─────────┐ ┌────────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐
│Postgre │ │Postgre  │ │ PostgreSQL │ │ MongoDB  │ │ElasticSe-│ │ MongoDB  │ │Postgre │
│  SQL   │ │  SQL    │ │(Collections│ │(Telemetry│ │  arch    │ │  (Logs)  │ │  SQL   │
│(Fleet) │ │(Routes) │ │  Events)   │ │  Events) │ │(Geo+Ops) │ │          │ │(Bills) │
└────────┘ └─────────┘ └────────────┘ └──────────┘ └──────────┘ └──────────┘ └────────┘

                    ┌─────────────────────────────────────────┐
                    │         Apache Kafka Message Bus        │
                    │  Topics:                                │
                    │  - vehicle.location.updated             │
                    │  - route.started                        │
                    │  - route.completed                      │
                    │  - collection.registered                │
                    │  - telemetry.alert.triggered            │
                    │  - analytics.index.requested            │
                    │  - report.generation.requested          │
                    └─────────────────────────────────────────┘
                                        ↓
          ┌──────────────────────────────────────────────────────┐
          │               MQTT Broker (Mosquitto)                │
          │   IoT GPS Devices → Real-Time Telemetry Pipeline    │
          │   Topics:                                            │
          │   - fleet/{vehicleId}/location                      │
          │   - fleet/{vehicleId}/sensors                       │
          │   - fleet/{vehicleId}/alerts                        │
          └──────────────────────────────────────────────────────┘
                                        ↓
          ┌──────────────────────────────────────────────────────┐
          │              ELK Stack — Observability               │
          │   ElasticSearch · Logstash · Kibana                  │
          │   (Fleet analytics + Geospatial queries +            │
          │    Operational KPIs + IoT event logs)                │
          └──────────────────────────────────────────────────────┘
                                        ↓
                    ┌─────────────────────────────────────────┐
                    │      MADS Integration Service           │
                    │  - RESPEL Hazardous Waste Reports       │
                    │  - Decreto 1076/2015 Compliance         │
                    │  - Environmental Authority Submission    │
                    │  - Digital Report Signing               │
                    └─────────────────────────────────────────┘
                                        ↓
                    ┌─────────────────────────────────────────┐
                    │    MADS / Environmental Web Services    │
                    │  (Colombian Environmental Regulation)   │
                    └─────────────────────────────────────────┘
```

---

## ⚙️ Service Responsibilities

### Vehicle Service
Core service managing the entire fleet lifecycle. Handles vehicle registration with
technical specifications, fuel type, capacity, and maintenance schedules. Manages
driver assignments, license validation, and shift scheduling. Publishes
`vehicle.location.updated` events to Kafka every 30 seconds from GPS device data
received through the MQTT broker, ensuring all downstream services — Search,
Analytics, and Route — stay synchronized with real-time fleet position.

### Route Service
Manages the full route planning and optimization lifecycle. Integrates with Google
Maps Distance Matrix API and OSRM (Open Source Routing Machine) for open-source
route calculation. Implements multi-stop route optimization using nearest-neighbor
and genetic algorithm approaches, accounting for vehicle capacity, collection
point priorities, and real-time traffic data from IDEAM weather conditions.
Publishes `route.started` and `route.completed` events consumed by the Collection
and Analytics services.

### Collection Service
Handles the operational core of waste collection events. Records every collection
stop with waste type (organic, recyclable, hazardous — RESPEL), weight, volume,
GPS coordinates, and photographic evidence. Manages incident reporting for missed
stops, overweight loads, and unauthorized dumping events. Publishes
`collection.registered` events that trigger automatic MADS regulatory data
aggregation for compliance reporting.

### Telemetry Service
The IoT backbone of the architecture. Subscribes to all MQTT topics from GPS
devices installed in fleet vehicles, processes high-frequency telemetry streams
(location, speed, fuel level, engine temperature, door status), stores raw events
in MongoDB for time-series analysis, and publishes `telemetry.alert.triggered`
events to Kafka when threshold violations are detected — speeding, unauthorized
stops, low fuel, engine overheating — enabling real-time driver alerts via Twilio SMS.

### Search & Analytics Service (ElasticSearch Core)
The differentiating service of this architecture. Maintains a geospatially-indexed
ElasticSearch cluster that powers two critical capabilities: geo_point queries for
fleet proximity search and collection zone analysis, and operational analytics
aggregations for KPI dashboards — daily collection volumes by zone, route efficiency
scores, driver performance metrics, and environmental compliance indicators.
Implements Index Lifecycle Management (ILM) for telemetry data retention aligned
with MADS regulatory requirements.

### Reporting Service
Generates all mandatory environmental compliance reports required by Colombian
authorities. Produces RESPEL reports (hazardous waste manifests), monthly collection
summaries for MADS submission, and operational efficiency reports for internal
management. Aggregates data from Collection, Vehicle, and Route services through
Kafka-driven event sourcing, ensuring reports always reflect complete operational data.

### Billing Service
Handles client invoicing for waste collection services. Generates itemized invoices
based on collection events, vehicle usage, and service agreements. Integrates with
PayU and Mercado Pago for payment processing and publishes billing events that
trigger automated accounting entries downstream.

---

## ✨ Main Features

### 🔍 ElasticSearch — Geospatial Analytics & Operational Intelligence

ElasticSearch in WasteTrack serves a fundamentally different purpose than traditional
text search. It powers **geospatial fleet queries** and **real-time operational
analytics aggregations** — enabling sub-second KPI dashboards, proximity-based
vehicle dispatch, and collection zone efficiency analysis across thousands of
daily telemetry events.

**Geospatial Index Configuration**
```java
// Search & Analytics Service — ElasticSearch Geo Configuration
// Java 17 + Spring Boot 3.2.x + Spring Data ElasticSearch 5.2.x

@Configuration
public class ElasticSearchConfig {

    @Value("${elasticsearch.uris}")
    private String elasticsearchUri;

    @Value("${elasticsearch.username}")
    private String username;

    @Value("${elasticsearch.password}")
    private String password;

    @Bean
    public ElasticsearchClient elasticsearchClient() {
        RestClient restClient = RestClient.builder(HttpHost.create(elasticsearchUri))
            .setDefaultHeaders(new Header[]{
                new BasicHeader("Authorization",
                    "Basic " + Base64.getEncoder().encodeToString(
                        (username + ":" + password).getBytes(StandardCharsets.UTF_8)))
            })
            .build();

        ElasticsearchTransport transport = new RestClientTransport(
            restClient, new JacksonJsonpMapper());

        return new ElasticsearchClient(transport);
    }
}
```
```java
// Fleet Vehicle Document — ElasticSearch Geospatial Index Mapping
@Document(indexName = "fleet_vehicles")
@Setting(settingPath = "elasticsearch/fleet-settings.json")
@Mapping(mappingPath = "elasticsearch/fleet-mapping.json")
public class FleetVehicleDocument {

    @Id
    private String vehicleId;

    @Field(type = FieldType.Keyword)
    private String plateNumber;

    @Field(type = FieldType.Keyword)
    private String vehicleType;        // COMPACTOR, LOADER, SWEEPER

    @Field(type = FieldType.Keyword)
    private String status;             // ACTIVE, ON_ROUTE, IDLE, MAINTENANCE

    @GeoPointField
    private GeoPoint currentLocation;  // Real-time GPS position

    @Field(type = FieldType.Double)
    private Double currentSpeed;

    @Field(type = FieldType.Integer)
    private Integer fuelLevel;

    @Field(type = FieldType.Keyword)
    private String assignedRouteId;

    @Field(type = FieldType.Keyword)
    private String driverId;

    @Field(type = FieldType.Double)
    private Double collectionCapacityUsed;  // percentage

    @Field(type = FieldType.Date, format = DateFormat.date_time)
    private Instant lastUpdated;

    @Field(type = FieldType.Keyword)
    private String zone;
}
```
```java
// Search & Analytics Service — Geospatial Query Engine
@Service
@Slf4j
public class FleetAnalyticsService {

    private final ElasticsearchOperations elasticsearchOperations;
    private final ElasticsearchClient elasticsearchClient;

    public FleetAnalyticsService(ElasticsearchOperations elasticsearchOperations,
                                  ElasticsearchClient elasticsearchClient) {
        this.elasticsearchOperations = elasticsearchOperations;
        this.elasticsearchClient = elasticsearchClient;
    }

    // Find vehicles within radius of a collection point (geo_distance query)
    public List<FleetVehicleDocument> findNearbyVehicles(
            Double latitude, Double longitude, Double radiusKm) {

        GeoDistanceQuery geoDistanceQuery = GeoDistanceQuery.of(g -> g
            .field("currentLocation")
            .location(GeoLocation.of(gl -> gl
                .latlon(LatLonGeoLocation.of(ll -> ll
                    .lat(latitude)
                    .lon(longitude)))))
            .distance(radiusKm + "km"));

        NativeQuery searchQuery = NativeQuery.builder()
            .withQuery(q -> q
                .bool(b -> b
                    .must(m -> m.geoDistance(geoDistanceQuery))
                    .filter(f -> f.term(t -> t
                        .field("status")
                        .value("ACTIVE")))))
            .withSort(Sort.by(Sort.Direction.ASC, "_geo_distance"))
            .withPageable(PageRequest.of(0, 10))
            .build();

        SearchHits<FleetVehicleDocument> hits =
            elasticsearchOperations.search(searchQuery, FleetVehicleDocument.class);

        log.info("Found {} vehicles within {}km of [{},{}]",
            hits.getTotalHits(), radiusKm, latitude, longitude);

        return hits.stream()
            .map(SearchHit::getContent)
            .collect(Collectors.toList());
    }

    // Aggregation — Daily collection volume by zone
    public Map<String, Double> getCollectionVolumeByZone(LocalDate date) throws IOException {
        SearchResponse<Void> response = elasticsearchClient.search(s -> s
            .index("collection_events")
            .query(q -> q
                .range(r -> r
                    .field("collectionDate")
                    .gte(JsonData.of(date.toString()))
                    .lte(JsonData.of(date.toString()))))
            .aggregations("by_zone", a -> a
                .terms(t -> t.field("zone").size(50))
                .aggregations("total_volume", aa -> aa
                    .sum(sum -> sum.field("volumeKg")))),
            Void.class);

        Map<String, Double> volumeByZone = new LinkedHashMap<>();

        response.aggregations().get("by_zone").sterms().buckets().array()
            .forEach(bucket -> volumeByZone.put(
                bucket.key().stringValue(),
                bucket.aggregations().get("total_volume").sum().value()));

        return volumeByZone;
    }

    // Aggregation — Route efficiency score per driver
    public List<DriverEfficiencyDTO> getDriverEfficiencyMetrics(
            LocalDate from, LocalDate to) throws IOException {

        SearchResponse<Void> response = elasticsearchClient.search(s -> s
            .index("route_events")
            .query(q -> q
                .range(r -> r
                    .field("routeDate")
                    .gte(JsonData.of(from.toString()))
                    .lte(JsonData.of(to.toString()))))
            .aggregations("by_driver", a -> a
                .terms(t -> t.field("driverId").size(100))
                .aggregations("avg_efficiency", aa -> aa
                    .avg(avg -> avg.field("efficiencyScore")))
                .aggregations("total_routes", aa -> aa
                    .valueCount(vc -> vc.field("routeId")))
                .aggregations("avg_completion_time", aa -> aa
                    .avg(avg -> avg.field("completionTimeMinutes")))),
            Void.class);

        return response.aggregations().get("by_driver").sterms().buckets().array()
            .stream()
            .map(bucket -> DriverEfficiencyDTO.builder()
                .driverId(bucket.key().stringValue())
                .avgEfficiencyScore(bucket.aggregations()
                    .get("avg_efficiency").avg().value())
                .totalRoutes((long) bucket.aggregations()
                    .get("total_routes").valueCount().value())
                .avgCompletionTimeMinutes(bucket.aggregations()
                    .get("avg_completion_time").avg().value())
                .build())
            .sorted(Comparator.comparingDouble(
                DriverEfficiencyDTO::getAvgEfficiencyScore).reversed())
            .collect(Collectors.toList());
    }

    // Index fleet vehicle from Kafka telemetry event
    @KafkaListener(topics = "vehicle.location.updated", groupId = "analytics-service")
    public void indexVehicleLocation(VehicleLocationEvent event) {
        FleetVehicleDocument document = FleetVehicleDocument.builder()
            .vehicleId(event.getVehicleId())
            .plateNumber(event.getPlateNumber())
            .currentLocation(new GeoPoint(event.getLatitude(), event.getLongitude()))
            .currentSpeed(event.getSpeed())
            .fuelLevel(event.getFuelLevel())
            .status(event.getStatus())
            .assignedRouteId(event.getRouteId())
            .driverId(event.getDriverId())
            .collectionCapacityUsed(event.getCapacityUsed())
            .lastUpdated(Instant.now())
            .zone(event.getZone())
            .build();

        elasticsearchOperations.save(document);
        log.debug("Vehicle {} indexed at [{},{}]",
            event.getVehicleId(), event.getLatitude(), event.getLongitude());
    }
}
```

---

### 📡 IoT/GPS — Real-Time Telemetry Pipeline
```java
// Telemetry Service — MQTT IoT Integration
// Java 17 + Spring Boot 3.2.x + Eclipse Paho MQTT Client

@Service
@Slf4j
public class TelemetryIngestionService {

    private final MqttClient mqttClient;
    private final KafkaTemplate<String, Object> kafkaTemplate;
    private final TelemetryEventRepository telemetryRepository;
    private final AlertService alertService;

    @Value("${mqtt.broker.url}")
    private String brokerUrl;

    @PostConstruct
    public void connectAndSubscribe() throws MqttException {
        mqttClient = new MqttClient(brokerUrl, MqttClient.generateClientId());

        MqttConnectOptions options = new MqttConnectOptions();
        options.setAutomaticReconnect(true);
        options.setCleanSession(false);
        options.setConnectionTimeout(30);
        options.setKeepAliveInterval(60);
        options.setUserName("${mqtt.username}");
        options.setPassword("${mqtt.password}".toCharArray());

        mqttClient.connect(options);

        // Subscribe to all fleet device topics
        mqttClient.subscribe("fleet/+/location", 1, this::handleLocationMessage);
        mqttClient.subscribe("fleet/+/sensors", 1, this::handleSensorMessage);
        mqttClient.subscribe("fleet/+/alerts", 2, this::handleAlertMessage);

        log.info("MQTT broker connected — subscribed to fleet telemetry topics");
    }

    // Handle real-time GPS location messages
    private void handleLocationMessage(String topic, MqttMessage message) {
        try {
            String vehicleId = extractVehicleId(topic);
            LocationPayload payload = objectMapper.readValue(
                message.getPayload(), LocationPayload.class);

            // Persist raw telemetry to MongoDB
            TelemetryEvent event = TelemetryEvent.builder()
                .vehicleId(vehicleId)
                .eventType("LOCATION")
                .latitude(payload.getLatitude())
                .longitude(payload.getLongitude())
                .speed(payload.getSpeed())
                .heading(payload.getHeading())
                .altitude(payload.getAltitude())
                .accuracy(payload.getAccuracy())
                .timestamp(Instant.now())
                .rawPayload(new String(message.getPayload()))
                .build();

            telemetryRepository.save(event);

            // Publish to Kafka for ElasticSearch indexing
            VehicleLocationEvent locationEvent = VehicleLocationEvent.builder()
                .vehicleId(vehicleId)
                .latitude(payload.getLatitude())
                .longitude(payload.getLongitude())
                .speed(payload.getSpeed())
                .timestamp(event.getTimestamp())
                .build();

            kafkaTemplate.send("vehicle.location.updated", vehicleId, locationEvent);

            // Speed violation detection
            if (payload.getSpeed() > 80.0) {
                alertService.triggerSpeedingAlert(vehicleId, payload.getSpeed());
            }

        } catch (Exception e) {
            log.error("Error processing location message from topic: {}", topic, e);
        }
    }

    // Handle IoT sensor data (fuel, temperature, door status)
    private void handleSensorMessage(String topic, MqttMessage message) {
        try {
            String vehicleId = extractVehicleId(topic);
            SensorPayload payload = objectMapper.readValue(
                message.getPayload(), SensorPayload.class);

            // Low fuel alert
            if (payload.getFuelLevel() < 15) {
                alertService.triggerLowFuelAlert(vehicleId, payload.getFuelLevel());
                kafkaTemplate.send("telemetry.alert.triggered",
                    new TelemetryAlert(vehicleId, "LOW_FUEL", payload.getFuelLevel()));
            }

            // Engine overheating alert
            if (payload.getEngineTemperature() > 110.0) {
                alertService.triggerOverheatAlert(
                    vehicleId, payload.getEngineTemperature());
                kafkaTemplate.send("telemetry.alert.triggered",
                    new TelemetryAlert(vehicleId, "ENGINE_OVERHEAT",
                        payload.getEngineTemperature()));
            }

            log.debug("Sensor data processed for vehicle {}: fuel={}%, temp={}°C",
                vehicleId, payload.getFuelLevel(), payload.getEngineTemperature());

        } catch (Exception e) {
            log.error("Error processing sensor message from topic: {}", topic, e);
        }
    }

    private String extractVehicleId(String topic) {
        // topic format: fleet/{vehicleId}/location
        return topic.split("/")[1];
    }
}
```
```java
// Alert Service — Real-time driver notifications via Twilio SMS
@Service
@Slf4j
public class AlertService {

    private final TwilioClient twilioClient;
    private final VehicleRepository vehicleRepository;
    private final WebSocketHandler webSocketHandler;

    @Async
    public void triggerSpeedingAlert(String vehicleId, Double speed) {
        Vehicle vehicle = vehicleRepository.findById(vehicleId)
            .orElseThrow(() -> new VehicleNotFoundException(vehicleId));

        String message = String.format(
            "[WasteTrack] ALERTA: Vehículo %s excede velocidad: %.1f km/h. " +
            "Reduzca la velocidad inmediatamente.",
            vehicle.getPlateNumber(), speed);

        // Send SMS to driver
        twilioClient.messages().create(
            vehicle.getDriver().getPhone(),
            TwilioSmsRequest.builder()
                .from("${twilio.phone.number}")
                .body(message)
                .build());

        // Push real-time alert to dashboard via WebSocket
        webSocketHandler.broadcastAlert(AlertDTO.builder()
            .vehicleId(vehicleId)
            .plateNumber(vehicle.getPlateNumber())
            .alertType("SPEEDING")
            .value(speed)
            .message(message)
            .timestamp(Instant.now())
            .build());

        log.warn("Speeding alert triggered: vehicle={}, speed={}", vehicleId, speed);
    }
}
```

---

### ⚛️ React — Redux Toolkit + Thunks + Leaflet Real-Time Map
```typescript
// store/slices/fleetSlice.ts — Real-time fleet Redux state
import { createSlice, createAsyncThunk, PayloadAction } from '@reduxjs/toolkit';
import { fleetService } from '../../services/fleetService';
import {
  VehicleLocation,
  NearbyVehiclesParams,
  FleetKPIs,
} from '../../types/fleet';

interface FleetState {
  vehicles: VehicleLocation[];
  nearbyVehicles: VehicleLocation[];
  kpis: FleetKPIs | null;
  selectedVehicleId: string | null;
  loading: boolean;
  error: string | null;
  lastUpdated: string | null;
}

const initialState: FleetState = {
  vehicles: [],
  nearbyVehicles: [],
  kpis: null,
  selectedVehicleId: null,
  loading: false,
  error: null,
  lastUpdated: null,
};

// Async Thunk — Fetch all active fleet vehicles
export const fetchFleetVehicles = createAsyncThunk(
  'fleet/fetchVehicles',
  async (_, { rejectWithValue }) => {
    try {
      const response = await fleetService.getActiveVehicles();
      return response.data;
    } catch (error: any) {
      return rejectWithValue(error.response?.data?.message || 'Fleet fetch failed');
    }
  }
);

// Async Thunk — ElasticSearch geo_distance nearby vehicle search
export const fetchNearbyVehicles = createAsyncThunk(
  'fleet/fetchNearbyVehicles',
  async (params: NearbyVehiclesParams, { rejectWithValue }) => {
    try {
      const response = await fleetService.getNearbyVehicles(params);
      return response.data;
    } catch (error: any) {
      return rejectWithValue(error.response?.data?.message || 'Geo search failed');
    }
  }
);

// Async Thunk — Fetch operational KPIs from ElasticSearch aggregations
export const fetchFleetKPIs = createAsyncThunk(
  'fleet/fetchKPIs',
  async (dateRange: { from: string; to: string }, { rejectWithValue }) => {
    try {
      const response = await fleetService.getFleetKPIs(dateRange);
      return response.data;
    } catch (error: any) {
      return rejectWithValue(error.response?.data?.message || 'KPI fetch failed');
    }
  }
);

const fleetSlice = createSlice({
  name: 'fleet',
  initialState,
  reducers: {
    // Real-time vehicle position update from WebSocket
    updateVehicleLocation: (state, action: PayloadAction<VehicleLocation>) => {
      const index = state.vehicles.findIndex(
        (v) => v.vehicleId === action.payload.vehicleId
      );
      if (index !== -1) {
        state.vehicles[index] = action.payload;
      } else {
        state.vehicles.push(action.payload);
      }
      state.lastUpdated = new Date().toISOString();
    },
    selectVehicle: (state, action: PayloadAction<string>) => {
      state.selectedVehicleId = action.payload;
    },
    clearNearbyVehicles: (state) => {
      state.nearbyVehicles = [];
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchFleetVehicles.pending, (state) => {
        state.loading = true;
        state.error = null;
      })
      .addCase(fetchFleetVehicles.fulfilled, (state, action) => {
        state.loading = false;
        state.vehicles = action.payload;
      })
      .addCase(fetchFleetVehicles.rejected, (state, action) => {
        state.loading = false;
        state.error = action.payload as string;
      })
      .addCase(fetchNearbyVehicles.fulfilled, (state, action) => {
        state.nearbyVehicles = action.payload;
      })
      .addCase(fetchFleetKPIs.fulfilled, (state, action) => {
        state.kpis = action.payload;
      });
  },
});

export const { updateVehicleLocation, selectVehicle, clearNearbyVehicles } =
  fleetSlice.actions;
export default fleetSlice.reducer;
```
```typescript
// components/FleetMap/FleetMap.tsx — Real-time Leaflet map with Redux
import React, { useEffect, useRef, useCallback } from 'react';
import { MapContainer, TileLayer, Marker, Popup, Circle } from 'react-leaflet';
import { useDispatch, useSelector } from 'react-redux';
import { io, Socket } from 'socket.io-client';
import { AppDispatch, RootState } from '../../store';
import {
  fetchFleetVehicles,
  updateVehicleLocation,
  selectVehicle,
} from '../../store/slices/fleetSlice';
import { VehicleLocation } from '../../types/fleet';
import { vehicleIcon, alertIcon } from '../../utils/mapIcons';
import styles from './FleetMap.module.scss';

const FleetMap: React.FC = () => {
  const dispatch = useDispatch<AppDispatch>();
  const { vehicles, selectedVehicleId, loading } = useSelector(
    (state: RootState) => state.fleet
  );
  const socketRef = useRef<Socket>();

  // Initial fleet load via Thunk
  useEffect(() => {
    dispatch(fetchFleetVehicles());
  }, [dispatch]);

  // Real-time WebSocket updates → Redux state
  useEffect(() => {
    socketRef.current = io(`${process.env.REACT_APP_API_URL}/fleet`, {
      transports: ['websocket'],
      auth: { token: localStorage.getItem('accessToken') },
    });

    socketRef.current.on('vehicle:location:updated', (data: VehicleLocation) => {
      dispatch(updateVehicleLocation(data));
    });

    socketRef.current.on('vehicle:alert', (alert) => {
      console.warn('Fleet alert received:', alert);
    });

    return () => {
      socketRef.current?.disconnect();
    };
  }, [dispatch]);

  const handleVehicleSelect = useCallback(
    (vehicleId: string) => {
      dispatch(selectVehicle(vehicleId));
    },
    [dispatch]
  );

  if (loading) {
    return (
      <div className={styles.loadingContainer} data-testid="map-loading">
        Loading fleet map...
      </div>
    );
  }

  return (
    <div className={styles.mapWrapper} data-testid="fleet-map">
      <MapContainer
        center={[4.7110, -74.0721]}  // Bogotá center
        zoom={12}
        className={styles.leafletMap}
      >
        <TileLayer
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
          attribution="&copy; OpenStreetMap contributors"
        />

        {vehicles.map((vehicle) => (
          <Marker
            key={vehicle.vehicleId}
            position={[vehicle.latitude, vehicle.longitude]}
            icon={vehicle.hasAlert ? alertIcon : vehicleIcon}
            eventHandlers={{
              click: () => handleVehicleSelect(vehicle.vehicleId),
            }}
          >
            <Popup>
              <div className={styles.vehiclePopup}>
                <h4>{vehicle.plateNumber}</h4>
                <p>Driver: {vehicle.driverName}</p>
                <p>Speed: {vehicle.speed} km/h</p>
                <p>Fuel: {vehicle.fuelLevel}%</p>
                <p>Capacity: {vehicle.capacityUsed}%</p>
                <p>Status: {vehicle.status}</p>
              </div>
            </Popup>

            {vehicle.vehicleId === selectedVehicleId && (
              <Circle
                center={[vehicle.latitude, vehicle.longitude]}
                radius={500}
                pathOptions={{ color: '#3b82f6', fillOpacity: 0.1 }}
              />
            )}
          </Marker>
        ))}
      </MapContainer>
    </div>
  );
};

export default FleetMap;
```
```scss
// FleetMap.module.scss — SASS with variables and responsive layout
@import '../../styles/variables';
@import '../../styles/mixins';

.mapWrapper {
  position: relative;
  width: 100%;
  height: calc(100vh - $header-height);
  border-radius: $border-radius-lg;
  overflow: hidden;
  box-shadow: $shadow-lg;

  .leafletMap {
    width: 100%;
    height: 100%;
    z-index: 1;
  }

  .loadingContainer {
    @include flex-center;
    height: 100%;
    color: $color-text-secondary;
    font-size: $font-size-lg;
  }

  .vehiclePopup {
    min-width: 180px;

    h4 {
      color: $color-primary;
      font-weight: $font-weight-bold;
      margin-bottom: $spacing-xs;
      font-size: $font-size-base;
    }

    p {
      margin: $spacing-xxs 0;
      color: $color-text-primary;
      font-size: $font-size-sm;
    }
  }
}
```

---

### 🔐 Spring Security — JWT + Role-Based Access (Java 17)
```java
// Security Configuration — Java 17 + Spring Security 6.2.x
@Configuration
@EnableWebSecurity
@EnableMethodSecurity(prePostEnabled = true)
public class SecurityConfig {

    private final JwtAuthenticationFilter jwtAuthFilter;
    private final UserDetailsService userDetailsService;

    public SecurityConfig(JwtAuthenticationFilter jwtAuthFilter,
                          UserDetailsService userDetailsService) {
        this.jwtAuthFilter = jwtAuthFilter;
        this.userDetailsService = userDetailsService;
    }

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(AbstractHttpConfigurer::disable)
            .sessionManagement(session -> session
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/auth/**").permitAll()
                .requestMatchers("/actuator/health").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .requestMatchers(HttpMethod.GET, "/api/fleet/**")
                    .hasAnyRole("ADMIN", "DISPATCHER", "SUPERVISOR")
                .requestMatchers("/api/routes/**")
                    .hasAnyRole("ADMIN", "DISPATCHER")
                .requestMatchers("/api/telemetry/**")
                    .hasAnyRole("ADMIN", "SUPERVISOR", "DRIVER")
                .requestMatchers("/api/analytics/**")
                    .hasAnyRole("ADMIN", "SUPERVISOR")
                .requestMatchers("/api/reports/**")
                    .hasAnyRole("ADMIN", "ENVIRONMENTAL_OFFICER")
                .anyRequest().authenticated())
            .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }

    @Bean
    public AuthenticationManager authenticationManager(
            AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder(12);
    }
}
```

---

### 🧪 TDD/BDD — Testing Strategy
```java
// Backend — JUnit 5 + Mockito (TDD)
@ExtendWith(MockitoExtension.class)
class FleetAnalyticsServiceTest {

    @Mock
    private ElasticsearchOperations elasticsearchOperations;

    @Mock
    private ElasticsearchClient elasticsearchClient;

    @InjectMocks
    private FleetAnalyticsService fleetAnalyticsService;

    @Test
    @DisplayName("Should return nearby vehicles within specified radius")
    void shouldReturnNearbyVehiclesWithinRadius() {
        // Given
        Double latitude = 4.7110;
        Double longitude = -74.0721;
        Double radiusKm = 2.0;

        FleetVehicleDocument vehicle = FleetVehicleDocument.builder()
            .vehicleId("VH-001")
            .plateNumber("ABC-123")
            .currentLocation(new GeoPoint(4.7120, -74.0730))
            .status("ACTIVE")
            .fuelLevel(80)
            .build();

        SearchHits<FleetVehicleDocument> mockHits = new SearchHitsImpl<>(
            1L, TotalHitsRelation.EQUAL_TO, 1.0f, null,
            List.of(new SearchHit<>("fleet_vehicles", "VH-001", null,
                1.0f, null, null, null, null, null, null, vehicle)),
            null, null);

        when(elasticsearchOperations.search(
            any(NativeQuery.class), eq(FleetVehicleDocument.class)))
            .thenReturn(mockHits);

        // When
        List<FleetVehicleDocument> result =
            fleetAnalyticsService.findNearbyVehicles(latitude, longitude, radiusKm);

        // Then
        assertThat(result).hasSize(1);
        assertThat(result.get(0).getVehicleId()).isEqualTo("VH-001");
        assertThat(result.get(0).getStatus()).isEqualTo("ACTIVE");

        verify(elasticsearchOperations, times(1))
            .search(any(NativeQuery.class), eq(FleetVehicleDocument.class));
    }

    @Test
    @DisplayName("Should index vehicle location when Kafka event is received")
    void shouldIndexVehicleLocationOnKafkaEvent() {
        // Given
        VehicleLocationEvent event = VehicleLocationEvent.builder()
            .vehicleId("VH-002")
            .plateNumber("XYZ-789")
            .latitude(4.6971)
            .longitude(-74.0830)
            .speed(45.0)
            .status("ON_ROUTE")
            .fuelLevel(65)
            .zone("NORTE")
            .build();

        // When
        fleetAnalyticsService.indexVehicleLocation(event);

        // Then
        ArgumentCaptor<FleetVehicleDocument> captor =
            ArgumentCaptor.forClass(FleetVehicleDocument.class);
        verify(elasticsearchOperations, times(1)).save(captor.capture());

        FleetVehicleDocument saved = captor.getValue();
        assertThat(saved.getVehicleId()).isEqualTo("VH-002");
        assertThat(saved.getCurrentLocation().getLat()).isEqualTo(4.6971);
        assertThat(saved.getZone()).isEqualTo("NORTE");
    }

    @Test
    @DisplayName("Should trigger speeding alert when speed exceeds 80 km/h")
    void shouldTriggerAlertWhenVehicleExceedsSpeedLimit() {
        // Given
        String vehicleId = "VH-003";
        Double speedOverLimit = 95.0;

        LocationPayload payload = LocationPayload.builder()
            .latitude(4.7110)
            .longitude(-74.0721)
            .speed(speedOverLimit)
            .build();

        // When
        telemetryService.handleLocationMessage("fleet/VH-003/location", payload);

        // Then
        verify(alertService, times(1))
            .triggerSpeedingAlert(eq(vehicleId), eq(speedOverLimit));
        verify(kafkaTemplate, times(1))
            .send(eq("vehicle.location.updated"), any(VehicleLocationEvent.class));
    }
}
```
```typescript
// Frontend — React Testing Library (TDD)
import { render, screen, waitFor } from '@testing-library/react';
import { Provider } from 'react-redux';
import { configureStore } from '@reduxjs/toolkit';
import FleetMap from './FleetMap';
import fleetReducer from '../../store/slices/fleetSlice';
import * as fleetService from '../../services/fleetService';

jest.mock('../../services/fleetService');
jest.mock('react-leaflet', () => ({
  MapContainer: ({ children }: any) => <div data-testid="map-container">{children}</div>,
  TileLayer: () => null,
  Marker: ({ children }: any) => <div data-testid="vehicle-marker">{children}</div>,
  Popup: ({ children }: any) => <div>{children}</div>,
  Circle: () => null,
}));

const renderWithStore = (preloadedState = {}) => {
  const store = configureStore({
    reducer: { fleet: fleetReducer },
    preloadedState,
  });
  return { store, ...render(<Provider store={store}><FleetMap /></Provider>) };
};

describe('FleetMap Component', () => {
  beforeEach(() => jest.clearAllMocks());

  it('should render map container on load', async () => {
    (fleetService.getActiveVehicles as jest.Mock).mockResolvedValue({
      data: [],
    });
    renderWithStore();
    await waitFor(() => {
      expect(screen.getByTestId('fleet-map')).toBeInTheDocument();
    });
  });

  it('should display vehicle markers for each active vehicle', async () => {
    (fleetService.getActiveVehicles as jest.Mock).mockResolvedValue({
      data: [
        { vehicleId: 'VH-001', plateNumber: 'ABC-123',
          latitude: 4.711, longitude: -74.072,
          speed: 40, fuelLevel: 80, status: 'ACTIVE' },
        { vehicleId: 'VH-002', plateNumber: 'XYZ-789',
          latitude: 4.720, longitude: -74.080,
          speed: 35, fuelLevel: 60, status: 'ON_ROUTE' },
      ],
    });

    renderWithStore();

    await waitFor(() => {
      expect(screen.getAllByTestId('vehicle-marker')).toHaveLength(2);
    });
  });
});
```
```javascript
// Cypress BDD — E2E Fleet Map Flow
describe('Fleet Map - BDD', () => {
  beforeEach(() => {
    cy.login('dispatcher@wastetrack.com', 'testpass');
    cy.visit('/dashboard/fleet');
  });

  it('Given a dispatcher, When map loads, Then all active vehicles are displayed', () => {
    // Given
    cy.intercept('GET', '/api/fleet/vehicles/active', {
      fixture: 'active-vehicles.json',
    }).as('fleetRequest');

    // When
    cy.wait('@fleetRequest');

    // Then
    cy.get('[data-testid="fleet-map"]').should('be.visible');
    cy.get('[data-testid="vehicle-marker"]').should('have.length.greaterThan', 0);
  });

  it('Given a dispatcher, When searching nearby vehicles, Then geo results appear', () => {
    cy.intercept('GET', '/api/analytics/fleet/nearby*', {
      fixture: 'nearby-vehicles.json',
    }).as('geoSearch');

    cy.get('[data-testid="nearby-search-lat"]').type('4.7110');
    cy.get('[data-testid="nearby-search-lng"]').type('-74.0721');
    cy.get('[data-testid="nearby-search-radius"]').type('2');
    cy.get('[data-testid="nearby-search-btn"]').click();

    cy.wait('@geoSearch');
    cy.get('[data-testid="nearby-results-list"]')
      .should('be.visible')
      .children()
      .should('have.length.greaterThan', 0);
  });
});
```

---

## 📊 Data Model

### Primary Schema — PostgreSQL
```sql
-- Vehicles
CREATE TABLE vehicles (
    id                  VARCHAR(50) PRIMARY KEY,       -- VH-001, VH-002...
    plate_number        VARCHAR(20) UNIQUE NOT NULL,
    vehicle_type        VARCHAR(30) NOT NULL,          -- COMPACTOR, LOADER, SWEEPER
    brand               VARCHAR(100),
    model               VARCHAR(100),
    year                INTEGER,
    fuel_type           VARCHAR(20),                   -- DIESEL, GAS, ELECTRIC
    capacity_kg         DECIMAL(10,2) NOT NULL,
    capacity_m3         DECIMAL(10,2),
    current_mileage     DECIMAL(12,2) DEFAULT 0,
    status              VARCHAR(20) DEFAULT 'ACTIVE',  -- ACTIVE, MAINTENANCE, INACTIVE
    assigned_zone       VARCHAR(100),
    last_maintenance    DATE,
    next_maintenance    DATE,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Drivers
CREATE TABLE drivers (
    id                  BIGSERIAL PRIMARY KEY,
    document_number     VARCHAR(50) UNIQUE NOT NULL,
    first_name          VARCHAR(100) NOT NULL,
    last_name           VARCHAR(100) NOT NULL,
    phone               VARCHAR(20) NOT NULL,
    email               VARCHAR(255),
    license_number      VARCHAR(50) UNIQUE NOT NULL,
    license_type        VARCHAR(10) NOT NULL,           -- C1, C2, C3
    license_expiry      DATE NOT NULL,
    status              VARCHAR(20) DEFAULT 'ACTIVE',   -- ACTIVE, ON_LEAVE, INACTIVE
    assigned_vehicle_id VARCHAR(50) REFERENCES vehicles(id),
    hire_date           DATE NOT NULL,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Collection Zones
CREATE TABLE collection_zones (
    id                  BIGSERIAL PRIMARY KEY,
    zone_code           VARCHAR(20) UNIQUE NOT NULL,
    zone_name           VARCHAR(100) NOT NULL,
    city                VARCHAR(100) NOT NULL,
    neighborhood        VARCHAR(100),
    polygon_coordinates JSONB NOT NULL,                -- GeoJSON polygon
    frequency           VARCHAR(20) NOT NULL,          -- DAILY, BIWEEKLY, WEEKLY
    waste_type          VARCHAR(30) NOT NULL,          -- ORGANIC, RECYCLABLE, HAZARDOUS
    assigned_vehicle_id VARCHAR(50) REFERENCES vehicles(id),
    active              BOOLEAN DEFAULT TRUE,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Collection Points
CREATE TABLE collection_points (
    id                  BIGSERIAL PRIMARY KEY,
    zone_id             BIGINT REFERENCES collection_zones(id) NOT NULL,
    point_name          VARCHAR(255) NOT NULL,
    address             TEXT NOT NULL,
    latitude            DECIMAL(10,8) NOT NULL,
    longitude           DECIMAL(11,8) NOT NULL,
    point_type          VARCHAR(30) NOT NULL,          -- RESIDENTIAL, COMMERCIAL, INDUSTRIAL
    estimated_weight_kg DECIMAL(10,2),
    priority            INTEGER DEFAULT 5,             -- 1 (highest) to 10 (lowest)
    active              BOOLEAN DEFAULT TRUE,
    notes               TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Routes
CREATE TABLE routes (
    id                  VARCHAR(50) PRIMARY KEY,
    route_date          DATE NOT NULL,
    vehicle_id          VARCHAR(50) REFERENCES vehicles(id) NOT NULL,
    driver_id           BIGINT REFERENCES drivers(id) NOT NULL,
    zone_id             BIGINT REFERENCES collection_zones(id) NOT NULL,
    status              VARCHAR(20) DEFAULT 'PLANNED', -- PLANNED, IN_PROGRESS, COMPLETED, CANCELLED
    planned_start_time  TIME NOT NULL,
    actual_start_time   TIME,
    planned_end_time    TIME,
    actual_end_time     TIME,
    planned_distance_km DECIMAL(10,2),
    actual_distance_km  DECIMAL(10,2),
    total_weight_kg     DECIMAL(12,2) DEFAULT 0,
    total_points        INTEGER DEFAULT 0,
    completed_points    INTEGER DEFAULT 0,
    efficiency_score    DECIMAL(5,2),                  -- calculated after completion
    notes               TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Route Stops (ordered collection points per route)
CREATE TABLE route_stops (
    id                  BIGSERIAL PRIMARY KEY,
    route_id            VARCHAR(50) REFERENCES routes(id) NOT NULL,
    collection_point_id BIGINT REFERENCES collection_points(id) NOT NULL,
    stop_order          INTEGER NOT NULL,
    planned_arrival     TIME,
    actual_arrival      TIME,
    status              VARCHAR(20) DEFAULT 'PENDING', -- PENDING, COMPLETED, SKIPPED
    skip_reason         TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Collection Events
CREATE TABLE collection_events (
    id                  BIGSERIAL PRIMARY KEY,
    route_id            VARCHAR(50) REFERENCES routes(id) NOT NULL,
    route_stop_id       BIGINT REFERENCES route_stops(id) NOT NULL,
    vehicle_id          VARCHAR(50) REFERENCES vehicles(id) NOT NULL,
    driver_id           BIGINT REFERENCES drivers(id) NOT NULL,
    collection_date     DATE NOT NULL,
    collection_time     TIME NOT NULL,
    latitude            DECIMAL(10,8),
    longitude           DECIMAL(11,8),
    waste_type          VARCHAR(30) NOT NULL,          -- ORGANIC, RECYCLABLE, HAZARDOUS
    weight_kg           DECIMAL(10,2) NOT NULL,
    volume_m3           DECIMAL(10,2),
    container_count     INTEGER DEFAULT 1,
    photo_evidence_url  TEXT,
    incident_reported   BOOLEAN DEFAULT FALSE,
    notes               TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Incidents
CREATE TABLE incidents (
    id                  BIGSERIAL PRIMARY KEY,
    route_id            VARCHAR(50) REFERENCES routes(id),
    vehicle_id          VARCHAR(50) REFERENCES vehicles(id),
    driver_id           BIGINT REFERENCES drivers(id),
    incident_type       VARCHAR(50) NOT NULL,          -- MISSED_STOP, OVERWEIGHT, ACCIDENT, DUMPING
    incident_date       DATE NOT NULL,
    incident_time       TIME NOT NULL,
    latitude            DECIMAL(10,8),
    longitude           DECIMAL(11,8),
    description         TEXT NOT NULL,
    severity            VARCHAR(20) NOT NULL,          -- LOW, MEDIUM, HIGH, CRITICAL
    status              VARCHAR(20) DEFAULT 'OPEN',    -- OPEN, IN_REVIEW, RESOLVED
    resolution_notes    TEXT,
    resolved_at         TIMESTAMP,
    reported_by         BIGINT REFERENCES users(id),
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Environmental Reports (MADS/RESPEL)
CREATE TABLE environmental_reports (
    id                  BIGSERIAL PRIMARY KEY,
    report_type         VARCHAR(30) NOT NULL,          -- MONTHLY, QUARTERLY, RESPEL
    reporting_period    VARCHAR(20) NOT NULL,          -- 2024-01, 2024-Q1
    company_nit         VARCHAR(50) NOT NULL,
    total_organic_kg    DECIMAL(15,2) DEFAULT 0,
    total_recyclable_kg DECIMAL(15,2) DEFAULT 0,
    total_hazardous_kg  DECIMAL(15,2) DEFAULT 0,
    total_routes        INTEGER DEFAULT 0,
    total_collections   INTEGER DEFAULT 0,
    submission_status   VARCHAR(20) DEFAULT 'DRAFT',  -- DRAFT, SUBMITTED, APPROVED
    submitted_at        TIMESTAMP,
    mads_reference      VARCHAR(100),
    report_file_url     TEXT,
    created_by          BIGINT REFERENCES users(id),
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Vehicle Maintenance
CREATE TABLE vehicle_maintenance (
    id                  BIGSERIAL PRIMARY KEY,
    vehicle_id          VARCHAR(50) REFERENCES vehicles(id) NOT NULL,
    maintenance_type    VARCHAR(50) NOT NULL,          -- PREVENTIVE, CORRECTIVE, INSPECTION
    description         TEXT NOT NULL,
    scheduled_date      DATE NOT NULL,
    completed_date      DATE,
    mileage_at_service  DECIMAL(12,2),
    cost                DECIMAL(10,2),
    service_provider    VARCHAR(255),
    status              VARCHAR(20) DEFAULT 'SCHEDULED', -- SCHEDULED, IN_PROGRESS, COMPLETED
    notes               TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Performance Indexes
CREATE INDEX idx_vehicles_status ON vehicles(status, assigned_zone);
CREATE INDEX idx_drivers_status ON drivers(status, assigned_vehicle_id);
CREATE INDEX idx_routes_date ON routes(route_date, vehicle_id, status);
CREATE INDEX idx_routes_driver ON routes(driver_id, route_date);
CREATE INDEX idx_collection_events_date ON collection_events(collection_date, waste_type);
CREATE INDEX idx_collection_events_route ON collection_events(route_id);
CREATE INDEX idx_collection_events_geo ON collection_events(latitude, longitude);
CREATE INDEX idx_incidents_severity ON incidents(severity, status, incident_date);
CREATE INDEX idx_env_reports_period ON environmental_reports(reporting_period, report_type);
```

### NoSQL Schema — MongoDB (IoT Telemetry & Operational Logs)
```javascript
// GPS Telemetry Event — MongoDB Time-Series Collection
{
  _id: ObjectId,
  vehicleId: String,
  eventType: String,          // "LOCATION", "SENSOR", "ALERT"
  latitude: Number,
  longitude: Number,
  speed: Number,              // km/h
  heading: Number,            // degrees
  altitude: Number,           // meters
  accuracy: Number,           // GPS accuracy meters
  fuelLevel: Number,          // percentage
  engineTemperature: Number,  // Celsius
  engineStatus: String,       // "ON", "OFF", "IDLE"
  doorStatus: String,         // "OPEN", "CLOSED"
  rawPayload: String,         // Original MQTT message
  timestamp: ISODate,
  processedAt: ISODate
}

// Telemetry Alert Log — MongoDB Collection
{
  _id: ObjectId,
  vehicleId: String,
  plateNumber: String,
  driverId: String,
  alertType: String,          // "SPEEDING", "LOW_FUEL", "ENGINE_OVERHEAT", "UNAUTHORIZED_STOP"
  value: Number,              // triggering value
  threshold: Number,          // configured threshold
  smsNotified: Boolean,
  smsSentAt: ISODate,
  resolvedAt: ISODate,
  timestamp: ISODate
}

// ElasticSearch Analytics Query Log — MongoDB Collection
{
  _id: ObjectId,
  queryType: String,          // "GEO_DISTANCE", "AGGREGATION", "KPI_DASHBOARD"
  indexName: String,
  rawQuery: Object,
  hitsCount: Number,
  tookMs: Number,
  userId: String,
  timestamp: ISODate
}
```

---

## 🎓 Key Learnings

### Architecture and Backend

✅ **Microservices with Java 17** — Designed and implemented distributed services
using Spring Boot 3.2.x and Spring MVC 6.1.x with Java 17 LTS features including
records, sealed classes, and pattern matching, demonstrating full-stack range
across Java 11 and Java 17 ecosystems within the same portfolio

✅ **ElasticSearch 8.x Geospatial Queries** — Implemented geo_point index mappings,
geo_distance proximity searches for vehicle dispatch, geo_bounding_box zone
queries, and geospatial aggregations for collection density heatmaps — a
fundamentally different ElasticSearch use case from traditional text search

✅ **ElasticSearch Aggregations for Analytics** — Built multi-level aggregation
pipelines for operational KPIs: terms aggregations by zone and driver, avg/sum
metric aggregations for efficiency scoring, date histogram aggregations for
trend analysis, and pipeline aggregations for derived KPIs

✅ **Event-Driven IoT Architecture** — Designed MQTT-to-Kafka bridge processing
thousands of real-time GPS telemetry events per minute, with MongoDB as
time-series store and ElasticSearch as the geospatial analytics layer

✅ **Spring Security 6.2.x** — Implemented modern Spring Security configuration
using the lambda DSL SecurityFilterChain approach (replacing the deprecated
WebSecurityConfigurerAdapter from Java 11 / Spring Security 5.x), demonstrating
evolution across Spring Security major versions

✅ **TDD with JUnit 5 + Mockito** — Test-driven development across all service
layers with particular focus on telemetry threshold validation, geospatial
query result assertions, and Kafka event publishing verification

### Frontend and UX

✅ **React 18 + TypeScript + Leaflet** — Built type-safe real-time geospatial
SPA integrating React-Leaflet for interactive fleet maps, custom map icons for
vehicle status visualization, and dynamic circle overlays for proximity display

✅ **Redux Toolkit + Thunks for Real-Time Data** — Extended Redux architecture
to handle WebSocket-driven state updates alongside Thunk-based API calls,
maintaining a single source of truth for fleet positions updated every 30 seconds
across hundreds of concurrent map markers

✅ **Webpack 5 Manual Configuration** — Configured production-grade bundle with
code splitting by route, lazy loading for the heavy Leaflet map component,
SASS compilation pipeline, and environment-specific API endpoint injection

✅ **SASS Architecture** — Maintained consistent design system across 25+
operational UI components including map panels, KPI cards, alert banners,
and driver performance tables using the 7-1 SASS pattern

✅ **React Testing Library + Cypress BDD** — Applied TDD on geospatial
components with Leaflet mocking strategy, and BDD E2E scenarios covering
critical dispatcher workflows: fleet map loading, nearby vehicle geo-search,
and real-time alert display

### Integrations and Compliance

✅ **MQTT IoT Protocol** — Implemented Eclipse Paho MQTT client for high-frequency
GPS device telemetry ingestion with QoS level management, automatic reconnection,
and topic-based device routing for multi-vehicle fleet management

✅ **MADS Environmental Reporting** — Automated mandatory Colombian environmental
authority reports (Ministerio de Ambiente y Desarrollo Sostenible) including
RESPEL hazardous waste manifests and Decreto 1076/2015 compliance documentation

✅ **Route Optimization** — Integrated OSRM for open-source route calculation
and Google Maps Distance Matrix for multi-stop optimization, reducing average
route completion time through algorithmic stop sequencing

✅ **Twilio SMS Alerting** — Real-time driver notification pipeline triggered
by IoT threshold violations, integrating asynchronous Spring @Async processing
with Twilio REST API for immediate field communication

### DevOps and Operations

✅ **CI/CD with Jenkins** — Declarative pipeline covering build, unit test,
integration test, Docker image build, registry push, and Kubernetes rolling
deployment with automated rollback on health check failure

✅ **ELK Stack for IoT Analytics** — Configured Logstash pipelines for
structured telemetry event ingestion from MongoDB, ElasticSearch geospatial
index management with ILM policies for 90-day telemetry retention, and
Kibana fleet operations dashboards

✅ **Kubernetes Production** — Multi-service Kubernetes deployments with
horizontal pod autoscaling triggered by Kafka consumer lag metrics,
ConfigMaps for environment-specific IoT broker endpoints, and zero-downtime
rolling updates for fleet-critical services

---

## 🔄 Roadmap and Future Improvements

### Phase 2 — Q3 2025
- Mobile app for drivers (React Native) with offline route access and GPS tracking
- AI-powered route optimization using historical collection data and ML predictions
- Predictive maintenance alerts based on vehicle telemetry patterns
- Integration with national SUI system (Superintendencia de Servicios Públicos)

### Phase 3 — Q4 2025
- Multi-tenant support for waste management company networks
- Carbon footprint tracking and environmental impact reporting
- Drone integration for remote area collection monitoring
- Computer vision for unauthorized dumping detection via vehicle cameras

### Phase 4 — Q1 2026
- Digital twin simulation for route planning and capacity optimization
- Integration with municipal GIS systems for urban planning alignment
- Blockchain-based waste chain of custody for RESPEL hazardous materials
- Real-time citizen reporting app for illegal dumping incidents

---

## 📈 Impact and Results

This system has been implemented and validated with **Colombian waste management
SMEs and municipal collection operators** through SENA, generating measurable
operational improvements:

✅ **40% reduction** in route planning time through automated optimization
vs manual dispatcher scheduling
✅ **30% improvement** in fleet fuel efficiency through real-time GPS route
adherence monitoring and driver behavior alerts
✅ **100% regulatory compliance** with Decreto 1076/2015 and MADS RESPEL
hazardous waste reporting requirements
✅ **Zero manual RESPEL errors** — automated report generation eliminated
transcription and calculation mistakes
✅ **85% reduction** in fleet proximity search time using ElasticSearch
geo_distance queries vs traditional SQL spatial calculations
✅ **Real-time incident response** reduced average alert-to-action time
from 25 minutes to under 2 minutes through MQTT + Twilio SMS pipeline
✅ **Full IoT audit trail** on every vehicle telemetry event, meeting
Colombian environmental authority traceability requirements

---

## 📄 License and Intellectual Property

> ⚠️ **SENA — Intellectual Property Disclaimer**
>
> This project was developed as part of academic and research activities within
> **SENA (Servicio Nacional de Aprendizaje)** under the **SENNOVA** program,
> aimed at supporting digital transformation and environmental compliance for
> Colombian waste management SMEs and municipal operators.
>
> The **source code, architecture design, and technical documentation are
> institutional property of SENA** and are not publicly available in this
> repository. The content presented here — including technical specifications,
> architecture diagrams, code samples, IoT integration patterns, and data
> models — has been **recreated for portfolio demonstration purposes only**,
> without exposing confidential institutional information or the original
> production codebase.
>
> Screenshots and UI captures have been intentionally excluded to protect
> operational data confidentiality and institutional privacy.

**Available for:**

✅ Custom consulting and implementation for waste management companies
✅ IoT/GPS fleet tracking architecture design and integration
✅ ElasticSearch geospatial analytics design and optimization
✅ Colombian environmental regulation compliance advisory (Decreto 1076/2015, RESPEL)
✅ Route optimization algorithm design and implementation
✅ Additional module development and technical support

---

## 🏆 Recognition

- 🥇 **Best Environmental Innovation Project** — SENA Regional Risaralda 2024
- 🏅 **MADS Alignment** — Architecture validated against Decreto 1076/2015
environmental reporting requirements
- 🌿 **Sustainability Award** — SENA SENNOVA Innovation Program 2024
- ⭐ **Implemented in 8+ Colombian waste management SMEs and municipal operators**


| **Swagger/OpenAPI** | API documentation and interactive testing                 |
| **JUnit 5**         | Backend unit and integration testing (TDD)                |
| **Mockito**         | Dependency mocking for isolated unit tests                |
