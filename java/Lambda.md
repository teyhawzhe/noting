# 1. 主要4種
---
1. Consumer<T\>
	1. Consumer就是x使用後不需要return
	2. (x) -> {  System.out.println(x);  };
2. Supplier<T\>
	1. Supplier就是不需要給予任何參數，就會return一個參數
	2. () -> {  return  Math.PI; }; 
3. Function<T, R\>
	1. Function就是提供一個參數，將其處理後return。
	2. (x) -> {  return x+1; };
4. Predicate<T\>
	1. Predicate就是驗證一個參數，在將結果return
	2. (x) -> {  return x==1; };
 	
---
# 2. 自訂lambda介面-@FunctionalInterface
***注意:***
1. 自訂lambda只能是interface介面
2. interface內只能有一個方法需要進行實做，default方法則不在此限制

## 範例:

		public class DemoApp {

			public static void main(String[] args) {
				Comsumer<String> cosumer1 = (x) ->{ System.out.println(x); };
				Comsumer<Integer> cosumer2 = (x) ->{ System.out.println(x+x); };
				cosumer1.print("自訂 Comsumer");
				cosumer2.print(100);
				cosumer1.print("--------------");
				cosumer1.print("自訂 Supplier");

				Supplier<Double> pi = ()->{ return Math.PI; };
				System.out.println(pi.getResult());
				cosumer1.print("--------------");
				cosumer1.print("自訂 Function");

				Function<String,Integer> total = (x) ->{ return x.length(); };
				System.out.println(total.process("123456")+"字元");

				cosumer1.print("--------------");
				cosumer1.print("自訂 Predicate");
				Predicate<Integer> isOdd = (x) -> { return x%2!=0; };
				System.out.println(" 5 is odd? "+isOdd.test(5));   
			}

		}

		@FunctionalInterface
		interface Comsumer<T>{
			public void print(T t);
		}

		@FunctionalInterface
		interface Supplier<T>{
			public T getResult();
		}

		@FunctionalInterface
		interface Function<T,K>{
			public K process(T t);
		}

		@FunctionalInterface
		interface Predicate<T>{
			public boolean test(T t);
		}


