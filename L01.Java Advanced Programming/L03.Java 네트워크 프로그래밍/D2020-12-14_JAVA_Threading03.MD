### Threading



#### ThreadEx03


#### 이런 방법으로 thread를 객체 생성도 가능

``` java
		Thread thread3 = new Thread(new UpperCaseAlphabetRunnableImpl());
```

#### thread 객체 실행

``` java
		thread3.start();
```


#### ThreadEx03 / 전체 코드

``` java
public class ThreadEx03 {
	public static void main(String[] args) {

		Thread thread1 = new DigitThread();
		Thread thread2 = new DigitThread();
		Thread thread3 = new Thread(new UpperCaseAlphabetRunnableImpl());
		
		thread1.start();
		thread2.start();
		thread3.start();

	}
}

```


``` java
public class UpperCaseAlphabet {

	public void print(){
	
	for(char c = 'A'; c <= 'Z'; c++) {
		System.out.print(c);
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	}
}


```

``` java
public class UpperCaseAlphabetRunnableImpl extends UpperCaseAlphabet implements Runnable {

	public void run() {
		print();
	}

}

```
