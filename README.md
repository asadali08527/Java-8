# Java-8
	Of course, Java 8 is greatest release in the Java world Since Java 5(released in 2004). Java 8 was released on March 3, 2014. In this tutorial, we will look into Java 8 features with examples. In this tutorial we will try to notice the differences by executing examples with java 8 and java 7.

## Part 1. 
	Lambda expressions & Functional Interfaces
## Part 2. 
	Stream API
## Part 3. 
	forEach() method in Iterable interface
## Part 4. 
	default and static methods in Interfaces
## Part 5. 
	Java Time API
## Part 6. 
	Collection API improvements
## Part 7. 
	Concurrency API improvements
## Part 8. 
	Java IO improvements
## Part 9. 
	Miscellaneous Core API improvements

###Lambda expressions & Functional Interfaces
	Before discussing Lambda expressions, let's first discuss something about Functional Interfaces in java 8.
#### Functional Interfaces
	+ FunctionalInterface is a new concept introduced in Java 8.
	+ An interface with exactly one abstract method is called as Functional Interface.
	+ @FunctionalInterface annotation is used to mark an interface as funtional interface.
	+ However the annotation @FunctionalInterface is optional,and it doesn’t do anything special to interface except a requirement 			check. just to avoid accidental addition of abstract methods in the functional interfaces we use this annotation, we can 		 think it like @Override annotation.
	+ Use of @FunctionalInterface annotation is not mandatory but it's best practice to use.
	+ java.lang.Runnable with single abstract method run() is a best example of functional interface.
#### Lambda expressions
	+ Lambda expressions (actually i call this as a lambda function or statements instead of  lambda expression because the expression part is substitutable) is a statement where function can be passed around either through argument or return value,because functions become objects.
	+ Java is a statically and strongly typed language. So, functions must have a type, in this case it’s an interface.
	+ In short lambda functions are objects that implement the functional interface. 
	+ Let's discuss an example and then we will discuss abount syntax 
##### Note - Lambda expression must have type and that type must have only one abstract method.

+ Before Java 8
```
Runnable r = new Runnable(){  
  public void run(){    
    System.out.println(“Running in another thread”);  
  }
};
```
+ Java 8
```
Runnable r = () -> System.out.println(“Running in another thread”);
```
	

###Part 2. Stream API
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
Tutorials will be updated soon
