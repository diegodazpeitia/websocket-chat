# Real-Time Chat Application

This project is a simple real-time chat application built with Go and WebSockets. It demonstrates how to create a chat room where users can send and receive messages instantly.

## Features

- Real-time communication using WebSockets.
- Broadcasts messages to all connected clients.
- Handles multiple clients simultaneously.

## Prerequisites

- Go 1.18 or later
- [Gorilla WebSocket](https://github.com/gorilla/websocket) library

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/real-time-chat.git
   cd real-time-chat
   ```

2. **Install dependencies:**

   Install the Gorilla WebSocket package using `go get`:

   ```bash
   go get github.com/gorilla/websocket
   ```

3. **Build the application:**

   ```bash
   go build -o chat-app
   ```

4. **Run the application:**

   ```bash
   ./chat-app
   ```

   The server will start and listen on port 8080.

## Usage

1. **Open the chat application:**

   Open a web browser and navigate to `http://localhost:8080`. You will see a welcome message: "Welcome to the Chat Room!"

2. **Connect to the WebSocket:**

   The application listens for WebSocket connections at `ws://localhost:8080/ws`. You can connect to this WebSocket endpoint using a WebSocket client in your web application or a WebSocket testing tool.

3. **Send and Receive Messages:**

   - **Send Message**: Use the WebSocket connection to send a JSON message with the following format:

     ```json
     {
       "username": "YourUsername",
       "message": "YourMessage"
     }
     ```

   - **Receive Message**: Messages sent by any client are broadcast to all connected clients.

## Code Overview

- **`main.go`**: The main entry point of the application. Sets up the HTTP server, handles WebSocket connections, and manages message broadcasting.

- **Functions**:
  - `homePage(w http.ResponseWriter, r *http.Request)`: Serves the homepage with a welcome message.
  - `handleConnections(w http.ResponseWriter, r *http.Request)`: Upgrades HTTP connections to WebSocket and listens for incoming messages.
  - `handleMessages()`: Broadcasts received messages to all connected clients.

- **Data Structures**:
  - `Message`: Represents a chat message with `Username` and `Message` fields.
  - `clients`: A map storing active WebSocket connections.
  - `broadcast`: A channel for broadcasting messages to clients.

## Example WebSocket Client

Here's a simple example of how you might connect to the WebSocket server using JavaScript:

```javascript
const ws = new WebSocket('ws://localhost:8080/ws');

ws.onopen = () => {
  console.log('Connected to WebSocket server');
};

ws.onmessage = (event) => {
  const msg = JSON.parse(event.data);
  console.log(`${msg.username}: ${msg.message}`);
};

function sendMessage(username, message) {
  const msg = JSON.stringify({ username, message });
  ws.send(msg);
}
```

## Contributing

Feel free to fork the repository and submit pull requests with improvements or bug fixes. 

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
