# Custom n8n Environment for EasyPanel

This directory contains a `Dockerfile` to build a custom n8n image that includes Python and `uv`. This allows the n8n MCP community node to execute Python-based MCP servers like `osm-mcp-server`.

## How to Deploy on EasyPanel

You do **not** need to deploy the `osm-mcp-server` itself as a service. Instead, you deploy a custom version of n8n that knows how to run it.

Follow these steps to deploy a new n8n service using this custom environment:

1.  **Go to Your EasyPanel Project** and click **"+ New"** to add a new service.

2.  **Choose "App"** as the service type.

3.  **Configure the Source:**
    *   **Source:** Git Repository
    *   **Repository:** Select your `open-streetmap-mcp` repository.
    *   **Branch:** `main`

4.  **Configure the Build:**
    *   **Build Method:** `Dockerfile`
    *   **Dockerfile Path:** `n8n/Dockerfile`

5.  **Configure Environment Variables:**
    *   Go to the "Environment" tab.
    *   **Crucially, copy all the environment variables from your existing n8n service to this new one.** This includes settings for your database, timezone, and any other configurations you have.
    *   Example variables you might need:
        *   `DB_TYPE`
        *   `DB_POSTGRESDB_HOST`
        *   `DB_POSTGRESDB_DATABASE`
        *   `DB_POSTGRESDB_USER`
        *   `DB_POSTGRESDB_PASSWORD`
        *   `N8N_ENCRYPTION_KEY`
        *   `GENERIC_TIMEZONE`

6.  **Configure Data Persistence:**
    *   Go to the "Advanced" tab.
    *   Under "Mounts", add a volume mount to persist your n8n data.
    *   **Host Path:** Choose a path on your server (e.g., `/opt/n8n_data_custom`)
    *   **Container Path:** `/home/node/.n8n`
    *   > **Note:** To migrate your existing workflows, you would first stop your old n8n service, copy the data from its volume to this new host path, and then start this new service.

7.  **Deploy:** Click the "Deploy" button.

8.  **Update Domain & Test:**
    *   Once deployed, go to the "Domains" tab and point your n8n domain to this new service.
    *   Log in to your new n8n instance and configure your MCP credentials. It should now successfully execute the `osm-mcp-server`. 