
# YOLOv11 Inference Pipeline

A scalable microservices architecture for computer vision inference using YOLOv11.

## Introduction

This project implements a high-performance, scalable inference pipeline for deploying YOLOv11 object detection models in production environments. The architecture is designed to handle high-throughput image processing workloads with reliability, scalability, and observability as core principles.

Key features:
- Decoupled microservices architecture
- Asynchronous task processing
- Horizontal scaling capabilities
- Containerized deployment
- Comprehensive monitoring

## Architecture Overview

The system consists of three decoupled microservices:

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│             │     │             │     │             │
│  FastAPI    │────▶│   Celery    │────▶│   Model     │
│  Service    │     │   Worker    │     │   Server    │
│             │     │             │     │             │
└─────────────┘     └─────────────┘     └─────────────┘
        │                                      │
        │                                      │
        ▼                                      ▼
┌─────────────┐                        ┌─────────────┐
│             │                        │             │
│  PostgreSQL │                        │   Redis     │
│  Database   │                        │             │
│             │                        │             │
└─────────────┘                        └─────────────┘
```

### Data Flow
1. Client sends image to FastAPI service
2. FastAPI validates request and queues task in Celery
3. Celery worker processes task and calls model server
4. Model server runs YOLOv11 inference
5. Results flow back to client through the same path

### Components
- **FastAPI Service**: Handles HTTP requests, authentication, and task orchestration
- **Celery Worker**: Processes asynchronous inference tasks
- **Model Server**: Serves YOLOv11 model for efficient inference
- **PostgreSQL**: Stores task metadata and results
- **Redis**: Serves as message broker and result backend

## Quick Start

