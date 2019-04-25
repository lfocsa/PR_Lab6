# PR_Lab6
```
public class Client {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        InetAddress ip = InetAddress.getLocalHost();
        byte sendByte[];
        byte receiveByte[] = new byte[1024];

        while (true) {
            //Data Sending
            Scanner input = new Scanner(System.in);
            System.out.print("Client:");
            String sendMessage = input.nextLine();
            sendByte = sendMessage.getBytes();
            DatagramPacket sendDatagramPacket = new DatagramPacket(sendByte, sendByte.length, ip, 8082);
            socket.send(sendDatagramPacket);

            //Data Receiving
            DatagramPacket receiveDatagramPacket = new DatagramPacket(receiveByte, receiveByte.length);
            socket.receive(receiveDatagramPacket);
            String receiveMessage = new String(receiveDatagramPacket.getData());
            receiveMessage = receiveMessage.trim();
            System.out.println("Server:" + receiveMessage);

        }
    }

}
```


```
public class Server {
    public static void main(String[] args) throws Exception {
        DatagramSocket serverSocket = new DatagramSocket(8082);
        System.out.println("[Server started... Waiting for client to connect]");
        byte receiveByte[] = new byte[1024];
        byte sendByte[];
        while (true) {
            //data receiving
            DatagramPacket receiveDatagramPacket = new DatagramPacket(receiveByte, receiveByte.length);
            serverSocket.receive(receiveDatagramPacket);
            String receivedMessage = new String(receiveDatagramPacket.getData());
            receivedMessage = receivedMessage.trim();
            System.out.println("Client:" + receivedMessage);

            //data sending
            Scanner input = new Scanner(System.in);
            System.out.print("Server:");
            String sendMessage = input.nextLine();
            sendByte = sendMessage.getBytes();
            InetAddress ip = receiveDatagramPacket.getAddress();
            int port = receiveDatagramPacket.getPort();
            DatagramPacket sendDatagramPacket = new DatagramPacket(sendByte, sendByte.length, ip, port);
            serverSocket.send(sendDatagramPacket);
        }
    }

}
```
