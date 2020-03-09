# JavaBasic-2
Inflearn - JavaProgramming Basic Course (renew ver.) 21강 인터페이스~

[21강 - 인터페이스](#21강---인터페이스)

[22강 - 추상클래스](#22강---추상클래스--abstract-class) 

[23강 - 람다식](#23강---람다식)

[24강 - 문자열 클래스](#24강---문자열-클래스)

[25강 - collections](#25강---collections)

[26강 - 예외처리](#26강---예외처리)

[27강 - 입력과 출력](#27강---입력과-출력)

[28강 - 네트워킹](#28강---네트워킹)


21강 - 인터페이스
----------------

21-1 인터페이스란?
`````
클래스와 달리 객체를 생성할 수는 없으며, 클래스에서 구현해야 하는 작업 명세서이다.
`````

21-2 인터페이스를 사용하는 이유
`````
인터페이스를 사용하는 이유는 많지만, 가장 큰 이유는 객체가 다양한 자료형 ( 타입 ) 을 가질 수 있기 때문이다.
`````
`````java
Ex) 
public class ImpleemntClass implements InterfaceA, InterfaceB, InterfaceC, InterfaceD{
	public ImplementClass(){
		...	
	}
}

InterfaceA ia = new ImplementClass();
InterfaceB ib = new ImplementClass();
InterfaceC ic = new ImplementClass();
InterfaceD id = new ImplementClass();


21-3 인터페이스 구현

public class Main {

	public static void main(String[] args) {
		InterfaceA ia = new InterfaceClass();
		InterfaceB ib = new InterfaceClass();		

		ia.funA();		// InterfaceClass로 생성했지만 자료형이 InterfaceA라 

funB()는 사용 X
		ib.funB();		// InterfaceClass로 생성했지만 자료형이 InterfaceB라 

funA()는 사용 X
	}

}

// 인터페이스를 이용한 클래스 

public class InterfaceClass implements InterfaceA, InterfaceB{
	

	public InterfaceClass() {
		System.out.println("--InterfaceClass--");
	}

	@Override
	public void funB() {
		System.out.println("--funA()--");
		
	}

	@Override
	public void funA() {
		System.out.println("--funB()--");
		
	}
}

// 인터페이스들

public interface InterfaceA {
	
	public void funA();
	
}

public interface InterfaceB {
	
	public void funB();
	
}
`````


22강 - 추상클래스 ( Abstract Class) 
----------

22-1 추상클래스란?
`````
클래스의 공통된 부분을 뽑아서 별도의 클래스 ( 추상클래스 ) 로 만들어 놓고, 이것을 상속해서 사용한다.

abstract 클래스의 특징
1. 멤버변수를 가진다.
2. abstract 클래스를 상속하기 위해서는 extends를 이용한다.
3. abstract 메서드를 가지며, 상속한 클래스에서 반드시 구현해야한다!!
4. 일반 메서드도 가질수 있다.
5. 일반 클래스와 마찬가지로 생성자도 있다.
`````

22-2 추상클래스 구현
`````
클래스 상속과 마찬가지로 extends 키워드를 이용해서 상속하고, abstract ( 추상 ) 메서드를 구현한다.
`````
`````java
Ex)


public class Main {
		public static void main(String[] args) {
			AbstractClassEx abs = new ClassEx(10, "java");
			abs.fun1();
			abs.fun2();			
		}

}

// 추상클래스 
public abstract class AbstractClassEx {
	int num;
	String str;
	
	public AbstractClassEx() {
		System.out.println("AbstractClassEx constructor");
	}

	public AbstractClassEx(int num, String str) {
		System.out.println("AbstractClassEx constructor");		
		this.num = num;
		this.str = str;
	}
	
	public void fun1() {
		System.out.println("-- fun1() START --");
	}
	
	// 추상메서드
	public abstract void fun2();
	
	
}

// 추상클래스 상속
public class ClassEx extends AbstractClassEx {
	public ClassEx() {
		System.out.println("ClassEx constructor");
	}
	
	public ClassEx(int i, String s) {
		super(i,s);
	}
	
	@Override
	public void fun2() {
		// TODO Auto-generated method stub
		System.out.println("-- fun2() START --");
	}
	
}

// 결과 

AbstractClassEx constructor
-- fun1() START --
-- fun2() START --
`````

22-4 인터페이스 vs 추상클래스
``````````
공통점 : 
추상메서드를 가진다. 
객체생성이 불가하며 자료형 ( 타입 ) 으로 사용된다.

차이점 : 
인터페이스 - 상수, 추상메서드만 가진다. 추상메서드를 구현만 하도록 한다. 다형성을 지원한다.
추상클래스 - 클래스가 가지는 모든 속성과 기능을 가진다. 추상 메서드 구현 및 상속의 기능을 가진다. 단일 상속만 지원한다.
```````````

23강 - 람다식
----------

23-1 람다식이란?
`````
익명 함수 ( anonymous function )을 이용해서 익명 객체를 생성하기 위한 식이다.
`````

23-2 람다식 구현
`````
람다식은 기본적으로 함수를 만들어 사용한다고 생각하면 된다.
`````
`````java
public class Main {
	public static void main(String[] args) {
		// 매개 변수와 실행문 만으로 작성한다. ( 접근자, 반환형, return 키워드 생략 )
		LambdaInterface1 li1 = (String s1, String s2, String s3) -> {System.out.println(s1+" "+s2+" "+s3);};
		li1.method("Hello", "Java", "World");		
		
		System.out.println();
		
		// 매개 변수가 1개이거나 타입이 같을 때, 타입을 생략할 수있다.
		LambdaInterface2 li2 = (s1) -> {System.out.println(s1);};
		li2.method("Hello");
		
		// 실행문이 1개일 때, '{}'를 생략 할 수 있다.
		LambdaInterface2 li3 = (s1) -> System.out.println(s1);
		li3.method("Hello");
		
		// 매개변수와 실행문이 1개일 때, '()'와 '{}' 를 생략할 수 있다.
		LambdaInterface2 li4 = s1 -> System.out.println(s1);
		li4.method("Hello");
		
		// 매개변수가 없을 때, '()'만 작성한다.
		LambdaInterface3 li5 = () -> System.out.println("no parameter");
		li5.method();
		
		// 변환 값이 있는 경우
		LambdaInterface4 li6 = (x,y) -> {
			int result = x+y;
			return result;
		};
		System.out.printf("li6.method(10,20) :  %d\n", li6.method(10, 20));
		
		LambdaInterface4 li7 = (x,y) -> {
			int result = x*y;
			return result;
		};
		System.out.printf("li6.method(10,20) :  %d\n", li7.method(10, 20));
	}
}

// 람다식
public interface LambdaInterface1 {
	public void method(String s1, String s2, String s3);
}

public interface LambdaInterface2 {
	public void method(String s1);
}

public interface LambdaInterface3 {
	public void method();
}

public interface LambdaInterface4 {
	public int method(int x, int y);
}
`````

24강 - 문자열 클래스
----------
24-1 String 객체와 메모리
`````
문자열을 다루는 String 클래스(객체)는 데이터가 변하면 메모리 상의 변화가 많아 속도가 느리다.

- 문자열이 변경되면 기존의 객체를 버리고, 새로운 객체를 메모리에 생성한다.
이때, 기존 객체는 GC에 의해서 메모리 회수가 이루어진다.
`````

24-2 StringBuffer, StringBuilder
`````
String 클래스의 단점을 보완한 클래스로 데이터가 변경되면 메모리에서 기존 객체를 재활용한다.

StringBuffer sf = new StringBuffer("JAVA");
sf.append("_8");

- 문자열이 변경되면 기존의 객체를 재활용한다.
- 속도는 StringBuilder가 조금 더 빠르며, 데이터 안정성은 StringBuffer가 조금 더 좋다.
`````

25강 - collections
---------------
25-1 List
`````
List는 인터페이스로 이를 구현한 클래스는 인덱스를 이용해서 데이터를 관리한다.
( Vector, ArrayList, LinkedList )
- 특징 :
1. 인덱스를 이용한다.
2. 데이터 중복이 가능하다.
`````
`````java
// ArrayList 객체생성
ArrayList<String> list = new ArrayList<String>();

// 데이터 추가
list.add("Hello");
list.add("Java");
list.add("World");

// 해당 인덱스에 추가 , 해당 인덱스에 있던 데이터가 뒤로 밀림
list.add(2, "Programing");

// 데이터 변경
list.set(1, "C");	// 첫번째데이터를 "C"로 변경

// 데이터 추출
String str = list.get(2);

// 데이터 제거
str = list.remove(2);

// 데이터 전체 제거 , 객체는 살아있음
list.clear();

// 데이터 유무
boolean b = list.isEmpty();
`````

25-2 Map
`````
Map은 인터페이스로 이를 구현한 클래스는 key를 이용해서 데이터를 관리한다.
(HashMap)
- 특징 : 
1. key를 이용한다.
2. key는 중복될 수 없다.
3. 데이터 중복이 가능하다.
`````
`````java
// HashMap 객체 생성
HashMap<Integer, String> map = new HashMap<Integer, String>();

// 데이터 추가
map.put(5,"Hello");
map.put(6,"Java");
map.put(7,"World");
System.out.println("map : "+map);
System.out.println("map.size() : "+map.size());

// 데이터 교체
map.put(6,"C"); // 원래있던 Java 사라짐

// 데이터 추출
str = map.get(5); // Hello

// 데이터 제거
map.remove(8); // key 값이 8

// 특정 키 포함 유무
b = map.containsKey(7); // true

// 특정 데이터 포함 유무
b = map.containsValue("World"); // true

// 데이터 전체 제거
map.clear();

// 데이터 유무
b = map.isEmpty(); // true
`````

26강 - 예외처리
------------
26-1 예외란?
`````
프로그램에 문제가 있는 것을 말하며,  예이로 인해 시스템 동작이 멈추는 것을 막는 것을 '예외처리'라고 한다.

Exception : 소프르웨어적으로 문제가 있는 것으로 개발자가 대처할 수있음
Error : 물리적으로 문제가 있는 것으로 개발자가 대처할 수 없음.

Checked Exception : '예외처리'를 반드시 해야하는 경우 ( 네트워크, 파일 시스템 등 )
Unchecked Exception : '예외처리'를 개발자의 판단에 맞기는 경우 ( 데이터 오류 등 )
`````

26-2 Exception 클래스
`````
Exception 클래스 하위클래스로 NullPointerException, NumberFormatException 등이 있다.

Ex)
NullPointerException : 객체를 가리키지 않고 있는 레퍼런스를 이용할 때
ArrayIndexOutOfBoundException : 배열에서 존재하지 않는 인덱스를 가리킬 때
NumberFormatException : 숫자데이터에 문자데이터 등을 넣었을 때
`````

26-3 try ~ catch
`````
개발자가 예외처리하기 가장 쉽고, 많이 사용되는 방법으로 예외가 발생할만한 부분을 try안쪽에 넣고 catch로 예외구분을 하여 잡는다.

try {
	예외가 발생할 수있는 코드
} catch(Exception e){
	예외가 발생했을 떄 처리할 코드
}
`````

26-4 다양한 예외처리
`````
Exception 및 하위 클래스를 이용해서 예외처리를 다양하게 할 수 있다.

여러 catch 조건부에 여러 Exception을 사용하는 것이 예제로 나옴
`````

26-5 finally
`````
예외 발생 여부에 상관없이 반드시 실행된다.

try {
	예외가 발생할 수있는 코드
} catch(ArrayIndexOutOfBoundsException e){
	예외가 발생했을 떄 처리할 코드
} catch(Exception e){
	예외가 발생했을 떄 처리할 코드
} finally {
	System.out.println("예외 발생 여부에 상관없이 언제나 실행 됩니다.");
}
`````

26-6 throws
`````
예외 발생 시 예외 처리를 직접하지 않고 호출한 곳으로 넘긴다.

public void firstMethod() throws Exception{ secondMethod(); } // 예외 발생하면 호출한 곳으로

public void  secondMethod() throws Exception{ thirdMethod(); } // 예외발생하면 firstMethod로 던짐

public void  thirdMethod() throws Exception{ ... } // 예외 발생 하면 secondMethod로 던짐
`````

27강 - 입력과 출력
------------

27-1 입/출력 이란?
`````
다른 곳의 데이터를 가져오는 것을 입력이라 하고, 다른 곳으로 데이터를 내보내는 것을 출력이라고 한다.
`````
![IO](https://user-images.githubusercontent.com/22463540/76242420-0e14d580-627a-11ea-8957-1f6ad5fd1cfd.png)

27-2 입/출력 기본 클래스
`````
입 / 출력에 사용되는 기본 클래스는 1byte단위로 데이터를 전송하는 InputStream, OutputStream이 있다.

27-3 FileInputStream / FileOutputStream

파일에 데이터를 읽고 / 쓰기 위한 클래스로 read(), write() 메서드를 이용한다.

@ FileInputStream

read() : 1byte씩 읽어온다.

read(byte[]) : 배열의 크기만큼 읽어온다.

@ FileOutputStream

write(byte[] b) : 전체 쓰기

write(byte[], int off, int len) : off (시작점), len (길이)
`````

27-4 파일 복사
`````
FileInputStream과 FileOutputStream을 이용하여 복사 ( 생략 ) 
`````

27-5 DataInputStream / DataOutputStream
`````
FileInputStream / FileOutputStream 을 개선

byte 단위의 입출력을 개선해서 문자열을 좀 더 편리하게 다룰 수 있다. 

new DataOutputStream(outputStream) 처럼 DataOutputStream에 넣어 사용
`````

27-6 BufferedReader, BufferedWriter
`````
byte 단위의 입출력을 개선해서 문자열을 좀 더 편리하게 다룰 수 있다.
`````


28강 - 네트워킹
-------

28-1 네트워크 데이터 입력 및 출력
`````
네트워크 대상 ( 객체 ) 사이에 입/출력( InputStream, OutputStream )을 이용해서 데이터를 입력하고 출력한다.
`````

28-2 소켓 ( Socket )
``````
네트워크상에서 데이터를 주고받기 위한 장치이다.
``````
28-3 Socket 클래스
`````
서버는 클라이언트를 맞을 준비를 하고 있다가 클라이언트의 요청에 반응한다.
`````
`````java
import java.net.ServerSocket;
import java.net.Socket;

public class Main {
	public static void main(String[] args) {
		ServerSocket serverSocket = null;
		Socket socket = null;
		
		try {
			serverSocket = new ServerSocket(9000);
			System.out.println("클라이언트 맞을 준비 완료!!");
			
			socket = serverSocket.accept(); 
			System.out.println("클라이언트 연결!!");
			
			System.out.println("socket : " + socket);
			
		}catch( Exception e) { // 네트워크와 관련된 것은 99퍼 예외처리를 해줘야한다고함
			e.printStackTrace();  
		}finally {
			try {
				// 자원 반납
				if(socket != null) socket.close();
				if(serverSocket != null) serverSocket.close();				
			}catch(Exception e) {
				e.printStackTrace();				
			}
		}
	}
}

// 결과

클라이언트 맞을 준비 완료!!
클라이언트 연결!!
socket : Socket[addr=/0:0:0:0:0:0:0:1,port=3579,localport=9000]
`````

28-4 Client와 Server 소켓 ( Socket )
`````
서버에서 ServerSocket을 준비하고 클라이언트에서 Socket을 이용해서 접속한다.
`````
`````java
// 서버

import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

public class MainClassServerSocket {

	public static void main(String[] args) {
		
		ServerSocket serverSocket = null;
		Socket socket = null;
		
		try {
			serverSocket = new ServerSocket(9000);
			System.out.println("클라이언트 맞을 준비 완료~~");
			
			socket = serverSocket.accept();
			System.out.println("클라이언트 연결~~");
			System.out.println("socket: " + socket);
			
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if(socket != null) socket.close();
				if(serverSocket != null) serverSocket.close();
			} catch (IOException e) {
				e.printStackTrace();
			}			
		}		
	}	
}


// 클라이언트 

import java.io.IOException;
import java.net.Socket;

public class MainClassSocket {

	public static void main(String[] args) {
		
		Socket socket = null;
		
		try {
			socket = new Socket("localhost", 9000);	//127.0.0.1
			System.out.println("서버 연결~~");
			System.out.println("socket: " + socket);
			
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if(socket != null) socket.close();
			} catch (IOException e) {
				e.printStackTrace();
			}			
		}		
	}
	
}
`````

28-5 양방향 통신
`````
클라이언트와 서버는 Socket, ServerSocket, InputStream, OutputStream을 이용해서 양방향 통신을 할 수 있다. (수업예제 lec28Pjt002)
`````




##### 강의를 무료로 풀어주신 인프런께 감사드립니다.
##### https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94_java-renew/


