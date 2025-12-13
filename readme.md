Simple Go webserver for Kubernetes to serve a test page.

## Run locally

```bash
cd /home/mj/work-webs/go-test-web
HELLO_MSG="umet.cz test page" go run .
```

Or without env vars:

```bash
go run .
```

Open:

- http://localhost:8080/
- http://localhost:8080/healthz
- http://localhost:8080/readyz

## Configuration

- `PORT` (default `8080`) – convenience for local/dev
- `ADDR` (default `:<PORT>`) – full listen address, e.g. `0.0.0.0:8080`
- `HELLO_MSG` (default `Hello from Go`) – message rendered on `/`

## Container

Build:

```bash
docker build -t go-test-web:local .
```

Run:

```bash
docker run --rm -p 8080:8080 -e HELLO_MSG="umet.cz test page" go-test-web:local
```
