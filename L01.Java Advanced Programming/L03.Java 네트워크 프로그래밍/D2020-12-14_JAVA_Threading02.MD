

### Threading



#### ThreadEx02


#### thread를 객체 여러개 생성

``` java
		Thread thread1 = new DigitThread();
		Thread thread2 = new DigitThread();
		Thread thread3 = new AlphabetThread();
```

#### thread 객체 여러개 실행

``` java
		thread1.start();
		thread2.start();
		thread3.start();
```


#### ThreadEx02 / 전체 코드

``` java
public class ThreadEx02 {
	public static void main(String[] args) {

		Thread thread1 = new DigitThread();
		Thread thread2 = new DigitThread();
		Thread thread3 = new AlphabetThread();
		
		thread1.start();
		thread2.start();
		thread3.start();
		
		for(char c = 'a'; c <= 'z'; c++) {
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
public class DigitThread extends Thread {
	@Override
	public void run() {
		for(int i = 0; i <=10; i++) {
			System.out.print(i);
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}			
		}
	}
}
```


``` java
public class AlphabetThread extends Thread{

	@Override
	public void run() {
		for(char c = 'a'; c <= 'z'; c++) {
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
