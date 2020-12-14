### TCP SOCKET PROGRAMMING BASICS

<table>
<tr align = 'center'>
<td>서버</td>
<td></td>
<td>클라이언트</td>
</tr>
<tr align = 'center'>
<td>소켓 객체 생성</td>
<td></td>
<td>소켓 객체 생성</td>
</tr>
<tr align = 'center'>
<td>bind</td>
<td></td>
<td></td>
</tr>
<tr align = 'center'>
<td>accept</td>
<td> <- </td>
<td>connect</td>
</tr>
<tr align = 'center'>
<td>read</td>
<td> <- </td>
<td>write</td>
</tr>
<tr align = 'center'>
<td>write</td>
<td> -> </td>
<td>read</td>
</tr>
<tr align = 'center'>
<td>close</td>
<td></td>
<td>close</td>
</tr>
</table>

### TCP Client

#### Socket 객체 생성

``` java
Socket socket = null;
socket = new Socket();
```

#### Connect (서버에 연결)

``` java
socket.connect(new InetSocketAddress(SERVER_IP,SERVER_PORT));
```

#### 쓰기

``` java
OutputStream os = socket.getOutputStream();
String data = "Hello World";
os.write(data.getBytes("UTF-8"));
```

#### 읽기

``` java
InputStream is = socket.getInputStream();
byte[] buffer = new byte[256];
int readByteCount = is.read(buffer);
```

#### close

``` java
if(readByteCount == -1) {
return;
}
```



#### TCP Client /전체 코드

``` java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.Socket;

public class TCPClient {
	private static final String SERVER_IP = "127.0.0.1";
	private static final int SERVER_PORT = 6000;
	
	public static void main(String[] args) {
		Socket socket = null;
		
		try {
			//1. 소켓 생성
			socket = new Socket();
			
			//2. 서버 연결
			socket.connect(new InetSocketAddress(SERVER_IP,SERVER_PORT));
			System.out.println("[client] connected!");
			
			//3. IOStream 받아오기
			InputStream is = socket.getInputStream();
			OutputStream os = socket.getOutputStream();
			
			//4. 쓰기
			String data = "Hello World";
			os.write(data.getBytes("UTF-8"));

			//5. 읽기
			byte[] buffer = new byte[256];
			int readByteCount = is.read(buffer);
			
			if(readByteCount == -1) {
				// server 정상종료
				System.out.println("[client] closed by server");
				return;
			}
			
			data = new String(buffer, 0, readByteCount, "UTF-8");
			System.out.println("[clinet] received:" + data);
			
		} catch (IOException e) {
			System.out.println("[client] error:" + e);
		} finally {
			try {
				if(socket != null && !socket.isClosed())
				socket.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		

	}

}
```

<br>
<hr>
<br>



### TCPServer

#### 1. Socket 객체 생성

``` java
serverSocket = new ServerSocket();
```

#### 2. 바인딩(binding): Socket Address(IP Address + Port)

``` java
serverSocket.bind(new InetSocketAddress("127.0.0.1", 6000));
```

#### 3. accept

``` java
Socket socket = serverSocket.accept();  // blocking
```

#### 연결된 주소값 출력
``` java
InetSocketAddress remoteInetSocketAddress = (InetSocketAddress)socket.getRemoteSocketAddress();
InetAddress remoteInetAddress = remoteInetSocketAddress.getAddress();
String remoteHostAddress = remoteInetAddress.getHostAddress();
int remotePort = remoteInetSocketAddress.getPort();
System.out.println("[server] connected by client[" + remoteHostAddress + ":" + remotePort + "]");
```

#### 4. IOStream 받아 오기

``` java
InputStream is = socket.getInputStream();
OutputStream os = socket.getOutputStream();
```

#### 5. 데이터 읽기

``` java
byte[] buffer = new byte[256];
int readByteCount = is.read(buffer); // blocking
```

#### 6. 데이터쓰기

``` java
os.write(data.getBytes("utf-8"));
```

#### 7. close

``` java
if(readByteCount == -1){
	break;
}
```

#### TCP Server /전체 코드

``` java 
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.InetSocketAddress;
import java.net.ServerSocket;
import java.net.Socket;

public class TCPServer {

	public static void main(String[] args) {
		ServerSocket serverSocket = null;
		
		try {
			//1. 서버소켓 생성
			serverSocket = new ServerSocket();
			
			//2. 바인딩(binding): Socket Address(IP Address + Port)
			serverSocket.bind(new InetSocketAddress("127.0.0.1", 6000));

			//3. accept
			Socket socket = serverSocket.accept();  // blocking
			
			InetSocketAddress remoteInetSocketAddress = (InetSocketAddress)socket.getRemoteSocketAddress();
			InetAddress remoteInetAddress = remoteInetSocketAddress.getAddress();
			String remoteHostAddress = remoteInetAddress.getHostAddress();
			int remotePort = remoteInetSocketAddress.getPort();
			System.out.println("[server] connected by client[" + remoteHostAddress + ":" + remotePort + "]");
			
			try {
				//4. IOStream 받아 오기
				InputStream is = socket.getInputStream();
				OutputStream os = socket.getOutputStream();
				
				while(true) {
					//5. 데이터 읽기
					byte[] buffer = new byte[256];
					int readByteCount = is.read(buffer); // blocking
					
					if(readByteCount == -1){
						// client가 소켓을 정상적으로 종료
						System.out.println("[server] closed by client");
						break;
					}
					
					String data = new String(buffer, 0, readByteCount, "UTF-8");
					System.out.println("[server] received:" + data);
					
					//6. 데이터쓰기
					os.write(data.getBytes("utf-8"));
				}
				
				
			} catch(IOException e) {
				System.out.println("[server] error:" + e);
			} finally {
				try {
					if(socket != null && !socket.isClosed()) {
						socket.close();
					}
				} catch(IOException e) {
					e.printStackTrace();
				}
			}
			
		} catch (IOException e) {
			System.out.println("[server] error:" + e);
		} finally {
			try {
				if(serverSocket != null && !serverSocket.isClosed()) {
					serverSocket.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		
	}

}
```
