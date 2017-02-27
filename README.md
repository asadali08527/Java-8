# Java-8
Of course, Java 8 is greatest release in the Java world Since Java 5. Java 8 was released on March 3, 2014. In this tutorial, we will look into Java 8 features with examples.

##Part 1. 
Lambda expressions
##Part 2. 
Functional Interfaces
##Part 3. 
Stream API
##Part 4. 
forEach() method in Iterable interface
##Part 5. 
default and static methods in Interfaces
##Part 6. 
Java Time API
##Part 7. 
Collection API improvements
##Part 8. 
Concurrency API improvements
##Part 9. 
Java IO improvements
##Part 10. 
Miscellaneous Core API improvements


##Part 3. Stream API
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
