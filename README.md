# SocketHandler
#### A flexible .NET WebSocket manager for connection handling, identifier-based routing, and broadcasting, with customizable Type
 
![Plugin Banners](https://github.com/user-attachments/assets/1147e680-7be5-4845-87f9-795f1615993c)

Install the package from NuGet:
```bash
dotnet add package SocketHandler
```
Or through the NuGet Package Manager Console:
```bash
Install-Package SocketHandler
```

## Features

- Connection Management: Easily add, remove, and manage WebSocket connections by ID or unique identifier.
- Targeted and Broadcast Messaging: Send messages to individual connections or broadcast to all active connections.
- Connection Identification: Assign unique identifiers for organized communication across clients.
 
## Usage
1. Setting Up the Connection Manager
> ConnectionManager<TData> allows you to manage WebSocket connections by connection ID and identifier.

```
using socket_handler.Interface;
using socket_handler.Implementation;
using System.Net.WebSockets;

var connectionManager = new ConnectionManager<string>();

// Adding a connection
connectionManager.AddConnection("connectionId1", webSocket, "userIdentifier");

// Sending data to a specific identifier
await connectionManager.SendDataToIdentifier("userIdentifier", "Hello User!");

// Broadcasting data to all connections
await connectionManager.SendDataAsync("Hello Everyone!");

``` 

2. Managing Connections with ConnectionHandler
> Use ConnectionHandler<TData> to handle incoming WebSocket connections and process messages from clients:

```
using socket_handler;

var connectionHandler = new ConnectionHandler<string>();

// Start handling a WebSocket connection
await connectionHandler.HandleConnectionAsync(webSocket, "connectionId1");
```

3. Interface for Dependency Injection

> The IConnectionManager<TData> interface outlines methods to:
> Add or remove connections
> Retrieve connections by ID or identifier
> Send messages to specific or all connections
> This supports dependency injection for testable, modular code.

```
public class MyWebSocketService
{
    private readonly IConnectionManager<string> _connectionManager;

    public MyWebSocketService(IConnectionManager<string> connectionManager)
    {
        _connectionManager = connectionManager;
    }

    public async Task BroadcastMessage(string message)
    {
        await _connectionManager.SendDataAsync(message);
    }
}
```

