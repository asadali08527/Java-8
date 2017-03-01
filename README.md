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
+ Lambdas (also known as closures) are the biggest and most awaited language change in the whole Java 8 release.
+ Lambda expressions (actually i call this as a lambda function or statements instead of  lambda expression because the expression part is substitutable) is a statement where function can be passed around either through argument or return value,because functions become objects.
+ Java is a statically and strongly typed language. So, functions must have a type, in this case it’s an interface.
+ In short lambda functions are objects that implement the functional interface. 
+ Let's discuss an example by executing using java 7 and java 8 and then we will discuss abount syntax 
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
#### Syntax
	parameter -> expression body
In its simplest form, a lambda could be represented as a comma-separated list of parameters, the –> symbol and the body. 	
##### Note-
+ Optional type declaration − 
No need to declare the type of a parameter. The compiler can inference the same from the value of the parameter.

+ Optional parenthesis around parameter − 
No need to declare a single parameter in parenthesis. For multiple parameters, parentheses are required.

+ Optional curly braces − 
No need to use curly braces in expression body if the body contains a single statement.

+ Optional return keyword − 
The compiler automatically returns the value if the body has a single expression to return the value. Curly braces are required 	to indicate that expression returns a value.

##### Examples
```
+ 	Arrays.asList( "a", "b", "d" ).forEach( e -> System.out.println( e ) );
```
```
Arrays.asList( "a", "b", "d" ).forEach( e -> {
    System.out.print( e );
    System.out.print( e );
	} );
```
Lambdas may return a value. The type of the return value will be inferred by compiler. The return statement is not required if the lambda body is just a one-liner. The two code snippets below are equivalent:

```
+ Arrays.asList( "a", "b", "d" ).sort( ( e1, e2 ) -> e1.compareTo( e2 ) );
```
and

```
Arrays.asList( "a", "b", "d" ).sort( ( e1, e2 ) -> {
    int result = e1.compareTo( e2 );
    return result;
} );
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
