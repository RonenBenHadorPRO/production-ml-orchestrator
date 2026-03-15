# Production-Grade ML Pipeline Orchestrator

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

This repository implements a high-performance, asynchronous ML pipeline orchestrator designed for large-scale production environments. Drawing from over 25 years of experience in AI engineering and leadership (Ex-Head of AI @ Driivz), this framework focuses on scalability, observability, and robust error handling.

## Overview

Modern ML systems require more than just model code; they need a resilient infrastructure to handle data drift, model performance degradation, and distributed task management. This orchestrator provides:

1.  **Distributed Task Queuing:** Leverages Redis and Celery for asynchronous processing of data ingestion, feature engineering, and model inference.
2.  **Integrated Observability:** Native Prometheus metrics and health check endpoints for monitoring throughput, latency, and model drift.
3.  **Model Versioning & Registry:** A modular structure for tracking and deploying multiple versions of ML models with ease.
4.  **Resiliency Patterns:** Implementation of circuit breakers, retries, and exponential backoff for external API calls and database operations.

## Project Structure

```text
├── src/
│   ├── core/
│   │   ├── config.py          # Environment-driven configuration
│   │   ├── orchestrator.py    # Main pipeline logic
│   │   └── registry.py        # Model and task registry
│   ├── tasks/
│   │   ├── feature_eng.py     # Feature engineering pipelines
│   │   └── inference.py       # Async inference logic
│   ├── utils/
│   │   ├── monitoring.py      # Prometheus and logging setup
│   │   └── resilience.py      # Circuit breakers and retries
│   └── main.py                # FastAPI entrypoint
├── tests/
│   └── test_orchestrator.py
├── docker-compose.yml
├── requirements.txt
└── README.md
```

## Getting Started

### Installation

```bash
pip install -r requirements.txt
```

### Usage

```python
from src.core.orchestrator import MLOrchestrator
from src.tasks.inference import XGBoostPredictor

# Initialize orchestrator with a versioned predictor
orchestrator = MLOrchestrator(predictor=XGBoostPredictor(version="v1.2"))

# Register a new inference task
task_id = orchestrator.dispatch(payload={"user_id": 123, "features": [...]})
print(f"Dispatched task: {task_id}")

# Fetch results asynchronously
result = orchestrator.get_result(task_id)
```

## Methodology

This orchestrator is built on the **Separation of Concerns** principle. The core logic handles the flow of data and tasks, while specialized modules handle feature extraction and model execution. This allows for independent scaling of different pipeline stages and simplifies the integration of new models.

## Future Directions

- Integration with Kubernetes for dynamic scaling of worker nodes.
- Native support for A/B testing and canary deployments.

## License

Distributed under the MIT License. See `LICENSE` for more information.
