# Next Core Web Server — User Guide for Developers

## Introduction

**Next Core Web Server** is a lightweight, easy-to-use HTTP server application designed for developers who want to quickly launch a web server from the command line (console) without deep programming knowledge.

This guide helps you understand how to **configure, start, and manage the web server application** to host your web content and dynamic pages using simple configuration files and folder structures.

---

## What This Is For

- Run a **local or public HTTP server** quickly via a console app.
- Serve **static files** (HTML, CSS, JS, images).
- Host **dynamic pages** by defining routes and views via JSON files.
- Customize MIME types and page layouts easily.
- No need to write or change C# source code.
- Manage server lifecycle (start/stop) via console commands.

---

## Quick Start

### 1. Prepare Your Server Folder Structure

You can download the each version from Release section


---

### 2. Configure Your Server

Create or edit an `appsettings.json` file or equivalent configuration with these key settings:

| Setting       | Description                                          | Example                      |
|---------------|------------------------------------------------------|------------------------------|
| Domain        | Hostname or IP address where the server listens      | "localhost" or "0.0.0.0"     |
| Port          | TCP port number for incoming HTTP requests           | 8080                         |
| Folders       | Paths to your Controllers, Shared resources, Root folder | Controllers: `./Controllers`<br>Shared: `./Shared`<br>Root: `/static` |
| MimeTypePath  | File path to your MIME types JSON file                | `./Configurations/MimeTypes.json`          |
| Layout        | Path to your main HTML layout template                | `./Views/Shared/Layout.html`        |

---

### 3. Run the Server

Run the console application executable:

```bash
NextCoreWebServer.exe
```

## Running the Server

- The server will read your configuration.
- Start listening on the specified domain and port.
- Output logs appear in the console window showing server status.

---

## 4. Access Your Web Server

- Open a browser.
- Navigate to `http://{Domain}:{Port}` (e.g., `http://localhost:8080`).
- Static files and dynamic routes defined in your controllers will be served.

---

## 5. Stop the Server

- In the console window, press `Ctrl+C` or close the window.
- The server will gracefully shut down and release the port.

---

## Configuration Details

### Controllers (Routing)

- Routes and pages are defined in JSON files inside the **Controllers** folder.
- Each route maps URL paths (e.g., `/home`) to an HTML or Blazora view.
- Metadata such as page title and description can be set per route.

Example controller JSON:

```json
{
  "Actions": [
    {
      "Paths": ["/home", "/welcome"],
      "Title": "Welcome Page",
      "View": "Views/Welcome.html"
    }
  ]
}
```

## Static Files

Files placed under your configured Root folder (e.g., `/static`) are served directly.

MIME types are automatically applied based on the `mime-types.json` file.

---

## MIME Types

This JSON file defines mappings from file extensions to MIME types.

You can extend it with additional types if needed.

Example snippet:

```json
{
  ".html": "text/html",
  ".css": "text/css",
  ".js": "application/javascript",
  ".png": "image/png"
}
```
## Layout Templates

Your HTML pages can be wrapped with a common layout template.

The layout file can include placeholders for dynamic content injection.

---

## Logging and Console Output

Success, information, warnings, and error messages will display in the console.

Use these logs to monitor server activity and troubleshoot.

---

## Advanced Tips

- To change server settings, modify your configuration files and restart the server.
- Add new routes by creating or editing controller JSON files.
- Place shared assets like CSS and images in the **Shared** folder.
- Keep your static assets organized under the static root for direct serving.

---

## Summary

**Next Core Web Server** enables developers to:

- Run a fully functional HTTP server from a simple console app.
- Configure routes and pages through JSON files — no coding required.
- Serve both static files and dynamic views easily.
- Manage the server with minimal setup and commands.



