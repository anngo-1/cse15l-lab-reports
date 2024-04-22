# Lab 2
## Part 1
### ChatServer.java code:
```
import java.io.IOException;
import java.net.URI;
import java.util.Arrays;
import java.util.ArrayList; 
import java.util.*;
class Handler implements URLHandler {

    ArrayList<String> chats = new ArrayList<>();


    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            if (chats.size() == 0) {
                return "    ";
            } else {
            StringBuilder builder = new StringBuilder();
            for (String value : chats) {
                builder.append(value);
            }
            String chatlog = builder.toString();
            return String.format("%s", chatlog);
            }
        } else if (url.getPath().equals("/test")) {
            return String.format("test path");
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                

                if (parameters[0].equals("s") && (parameters[1].split("&"))[1].equals("user")) {
                    chats.add(parameters[2] + ": " + parameters[1].split("&")[0] + "\n");
                StringBuilder builder = new StringBuilder();
                for (String value : chats) {
                    builder.append(value);
                }
                String chatlog = builder.toString();
                    return String.format("%s", chatlog);
                } else {
                    return "Incorrect usage!";
                }
            }
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```
Code to create the server was reused from wavelet's Server.java.


### Root path of the server
In this case, only the root path URL is needed. Some error checking is done to ensure there are no issues when there are no problems when the chat server is empty. It will simply display what has already been added to the chat server, so this screenshot is displaying some text I previously added.

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/a971c435-5130-4ddc-b39e-162414f655d5)

### Add Message Example 1
Add message functionality, with the path ```/add-message?s=I%20how%20good&user=hello2```. It returns the new chatlog, with the message added. The path denotes the s parameter (the actual message) as "I how good", and the user parameter as "hello2".
- The method being called in the code is handleRequest. 
- The relevant argument is only the URL, which will change depending on what kind of message we want to add to our chat server. The value for the url in this case is `http://localhost:4003//add-message?s=I%20how%20good&user=hello2`
-  This code will add the formatted message, `hello2: I how good` into an String ArrayList, which is then returned as a response after some formatting with a StringBuilder. The ArrayList before is `[hello1: I dasdas good]`, the ArrayList after running this path is `[hello1: I dasdas good, hello2: I how good]`
  
![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/137ccf79-fe74-4188-8ef9-98a673e3a58a)

### Add Message Example 2
Another screenshot of add message, with the path `/add-message?s=hi!&user=dog`. The path denotes the s parameter (the actual message) as "hi!", and the user parameter as "dog"
- The method being called in the code is handleRequest.
- The relevant argument is only the URL, which will change depending on what kind of message we want to add to our chat server. The value for the url in this case is `http://localhost:4003/add-message?s=hi!&user=dog`
-  This code will add the formatted message, `dog: hi!` into an String ArrayList, which is then returned as a response after some formatting with a StringBuilder. The ArrayList before is `[hello1: I dasdas good, hello2: I how good]`, the ArrayList after running this path is `[hello1: I dasdas good, hello2: I how good, dog: hi!]`
  
![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/1d7606ca-67ad-463a-a377-a34fb336a388)

## Part 2
1. ```ls``` with absolute path to private key (on local machine)
   
![Screenshot from 2024-04-16 14-48-36](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/e58416ff-9ecf-424a-aa52-927dec16cbd6)

2. ```ls``` with absolute path to public key (on ieng6)

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/14ec2175-c868-4d36-a94b-5896006a8b4f)

3. `ssh` into ieng6 without being asked for a password

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/e869a7b4-07ba-46bd-bd64-d8103130e0c1)

## Part 3
I learned about server implementation in Java. I also learned how to use access a remote school computer using ssh, and setting up ssh on my machine with ssh-keygen. 
