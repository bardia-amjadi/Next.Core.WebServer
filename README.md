# Next.Core.WebServer

## Overview

`Next.Core.WebServer` is a lightweight HTTP server implementation based on .NET's `HttpListener`. It serves static files and dynamic content using configurable routes loaded from JSON controller files. The server supports HTML page layouts, query parameter binding, and MIME type resolution.

---

## Features

- Configurable server URL (domain and port) via `AppSettings`.
- Loading routes and actions dynamically from JSON controller files.
- Serving static files from a specified root folder.
- Supports simple view templates with optional layouts.
- Query parameter binding for dynamic content rendering.
- MIME type detection for common web file extensions.
- Graceful start and stop with cancellation token support.
- Console logging for key server events (info, success, errors).
- Basic 404 and 500 error handling with custom error pages.

---

## Project Structure

- `WebServerProvider` class: Core HTTP server logic, route management, request handling.
- `Program` class: Console app launcher, server lifecycle management, and administrative setup.
- `AppSettings` class (not shown): Configuration model with properties like `Domain`, `Port`, folder paths, layout, and special folders.

---

## Usage

### Running the Server

- Make sure the program runs with Administrator privileges (required for host and URL ACL changes).
- Place your controller JSON files in the configured controllers folder (e.g. `I:\Localhost\Controllers`).
- Configure your app settings JSON (e.g. `I:\Localhost\AppSettings.json`) with domain, port, and folder paths.
- Run the console application. It will:
  - Set URL ACL and hosts file entries.
  - Start the HTTP listener.
  - Accept incoming HTTP requests.
  - Serve static files or render dynamic views with optional layouts.
  - Handle user input to restart or stop the server.

---

## Configuration Example (`AppSettings.json`)

```json
{
  "Domain": "localhost",
  "Port": 8080,
  "Tilda": "I:\\Localhost",
  "Layout": "I:\\Localhost\\Layouts\\MainLayout.html",
  "Folders": {
    "Shared": "I:\\Localhost\\Shared"
  },
  "SpecialFolders": {
    "Root": "/wwwroot/"
  }
}
## Controllers and Routes

Controllers are defined as JSON files ending with `Controller.json`. Each contains a list of actions/routes with:

- **Paths:** List of URL paths matching this action.
- **View:** Path to the HTML view template.
- **Icon:** Optional favicon path.

### Example route loading:

- Loads all `*Controller.json` files from the controllers folder.
- Aggregates all actions for routing.
- Matches incoming requests to routes by exact path.

---

## Request Handling

- Requests starting with special folders like `/wwwroot/` serve static files from the configured root folder.
- Other requests are matched against registered routes.
- If matched, the server reads the view file, applies the layout (if any), and replaces placeholders with query parameters.
- Responds with the rendered HTML.
- If not matched, responds with a 404 page.
- On exceptions, responds with a 500 Internal Server Error.

---

## Layout and Template Processing

- Views can specify layout with `{{Layout="path"}}`.
- If `{{Layout="none"}}` is present, no layout is applied.
- Layout files have a `{{Body}}` placeholder replaced by the view content.
- Query parameters replace placeholders like `{{Model.key}}` inside the final page.

---

## MIME Types

Common MIME types supported include:

| Extension     | MIME Type               |
|---------------|------------------------|
| .png          | image/png              |
| .jpg / .jpeg  | image/jpeg             |
| .gif          | image/gif              |
| .ico          | image/x-icon           |
| .css          | text/css               |
| .js           | application/javascript |
| .html         | text/html              |
| .json         | application/json       |
| .svg          | image/svg+xml          |
| .woff / .woff2| font/woff, font/woff2  |
| .ttf          | font/ttf               |

---

## Console Commands

- **Backspace:** Stop the server and exit.
- **Enter:** Clear the console screen.
- **Spacebar:** Restart the server.

---

## Prerequisites

- .NET runtime compatible with HttpListener API.
- Administrator privileges to configure URL ACLs and hosts entries.

---

## Logging

The server logs key events via `CoreConsole` methods:

- `Information()`
- `Success()`
- `Warning()`
- `SimpleError()`
- `Error()`

These log to the console with different severity levels.

---

## Example of a Controller JSON (`ExampleController.json`)

```json
{
  "Actions": [
    {
      "Paths": ["/home", "/index"],
      "View": "I:\\Localhost\\Views\\Home.html",
      "Icon": "./favicon.ico"
    },
    {
      "Paths": ["/about"],
      "View": "I:\\Localhost\\Views\\About.html"
    }
  ]
}
## Extending and Customizing

- Add more routes by creating additional controller JSON files.
- Customize the layout and views to fit your website's design.
- Extend MIME types by updating the `MimeTypes` dictionary in the server code.
- Implement additional logging or error handling inside the `HandleRequestAsync` method.
