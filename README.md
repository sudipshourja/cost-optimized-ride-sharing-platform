# 🚕 Cost-Optimized Ride-Sharing Platform

### A Serverless Approach to Scalable Urban Mobility

This project represents a full-stack, production-ready ride-sharing platform designed to solve the most significant pain point in the industry: **astronomical mapping and routing overhead.** By moving away from proprietary Map APIs, this architecture achieves a 90%+ reduction in operational mapping costs.

## 🎯 The Challenge

Most ride-sharing startups fail due to "The Google Maps Tax." As a platform scales, the cost of map tile loads and routing requests scales linearly, often eating the entire profit margin.

## 💡 The Solution: A Decentralized Map Stack

We built a custom geospatial infrastructure that replaces expensive third-party dependencies with a high-performance, self-maintained stack.

### 1. The Mobile Experience (Frontend)

* **React Native:** A single codebase serving both iOS and Android with native-level performance.
* **Maplibre GL:** Used as the core rendering engine. It allows for full control over the map's visual style without per-view fees.

### 2. The Serverless Map Pipeline (Storage & Delivery)

Instead of a traditional database or a paid tile service, we implemented a **Serverless Vector Tile** strategy:

* **PMTiles:** We package global or regional map data into a single, optimized `.pmtiles` archive.
* **Cloudflare R2 & Workers:** * The map data sits in R2 (S3-compatible storage) with zero egress fees.
* **Cloudflare Workers** execute logic at the edge, fetching only the specific "byte-ranges" of the map the user is currently looking at.
* **Result:** Extremely low latency and near-zero cost for tile delivery.



### 3. Self-Hosted Navigation (Routing Engine)

To handle ETAs, driver dispatch, and turn-by-turn navigation:

* **Infrastructure:** We configured a self-hosted instance of open-source routing tools (such as Valhalla or OSRM).
* **Customization:** This allows for custom routing profiles (e.g., avoiding small alleys for cars) that are often restricted in commercial APIs.

---

## 🏗 System Architecture

| Layer | Technology | Purpose |
| --- | --- | --- |
| **Client** | React Native + Maplibre | User Interface & Map Rendering |
| **CDN / Edge** | Cloudflare Workers | Serverless Tile Request Handling |
| **Storage** | Cloudflare R2 | Hosting PMTiles (Vector Data) |
| **Routing** | Self-Hosted Open Source | Pathfinding, ETA, and Distance Matrix |

---

## 💰 Economic Impact

By utilizing this stack, the platform bypasses the traditional billing models:

* **No "Per Map Load" fees.**
* **No "Per Route" fees.**
* **No "Per Autocomplete" fees.**
* **Total Cost:** Limited only to base server/cloud storage costs, regardless of user volume growth.
