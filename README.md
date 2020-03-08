# JavaBasic-2
Inflearn - JavaProgramming Basic Course (renew ver.) 21강 인터페이스~

[21강 - 인터페이스](#21강---인터페이스)
[22강 - 추상클래스](#22강---추상클래스--Abstract-Class) 
[23강 - 람다식](#23강---람다식)

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
