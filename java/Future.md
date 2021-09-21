# Future
---
Future非同步執行，例如現在我在玩遊戲，我用手機打開ubereat訂購餐點<-(這就是非同步，我訂購後不需要執行)，當ubereat在某個時間點送到時，才需要去拿取餐點(只需要在特定的時間內取回結果)。

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.TimeUnit;

public class FutureDemo {

	public static void main(String[] args) throws Exception {
		// 建立執行序管理池
		ExecutorService service = Executors.newSingleThreadExecutor();

		// submit 支援 Callable 與 Runnable
		Future<String> alpha = service.submit(upperCase("abc"));

		System.out.println("我要變大寫");

		// 5秒後結果執行結束
		// get裡面的是等待執行的時間6是數字，TimeUnit是時間單位
		System.out.println(alpha.get(6, TimeUnit.SECONDS));

		System.out.println("我要變小寫");

		alpha = (Future<String>) service.submit(lowerCase(alpha.get()));
		alpha.get();

		// 關閉管理池
		service.shutdown();
	}

	// Callable
	public static Callable<String> upperCase(String n) {
		return () -> {
			System.out.println("upperCase");
			// 休眠5秒
			TimeUnit.SECONDS.sleep(5);
			return n.toUpperCase();
		};
	}

	// Runnable
	public static Runnable lowerCase(String n) {
		return () -> {
			System.out.println("lowerCase");
			System.out.println(n.toLowerCase());
		};
	}

}
```
```
out put:
我要變大寫
upperCase
ABC
我要變小寫
lowerCase
abc

```
