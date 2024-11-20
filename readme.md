# API Gateway Service

## Overview

The **API Gateway Service** acts as an orchestration layer to mediate and route incoming requests to appropriate microservices. It also includes features like request rate limiting and authentication to ensure secure and efficient communication.

## Features

- **Request Orchestration**: Routes requests to backend services using the `http-proxy-middleware` library.
- **Authentication Layer**: Validates requests by checking user authentication through an external authentication service.
- **Rate Limiting**: Protects the service from excessive requests using `express-rate-limit`.
- **Logging**: Provides detailed request logs using the `morgan` library.

## Project Setup

### Steps to Set Up the Project

1. **Clone the Repository**

   ```bash
   git clone https://github.com/PriyanshuPatel23/API_GATEWAY.git
   ```

2. **Install Dependencies**
   `npm install`

3. **Start the Server**
   `npm start`

## How it works

### Rate Limiting: All requests are limited to 5 requests per 2 minutes per client.

### Authentication:

- For routes starting with /bookingservice, the gateway validates the request by sending the x-access-token header to the authentication service (http://localhost:3001/api/v1/isauthenticated).
- If authenticated, the request proceeds to the next middleware.
- If not authenticated, a 401 Unauthorized response is returned.

### Request Proxying:

- After authentication, requests to /bookingservice are proxied to the Booking Service at http://localhost:3002 using http-proxy-middleware.

### Health Check Endpoint:

- GET /home provides a simple health check response with a message ok.

## Example Usage

### Authenticated Request:

- Send a request to /bookingservice with a valid x-access-token header.
  The gateway validates the token and forwards the request to the Booking Service.
  Rate-Limited Requests:

- Exceeding the rate limit results in a 429 Too Many Requests response.
