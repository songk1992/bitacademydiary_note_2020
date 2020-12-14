

### Threading



#### ThreadEx01


#### thread 객체 생성

``` java
Thread thread = new DigitThread();
```

#### thread 객체 실행

``` java
thread.start();
```


#### ThreadEx01 / 전체 코드

``` java
public class ThreadEx01 {

	public static void main(String[] args) {
//		for(int i = 0; i <=10; i++) {
//			System.out.print(i);
//		}
		
		Thread thread = new DigitThread();
		thread.start();
		
		for(char c = 'a'; c <= 'z'; c++) {
			System.out.print(c);
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
