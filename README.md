# 📚 Spring Boot + Elasticsearch – Assignment A

This project is a simple course search service using **Spring Boot** and **Elasticsearch**. It allows full-text search and filtering by category, type, price, age range, and upcoming session date.

---

## 🚀 How to Run

### 1. Start Elasticsearch via Docker

Make sure Docker is installed. Open terminal in the project root (where `docker-compose.yml` is present) and run:

```bash
docker-compose up -d
```

> This  up an Elasticsearch container locally.

---

### 2. Run Spring Boot Project

Open terminal at project root and run:

```bash
./mvnw spring-boot:run
```

OR if you're on Windows:

```bash
mvn spring-boot:run
```

---

### 3. Data Loading (Auto)

Sample data is auto-loaded on application startup from:

```
src/main/resources/sample-courses.json
```

## 🔍 API Endpoint

**Base URL**  
```
http://localhost:8080/api/search
```

Supports the following filters via query parameters:

- `q` → Search text (title or description)
- `category` → Course category
- `type` → Course type (e.g., Video, Live)
- `minAge`, `maxAge` → Age range
- `minPrice`, `maxPrice` → Price range
- `startDate` → Filter courses starting after a date
- `sort` → Sorting (`priceAsc`, `priceDesc`, default is date)
- `page`, `size` → Pagination

---

## 🧪 Sample CURL Requests

### 1. Search all courses
```bash
curl "http://localhost:8080/api/search"
```

### 2. Search for 'java' in title/description
```bash
curl "http://localhost:8080/api/search?q=java"
```

### 3. Filter by category and type
```bash
curl "http://localhost:8080/api/search?category=Programming&type=Video"
```

### 4. Apply age and price range filters
```bash
curl "http://localhost:8080/api/search?minAge=10&maxAge=20&minPrice=100&maxPrice=1000"
```

### 5. Sort by price ascending with pagination
```bash
curl "http://localhost:8080/api/search?sort=priceAsc&page=0&size=5"
```

---

## 📁 Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/example/elastic_search_demo/
│   │       ├── config/            # Elasticsearch config (ElasticConfig.java)
│   │       ├── controller/        # API controller (SearchController.java)
│   │       ├── service/           # Business logic (SearchService.java, StartUpListener.java)
│   │       ├── entity/            # Entity class (BookDetailEntity.java)
│   │       └── dto/               # DTOs for request/response
│   └── resources/
│       ├── sample-courses.json   # Sample data loaded at startup
│       └── application.yml       # App config
```

---

## 🐳 docker-compose.yml (must be in root)

```yaml
version: '3.7'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.11.1
    container_name: elasticsearch
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
      - ES_JAVA_OPTS=-Xms512m -Xmx512m
    ports:
      - "9200:9200"
```
