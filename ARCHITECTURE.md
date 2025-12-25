# System Architecture

## Overview
Gemini Video Lecturer is designed as a **Microservices Architecture** on a **Hybrid Intelligence** model.

## 📐 Architecture Diagram
```mermaid
graph TD
    User[User (Browser)] -->|Next.js (Port 3000)| Frontend
    Frontend -->|API Request| Backend[FastAPI Backend (Port 8000)]
    
    subgraph "Hybrid Intelligence Routing"
        Backend -->|Router| Classifier{Complexity?}
        Classifier -->|Simple| Standard[Standard Mode (Gemini Flash)]
        Classifier -->|Visual| Native[Native Mode (Gemini Pro Video)]
        Classifier -->|Retrieval| RAG[Visual RAG (Graphon)]
    end
    
    Standard -->|Response| Backend
    Native -->|Response| Backend
    RAG -->|Response| Backend
```

## 🏗️ Components

### 1. Frontend (Next.js)
*   User Interface for URL input and results display.
*   **Video Synchronization**: Interactive timeline clicks seek the YouTube player.
*   **Markdown Rendering**: Displays rich text summaries.

### 2. Backend (FastAPI)
*   **Orchestrator**: Manages the analysis flow.
*   **Downloader**: Uses `yt-dlp` to fetch audio/video.
*   **Gemini Service**: Handles interaction with Google's Generative AI models.

### 3. Data Infrastructure
*   **Docker Volumes**: Persistent storage for downloaded media caches.
*   **GCP Compute Engine**: Hosts the containerized application.

## 🔐 Security
*   **Environment Variables**: API keys managed via `.env` files, not hardcoded.
*   **Firewall**: GCP VPC Firewall rules strictly limit ingress traffic to ports 3000 (UI) and 8000 (API).
