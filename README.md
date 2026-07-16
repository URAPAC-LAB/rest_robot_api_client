# REST Robot API Client

> A single-file browser application for sending HTTP requests and inspecting responses —
> similar to Postman, but requiring no installation. Open `index.html` directly in any modern
> browser.

Refer to <https://app.swaggerhub.com/organizations/universalrobots-api> for the latest
documentation on the UR Robot API.

## Key capabilities

- Send **GET, POST, PUT, PATCH, and DELETE** requests
- Add custom **headers** with a key-value editor
- Write a **JSON request body**
- View formatted **response body and headers**
- Quick-access built-in **JSONPlaceholder** examples
- **Universal Robots (UR) API** quick-select panel
- **Request history** (last 20 requests auto-saved)
- **Dark and light themes**
- **Adjustable font size**

## Interface layout

The application is divided into four main areas:

- **Top bar** — method selector, URL input, Send button, and utility buttons
- **Left sidebar** — request history
- **Main workspace** — request headers/body editor and response panel
- **Right sidebar** — built-in example collections

The UR API panel (see below) sits between the top bar and the workspace, and is hidden by default.

## Sending a basic request

### GET

1. Select **GET** from the method dropdown on the left of the URL bar.
2. Type or paste a URL into the address field (e.g. `https://jsonplaceholder.typicode.com/posts/1`).
3. Click **Send**.
4. The response body appears in the lower workspace panel. The status code, time, and size are
   shown above the response.

### POST / PUT / PATCH

1. Select the desired method (POST, PUT, or PATCH).
2. Enter the endpoint URL.
3. Click the **Body** tab in the request panel and type a JSON payload.
4. Add a `Content-Type: application/json` header in the **Headers** tab (the UR API panel does
   this automatically).
5. Click **Send**.

### Response panel

The response panel has two tabs:

- **Body** — formatted and syntax-highlighted JSON (or raw text)
- **Headers** — all response headers returned by the server

A **Copy** button at the top right copies the raw response body to the clipboard.

## Headers editor

Click the **Headers** tab in the request panel to add custom request headers.

- Click **+ Add Header** to insert a new key-value row.
- Type the header name in the left field and its value in the right field.
- Click the red **x** button on the right to remove a row.

Common headers:

| Header | Use |
|---|---|
| `Content-Type: application/json` | Required for JSON body requests |
| `Authorization: Bearer <token>` | For authenticated endpoints |
| `Accept: application/json` | Request JSON responses |

## Universal Robots (UR) API panel

The UR API panel provides quick access to the Universal Robots Robot API. Click the **UR API**
button in the top bar to open or close it.

Refer to <https://app.swaggerhub.com/organizations/universalrobots-api> for the latest
documentation on the Robot API.

### Connecting to a robot

1. Enter your robot's base URL in the **Robot URL** field (e.g. `http://192.168.1.100`).
2. Select an API domain from the **Domain** dropdown: License, Program, Robotstate, or System.
3. Select an endpoint from the **Endpoint** dropdown.
4. Click **Load** to populate the main request form.
5. Click **Send** as usual.

### Endpoints with path parameters

Some endpoints require values embedded in the URL path (e.g. `vendor_id` and `product_code` for
the License API). When such an endpoint is selected, input boxes appear in the panel for each
parameter. Fill in the parameter values before clicking **Load** — the values are substituted
into the URL automatically.

### Automatic Content-Type header

For PUT and POST endpoints that include a request body, the UR API panel automatically adds a
`Content-Type: application/json` header when loading the endpoint. You do not need to add it
manually.

### CORS and network errors

> **Note:** If the app is opened from a `file://` URL (double-clicked), the browser may block
> requests to `http://` robot addresses. For best results, serve the file over a local HTTP
> server (e.g. `python -m http.server 3456`) and open
> `http://localhost:3456/rest-client.html`.

> **Note:** Robot firmware must have CORS headers enabled. If you see "Failed to fetch", confirm
> the robot IP is reachable from your machine by opening the URL directly in a browser tab first.

## Request history

Every request is automatically saved in the left sidebar. Up to 20 recent requests are stored.

- Click any history entry to restore the method, URL, headers, and body.
- History persists across page reloads (stored in browser `localStorage`).

## Built-in example collections

The right sidebar contains pre-built request examples. Click any item to load it into the
request form immediately. The JSONPlaceholder collection covers all common HTTP methods against
a public test API:

- GET all posts
- GET post by ID
- POST create post
- PUT replace post
- PATCH update post
- DELETE post
- GET users

## Appearance settings

### Dark / Light theme

Click the theme toggle button in the top bar to switch between dark (default) and light themes.
The preference is saved and restored on reload.

### Font size

Use the **A-** and **A+** buttons in the top bar to decrease or increase the interface font size.
The zoom level ranges from 70% to 180% in 10% steps and is saved across sessions.

## Troubleshooting

### Failed to fetch / Network Error

- Verify the URL is reachable (open it directly in a browser tab).
- Robot endpoints use HTTP — the app detects private IP ranges and uses `http://` automatically.
- If running from `file://`, switch to `http://localhost:3456/rest-client.html`.
- Check that the robot is powered on and the network interface is connected.

### 422 Unprocessable Entity

- This means the server received the request but rejected the body format.
- Ensure `Content-Type: application/json` is set (the UR panel adds this automatically).
- Check that the JSON body is valid and matches the expected schema shown in the Body hint.

### CORS Error

- CORS is enforced by the browser when a web page makes cross-origin requests.
- For robot endpoints, the robot firmware must send CORS response headers.
- For public APIs, ensure you are using the correct URL (`https://` for non-local addresses).

## Files

| File | Description |
|---|---|
| [`index.html`](./index.html) | The application — open in any modern browser |
| [`rest-_robotapi client-user-manual.docx`](./rest-_robotapi%20client-user-manual.docx) | Full user manual (Word document) |

A live, hosted version is available via GitHub Pages:
**https://rando5701.github.io/rest_robot_api_client/**

---

*Version 1.0 | June 2026*