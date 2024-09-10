# Infrastructure Study for Hasura

## Overview

Hasura is a powerful open-source engine that auto-generates GraphQL APIs from your PostgreSQL database. It simplifies and accelerates the process of building scalable and real-time applications by handling many complex backend tasks out-of-the-box. With Hasura, developers can focus on creating features while reducing the need to write custom backend code.

However, to effectively work with Hasura in production environments, it is important to have a foundational understanding of key infrastructure technologies such as Linux, Docker, Kubernetes, PostgreSQL, and Redis. These technologies provide the backbone for deploying, managing, and scaling Hasura-based applications.

## Why Learn These Technologies?

### 1. **Linux**
   - **Reason**: Linux is the operating system used in most cloud servers and development environments. Knowing Linux basics is essential for configuring, troubleshooting, and securing the systems where Hasura and its dependencies run.
   - **Skills**: Command-line operations, file permissions, process management, and networking.

### 2. **Docker**
   - **Reason**: Hasura is often deployed as a Docker container. Understanding Docker enables you to easily set up isolated development environments, run Hasura locally, and deploy it to production with consistency.
   - **Skills**: Container management, image creation, and Docker Compose.

### 3. **Kubernetes**
   - **Reason**: Kubernetes is the leading platform for orchestrating containerized applications at scale. It provides mechanisms for scaling, monitoring, and updating Hasura services in a production environment.
   - **Skills**: Deploying and managing containers, scaling, and automating processes using Kubernetes.

### 4. **PostgreSQL**
   - **Reason**: PostgreSQL is the core database used by Hasura to store and manage application data. A deep understanding of PostgreSQL will help you optimize database performance, write complex queries, and manage migrations effectively.
   - **Skills**: Database design, query optimization, backup/restore, and indexing.

### 5. **Redis**
   - **Reason**: Redis can be integrated with Hasura to provide caching, improve query performance, handle session management, and facilitate Pub/Sub messaging. Redis is crucial for optimizing and scaling real-time applications.
   - **Skills**: Key-value data storage, caching, Pub/Sub systems, and persistence strategies.

## Learning Path

To make the most of Hasura and build robust applications, start by understanding each of these technologies in the following order:
1. **Linux** – Master the foundational system where everything runs.
2. **Docker** – Learn to containerize Hasura and its dependencies for consistent environments.
3. **PostgreSQL** – Get comfortable with Hasura’s core database.
4. **Redis** – Explore how to use Redis for caching and real-time messaging.
5. **Kubernetes** – Finally, dive into orchestration for deploying and scaling your applications.

By mastering these technologies, you'll be well-prepared to work with Hasura efficiently in both development and production environments.

## How to Use This Repository

This repository contains separate documentation files for each of the core technologies:

- [Linux Basics](./2.%20Linux.md)
- [Docker Overview](./3.%20Docker.md)
- [Kubernetes Basics](./4.%20Kubernetes.md)
- [PostgreSQL Overview](./5.%20Postgresql.md)
- [Redis Overview](./6.%20Redis.md)

Feel free to explore each file and use them as references during your learning journey. This documentation is designed to help you build a strong foundation for deploying and managing Hasura in real-world applications.

Happy learning!
