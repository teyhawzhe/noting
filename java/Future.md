# Future
---
Future非同步執行，例如現在我在玩遊戲，我用手機打開ubereat訂購餐點<-(這就是非同步，我訂購後不需要執行)，當ubereat在某個時間點送到時，才需要去拿取餐點(只需要在特定的時間內取回結果)。

	import java.util.concurrent.ExecutionException;
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	import java.util.concurrent.Future;

	public class FutureDemo {

		public static void main(String[] args) throws InterruptedException, ExecutionException {
			// 建立執行序管理池
			ExecutorService service = Executors.newCachedThreadPool();
			Future<String> hello = asyncDo(service, "hello");
			
			// 取出非同步結果 thread等到hello執行完畢
			String returnHello = hello.get();
			
			System.out.println(returnHello);

			hello = asyncDo(service, "hello1");
		
			String returnHello1 = hello.get();
			
			System.out.println(returnHello1);
			// 關閉管理池
			service.shutdown();
		}

		// return 一個非同步方法 
		public static Future<String> asyncDo(ExecutorService service, String x) {
			return service.submit(() -> {
				return x + " == " + x;
			});
		}

	}

input:
hello == hello
hello1 == hello1
