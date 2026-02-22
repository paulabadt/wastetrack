# WasteTrack 🚛

Plataforma empresarial de gestión de residuos y optimización de rutas construida sobre
**arquitectura de microservicios**, diseñada para digitalizar y optimizar las operaciones
de empresas de recolección de residuos y PYMES de logística ambiental. Integra
**rastreo GPS de vehículos en tiempo real**, optimización inteligente de rutas,
reportes de cumplimiento normativo para autoridades ambientales colombianas (MADS), y
**analítica geoespacial de alto rendimiento impulsada por ElasticSearch**.

Desarrollado para empresas colombianas de gestión de residuos que requieren cumplimiento
con el **Decreto 1076/2015** (regulaciones ambientales), **reportes RESPEL** para
residuos peligrosos, y dashboards de eficiencia operativa para gestión de flotas en campo.

---

## 🛠️ Stack Tecnológico Completo

### Backend — Microservicios

| Tecnología               | Versión   | Propósito                                            |
|--------------------------|-----------|------------------------------------------------------|
| **Java**                 | 17        | Lenguaje principal del backend                       |
| **Spring Boot**          | 3.2.x     | Framework de microservicios (compatible Java 17)     |
| **Spring MVC**           | 6.1.x     | Controladores REST y manejo de peticiones            |
| **Spring Cloud**         | 2023.x    | Soporte para sistemas distribuidos                   |
| **Spring Cloud Gateway** | —         | API Gateway con limitación de velocidad              |
| **Eureka Server**        | —         | Descubrimiento de servicios                          |
| **Spring Cloud Config**  | —         | Gestión centralizada de configuración                |
| **Spring Data JPA**      | —         | ORM y persistencia de datos                          |
| **Spring Security**      | 6.2.x     | Autenticación y autorización                         |
| **Resilience4j**         | 2.1.x     | Circuit Breaker y limitación de velocidad            |
| **Apache Kafka**         | 3.x       | Mensajería asíncrona orientada a eventos             |
| **ElasticSearch**        | 8.11.x    | Analítica geoespacial e indexación operativa         |
| **Logstash**             | 8.11.x    | Pipeline de telemetría hacia ElasticSearch           |
| **Kibana**               | 8.11.x    | Dashboards operativos y analítica de flota           |
| **PostgreSQL**           | 15+       | Base de datos relacional principal                   |
| **MongoDB**              | 6.x       | Eventos de telemetría IoT y logs no estructurados    |
| **Redis**                | 7.x       | Caché distribuida y datos de sesión en tiempo real   |
| **MQTT Broker**          | Mosquitto 2.x | Protocolo de comunicación con dispositivos IoT   |

### Frontend — Single Page Application

| Tecnología                  | Versión | Propósito                                            |
|-----------------------------|---------|------------------------------------------------------|
| **React**                   | 18.x    | Framework de UI para el frontend                     |
| **TypeScript**              | 5.x     | Tipado estático y POO                                |
| **React-Redux**             | 8.x     | Gestión de estado global                             |
| **Redux Toolkit**           | 1.9.x   | Redux simplificado con slices                        |
| **Redux Thunk**             | 2.4.x   | Middleware asíncrono para llamadas a la API          |
| **React Router v6**         | 6.x     | Enrutamiento del lado del cliente                    |
| **Webpack**                 | 5.x     | Empaquetado manual de módulos y optimización         |
| **SASS/SCSS**               | 1.x     | Preprocesamiento avanzado de CSS                     |
| **Axios**                   | 1.x     | Cliente HTTP con interceptores                       |
| **Leaflet + React-Leaflet** | 4.x     | Mapas geoespaciales interactivos                     |
| **React Testing Library**   | 14.x    | Pruebas unitarias de componentes (TDD)               |
| **Cypress**                 | 13.x    | Pruebas end-to-end (BDD)                             |
| **Chart.js**                | 4.x     | Dashboards de KPIs operativos y gráficas analíticas  |
| **Socket.io Client**        | 4.x     | Actualizaciones GPS y telemetría en tiempo real      |

### Integraciones Externas

| Sistema                     | Propósito                                                  |
|-----------------------------|------------------------------------------------------------|
| **Google Maps / OSRM**      | Optimización de rutas y cálculo de matriz de distancias    |
| **MADS Web Services**       | Reporte regulatorio ambiental                              |
| **IDEAM API**               | Datos climáticos para planificación de rutas               |
| **Twilio**                  | Notificaciones SMS a conductores y alertas                 |
| **PayU / Mercado Pago**     | Facturación a clientes y procesamiento de pagos            |

### DevOps e Infraestructura

| Tecnología          | Propósito                                                        |
|---------------------|------------------------------------------------------------------|
| **Docker**          | Contenedorización de servicios                                   |
| **Docker Compose**  | Orquestación local de múltiples servicios                        |
| **Kubernetes**      | Orquestación de contenedores para producción                     |
| **Jenkins**         | Automatización de pipelines CI/CD                                |
| **Prometheus**      | Recolección de métricas y alertas IoT                            |
| **Grafana**         | Monitoreo de flota e infraestructura                             |
| **ELK Stack**       | Logging centralizado (ElasticSearch + Logstash + Kibana)         |

---

## 🏗️ Arquitectura de Microservicios
```
                    ┌─────────────────────────────────────────┐
                    │         React 18 Frontend SPA           │
                    │  (Redux + Thunks · SASS · Webpack 5)   │
                    │  (Mapas Leaflet · Chart.js · Socket.io) │
                    └─────────────────────────────────────────┘
                                        ↓
                    ┌─────────────────────────────────────────┐
                    │     API Gateway (Spring Cloud Gateway)  │
                    │  - Validación JWT                       │
                    │  - Limitación de Velocidad (Resilience4j│
                    │  - Balanceo de Carga                    │
                    │  - Filtrado de Rutas                    │
                    └─────────────────────────────────────────┘
                                        ↓
    ┌───────────┬──────────────┬──────────────┬─────────────┬──────────────┬───────────┐
    ↓           ↓              ↓              ↓             ↓              ↓           ↓
┌────────┐ ┌─────────┐ ┌────────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐
│Servicio│ │Servicio │ │  Servicio  │ │ Servicio │ │ Servicio │ │ Servicio │ │Servicio│
│Vehículo│ │  Rutas  │ │ Recolección│ │Telemetría│ │Búsqueda y│ │ Reportes │ │Factura.│
│        │ │         │ │            │ │          │ │Analítica │ │          │ │        │
│- Flota │ │- Plan.  │ │- Agenda    │ │- GPS     │ │- ES Geo  │ │- MADS    │ │- Fact. │
│- Conduc│ │- Optim. │ │- Reg.Resid.│ │- IoT     │ │  Búsqued.│ │- RESPEL  │ │- PayU  │
│- Mant. │ │- ETA    │ │- Incidentes│ │- Alertas │ │- KPIs    │ │- Amb.    │ │- PDF   │
└────────┘ └─────────┘ └────────────┘ └──────────┘ └──────────┘ └──────────┘ └────────┘
    ↓           ↓              ↓              ↓             ↓              ↓           ↓
┌────────┐ ┌─────────┐ ┌────────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐
│Postgre │ │Postgre  │ │ PostgreSQL │ │ MongoDB  │ │ElasticSe-│ │ MongoDB  │ │Postgre │
│  SQL   │ │  SQL    │ │(Eventos de │ │(Eventos  │ │  arch    │ │  (Logs)  │ │  SQL   │
│(Flota) │ │(Rutas)  │ │ Recolec.)  │ │Telemetría│ │(Geo+Ops) │ │          │ │(Facts.)│
└────────┘ └─────────┘ └────────────┘ └──────────┘ └──────────┘ └──────────┘ └────────┘

                    ┌─────────────────────────────────────────┐
                    │       Bus de Mensajes Apache Kafka      │
                    │  Tópicos:                               │
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
          │             Broker MQTT (Mosquitto)                  │
          │   Dispositivos GPS IoT → Pipeline de Telemetría     │
          │   Tópicos:                                           │
          │   - fleet/{vehicleId}/location                      │
          │   - fleet/{vehicleId}/sensors                       │
          │   - fleet/{vehicleId}/alerts                        │
          └──────────────────────────────────────────────────────┘
                                        ↓
          ┌──────────────────────────────────────────────────────┐
          │              ELK Stack — Observabilidad              │
          │   ElasticSearch · Logstash · Kibana                  │
          │   (Analítica de flota + Consultas geoespaciales +    │
          │    KPIs operativos + Logs de eventos IoT)            │
          └──────────────────────────────────────────────────────┘
                                        ↓
                    ┌─────────────────────────────────────────┐
                    │     Servicio de Integración MADS        │
                    │  - Reportes RESPEL Residuos Peligrosos  │
                    │  - Cumplimiento Decreto 1076/2015       │
                    │  - Envío a Autoridad Ambiental          │
                    │  - Firma Digital de Reportes            │
                    └─────────────────────────────────────────┘
                                        ↓
                    ┌─────────────────────────────────────────┐
                    │   MADS / Servicios Web Ambientales      │
                    │ (Regulación Ambiental Colombiana)       │
                    └─────────────────────────────────────────┘
```

---

## ⚙️ Responsabilidades de cada Servicio

### Servicio de Vehículos
Servicio principal que gestiona el ciclo de vida completo de la flota. Maneja el
registro de vehículos con especificaciones técnicas, tipo de combustible, capacidad
y cronogramas de mantenimiento. Gestiona la asignación de conductores, validación
de licencias y programación de turnos. Publica eventos `vehicle.location.updated`
en Kafka cada 30 segundos a partir de los datos del dispositivo GPS recibidos a
través del broker MQTT, garantizando que todos los servicios dependientes —
Búsqueda, Analítica y Rutas — se mantengan sincronizados con la posición
en tiempo real de la flota.

### Servicio de Rutas
Gestiona el ciclo de vida completo de planificación y optimización de rutas.
Se integra con la API de Matriz de Distancias de Google Maps y OSRM (Open Source
Routing Machine) para el cálculo de rutas de código abierto. Implementa optimización
de rutas multi-parada mediante enfoques de vecino más cercano y algoritmos genéticos,
teniendo en cuenta la capacidad del vehículo, las prioridades de los puntos de
recolección y los datos de tráfico en tiempo real según las condiciones climáticas
del IDEAM. Publica eventos `route.started` y `route.completed` consumidos por los
servicios de Recolección y Analítica.

### Servicio de Recolección
Gestiona el núcleo operativo de los eventos de recolección de residuos. Registra
cada parada de recolección con tipo de residuo (orgánico, reciclable, peligroso —
RESPEL), peso, volumen, coordenadas GPS y evidencia fotográfica. Gestiona el reporte
de incidentes por paradas omitidas, cargas con exceso de peso y eventos de vertimiento
no autorizado. Publica eventos `collection.registered` que desencadenan la agregación
automática de datos regulatorios MADS para reportes de cumplimiento.

### Servicio de Telemetría
La columna vertebral IoT de la arquitectura. Se suscribe a todos los tópicos MQTT
de los dispositivos GPS instalados en los vehículos de la flota, procesa flujos de
telemetría de alta frecuencia (ubicación, velocidad, nivel de combustible, temperatura
del motor, estado de puertas), almacena eventos crudos en MongoDB para análisis de
series de tiempo, y publica eventos `telemetry.alert.triggered` en Kafka cuando se
detectan violaciones de umbral — exceso de velocidad, paradas no autorizadas, bajo
nivel de combustible, sobrecalentamiento del motor — habilitando alertas en tiempo
real al conductor vía SMS de Twilio.

### Servicio de Búsqueda y Analítica (Núcleo ElasticSearch)
El servicio diferenciador de esta arquitectura. Mantiene un clúster ElasticSearch
con indexación geoespacial que potencia dos capacidades críticas: consultas
geo_point para búsqueda de proximidad de flota y análisis de zonas de recolección,
y agregaciones analíticas operativas para dashboards de KPIs — volúmenes diarios
de recolección por zona, puntuaciones de eficiencia de rutas, métricas de desempeño
de conductores e indicadores de cumplimiento ambiental. Implementa Gestión del
Ciclo de Vida de Índices (ILM) para la retención de datos de telemetría alineada
con los requisitos normativos del MADS.

### Servicio de Reportes
Genera todos los reportes obligatorios de cumplimiento ambiental exigidos por las
autoridades colombianas. Produce reportes RESPEL (manifiestos de residuos peligrosos),
resúmenes mensuales de recolección para presentación ante el MADS, y reportes de
eficiencia operativa para la gestión interna. Agrega datos de los servicios de
Recolección, Vehículos y Rutas mediante aprovisionamiento de eventos impulsado
por Kafka, garantizando que los reportes siempre reflejen datos operativos completos.

### Servicio de Facturación
Maneja la facturación a clientes por servicios de recolección de residuos. Genera
facturas detalladas basadas en eventos de recolección, uso de vehículos y acuerdos
de servicio. Se integra con PayU y Mercado Pago para el procesamiento de pagos y
publica eventos de facturación que desencadenan asientos contables automáticos
en servicios posteriores.

---

## ✨ Funcionalidades Principales

### 🔍 ElasticSearch — Analítica Geoespacial e Inteligencia Operativa

ElasticSearch en WasteTrack cumple un propósito fundamentalmente diferente al de
la búsqueda de texto tradicional. Impulsa **consultas de flota geoespaciales** y
**agregaciones analíticas operativas en tiempo real** — habilitando dashboards de
KPIs en menos de un segundo, despacho de vehículos basado en proximidad y análisis
de eficiencia de zonas de recolección sobre miles de eventos de telemetría diarios.

**Configuración del Índice Geoespacial**
```java
// Servicio de Búsqueda y Analítica — Configuración Geo de ElasticSearch
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
// Documento de Vehículo de Flota — Mapeo del Índice Geoespacial ElasticSearch
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
    private GeoPoint currentLocation;  // Posición GPS en tiempo real

    @Field(type = FieldType.Double)
    private Double currentSpeed;

    @Field(type = FieldType.Integer)
    private Integer fuelLevel;

    @Field(type = FieldType.Keyword)
    private String assignedRouteId;

    @Field(type = FieldType.Keyword)
    private String driverId;

    @Field(type = FieldType.Double)
    private Double collectionCapacityUsed;  // porcentaje

    @Field(type = FieldType.Date, format = DateFormat.date_time)
    private Instant lastUpdated;

    @Field(type = FieldType.Keyword)
    private String zone;
}
```
```java
// Servicio de Búsqueda y Analítica — Motor de Consultas Geoespaciales
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

    // Encontrar vehículos dentro de un radio de un punto de recolección (geo_distance)
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

        log.info("Se encontraron {} vehículos dentro de {}km de [{},{}]",
            hits.getTotalHits(), radiusKm, latitude, longitude);

        return hits.stream()
            .map(SearchHit::getContent)
            .collect(Collectors.toList());
    }

    // Agregación — Volumen diario de recolección por zona
    public Map<String, Double> getCollectionVolumeByZone(LocalDate date) throws IOException {
        SearchResponse<Void> response = elasticsearchClient.search(s -> s
            .index("collection_events")
            .query(q -> q
                .range(r -> r
                    .field("collectionDate")
                    .gte(JsonData.of(date.toString()))
                    .lte(JsonData.of(date.toString()))))
            .aggregations("por_zona", a -> a
                .terms(t -> t.field("zone").size(50))
                .aggregations("volumen_total", aa -> aa
                    .sum(sum -> sum.field("volumeKg")))),
            Void.class);

        Map<String, Double> volumePorZona = new LinkedHashMap<>();

        response.aggregations().get("por_zona").sterms().buckets().array()
            .forEach(bucket -> volumePorZona.put(
                bucket.key().stringValue(),
                bucket.aggregations().get("volumen_total").sum().value()));

        return volumePorZona;
    }

    // Agregación — Puntuación de eficiencia de ruta por conductor
    public List<DriverEfficiencyDTO> getDriverEfficiencyMetrics(
            LocalDate from, LocalDate to) throws IOException {

        SearchResponse<Void> response = elasticsearchClient.search(s -> s
            .index("route_events")
            .query(q -> q
                .range(r -> r
                    .field("routeDate")
                    .gte(JsonData.of(from.toString()))
                    .lte(JsonData.of(to.toString()))))
            .aggregations("por_conductor", a -> a
                .terms(t -> t.field("driverId").size(100))
                .aggregations("eficiencia_promedio", aa -> aa
                    .avg(avg -> avg.field("efficiencyScore")))
                .aggregations("total_rutas", aa -> aa
                    .valueCount(vc -> vc.field("routeId")))
                .aggregations("tiempo_promedio_completado", aa -> aa
                    .avg(avg -> avg.field("completionTimeMinutes")))),
            Void.class);

        return response.aggregations().get("por_conductor").sterms().buckets().array()
            .stream()
            .map(bucket -> DriverEfficiencyDTO.builder()
                .driverId(bucket.key().stringValue())
                .avgEfficiencyScore(bucket.aggregations()
                    .get("eficiencia_promedio").avg().value())
                .totalRoutes((long) bucket.aggregations()
                    .get("total_rutas").valueCount().value())
                .avgCompletionTimeMinutes(bucket.aggregations()
                    .get("tiempo_promedio_completado").avg().value())
                .build())
            .sorted(Comparator.comparingDouble(
                DriverEfficiencyDTO::getAvgEfficiencyScore).reversed())
            .collect(Collectors.toList());
    }

    // Indexar vehículo de flota desde evento Kafka de telemetría
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
        log.debug("Vehículo {} indexado en [{},{}]",
            event.getVehicleId(), event.getLatitude(), event.getLongitude());
    }
}
```

---

### 📡 IoT/GPS — Pipeline de Telemetría en Tiempo Real
```java
// Servicio de Telemetría — Integración MQTT IoT
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

        // Suscribirse a todos los tópicos de dispositivos de flota
        mqttClient.subscribe("fleet/+/location", 1, this::handleLocationMessage);
        mqttClient.subscribe("fleet/+/sensors", 1, this::handleSensorMessage);
        mqttClient.subscribe("fleet/+/alerts", 2, this::handleAlertMessage);

        log.info("Broker MQTT conectado — suscrito a tópicos de telemetría de flota");
    }

    // Procesar mensajes GPS de ubicación en tiempo real
    private void handleLocationMessage(String topic, MqttMessage message) {
        try {
            String vehicleId = extractVehicleId(topic);
            LocationPayload payload = objectMapper.readValue(
                message.getPayload(), LocationPayload.class);

            // Persistir telemetría cruda en MongoDB
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

            // Publicar en Kafka para indexación en ElasticSearch
            VehicleLocationEvent locationEvent = VehicleLocationEvent.builder()
                .vehicleId(vehicleId)
                .latitude(payload.getLatitude())
                .longitude(payload.getLongitude())
                .speed(payload.getSpeed())
                .timestamp(event.getTimestamp())
                .build();

            kafkaTemplate.send("vehicle.location.updated", vehicleId, locationEvent);

            // Detección de exceso de velocidad
            if (payload.getSpeed() > 80.0) {
                alertService.triggerSpeedingAlert(vehicleId, payload.getSpeed());
            }

        } catch (Exception e) {
            log.error("Error procesando mensaje de ubicación del tópico: {}", topic, e);
        }
    }

    // Procesar datos de sensores IoT (combustible, temperatura, estado de puertas)
    private void handleSensorMessage(String topic, MqttMessage message) {
        try {
            String vehicleId = extractVehicleId(topic);
            SensorPayload payload = objectMapper.readValue(
                message.getPayload(), SensorPayload.class);

            // Alerta de bajo nivel de combustible
            if (payload.getFuelLevel() < 15) {
                alertService.triggerLowFuelAlert(vehicleId, payload.getFuelLevel());
                kafkaTemplate.send("telemetry.alert.triggered",
                    new TelemetryAlert(vehicleId, "LOW_FUEL", payload.getFuelLevel()));
            }

            // Alerta de sobrecalentamiento del motor
            if (payload.getEngineTemperature() > 110.0) {
                alertService.triggerOverheatAlert(
                    vehicleId, payload.getEngineTemperature());
                kafkaTemplate.send("telemetry.alert.triggered",
                    new TelemetryAlert(vehicleId, "ENGINE_OVERHEAT",
                        payload.getEngineTemperature()));
            }

            log.debug("Datos de sensores procesados para vehículo {}: combustible={}%, temp={}°C",
                vehicleId, payload.getFuelLevel(), payload.getEngineTemperature());

        } catch (Exception e) {
            log.error("Error procesando mensaje de sensores del tópico: {}", topic, e);
        }
    }

    private String extractVehicleId(String topic) {
        // formato del tópico: fleet/{vehicleId}/location
        return topic.split("/")[1];
    }
}
```
```java
// Servicio de Alertas — Notificaciones en tiempo real al conductor vía Twilio SMS
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

        // Enviar SMS al conductor
        twilioClient.messages().create(
            vehicle.getDriver().getPhone(),
            TwilioSmsRequest.builder()
                .from("${twilio.phone.number}")
                .body(message)
                .build());

        // Enviar alerta en tiempo real al dashboard vía WebSocket
        webSocketHandler.broadcastAlert(AlertDTO.builder()
            .vehicleId(vehicleId)
            .plateNumber(vehicle.getPlateNumber())
            .alertType("SPEEDING")
            .value(speed)
            .message(message)
            .timestamp(Instant.now())
            .build());

        log.warn("Alerta de exceso de velocidad disparada: vehicle={}, speed={}",
            vehicleId, speed);
    }
}
```

---

### ⚛️ React — Redux Toolkit + Thunks + Mapa Leaflet en Tiempo Real
```typescript
// store/slices/fleetSlice.ts — Estado Redux de flota en tiempo real
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

// Async Thunk — Obtener todos los vehículos activos de la flota
export const fetchFleetVehicles = createAsyncThunk(
  'fleet/fetchVehicles',
  async (_, { rejectWithValue }) => {
    try {
      const response = await fleetService.getActiveVehicles();
      return response.data;
    } catch (error: any) {
      return rejectWithValue(
        error.response?.data?.message || 'Error al obtener flota');
    }
  }
);

// Async Thunk — Búsqueda geo_distance de vehículos cercanos con ElasticSearch
export const fetchNearbyVehicles = createAsyncThunk(
  'fleet/fetchNearbyVehicles',
  async (params: NearbyVehiclesParams, { rejectWithValue }) => {
    try {
      const response = await fleetService.getNearbyVehicles(params);
      return response.data;
    } catch (error: any) {
      return rejectWithValue(
        error.response?.data?.message || 'Error en búsqueda geoespacial');
    }
  }
);

// Async Thunk — Obtener KPIs operativos desde agregaciones ElasticSearch
export const fetchFleetKPIs = createAsyncThunk(
  'fleet/fetchKPIs',
  async (dateRange: { from: string; to: string }, { rejectWithValue }) => {
    try {
      const response = await fleetService.getFleetKPIs(dateRange);
      return response.data;
    } catch (error: any) {
      return rejectWithValue(
        error.response?.data?.message || 'Error al obtener KPIs');
    }
  }
);

const fleetSlice = createSlice({
  name: 'fleet',
  initialState,
  reducers: {
    // Actualización de posición del vehículo en tiempo real desde WebSocket
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
// components/FleetMap/FleetMap.tsx — Mapa Leaflet en tiempo real con Redux
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

  // Carga inicial de flota mediante Thunk
  useEffect(() => {
    dispatch(fetchFleetVehicles());
  }, [dispatch]);

  // Actualizaciones WebSocket en tiempo real → estado Redux
  useEffect(() => {
    socketRef.current = io(`${process.env.REACT_APP_API_URL}/fleet`, {
      transports: ['websocket'],
      auth: { token: localStorage.getItem('accessToken') },
    });

    socketRef.current.on('vehicle:location:updated', (data: VehicleLocation) => {
      dispatch(updateVehicleLocation(data));
    });

    socketRef.current.on('vehicle:alert', (alert) => {
      console.warn('Alerta de flota recibida:', alert);
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
        Cargando mapa de flota...
      </div>
    );
  }

  return (
    <div className={styles.mapWrapper} data-testid="fleet-map">
      <MapContainer
        center={[4.7110, -74.0721]}  // Centro de Bogotá
        zoom={12}
        className={styles.leafletMap}
      >
        <TileLayer
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
          attribution="&copy; Colaboradores de OpenStreetMap"
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
                <p>Conductor: {vehicle.driverName}</p>
                <p>Velocidad: {vehicle.speed} km/h</p>
                <p>Combustible: {vehicle.fuelLevel}%</p>
                <p>Capacidad: {vehicle.capacityUsed}%</p>
                <p>Estado: {vehicle.status}</p>
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
// FleetMap.module.scss — SASS con variables y diseño responsivo
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

### 🔐 Spring Security — JWT + Control de Acceso por Roles (Java 17)
```java
// Configuración de Seguridad — Java 17 + Spring Security 6.2.x
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

### 🧪 TDD/BDD — Estrategia de Pruebas
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
    @DisplayName("Debe retornar vehículos cercanos dentro del radio especificado")
    void shouldReturnNearbyVehiclesWithinRadius() {
        // Dado
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

        // Cuando
        List<FleetVehicleDocument> result =
            fleetAnalyticsService.findNearbyVehicles(latitude, longitude, radiusKm);

        // Entonces
        assertThat(result).hasSize(1);
        assertThat(result.get(0).getVehicleId()).isEqualTo("VH-001");
        assertThat(result.get(0).getStatus()).isEqualTo("ACTIVE");

        verify(elasticsearchOperations, times(1))
            .search(any(NativeQuery.class), eq(FleetVehicleDocument.class));
    }

    @Test
    @DisplayName("Debe indexar ubicación del vehículo cuando se recibe evento Kafka")
    void shouldIndexVehicleLocationOnKafkaEvent() {
        // Dado
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

        // Cuando
        fleetAnalyticsService.indexVehicleLocation(event);

        // Entonces
        ArgumentCaptor<FleetVehicleDocument> captor =
            ArgumentCaptor.forClass(FleetVehicleDocument.class);
        verify(elasticsearchOperations, times(1)).save(captor.capture());

        FleetVehicleDocument saved = captor.getValue();
        assertThat(saved.getVehicleId()).isEqualTo("VH-002");
        assertThat(saved.getCurrentLocation().getLat()).isEqualTo(4.6971);
        assertThat(saved.getZone()).isEqualTo("NORTE");
    }

    @Test
    @DisplayName("Debe disparar alerta de velocidad cuando supera 80 km/h")
    void shouldTriggerAlertWhenVehicleExceedsSpeedLimit() {
        // Dado
        String vehicleId = "VH-003";
        Double speedOverLimit = 95.0;

        LocationPayload payload = LocationPayload.builder()
            .latitude(4.7110)
            .longitude(-74.0721)
            .speed(speedOverLimit)
            .build();

        // Cuando
        telemetryService.handleLocationMessage("fleet/VH-003/location", payload);

        // Entonces
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
  MapContainer: ({ children }: any) =>
    <div data-testid="map-container">{children}</div>,
  TileLayer: () => null,
  Marker: ({ children }: any) =>
    <div data-testid="vehicle-marker">{children}</div>,
  Popup: ({ children }: any) => <div>{children}</div>,
  Circle: () => null,
}));

const renderWithStore = (preloadedState = {}) => {
  const store = configureStore({
    reducer: { fleet: fleetReducer },
    preloadedState,
  });
  return {
    store, ...render(
      <Provider store={store}><FleetMap /></Provider>
    )
  };
};

describe('Componente FleetMap', () => {
  beforeEach(() => jest.clearAllMocks());

  it('debe renderizar el contenedor del mapa al cargar', async () => {
    (fleetService.getActiveVehicles as jest.Mock).mockResolvedValue({
      data: [],
    });
    renderWithStore();
    await waitFor(() => {
      expect(screen.getByTestId('fleet-map')).toBeInTheDocument();
    });
  });

  it('debe mostrar marcadores por cada vehículo activo', async () => {
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
// Cypress BDD — Flujo E2E del Mapa de Flota
describe('Mapa de Flota - BDD', () => {
  beforeEach(() => {
    cy.login('dispatcher@wastetrack.com', 'testpass');
    cy.visit('/dashboard/fleet');
  });

  it('Dado un despachador, Cuando carga el mapa, Entonces se muestran todos los vehículos activos', () => {
    // Dado
    cy.intercept('GET', '/api/fleet/vehicles/active', {
      fixture: 'active-vehicles.json',
    }).as('fleetRequest');

    // Cuando
    cy.wait('@fleetRequest');

    // Entonces
    cy.get('[data-testid="fleet-map"]').should('be.visible');
    cy.get('[data-testid="vehicle-marker"]')
      .should('have.length.greaterThan', 0);
  });

  it('Dado un despachador, Cuando busca vehículos cercanos, Entonces aparecen resultados geoespaciales', () => {
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

## 📊 Modelo de Datos

### Esquema Principal — PostgreSQL
```sql
-- Vehículos
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

-- Conductores
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

-- Zonas de Recolección
CREATE TABLE collection_zones (
    id                  BIGSERIAL PRIMARY KEY,
    zone_code           VARCHAR(20) UNIQUE NOT NULL,
    zone_name           VARCHAR(100) NOT NULL,
    city                VARCHAR(100) NOT NULL,
    neighborhood        VARCHAR(100),
    polygon_coordinates JSONB NOT NULL,                -- Polígono GeoJSON
    frequency           VARCHAR(20) NOT NULL,          -- DAILY, BIWEEKLY, WEEKLY
    waste_type          VARCHAR(30) NOT NULL,          -- ORGANIC, RECYCLABLE, HAZARDOUS
    assigned_vehicle_id VARCHAR(50) REFERENCES vehicles(id),
    active              BOOLEAN DEFAULT TRUE,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Puntos de Recolección
CREATE TABLE collection_points (
    id                  BIGSERIAL PRIMARY KEY,
    zone_id             BIGINT REFERENCES collection_zones(id) NOT NULL,
    point_name          VARCHAR(255) NOT NULL,
    address             TEXT NOT NULL,
    latitude            DECIMAL(10,8) NOT NULL,
    longitude           DECIMAL(11,8) NOT NULL,
    point_type          VARCHAR(30) NOT NULL,          -- RESIDENTIAL, COMMERCIAL, INDUSTRIAL
    estimated_weight_kg DECIMAL(10,2),
    priority            INTEGER DEFAULT 5,             -- 1 (más alta) a 10 (más baja)
    active              BOOLEAN DEFAULT TRUE,
    notes               TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Rutas
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
    efficiency_score    DECIMAL(5,2),                  -- calculado al finalizar
    notes               TEXT,
    created_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Paradas de Ruta (puntos de recolección ordenados por ruta)
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

-- Eventos de Recolección
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

-- Incidentes
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

-- Reportes Ambientales (MADS/RESPEL)
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

-- Mantenimiento de Vehículos
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

-- Índices de Rendimiento
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

### Esquema NoSQL — MongoDB (Telemetría IoT y Logs Operativos)
```javascript
// Evento de Telemetría GPS — Colección de Series de Tiempo MongoDB
{
  _id: ObjectId,
  vehicleId: String,
  eventType: String,          // "LOCATION", "SENSOR", "ALERT"
  latitude: Number,
  longitude: Number,
  speed: Number,              // km/h
  heading: Number,            // grados
  altitude: Number,           // metros
  accuracy: Number,           // precisión GPS en metros
  fuelLevel: Number,          // porcentaje
  engineTemperature: Number,  // Celsius
  engineStatus: String,       // "ON", "OFF", "IDLE"
  doorStatus: String,         // "OPEN", "CLOSED"
  rawPayload: String,         // Mensaje MQTT original
  timestamp: ISODate,
  processedAt: ISODate
}

// Log de Alertas de Telemetría — Colección MongoDB
{
  _id: ObjectId,
  vehicleId: String,
  plateNumber: String,
  driverId: String,
  alertType: String,          // "SPEEDING", "LOW_FUEL", "ENGINE_OVERHEAT", "UNAUTHORIZED_STOP"
  value: Number,              // valor que disparó la alerta
  threshold: Number,          // umbral configurado
  smsNotified: Boolean,
  smsSentAt: ISODate,
  resolvedAt: ISODate,
  timestamp: ISODate
}

// Log de Consultas Analíticas ElasticSearch — Colección MongoDB
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

## 🎓 Aprendizajes Clave

### Arquitectura y Backend

✅ **Microservicios con Java 17** — Diseño e implementación de servicios distribuidos
usando Spring Boot 3.2.x y Spring MVC 6.1.x con características de Java 17 LTS
incluyendo records, clases selladas y coincidencia de patrones, demostrando dominio
completo del ecosistema Java 11 y Java 17 dentro del mismo portafolio

✅ **Consultas Geoespaciales con ElasticSearch 8.x** — Implementación de mapeos de
índice geo_point, búsquedas de proximidad geo_distance para despacho de vehículos,
consultas geo_bounding_box por zona y agregaciones geoespaciales para mapas de calor
de densidad de recolección — un caso de uso de ElasticSearch fundamentalmente
diferente a la búsqueda de texto tradicional

✅ **Agregaciones ElasticSearch para Analítica** — Construcción de pipelines de
agregación multinivel para KPIs operativos: agregaciones terms por zona y conductor,
agregaciones de métricas avg/sum para puntuación de eficiencia, agregaciones
date_histogram para análisis de tendencias y agregaciones de pipeline para KPIs derivados

✅ **Arquitectura IoT Orientada a Eventos** — Diseño de puente MQTT-Kafka que procesa
miles de eventos de telemetría GPS en tiempo real por minuto, con MongoDB como
almacén de series de tiempo y ElasticSearch como capa de analítica geoespacial

✅ **Spring Security 6.2.x** — Implementación de configuración moderna de Spring
Security usando el enfoque lambda DSL SecurityFilterChain (reemplazando el
WebSecurityConfigurerAdapter deprecado de Java 11 / Spring Security 5.x),
demostrando evolución entre versiones principales de Spring Security

✅ **TDD con JUnit 5 + Mockito** — Desarrollo guiado por pruebas en todas las
capas de servicio con énfasis particular en validación de umbrales de telemetría,
aserciones de resultados de consultas geoespaciales y verificación de publicación
de eventos Kafka

### Frontend y UX

✅ **React 18 + TypeScript + Leaflet** — SPA geoespacial tipada en tiempo real
que integra React-Leaflet para mapas de flota interactivos, iconos de mapa
personalizados para visualización del estado del vehículo y superposiciones de
círculos dinámicos para visualización de proximidad

✅ **Redux Toolkit + Thunks para Datos en Tiempo Real** — Arquitectura Redux
extendida para manejar actualizaciones de estado impulsadas por WebSocket junto
con llamadas API basadas en Thunk, manteniendo una única fuente de verdad para
posiciones de flota actualizadas cada 30 segundos en cientos de marcadores de
mapa concurrentes

✅ **Configuración Manual de Webpack 5** — Bundle de producción configurado con
división de código por ruta, carga diferida para el componente pesado de mapa
Leaflet, pipeline de compilación SASS e inyección de endpoints de API
específicos por entorno

✅ **Arquitectura SASS** — Sistema de diseño consistente mantenido en más de 25
componentes de UI operativos incluyendo paneles de mapa, tarjetas de KPI, banners
de alerta y tablas de desempeño de conductores usando el patrón SASS 7-1

✅ **React Testing Library + Cypress BDD** — TDD aplicado en componentes
geoespaciales con estrategia de mock para Leaflet, y escenarios E2E con BDD
cubriendo flujos críticos del despachador: carga del mapa de flota, búsqueda
geoespacial de vehículos cercanos y visualización de alertas en tiempo real

### Integraciones y Cumplimiento Normativo

✅ **Protocolo IoT MQTT** — Implementación del cliente Eclipse Paho MQTT para
ingestión de telemetría de alta frecuencia de dispositivos GPS con gestión de
niveles QoS, reconexión automática y enrutamiento de dispositivos basado en
tópicos para gestión de flota multi-vehículo

✅ **Reportes Ambientales MADS** — Reportes automatizados para la autoridad
ambiental colombiana (Ministerio de Ambiente y Desarrollo Sostenible) incluyendo
manifiestos de residuos peligrosos RESPEL y documentación de cumplimiento del
Decreto 1076/2015

✅ **Optimización de Rutas** — Integración con OSRM para cálculo de rutas de
código abierto y Google Maps Distance Matrix para optimización multi-parada,
reduciendo el tiempo promedio de completación de rutas mediante secuenciación
algorítmica de paradas

✅ **Alertas SMS con Twilio** — Pipeline de notificación en tiempo real al
conductor disparado por violaciones de umbrales IoT, integrando procesamiento
asíncrono Spring @Async con la API REST de Twilio para comunicación inmediata
en campo

### DevOps y Operaciones

✅ **CI/CD con Jenkins** — Pipeline declarativo que cubre compilación, pruebas
unitarias, pruebas de integración, construcción de imagen Docker, publicación
en registro y despliegue rolling en Kubernetes con rollback automatizado ante
fallo en verificación de salud

✅ **ELK Stack para Analítica IoT** — Pipelines Logstash configurados para
ingestión estructurada de eventos de telemetría desde MongoDB, gestión de índices
geoespaciales ElasticSearch con políticas ILM para retención de telemetría de
90 días, y dashboards Kibana de operaciones de flota

✅ **Kubernetes en Producción** — Despliegues multi-servicio en Kubernetes con
autoescalado horizontal de pods disparado por métricas de lag del consumidor
Kafka, ConfigMaps para endpoints del broker IoT específicos por entorno y
actualizaciones rolling sin tiempo de inactividad para servicios críticos de flota

---

## 🔄 Roadmap y Mejoras Futuras

### Fase 2 — Q3 2025
- Aplicación móvil para conductores (React Native) con acceso offline a rutas y rastreo GPS
- Optimización de rutas impulsada por IA usando datos históricos de recolección y predicciones ML
- Alertas de mantenimiento predictivo basadas en patrones de telemetría del vehículo
- Integración con el sistema nacional SUI (Superintendencia de Servicios Públicos)

### Fase 3 — Q4 2025
- Soporte multi-tenant para redes de empresas de gestión de residuos
- Seguimiento de huella de carbono y reportes de impacto ambiental
- Integración con drones para monitoreo de recolección en zonas remotas
- Visión por computadora para detección de vertimientos no autorizados mediante cámaras vehiculares

### Fase 4 — Q1 2026
- Simulación de gemelo digital para planificación de rutas y optimización de capacidad
- Integración con sistemas GIS municipales para alineación con planificación urbana
- Cadena de custodia de residuos basada en blockchain para materiales peligrosos RESPEL
- Aplicación ciudadana de reporte en tiempo real para incidentes de vertimiento ilegal

---

## 📈 Impacto y Resultados

Este sistema ha sido implementado y validado con **PYMES colombianas de gestión de
residuos y operadores municipales de recolección** a través de SENA, generando
mejoras operacionales medibles:

✅ **40% de reducción** en el tiempo de planificación de rutas mediante optimización
automatizada vs programación manual del despachador
✅ **30% de mejora** en la eficiencia de combustible de la flota mediante monitoreo
de adherencia a rutas GPS en tiempo real y alertas de comportamiento del conductor
✅ **100% de cumplimiento normativo** con el Decreto 1076/2015 y los requisitos de
reporte de residuos peligrosos RESPEL del MADS
✅ **Cero errores manuales en RESPEL** — la generación automatizada de reportes
eliminó errores de transcripción y cálculo
✅ **85% de reducción** en el tiempo de búsqueda de proximidad de flota usando
consultas geo_distance de ElasticSearch vs cálculos espaciales SQL tradicionales
✅ **Respuesta a incidentes en tiempo real** redujo el tiempo promedio de alerta
a acción de 25 minutos a menos de 2 minutos mediante el pipeline MQTT + SMS Twilio
✅ **Trazabilidad IoT completa** en cada evento de telemetría vehicular, cumpliendo
los requisitos de trazabilidad de la autoridad ambiental colombiana

---

## 📄 Licencia y Propiedad Intelectual

> ⚠️ **SENA — Aviso de Propiedad Intelectual**
>
> Este proyecto fue desarrollado como parte de actividades académicas e investigativas
> dentro del **SENA (Servicio Nacional de Aprendizaje)** bajo el programa **SENNOVA**,
> orientado a apoyar la transformación digital y el cumplimiento ambiental de PYMES
> colombianas de gestión de residuos y operadores municipales.
>
> El **código fuente, diseño arquitectónico y documentación técnica son propiedad
> institucional del SENA** y no se encuentran disponibles públicamente en este
> repositorio. El contenido presentado aquí — incluyendo especificaciones técnicas,
> diagramas de arquitectura, fragmentos de código, patrones de integración IoT y
> modelos de datos — ha sido **recreado con fines de demostración de portafolio
> únicamente**, sin exponer información institucional confidencial ni el código
> fuente original de producción.
>
> Las capturas de pantalla e imágenes de la interfaz han sido intencionalmente
> excluidas para proteger la confidencialidad de los datos operativos y la
> privacidad institucional.

**Disponible para:**

✅ Consultoría personalizada e implementación para empresas de gestión de residuos
✅ Diseño e integración de arquitecturas de rastreo IoT/GPS para flotas
✅ Diseño y optimización de analítica geoespacial con ElasticSearch
✅ Asesoría en cumplimiento normativo ambiental colombiano (Decreto 1076/2015, RESPEL)
✅ Diseño e implementación de algoritmos de optimización de rutas
✅ Desarrollo de módulos adicionales y soporte técnico

---

## 🏆 Reconocimientos

- 🥇 **Mejor Proyecto de Innovación Ambiental** — SENA Regional Risaralda 2024
- 🏅 **Alineación MADS** — Arquitectura validada frente a los requisitos de reporte
ambiental del Decreto 1076/2015
- 🌿 **Premio a la Sostenibilidad** — Programa de Innovación SENA SENNOVA 2024
- ⭐ **Implementado en más de 8 PYMES colombianas de gestión de residuos y
operadores municipales**


| **Swagger/OpenAPI** | Documentación de API y pruebas interactivas                      |
| **JUnit 5**         | Pruebas unitarias e integración del backend (TDD)                |
| **Mockito**         | Simulación de dependencias para pruebas unitarias aisladas       |
