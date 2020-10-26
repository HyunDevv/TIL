# Network

- http protocol
- TCP/IP protocol

## thread

- 프로세스 : 프로그램을 수행하는 데 필요한 **데이터와 메모리 등의 자원 그리고 쓰레드로 구성** (최소 하나 이상의 쓰레드가 존재하며, 둘 이상의 쓰레드를 가진 프로세스를 '멀티쓰레드 프로세스' 라고 한다)

  - **멀티쓰레드 프로세스**는 여러 쓰레드가 같은 프로세스 내에서 자원을 공유하면서 작업을 하기 때문에 발생할 수 있는 **동기화, 교착상태와 같은 문제**들을 고려해 신중히 프로그래밍해야 한다.

- 쓰레드 : 프로세스의 자원을 이용해서 실제로 작업을 수행하는 것 

  

### 쓰레드 구현 (extends Thread 방법)

```java
package com.thread;

// java는 thread 사용!
class T extends Thread{

	String name;
	
	public T() {}
	public T(String name) {
		this.name = name;
	}
	
	// run 함수를 사용한다
	@Override
	public void run() {
		for(int i=0;i<=100;i++) {
			System.out.println(name+":"+i);
			try {
				Thread.sleep(200);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
	
}


// 메인
public class Test {

	public static void main(String[] args) {
		// 동시에 동작된다!!!!!
		T t1 = new T("T1");
		t1.start();        // T1의 run함수가 실행된다!
		T t2 = new T("T2");
		t2.start();     
	}

}
```

### 쓰레드 구현 (implements Runnable 방법)

```java
package com.thread;

// java는 thread 사용! Runnable에서 implements
class Th implements Runnable{

	String name;
	
	public Th() {}
	public Th(String name) {
		this.name = name;
	}
	
	// run 함수를 사용한다
	@Override
	public void run() {
		for(int i=0;i<=100;i++) {
			System.out.println(name+":"+i);
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
	
}


// 메인
public class Test2 {

	public static void main(String[] args) {
		// 동시에 동작된다!!!!!
		//Runnable일때 쓰레드 만드는 방법 주의!! Thread를 만들고 그 안에 넣는다!
		Thread t1 = new Thread(new Th("T1"));
		t1.start();        // T1의 run함수가 실행된다!
		Thread t2 = new Thread(new Th("T2"));
		t2.start();     
	}

}
```



### 쓰레드의 우선순위

> 우선순위 범위는 1~10이며 숫자가 높을 수록 우선순위가 높다.
>
> 하지만, 멀티코어에서 실행하면 차이가 없다

```java
public class Test {

	public static void main(String[] args) {
		// 동시에 동작된다!!!!!
		T t1 = new T("T1");
		t1.start();        // T1의 run함수가 실행된다!
		t1.setPriority(10); // 높을수록 많은 프로세스를 점유한다
		T t2 = new T("T2");
		t2.start();
		t2.setPriority(1);
	}

}
```



### 데몬 쓰레드

> 일반 쓰레드가 모두 종료되면 데몬 쓰레드는 강제적으로 자동 종료된다.

```java
package com.thread;

class TT extends Thread{

	@Override
	public void run() {
		while(true) {
			System.out.println("Thread ....");
			try {
				Thread.sleep(500);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
	
}


public class Test4 {

	public static void main(String[] args) throws InterruptedException {
		TT tt = new TT();
		tt.setDaemon(true); // 메인 Application(프로세스)이 죽으면 같이 죽는다
		tt.start();
		tt.interrupt();
		Thread.sleep(10000);
		System.out.println("End Application....");
	}

}
```



### join()과 yield()

- join() - 다른 쓰레드의 작업을 기다린다
- yield() - 다른 쓰레드에게 양보한다

```java
th1.join(); //th1이 끝날때 까지 아래 구문 실행을 멈춘다
// th1의run()이 다 끝난 후 아래 실행
System.out.println(th1.getSum()+" "+th2.getSum());
```





### 쓰레드의 동기화(synchronization)

> 같은 정보를 공유할 때 한 쓰레드가 진행중인 작업을 다른 쓰레드가 간섭하지 못하게 막는것



### 쓰레드 제어 예제

```java
package com.sus;

import java.util.Scanner;

class Th extends Thread{

	boolean stop = false;
	boolean sus = false;
	public void setStop(boolean stop) {
		this.stop = stop;
	}
	public void setSus(boolean sus) {
		this.sus = sus;
	}
	
	@Override
	public void run() {
		while(true) {
			if(stop == true) {
				System.out.println("Stop Thread ...");
				break;
			}
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			if(sus != true) {
				System.out.println("Downloading ...");
			}
		}
		System.out.println("End Thread ...");
	}
	
}



public class Test {
	
	public static void main(String[] args) {
	
		Th th = new Th();
		Scanner sc = new Scanner(System.in);
		while(true) {
			System.out.println("Input cmd");
			String cmd = sc.nextLine();
			if(cmd.equals("start")) {
				th.start();
			}else if(cmd.equals("stop")){
				th.setStop(true);
			}else if(cmd.equals("sus")){
				th.setSus(true);
			}else if(cmd.equals("res")){
				th.setSus(false);
			}else if(cmd.equals("q")){
				th.setSus(true);
				break;
			}
		}
		

	}

}

```





## 입출력

- I/O란 Input과 Output의 약자로 입력과 출력, 입출력이라고 한다
- 입출력은 컴퓨터 내부 또는 외부의 장치와 프로그램간의 데이터를 주고받는 것을 말한다.



- 스트림이란 데이터를 운반하는데 사용되는 연결통로이다.
- 스트림은 단방향통신만 가능하기 때문에 입력스트림과 출력스트림 2개가 필요하다.



- BufferedInput/OutputStream - 빠른 처리



### 바이트기반 스트림

```java
package com.io;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;

//바이트기반 스트림인 InputStream와 OutputStream를 사용해보자! (입출력 단위가 1바이트)
public class Test1 {
	
	public static void main(String[] args) {
		String file = "c:\\network\\d01\\src\\text.txt";
		FileInputStream fis = null;
		BufferedInputStream bis = null;
		FileOutputStream fos = null;
		BufferedOutputStream bos = null;
		try {
			fis = new FileInputStream(file);
			bis = new BufferedInputStream(fis); // fis를 넣어서 기능확장, 속도증가
			fos = new FileOutputStream("text2.txt");
			bos = new BufferedOutputStream(fos); // fos를 넣어서 기능확장, 속도증가
			int data = 0;
			// 끝 자리가 아닐때까지
			while((data=fis.read()) != -1) {
				bos.write(data); // 읽어드린걸 저장한다
				System.out.println((char)data);  // 바이트단위로 읽었다
			}
			System.out.println(fis.available());
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			// fis도 같이 close됨!
			if(bis != null) {
				try {
					bis.close();   // ** 꼭 close를 해주어야 한다!!! **
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			// bos도 같이 close됨!
			if(bos != null) {
				try {
					bos.close();   // ** 꼭 close를 해주어야 한다!!! **
				} catch (IOException e) {
					e.printStackTrace();
				}
			}	
		}
	}
	
}
```



### 문자기반 스트림

```java
package com.io;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

//문자기반 스트림인 Reader와 Writer를 사용해보자!
public class Test2 {
	
	public static void main(String[] args) {
		String file = "c:\\network\\d01\\src\\text.txt";
		FileReader fis = null;
		BufferedReader bis = null;
		FileWriter fos = null;
		BufferedWriter bos = null;
		try {
			fis = new FileReader(file);
			bis = new BufferedReader(fis); // fis를 넣어서 기능확장, 속도증가
			fos = new FileWriter("text2.txt");
			bos = new BufferedWriter(fos); // fos를 넣어서 기능확장, 속도증가
			String data = "";
			// 끝 자리가 아닐때까지, readLine()은 BufferedReader에만 있다
			while((data=bis.readLine()) != null) {
				bos.write(data); // 읽어드린걸 저장한다
				System.out.println(data);  // 바이트단위로 읽었다
			}
			//System.out.println(fis.available());
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			// fis도 같이 close됨!
			if(bis != null) {
				try {
					bis.close();   // ** 꼭 close를 해주어야 한다!!! **
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			// bos도 같이 close됨!
			if(bos != null) {
				try {
					bos.close();   // ** 꼭 close를 해주어야 한다!!! **
				} catch (IOException e) {
					e.printStackTrace();
				}
			}	
		}
	
		
	}
}
```



### 객체 입출력 예제

```java
package com.io;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

// 객체를 I/O한다
public class Test3 {

	public static void main(String[] args) {
		User user = new User("id01", "이말숙");
		
		FileOutputStream fos = null;
		BufferedOutputStream bos = null;
		ObjectOutputStream oos = null;
		
		try {
			fos = new FileOutputStream("user.serial");
			bos = new BufferedOutputStream(fos);
			oos = new ObjectOutputStream(bos);
			oos.writeObject(user);
			System.out.println("Write Complete ...");
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} // 확장자명은 상관없다 
		 finally {
			 if(oos != null) {
				 try {
					oos.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			 }
		 }
		
		FileInputStream fis = null;
		BufferedInputStream bis = null;
		ObjectInputStream ois = null;
		
		try {
			fis = new FileInputStream("user.serial");
			bis = new BufferedInputStream(fis);
			ois = new ObjectInputStream(bis);
			User readUser =null;
			readUser = (User)ois.readObject();
			System.out.println(readUser);
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if(ois != null) {
				try {
					ois.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		
		
	} // end main 
	
}
```



