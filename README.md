# this_is_java

## TCP 네트워킹
 1. TCP는 연결 지향적 프로토콜로 클라이언트와 서버가 연결된 상태에서 테이터를 주고받는다.
		  	- 장점 : 데이터를 정확하고 안정적으로 전달한다.
				- 단점 : 데이터를 보내기 전에 반드시 연결이 형성되어야 하고(가장 시간이 많이 걸리는 작업), 고정된 통신 선로가 최단선(네트워크 길이 측면)이 아닐 경우 상대적으로 UDP보다 데이터 전송 속도가 느릴수 있다.
		
1. ServerSocket과 Socket의 용도
		 	 -	TCP서버의 역할 2가지 : 1.클라이언트가 연결 요청을 해오면 연결 수락 2.연결된 클라이언트와 통신
		 	 - 자바에서는 이 두 역할별로 별도의 클래스 제공
		 	 - java.net.ServerSocket : 클라이언트의 연결 요청을 기다리면서 연결 수락 담당
		 	 - java.net.Socket : 연결된 클라이언트와 통신을 담당
		 		**  즉. 클라이언트가 연결 요청을 해오면 ServerSocket은 연결을  수락하고 통신용 Socket을 만든다. **
        
1. 서버를 개발하려면 우선 ServerSocket객체를 얻어야 한다.
		- ServerSocket을 생성할 때 해당 포트가 이미 다른 츠로그램에서 사용중이라면 예외 발생
		1. 첫번째 방법
			``` 
      ServerSocket serverSocket1 = new ServerSocket(5001);
      ```
			
		1. 두번째 방법
			- 디폴트 생성자로 객체를 생성하고 포트바인딩을 위해 bind()메소드 호출
			- bind() 메소드이 매개값은 포트 정보를 가지고 있는 InetSocketAddress
			```
      ServerSocket serverSocket2 = new ServerSocket();
			serverSocket2.bind(new InetSocketAddress(5001));
			```
      
			//포트바인딩이 끝나면 클라이언트 연결 수락을 위해 accept()메소드를 실행해야 한다.
			//accept()메소드는 클라이언트가 연결 요청하기 전까지 스레드 대기상테이다.
			
			//연결된 클라이언트의 IP와 포트 정보를 알아내기
			
			//더이상 클라이언트 연결 수락이 필요없으면 ServerSocket의 close()메소드를 호촐
			//그래야 다른 프로그램에서 해당 포트를 재사용할 수 있기 때문
