# Java-8
Of course, Java-8 is greatest release within the Java world, since Java-5(released in 2004). Java-8 was released on 3rd March, 2014. During this tutorial, we are going to look into Java-8 features with examples. In this tutorial we are going to try and notice the variations by executing java code examples with Java-8 and Java-7.

## Part 1. 
Lambda expressions & Functional Interfaces
## Part 2. 
Stream API
## Part 3. 
forEach() method in Iterable interface
## Part 4. 
default and static methods in Interfaces
## Part 5. 
Java Time API(Joda time API)
## Part 6. 
Collection API improvements
## Part 7. 
Concurrency API improvements
## Part 8. 
Java IO improvements
## Part 9. 
Miscellaneous Core API improvements
## Part 10.
- Some of the important predefined functional interfaces
    - Functions
    - Predicates
    - Supplier
    - Consumer

### Lambda expressions & Functional Interfaces
	Before discussing Lambda expressions, let's first discuss something about Functional Interfaces in java 8.
#### Functional Interfaces
+ Functional Interface is a new concept introduced in Java 8.
+ An interface with exactly one abstract method is called as Functional Interface.
+ @FunctionalInterface annotation is used to mark an interface as funtional interface.
+ However the annotation @FunctionalInterface is optional,and it doesn’t do anything special to interface except a requirement 			check. just to avoid accidental addition of abstract methods in the functional interfaces we use this annotation, we can 		 think it like @Override annotation.
+ Use of @FunctionalInterface annotation is not mandatory but it's best practice to use just because if someone adds just one another method to the interface definition, it will not be functional anymore and compilation process will fail. To overcome this fragility and explicitly declare the intent of the interface as being functional.
+ java.lang.Runnable with single abstract method run() is a best example of functional interface. java.util.concurrent.Callable could be another great example of functional interface.
+ all existing interfaces in Java library have been annotated with @FunctionalInterface as well.

##### Example
```
@FunctionalInterface
public interface Functional {
    void abstractMethod();
}
```
One thing to keep in mind: default and static methods do not break the functional interface contract and may be declared:
```
@FunctionalInterface
public interface FunctionalDefaultMethods {
    void abstractMethod();
    default void defaultMethod() {  
    /*
    ...........
    method body
    */
    }       
}

```
#### Lambda expressions
+ Lambda (also  referred to as closures) is the biggest and most hoped language modification within the whole Java-8 release.
+ Lambda expressions (actually i call this as a lambda function or statements instead of lambda expression because the expression part is substitutable) is a statement where function can be passed around either through argument or return value,because functions become objects.
+ Java is a statically and strongly typed language. So, functions must have a type, in this case it’s an interface.
+ In short lambda functions are objects that implement the functional interface. 
+ Let's discuss an example by executing using java 7 and java 8 and then we will discuss abount syntax.

##### Note - Lambda expression must have type and that type must have only one abstract method.
```
	// Before Java 8
	Runnable r = new Runnable(){  
  	public void run(){    
   	 System.out.println(“Running in another thread”);  
 	 }
	};

	// Since Java 8
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
		Arrays.asList( "a", "b", "d" ).forEach( e -> System.out.println( e ) );
```
is similar to
```
Arrays.asList( "a", "b", "d" ).forEach( e -> {
    System.out.print( e );
	} );
```
Lambdas may return a value. The type of the return value will be inferred by compiler. The return statement is not required if the lambda body is just a one-liner. The two code snippets below are equivalent:

```
		Arrays.asList( "a", "b", "d" ).sort( ( e1, e2 ) -> e1.compareTo( e2 ) );
```
and
```
Arrays.asList( "a", "b", "d" ).sort( ( e1, e2 ) -> {
    int result = e1.compareTo( e2 );
    return result;
} );
```
##### Variables inside Lambda expressions.
let's have a look on below code snippet
```
interface Evaluate{
    public void method1();
}
class Person{
    int maxAge=100;                     // instance variable of class Person
    public void method2(){
        int age=30;                     // local variable of method 2
        Evaluate e=()->{                // lambda expression
            System.out.println(maxAge);
            System.out.println(age);
        };
        e.method1();
    }
    	public static void main(String[] args) {
    	    Person person=new Person();
    	    person.method2();           //output 100  and 30
    	}
}
```
Executing above code returns the ouput `100` and `30` without any error, which means from Lambda expression we can access enclosing class variables(`maxAge`) and enclosing method variables(`age`). 
So far so good,, but let's have a look on below code snippet where we are trying to mutate the value of class variable and method variable inside Lambda expresions.
```
interface Evaluate{
    public void method1();
}
class Person{
    int maxAge=100;                     
    public void method2(){
        int age=30;                     
        Evaluate e=()->{                
            maxAge=65;                  // Works perfectly without any error
            age= 20;                    // compile time error
            System.out.println(maxAge);
            System.out.println(age);
        };
        e.method1();
    }
    	public static void main(String[] args) {
    	    Person person=new Person();
    	    person.method2();           
    	}
}
```
Exceuting above code will result in compile time error saying 
> local variable referenced from lambda expression must be final, or effectively final

this is because, a local variable referenced from Lmabda expressions are always final in nature, irrespective of declaration. Here `age` is a local variable which is being referenced from Lambda expression is by default final.

> Note- A local variable not being referenced from Lambda expressions are not final, but if it is being referenced from Lambda expressions is by effectively final.
#### Lambda expressions and it's advantage
  - Through Lambda expressions we can enable functional programming in Java.
  - Readability could be improved by reducing code length through Lambda expressions.
  - Complexity of Anonymous class could be resolved upto some extent.
  - We can pass functions/procedures as an arguments.
  - Functions and procedure can also be treated as a value.
  - Parallel procesing could easily be achieved through Lambda expressions.


# Anonymous inner class Vs Lambda expressions

| Anonymous Inner Class                      | Lambda Expressions              |
| ----------------------------               | --------------------------   |
| Class without name                         | Function without name |
| It can extend abstract as well as concrete class| It can't extend abstract or  concrete class |
| It can implements an interface that contains any number of abstract methods                               | It can implements an interface that contains only one abstract methods(functional interface)  |
| It can be instantiated(object can be craeted)                                    |It can't be instantiated (object creation is not possile)   |
| Inside Anonymous Inner class we can declare instance variable                                     | We can't declare instance variable, whatever variable is declared are considered as local variable |
| Inside Anonymous Inner class `this` always referes to current anonymous class object but not outer class object.                        |`this` always referes to current outer class object i.e., enclosing object.      |
Good to use if we want to handle multiple methods.|Good to use if we want to handle interface with single abstract methods(functional interface).|
|At the time of compilation a separate class file will be generated.|No separate class file will be generated.|
|Memory will be generated on demand whenever we are creating objects| Lambda expresion resides in permanent memory of JVM(method area)


### Part 2. Stream API

Stream allows us to process objects from collections. In java 8, `Stream` is an interface present under `java.util.stream` package.
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
Now we will discuss various methods available under stream API.
### filter()
```
//Find out even number from the below list in a separate list.
List<Integer> list=new ArrayList<Integer>();
list.add(5);
list.add(10);
list.add(15);
list.add(20);
//Before Java 8
List<Integer> evenList=new ArrayList<Integer>();
for(Integer number:list){
    if(number%2==0)
      evenList.add(number);
}
System.out.println(evenList); // output 10,20
//After Java 8
List<Integer> evenList=list.stream().filter(f->f%2==0).collect(Collectors.toList());
```
### map()
```
//Add some grace marks to below list of marks.
List<Integer> marks=new ArrayList<Integer>();
marks.add(35);
marks.add(40);
marks.add(45);
marks.add(50);

//Before Java 8
List<Integer> markWithGrace=new ArrayList<Integer>();
for(Integer number:list){
      markWithGrace.add(number+5);
}
System.out.println(evenList); // output 40,45,50,55

//After Java 8
List<Integer> markWithGrace=list.stream().map(f->f+5).collect(Collectors.toList());
// output 40,45,50,55
```
> Note- filter() method always takes `predicate` as an argument where as map() method takes `function` as an argument.
`Predicate` is always a boolean valued function, its return type is always boolean. where as 'Function' is non boolean valued function, it's return type could be of any type other than boolean.

### count()
```
//Count marks having score of less than 45.
List<Integer> marks=new ArrayList<Integer>();
marks.add(35);
marks.add(40);
marks.add(45);
marks.add(50);
long marksLessThan45=marks.stream().filter(f->f<45).count();
//output 2
```
> return type of `count()` method is always `long`. It used to count the number of objects presents inside a collection.

### sorted()
```
//Sort the list of marks in natural sorting order.
List<Integer> marks=new ArrayList<Integer>();
marks.add(55);
marks.add(60);
marks.add(45);
marks.add(50);
List<Integer> sortedMarks=marks.stream().sorted().collect(Collectors.toList());
//output 45, 50, 55,60
OR
List<Integer> sortedMarks=marks.stream().sorted((o1,o2)->o1.compareTo(o2)).collect(Collectors.toList());
//output 60,55,50,45
```
> if you want to achieve descending sorting order, use custom comparator under lambda function, as shown below
```
List<Integer> sortedMarks=marks.stream().sorted((o1,o2)->(o1<o2)?1:(o1>o2)?-1:0).collect(Collectors.toList());
//output 60,55,50,45
```
OR
```
List<Integer> sortedMarks=marks.stream().sorted((o1,o2)->o2.compareTo(o1)).collect(Collectors.toList());
//output 60,55,50,45
```
OR
```
List<Integer> sortedMarks=marks.stream().sorted((o1,o2)->-o1.compareTo(o2)).collect(Collectors.toList());
//output 60,55,50,45
```
Sorting String elements under collections
```
//Sort the list of String in natural sorting order.
List<String> person=new ArrayList<String>();
person.add("Asad");
person.add("Ali");
person.add("James");
person.add("Bond");
List<String> sortedPerson=person.stream().sorted().collect(Collectors.toList());
//output Ali, Asad, Bond,James
OR
List<String> sortedMarks=marks.stream().sorted((o1,o2)->-o1.compareTo(o2)).collect(Collectors.toList());
//output James,Bond,Ali,Asad
```
Sorting String elements under collections based on length of String
```
//Sort the list of marks in natural sorting order.
List<String> person=new ArrayList<String>();
person.add("Asad Hussain");//12
person.add("Ali Abbas");//9
person.add("James Bond");//10
person.add("Bond Michel");//11
Comparator<String> c=(s1,s2)->{
    int l1=s1.length();
    int l2=s2.length();
    if(l1<l2) return -1;
    else if(l1>l2) return +1;
    else return s1.compareTo(s2);
}
List<String> sortedPerson=person.stream().sorted(c).collect(Collectors.toList());
//output Ali Abbas, James Bond, Bond Michel,Asad Hussain
```
### min() and max()
min and max object among a list is always comes under context of sorting.
Consider an array, `[5,3,10,15,4]` if we want to find min and max element then first it needs to be sorted. If the above array is sorted in ascending order then it will look like `[3,4,5,10,15]`, so `min` element would be `3` and `max` element would be `15`, but if this array is sored in descending order then it will look like `[15,10,5,4,3]` so here min element would be `15` and max element would be `3`.

> Note- In a sorted list `min` element always refer to first element in the list(pointed to 0th index), whereas `max` element refers to last element of the list.
```
//Find min and max element in the list.
List<Integer> marks=new ArrayList<Integer>();
marks.add(55);
marks.add(60);
marks.add(45);
marks.add(50);
Integer minElementt=marks.stream().min((o1,o2)->o1.compareTo(o2)).get();
//output 45
OR
Integer maxElementt=marks.stream().max((o1,o2)->o1.compareTo(o2)).get();
//output 60
```
> Note- `min` and `max`  method always takes comparator as an arguments

### forEach()
```
//Print each element in the list.
List<Integer> marks=new ArrayList<Integer>();
marks.add(55);
marks.add(60);
marks.add(45);
marks.add(50);
marks.stream().forEach(System.out::print);
//output 55 60 45 50
OR
Consumer<Integer> c=i->{
    System.out.println("You marks is "+ i);
};
marks.stream().forEach(c);
//output
You marks is 55
You marks is 60
You marks is 45
You marks is 50
```
forEach method is responsible to loop through each element available in the list. Here Consumer is a predefined functional interface which is an argument to forEach method. Above code could also be written in a single statement as follows.
```
marks.stream().forEach(i->{
    System.out.println("You marks is "+ i);
});
```
### toArray()
It convert stream of object into an array.
```
//convert stream of object into an array
List<Integer> marks=new ArrayList<Integer>();
marks.add(55);
marks.add(60);
marks.add(45);
marks.add(50);
Integer i[]=marks.stream().toArray(Integer[]::new);
Stream.of(i).forEach(System.out::println);// print each element inside array
```
`Integer[]::new` is called as constructor reference, which returns a new object of an array of Integer type.

Tutorials will be updated soon
