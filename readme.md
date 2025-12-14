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

## Release / versioning

This repo publishes images to GHCR on SemVer tags.

- Create a tag like `v0.1.0` and push it.
- GitHub Actions will:
	- build + push `ghcr.io/mj41/go-test-web:v0.1.0`
	- create a GitHub Release for that tag

The running service exposes its build version at `GET /version`.

### If GHCR push fails (permission_denied: write_package)

Two common fixes:

1) In the GitHub repo settings, enable write permissions for Actions:
	- Settings → Actions → General → Workflow permissions → select "Read and write permissions".

2) Or use a Personal Access Token for GHCR pushes:
	- Create a PAT with `write:packages` (and `read:packages`).
	- Add it as a repository secret named `GHCR_TOKEN`.
	- The release workflow will prefer `GHCR_TOKEN` over `GITHUB_TOKEN`.
