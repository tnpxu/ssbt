Project: SSBT (Structured Stream Build Tool)
This document outlines the development roadmap for the SSBT. Our goal is to build a robust and flexible engine for ingesting data from various sources, processing it with Apache Spark, and sinking it to multiple destinations.

Roadmap
We will follow Semantic Versioning (SemVer) for our releases.

v0.1.0 - Foundation & Core Connectors (Alpha)
Theme: Establish the core framework, basic Spark integration (including streaming core), essential local/Kafka connectors, and initial build/config design.

Foundation:

[0.1.0-F1] Initial project structure and build tool design (sbt):

sbt project setup and modularization strategy.

Dependency management approach.

Initial considerations for plugin management (e.g., for formatting, testing).

Basic packaging strategy defined (e.g., using sbt-native-packager for universal archives).

[0.1.0-F2] Core Spark Session management and initial configuration design:

Utilities for creating and managing SparkSession.

Basic parameterization for Spark jobs (e.g., command-line arguments, simple property files).

Initial thoughts on environment-specific configurations.

[0.1.0-F3] Common utility functions for data manipulation and logging.

[0.1.0-F4] Basic abstraction layer for Source and Sink components (for batch and streaming).

[0.1.0-F5] Initial testing framework setup (ScalaTest/Specs2).

[0.1.0-F6] Spark Structured Streaming Core Integration:

Foundational support for Spark Structured Streaming concepts within the framework.

Basic abstractions for streaming sources/sinks.

Initial considerations for trigger management and checkpointing mechanisms.

Sources:

[0.1.0-S1] File Source (Batch): Implement connector for reading from local file systems (CSV, JSON, Parquet).

Support for basic schema inference.

Path globbing.

[0.1.0-S2] Kafka Source (Batch & Initial Streaming): Implement connector for consuming data from Apache Kafka topics.

Support for basic deserialization (String, Avro - if schema registry is simple).

Offset management (earliest, latest for batch; initial streaming support).

Sinks:

[0.1.0-K1] File Sink (Batch): Implement connector for writing Spark DataFrames to local file systems (CSV, JSON, Parquet).

Support for various save modes (overwrite, append, ignore, errorifexists).

[0.1.0-K2] Kafka Sink (Batch & Initial Streaming): Implement connector for producing data to Apache Kafka topics.

Support for basic serialization (String, Avro - if schema registry is simple).

Initial support for streaming writes.

Goals for v0.1.0:

Prove core concepts and Spark integration for both batch and basic streaming.

Provide fundamental building blocks for simple file and Kafka based ETL pipelines.

Establish initial build and configuration patterns.

Internal testing and API refinement.

v0.2.0 - Expanding Connectors, Cloud Integration & Enhanced Config (Beta)
Theme: Enhance connector capabilities, introduce initial support for cloud blob storage, formalize configuration, and improve error handling.

Foundation:

[0.2.0-F1] Improved and Formalized Configuration Management:

Adoption of a robust configuration library (e.g., HOCON/TypeSafe Config).

Clear configuration hierarchy (defaults, environment-specific, job-specific).

Support for configuration validation.

[0.2.0-F2] Enhanced error handling and reporting mechanisms within the framework.

[0.2.0-F3] Basic metrics collection for job execution (batch and streaming).

[0.2.0-F4] Refine Source/Sink API based on v0.1.0 feedback, ensuring consistency for batch and streaming.

Sources:

[0.2.0-S1] File Source Enhancement (Batch & Streaming):

Support for partitioned data reading.

More robust schema handling and evolution.

Support for discovering new files in a directory for streaming (file stream source).

[0.2.0-S2] Kafka Source Enhancement (Streaming & Batch):

Support for Kafka headers.

Integration with Schema Registry (e.g., Confluent Schema Registry) for Avro/Protobuf.

More granular offset management options and robust checkpointing for streaming.

[0.2.0-S3] Blob Storage Source (Initial - Batch & Streaming): Implement connector for reading from a chosen cloud blob storage (e.g., AWS S3 - select one as initial focus).

Support for CSV, JSON, Parquet.

Basic authentication mechanisms (e.g., access keys).

Initial support for streaming from blob storage (e.g., file discovery).

Sinks:

[0.2.0-K1] File Sink Enhancement (Batch & Streaming):

Support for writing partitioned data.

Options for compression codecs.

Robust output modes for streaming (append, complete, update).

[0.2.0-K2] Kafka Sink Enhancement (Streaming & Batch):

Support for Kafka headers and custom partitioners.

Integration with Schema Registry for Avro/Protobuf.

[0.2.0-K3] Blob Storage Sink (Initial - Batch & Streaming): Implement connector for writing to a chosen cloud blob storage (e.g., AWS S3 - consistent with source).

Support for CSV, JSON, Parquet.

Basic authentication mechanisms.

Support for streaming writes with checkpointing.

Goals for v0.2.0:

Enable basic cloud data integration for batch and streaming.

More robust and feature-rich Kafka and file connectors.

Formalized configuration system.

Gather user feedback for API stability.

v0.3.0 - Advanced Streaming, Multi-Cloud & Operational Features (Beta)
Theme: Add support for more cloud providers, enhance Spark Structured Streaming capabilities, and improve operational aspects like data quality and documentation.

Foundation:

[0.3.0-F1] Pluggable authentication/credential management for cloud services.

[0.3.0-F2] Framework for defining and executing data quality checks (for batch and streaming data).

[0.3.0-F3] Advanced Spark Structured Streaming features:

Support for watermarking and handling late data.

State management abstractions (e.g., mapGroupsWithState, flatMapGroupsWithState).

More sophisticated trigger options.

[0.3.0-F4] Documentation improvements (API docs, comprehensive usage examples for batch and streaming).

Sources:

[0.3.0-S1] Blob Storage Source (Expanded): Add support for one to two additional cloud blob storages (e.g., Azure Blob Storage, Google Cloud Storage) for batch and streaming.

Consistent feature set across supported blob stores.

Support for more advanced authentication (e.g., IAM roles, service principals).

[0.3.0-S2] File Source (Advanced):

Support for additional file formats (e.g., ORC, Avro files) for batch and streaming.

Schema registry integration for file-based Avro/Protobuf.

Sinks:

[0.3.0-K1] Blob Storage Sink (Expanded): Add support for one to two additional cloud blob storages (consistent with sources) for batch and streaming.

Consistent feature set across supported blob stores.

Support for more advanced authentication.

[0.3.0-K2] File Sink (Advanced):

Support for additional file formats (e.g., ORC, Avro files) for batch and streaming.

Schema registry integration for file-based Avro/Protobuf.

[0.3.0-K3] Transactional Sinks (Exploration): Investigate and potentially implement initial support for transactional writes for specific sinks (e.g., Delta Lake format on blob storage for batch and streaming).

Goals for v0.3.0:

Broader cloud compatibility for batch and streaming.

Mature support for common streaming use cases.

Enhanced data reliability and operational visibility.

Prepare for a stable v1.0.0 release.

v1.0.0 - Stable Release
Theme: Production readiness, API stability, comprehensive documentation, and performance optimizations for both batch and streaming.

Foundation:

[1.0.0-F1] API stabilization - No breaking changes planned for 1.x minor releases.

[1.0.0-F2] Performance testing and optimization across core components and connectors (batch and streaming).

[1.0.0-F3] Comprehensive official documentation covering all features.

[1.0.0-F4] Hardening security aspects (dependency scanning, secure defaults).

[1.0.0-F5] Finalize and polish testing suite for high coverage (unit, integration, E2E for batch and streaming).

Sources & Sinks:

[1.0.0-CS1] Ensure all supported Source and Sink connectors are stable, well-tested, and feature-complete according to the defined scope for batch and streaming.

[1.0.0-CS2] Consistent error handling and retry mechanisms across all connectors.

[1.0.0-CS3] Performance benchmarks for key connectors.

Goals for v1.0.0:

A stable, reliable, and performant engine for production use (batch and streaming).

Clear and comprehensive documentation for users.

Establish a solid base for future enhancements.

Future (Post v1.0.0)
Additional Connectors:

Databases (JDBC sources/sinks - batch & streaming CDC).

NoSQL databases (batch & streaming).

Data warehouse systems (e.g., Snowflake, BigQuery, Redshift connectors - batch & micro-batch/streaming).

Other messaging systems (e.g., Pulsar, RabbitMQ).

Advanced Processing:

More sophisticated data quality rule engine with streaming support.

Schema evolution management tools with streaming considerations.

Integration with workflow orchestrators (e.g., Airflow, Dagster) for batch and streaming pipeline management.

Operational Improvements:

Enhanced monitoring and alerting integration (e.g., Prometheus, Grafana) for streaming metrics.

Web UI for managing and monitoring jobs (potentially).

Spark Ecosystem:

Support for newer Spark versions and features as they are released.

Deeper integration with Delta Lake / Iceberg / Hudi for reliable streaming and batch.

This roadmap is a living document and may be adjusted based on development progress, community feedback, and evolving project priorities.