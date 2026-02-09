# Fatafat Sewa API Documentation

This directory contains the "Real" API documentation for Fatafat Sewa, generated as an OpenAPI 3.0 Specification.

## Contents
- `openapi.json`: The OpenAPI (Swagger) Specification file describing all endpoints.
- `index.html`: A standalone HTML viewer using [Redoc](https://github.com/Redocly/redoc) to render the documentation beautifully.
- `Checkout_Documentation.md`: Detailed guide for the Checkout API payload and response structure.

## How to View
To view the documentation, you can simply serve this directory.

### Method 1: Using Python (Simplest)
If you have Python installed, run:
```bash
python3 -m http.server 8001
```
Then open [http://localhost:8001](http://localhost:8001) in your browser.

### Method 2: Using Node.js http-server
```bash
npx http-server . -p 8001
```
Then open [http://localhost:8001](http://localhost:8001).

### Method 3: VS Code Live Server
If you use VS Code, right-click `index.html` and select "Open with Live Server".

## Updating Documentation
To add new endpoints, edit the `openapi.json` file following the OpenAPI 3.0 standard. The `index.html` will automatically reflect changes upon refresh.
