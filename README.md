# Java-8
In this tutorial, we will look into Java 8 features with examples.

```
public class IntStream_1 {
	public static void main(String[] args) {
   	        System.out.println(isPrime(1));
		System.out.println(isPrime(2));
		System.out.println(isPrime(3));
		System.out.println(isPrime(4));
 }
    
    private static boolean isPrime(int number) {
		/**
		 * Java-7
		 */
		for (int i = 2; i < number; i++) {
			if (number % i == 0)
				return false;
		}
		return number > 1;
	}
  
	/*  private static boolean isPrime(int number) {
		/**
		 * Java-8
		 */
		return number > 1 && IntStream.range(2, number).noneMatch(i -> number % i == 0);
		}*/
}
```
