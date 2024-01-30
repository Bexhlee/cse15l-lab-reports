# Lab Report 2 - Servers and SSH Keys (Week 3)

## Part 1 - `ChatServer.java`

```java
import java.io.IOException;
import java.net.URI;

// A simple class to represent a chat message
class ChatMessage {
    String user;
    String message;

    public ChatMessage(String user, String message) {
        this.user = user;
        this.message = message;
    }

    // This method is used to format the chat message as a string
    @Override
    public String toString() {
        return user + ": " + message + "\n";
    }
}

class ChatServerHandler implements URLHandler {
    // Define a maximum number of messages the server can hold
    private static final int MAX_MESSAGES = 200;
    // Array to store chat messages
    private ChatMessage[] messages = new ChatMessage[MAX_MESSAGES];
    // Counter for the number of messages currently stored
    private int messageCount = 0;

    public String handleRequest(URI url) {
        // Check if the URL path is for adding a message
        if (url.getPath().equals("/add-message")) {
            // Get the query part of the URL
            String query = url.getQuery();
            // Check if the query is null or empty
            if (query == null || query.isEmpty()) {
                return "Invalid request. No query parameters found.";
            }

            // Split the query into parameters
            String[] params = query.split("&");
            // Check if there are exactly two parameters
            if (params.length != 2) {
                return "Invalid request. Expected two parameters.";
            }

            String user = null, message = null;
            for (String param : params) {
                String[] keyValue = param.split("=");
                // Check if each parameter is in key=value format
                if (keyValue.length != 2) {
                    return "Invalid parameter format.";
                }
                // Assign values to user and message based on parameter name
                if ("user".equals(keyValue[0])) {
                    user = keyValue[1];
                } else if ("s".equals(keyValue[0])) {
                    message = keyValue[1];
                }
            }

            // Check if both user and message are provided
            if (user == null || message == null) {
                return "Missing user or message parameter.";
            }

            // Check if the message limit has been reached
            if (messageCount >= MAX_MESSAGES) {
                return "Message limit reached.";
            }

            // Store the new message
            messages[messageCount++] = new ChatMessage(user, message);
        }

        // Return the current state of the chat log
        return getCurrentChatLog();
    }

    // Method to construct the current chat log as a string
    private String getCurrentChatLog() {
        if (messageCount == 0) {
            return "No Messages!";
        }
        StringBuilder chatLog = new StringBuilder();
        for (int i = 0; i < messageCount; i++) {
            chatLog.append(messages[i]);
        }
        return chatLog.toString();
    }
}

public class ChatServer {
    public static void main(String[] args) throws IOException {
        // Check for the presence of the port argument
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        // Convert the port argument to an integer
        int port = Integer.parseInt(args[0]);
        // Start the server on the given port with the ChatServerHandler
        Server.start(port, new ChatServerHandler());
    }
}
```
### Screenshots

<img width="823" alt="Screenshot 2024-01-29 at 9 18 28 PM" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/43a60516-0a47-4893-a786-d035e5e6d585">

> **Methods Called:**
> - `handleRequest(URI url)` , `getCurrentChatLog()`.
> **Arguments and Field Values:**
URI url is http://ieng6-202.ucsd.edu:4000/add-message?s=Hello&user=jpolitz.
user is "jpolitz", message is "Hello".
messageCount was incremented by 1.
A new ChatMessage was added to messages.
Field Changes:
messages now includes the new message from "jpolitz".
messageCount increases by 1.

<img width="823" alt="Screenshot 2024-01-29 at 9 18 59 PM" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/89fe45e5-61fe-4464-b840-32b47b43cd25">

