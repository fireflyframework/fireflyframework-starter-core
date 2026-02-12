# Firefly Framework - Core

[![CI](https://github.com/fireflyframework/fireflyframework-core/actions/workflows/ci.yml/badge.svg)](https://github.com/fireflyframework/fireflyframework-core/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-21%2B-orange.svg)](https://openjdk.org)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green.svg)](https://spring.io/projects/spring-boot)

> Core framework module providing WebFlux configuration, actuator setup, resilience, tracing, and service registry integration.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Overview

Firefly Framework Core is the foundational runtime module that every Firefly-based microservice includes. It provides auto-configured WebFlux settings, WebClient configuration with resilience patterns, Actuator health and metrics endpoints, distributed tracing, and service registry integration.

The module handles cross-cutting concerns including banner display, web filters, transaction context propagation, cloud configuration, and step event publishing for the transactional engine. It integrates with Spring Cloud Config for centralized configuration and supports service discovery through configurable registry adapters.

Core is designed to be included as a transitive dependency through higher-level modules like `fireflyframework-domain` or `fireflyframework-application`, but can also be used directly for custom microservice setups.

## Features

- WebFlux auto-configuration with customizable WebClient settings
- Resilient WebClient with circuit breaker and retry patterns
- Spring Boot Actuator configuration (health, info, metrics, tracing)
- JVM, HTTP client, thread pool, and application metrics
- Database and cache health indicators
- OpenTelemetry distributed tracing integration
- Spring Cloud Config client auto-configuration
- Service registry integration (Eureka, Consul, Kubernetes)
- Step event publishing bridge for the transactional engine
- Firefly branded startup banner
- Transaction context web filter
- Logstash-compatible structured logging
- Cloud configuration properties management

## Requirements

- Java 21+
- Spring Boot 3.x
- Maven 3.9+

## Installation

```xml
<dependency>
    <groupId>org.fireflyframework</groupId>
    <artifactId>fireflyframework-core</artifactId>
    <version>26.02.03</version>
</dependency>
```

## Quick Start

```java
import org.fireflyframework.core.web.client.WebClientTemplate;

@Service
public class ExternalService {

    private final WebClientTemplate webClient;

    public ExternalService(WebClientTemplate webClient) {
        this.webClient = webClient;
    }

    public Mono<Response> callApi(String path) {
        return webClient.get(path, Response.class);
    }
}
```

## Configuration

```yaml
firefly:
  core:
    web-client:
      connect-timeout: 5000
      read-timeout: 10000
    resilience:
      circuit-breaker:
        enabled: true
        failure-rate-threshold: 50
    cloud-config:
      enabled: true
      uri: http://config-server:8888
    service-registry:
      enabled: true
      type: eureka

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
```

## Documentation

Additional documentation is available in the [docs/](docs/) directory:

- [Overview](docs/OVERVIEW.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Configuration](docs/CONFIGURATION.md)
- [Quickstart](docs/QUICKSTART.md)
- [Api](docs/API.md)
- [Integrations](docs/INTEGRATIONS.md)

## Contributing

Contributions are welcome. Please read the [CONTRIBUTING.md](CONTRIBUTING.md) guide for details on our code of conduct, development process, and how to submit pull requests.

## License

Copyright 2024-2026 Firefly Software Solutions Inc.

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
