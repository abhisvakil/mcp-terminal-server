# Containerized MCP Terminal Server 🚀

## Why Containerize Your MCP Server?

Containerization is a cornerstone of modern DevOps and AI workflows. By packaging your Model Context Protocol (MCP) server in Docker, you gain:

- **Portability:** Run your server anywhere—locally, in the cloud, or in CI/CD pipelines.
- **Reproducibility:** Eliminate "works on my machine" issues with consistent environments.
- **Isolation:** Keep dependencies and runtime separate from your host system.
- **Security:** Limit access to only what the container needs.
- **Scalability:** Easily scale up with Docker Compose, Kubernetes, or cloud services.

---

## 🏗️ Project Structure

```
mcp-terminal-server-docker/
├── terminal_server/
│   ├── Dockerfile           # Docker build instructions
│   ├── terminal_server.py   # Main MCP server code
│   ├── requirements.txt     # Python dependencies
│   └── ...                  # Other server files
├── README.md                # This file
├── LICENSE                  # License file
```

---

## 🚀 Quick Start: Run Your MCP Server in Docker

### 1. **Build the Docker Image**

```bash
cd terminal_server
# Build the Docker image (name it as you like)
docker build -t terminal_server_docker .
```

### 2. **Run the MCP Server in a Container**

```bash
docker run -i --rm --init \
  -e DOCKER_CONTAINER=true \
  -v /Users/yourusername/mcp/workspace:/root/mcp/workspace \
  terminal_server_docker
```
- Replace `/Users/yourusername/mcp/workspace` with your actual workspace path.
- The `-i` flag keeps stdin open for stdio transport (required for Claude Desktop integration).

---

## 🖥️ Integrate with Claude Desktop

1. **Edit your Claude Desktop config** (usually at `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "terminal_server": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "--init",
        "-e", "DOCKER_CONTAINER=true",
        "-v", "/Users/yourusername/mcp/workspace:/root/mcp/workspace",
        "terminal_server_docker"
      ]
    }
  }
}
```
- Make sure the volume path matches your actual user directory.
- Save and **restart Claude Desktop**.

---

## 🛠️ Best Practices for Containerized AI Tooling

- **Environment Variables:** Use `-e` flags for secrets, API keys, or config.
- **Minimal Images:** Use slim Python images and only install what you need.
- **Volume Mounts:** Only mount directories you want the container to access.
- **Logs & Debugging:** Use `docker logs` and check Claude logs for troubleshooting.
- **CI/CD:** Add Docker build and push steps to your pipeline for automated deployments.

---

## 📚 Learn More
- [Docker Documentation](https://docs.docker.com/)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)
- [Claude Desktop MCP Guide](https://docs.anthropic.com/claude/docs/model-context-protocol-mcp)

---

## 📝 License

MIT License. See [LICENSE](LICENSE) for details.

---

**Containerization is the future of AI tool orchestration. By running your MCP server in Docker, you ensure reliability, security, and scalability for all your AI-powered workflows.** 