# OpenELIS-Odoo Integration

This project provides a Docker-based integration between OpenELIS (Open Electronic Laboratory Information System) and Odoo, enabling seamless laboratory management and business process integration.

## Prerequisites

- Docker
- Docker Compose
- Git

## Project Structure

```
.
├── configs/
│   ├── nginx/
│   ├── odoo/
│   └── openelis/
├── docker-compose.yml
└── README.md
```

## Services

### OpenELIS Components
- **OpenELIS Web Application** (oe.openelis.org)
  - Port: 8080 (HTTP), 8443 (HTTPS)
  - Main laboratory information system

- **FHIR Server** (fhir.openelis.org)
  - Port: 8081 (HTTP), 8444 (HTTPS)
  - Healthcare interoperability interface

- **Frontend** (frontend.openelis.org)
  - User interface for OpenELIS

- **Database**
  - PostgreSQL 14.4
  - Port: 15432
  - Stores OpenELIS data

### Odoo Components
- **Odoo Server**
  - Port: 8069
  - Business management system

- **Odoo Database**
  - PostgreSQL 13
  - Stores Odoo data

### Supporting Services
- **Nginx Proxy**
  - Ports: 80 (HTTP), 443 (HTTPS)
  - Handles routing and SSL termination

- **Certificate Service**
  - Manages SSL/TLS certificates
  - Generates keystore and truststore

## Getting Started

1. Clone the repository:
   ```bash
   git clone [repository-url]
   cd OpenELIS-Odoo-Integration
   ```

2. Create necessary configuration files:
   - Place your configuration files in the `configs/` directory
   - Ensure all required environment variables are set

3. Start the services:
   ```bash
   docker-compose up -d
   ```

4. Access the applications:
   - OpenELIS: https://localhost:8443
   - Odoo: http://localhost:8069
   - FHIR Server: https://localhost:8444

## Configuration

### OpenELIS Configuration
- Database configuration: `configs/openelis/database/database.env`
- Tomcat configuration: `configs/openelis/tomcat/`
- Properties files: `configs/openelis/properties/`

### Odoo Configuration
- Configuration files: `configs/odoo/config/`
- Custom addons: `configs/odoo/addons/`

### Nginx Configuration
- Main configuration: `configs/nginx/nginx.conf`

## Security

The system uses SSL/TLS certificates for secure communication. Certificates are automatically generated and managed by the certificate service.

## Volumes

The following volumes are used for data persistence:
- `db-data2`: OpenELIS database data
- `odoo-web-data`: Odoo web data
- `odoo-db-data`: Odoo database data
- `key_trust-store-volume`: SSL certificates and keys
- `lucene_index-vol`: Search index data

## Troubleshooting

1. Check service logs:
   ```bash
   docker-compose logs [service-name]
   ```

2. Verify network connectivity:
   ```bash
   docker network inspect hie
   ```

3. Check certificate status:
   ```bash
   docker-compose logs certs
   ```