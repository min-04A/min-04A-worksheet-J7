# J7 WorkSheet

1. <ins>What is inside a packet?</ins>
**Header** and **payload**. Header stores the address of where to send the packet. Payload stores the data or message.

2. <ins>What is the purpose of an internet layer in the TCP/IP protocol? What do you, as a client, need to specify in this protocol?</ins>
The purpose of the internet layer is **to interconnect networks**. The internet layer both describes the protocols for how networks interconnect with each other and the way that computers are identified, via the internet protocol address or ip address. I need to **specify an internet protocol address or ip address**.

3. <ins>What is the purpose of the transport layer in the TCP/IP protocol? What do you, as a client, need to specify in this protocol?</ins>
The transport layer provides an abstraction for those two processes to appear as if they are communicating directly with each other. Since many processes can be communicating on the network at the same time, the transport layer also **provides a mechanism, called ports, to differentiate communication destined for one process versus another**. It needs to **specify destination port numbers** where you will send data to. 

4. <ins>What is the difference between SMTP and HTTP?</ins>
At the application layer, additional protocols are available depending on the task at hand. **SMTP is used to transmit email messages and HTTP is used to download web content**. The application layer is the domain where we get to choose what data is sent and received and how that data is interpreted.

5. <ins>What is the difference between an IP address and a domain name?</ins>
An **IP address is a numerical label** assigned to each device connected to a computer network that uses the Internet Protocol, while a **domain name is a human-readable address** that maps to that IP address, making it easier to remember and use. 

6. <ins>How does the operating system use ports?</ins>
The port address is a way for the Operating System to divide up the data arriving from the network based on the destination process. The **ports allow the operating system to differentiate traffic** for each application.

7. <ins>Write code that creates a socket connection to ip address 123.45.678.900 at port 4040. Then, print a color to that socket’s output.</ins>
```
import java.util.*;
import java.net.*;
import java.io.*;

public class ColorSocket {
    public static void main(String[] args) {
        String ip = "123.45.678.900"; 
        int port = 4040;
        String color = "red";
        Socket socket = null;

        try
        {
            socket = new Socket(ip, port);
        }

        catch (Exception e)
        {
            System.err.println("Cannot Connect");
            System.exit(1);
        }

        try
        {
            PrintWriter pw = new PrintWriter(socket.getOutputStream());
            pw.println(color);
            pw.close();
            socket.close();
        }

        catch (Exception e)
        {
            System.err.print("IOException");
            System.exit(1);
        }
    }
}
```

8. <ins>What is the difference between a socket’s input stream and its output stream?</ins>
A socket's **input stream is used for reading data received** from the other end of the connection, while its **output stream is used for writing data to be sent** to the other end. 

9. <ins>What is the difference between a Socket and a SocketServer?</ins>
Once the serverSocket is established we call accept(), which returns a new Socket that is used to communicate with that client. A **ServerSocket object waits for connections**. A **Socket object initiates a connection**.

10. <ins>How are threads useful with servers? How does a server manage to always be listening for sockets trying to connect?</ins>
**Threads let a server handle multiple clients at once**. Without threads, the server would be stuck handling one client at a time. A main thread runs in a loop, calling accept() to wait for client connections. **When a client connects, the server spawns a new thread (or uses a thread pool) to handle that client and keeps listening for new connections in the main thread**.