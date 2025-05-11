
# YOLOv11 Inference Pipeline

A scalable microservice architecture for computer vision inference using YOLOv11.

## Introduction

In this project I implemented a simple high-performance, scalable inference pipeline for deploying YOLOv11 object detection models in production environments. The architecture is designed to handle high-throughput image processing workloads with reliability, scalability, and observability as core principles.

Key features:
- Decoupled microservices architecture
- Asynchronous task processing
- Horizontal scaling capabilities
- Containerized deployment
- Comprehensive monitoring

### Data Flow
1. Client sends image to FastAPI service
2. FastAPI validates request and queues task in Celery
3. Celery worker processes task, runs YOLOv11 inference, and stores the result in PostgreSQL database

### Components
- **FastAPI Service**: Handles HTTP requests, authentication, and task orchestration
- **Celery Worker**: Processes asynchronous inference tasks and serves YOLOv11 model for efficient inference
- **PostgreSQL**: Stores inference results
- **Rabbitmq**: Serves as message broker
- **SQLite**: Serves as a result backend
