# Lab Report 2 - Servers and SSH Keys (Week 3)

## Part 1
Write a web server called `ChatServer` that supports the path and behavior described below. It should keep track of a single string that gets added to by incoming requests. The requests should look like this:

`/add-message?s=<string>&user=<string>`

The effect of this request is to concatenate the string given after `user=`, a colon (`:`), and then the string after `s`, a newline (`\n`), and then respond with the entire string so far. That is, it adds a chat message of the form `<user>: <message>`

So, for example, after

```
/add-message?s=Hello&user=jpolitz
```

The page should show

```
jpolitz: Hello
```

and after

```
/add-message?s=How are you&user=yash
```

the page should show

```
jpolitz: Hello
yash: How are you
```

(Some browsers might show this as `How%20are%20you` with a special character replacing the spaces; don't worry about fixing that for this example. If you want to look it up it has to do with URL encoding, a topic we won't address right now.)

You can assume that the `s=` parameter always comes before the `user=` parameter, and they are always separated by a `&` as shown above.

Show the code for your `ChatServer`, and two screenshots of using `/add-message`.

For **each** of the two screenshots, describe:

- Which methods in your code are called?
- What are the relevant arguments to those methods, and the values of any relevant fields of the class?
- How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.


By *values*, we mean specific `String`s, `int`s, `URI`s, and so on. `"abc"` is a value, `456` is a value, `new URI("http://...")` is a value, and so on.)

<br>

### `ChatServer.java`

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
>   
> **Arguments and Field Values:**
> - `URI url`is `http://ieng6-202.ucsd.edu:4000/add-message?s=Hello&user=jpolitz`.
> - `user` is 'jpolitz'.
> - `message` is `Hello`.
> - > - `messageCount` incremented by 1.
> **Field Changes:**
> - `messageCount = 1`.
> - A new `ChatMessage` was added to `messages` as `user = "jpolitz", message = "Hello"`.

<img width="823" alt="Screenshot 2024-01-29 at 9 18 59 PM" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/89fe45e5-61fe-4464-b840-32b47b43cd25">

> **Methods Called:**
> - `handleRequest(URI url)` , `getCurrentChatLog()`.
>   
> **Arguments and Field Values:**
> - `URI url`is `http://ieng6-202.ucsd.edu:4000/add-message?s=How%20are%20you&user=yash`.
> - `user` is 'yash'.
> - `message` is `How are you`.
> - `messageCount` incremented by 1.
> 
> **Field Changes:**
> - `messageCount = 2`
> - A new `ChatMessage` was added to `messages` as `user = "yash", message = "How are you"`.

## Part 2
Using the command line, show with `ls` and take screenshots of:

- The absolute path to the *private* key for your SSH key for logging into `ieng6` (on your computer, an EdStem workspace, or on the home directory of the lab computer)
- The absolute path to the *public* key for your SSH key for logging into `ieng6` (this is the one you copied to your account on ieng6, so it should be a path on ieng6's file system)
- A terminal interaction where you log into your `ieng6` account *without* being asked for a password.

### Private Key
<img width="897" alt="Screenshot 2024-01-30 at 11 08 53 AM" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/47620ab6-422a-441f-acd0-c0a2568446d7">

> **Absolute Path:** `/Users/rebekaheast/.ssh/id_rsa` 

### Public Key
<img width="897" alt="Screenshot 2024-01-30 at 11 07 46 AM" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/fd58ebce-1f11-4c45-8f00-36c1ac10c793">

> **Absolute Path:** `/home/linux/ieng6/oce/13/hak033/.ssh/authorized_keys` 

### Successful Log On with Key
![image](https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/e9200723-b15e-4ddb-b4ea-ed167b81b15b)

## Part 3
In a couple of sentences, describe something you learned from lab in week 2 or 3 that you didn't know before.


> In the lab, I learned how to effectively use Visual Studio Code (VSCode) as an integrated development environment. This would include understanding its user interface, learning to navigate and manage files within VSCode, and utilizing its built-in terminal for executing various commands. 
