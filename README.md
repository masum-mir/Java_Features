# Java_Features


## Java 8: 

  ### Lambdas:
```  
 Runnable runnable = new Runnable(){
       @Override
       public void run(){
         System.out.println("Hello world !");
       }
     };
   ```  
With lambdas, the same code looks like this:

> Runnable runnable = () -> System.out.println("Hello world two!");

You also got method references, repeating annotations, default methods for interfaces and a few other language features.

### Collections & Streams:

> List<String> list = Arrays.asList("franz", "ferdinand", "fiel", "vom", "pferd");

With the Streams API, you can do the following:
```
 list.stream()
    .filter(name -> name.startsWith("f"))
    .map(String::toUpperCase)
    .sorted()
    .forEach(System.out::println);
```

## Java 9 :

### Collections: 
Collections got a couple of new helper methods, to easily construct Lists, Sets and Maps.

> List<String> list = List.of("one", "two", "three");
> Set<String> set = Set.of("one", "two", "three");
> Map<String, String> map = Map.of("foo", "one", "bar", "two");

### Streams
Streams got a couple of additions, in the form of takeWhile,dropWhile,iterate methods.
```
 Stream<String> stream = Stream.iterate("", s -> s + "s")
  .takeWhile(s -> s.length() < 10);
```
### Optionals: 
Optionals got the sorely missed ifPresentOrElse method.

> user.ifPresentOrElse(this::displayAccount, this::displayLogin);

### Interfaces: 
Interfaces got private methods:
```
 public interface MyInterface {
    private static void myPrivateMethod(){
        System.out.println("Yay, I am private!");
    }
 }
```
 ## Java 10:
There have been a few changes to Java 10, like Garbage Collection etc. But the only real change you as a developer will likely see is the introduction of the "var"-keyword, also called local-variable type inference.

Local-Variable Type Inference: var-keyword
// Pre-Java 10

> String myName = "Marco";

// With Java 10

> var myName = "Marco"

## Java 14:

Switch Expression (Standard)
```
 int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    default      -> {
      String s = day.toString();
      int result = s.length();
      yield result;
    }
};
```
## Java 15:
### Text-Blocks / Multiline Strings: 
```
 String text = """
                Lorem ipsum dolor sit amet, consectetur adipiscing \
                elit, sed do eiusmod tempor incididunt ut labore \
                et dolore magna aliqua.\
                """;
```
## Java 16:

Pattern Matching for instanceof:
```
 if (obj instanceof String) {
    String s = (String) obj;
    // e.g. s.substring(1)
}
```
You can now do this:
```
 if (obj instanceof String s) {
    // Let pattern matching do the work!
    // ... s.substring(1)
}
```
## Java 17:

Sealed classes and interfaces restrict which classes or interfaces can extend or implement them. 

1) Sealed classes are declared using sealed modifier and permits clause. permits clause specifies the sub classes which can extend the current sealed class.
```
 package Java17Concepts;
 
 sealed class SuperClass permits SubClassOne, SubClassTwo
{
    //Sealed Super Class
}
 
 final class SubClassOne extends SuperClass
{
    //Final Sub Class
}
 
 final class SubClassTwo extends SuperClass
{
    //Final Sub Class
}

 package Java17Concepts;
 
 sealed class SuperClass permits SubClassOne, SubClassTwo
{
    //Sealed Super Class
}
 
 final class SubClassOne extends SuperClass
{
    //Final Sub Class
}
 
 final class SubClassTwo extends SuperClass
{
    //Final Sub Class
}
```
2) Permitted sub classes must be in the same package or in the same module as that of a sealed super class.

3) Permitted sub classes must be either final or sealed or non-sealed. If you don’t declare permitted sub classes with any one of these modifiers, you will get compile time error.
```
 package Java17Concepts;
 
 sealed class SuperClass permits SubClassOne, SubClassTwo, SubClassThree
{
    //Sealed Super Class
}
 
 final class SubClassOne extends SuperClass
{
    //Final Sub Class
}
 
 sealed class SubClassTwo extends SuperClass permits AnotherSubClass
{
    //Sealed Sub Class permitting another sub class to extend it further
}
 
 non-sealed class SubClassThree extends SuperClass
{
    //non-sealed sub class
}
 
 final class AnotherSubClass extends SubClassTwo
{
    //Final sub class of SubClassTwo
}
 package Java17Concepts;
 
 sealed class SuperClass permits SubClassOne, SubClassTwo, SubClassThree
{
    //Sealed Super Class
}
 
 final class SubClassOne extends SuperClass
{
    //Final Sub Class
}

 sealed class SubClassTwo extends SuperClass permits AnotherSubClass
{
    //Sealed Sub Class permitting another sub class to extend it further
}
 
 non-sealed class SubClassThree extends SuperClass
{
    //non-sealed sub class
}
 
 final class AnotherSubClass extends SubClassTwo
{
    //Final sub class of SubClassTwo
}
```
4) final permitted sub classes can not be extended further, sealed permitted sub classes are extended further by only permitted sub classes and non-sealed permitted sub classes can be extended by anyone.

5) Sealed class must and should specify its permitted sub classes using permits clause otherwise there will be a compilation error.
```
 sealed class AnyClass 
{
    //Compile Time Error : Sealed class must specify permitted sub classes
}
```
6) Permitted sub classes must and should extend their sealed super class directly.
```
package Java17Concepts;
 
 sealed class SuperClass permits SubClassOne, SubClassTwo
{
    //Sealed Super Class
}
 
 final class SubClassOne 
{
    //Compile Time Error : It must extend SuperClass
}
 
 non-sealed class SubClassTwo 
{
    //Compile Time Error : It must extend SuperClass
}
```
7) In the same way, you can also declare sealed interfaces with permitted sub interfaces or sub classes.
```
 package Java17Concepts;
 
 sealed interface SealedInterface permits SubInterface, SubClass
{
    //Sealed Super Interface
}
 
 non-sealed interface SubInterface extends SealedInterface
{
    //Non-sealed Sub Interface
}
 
 non-sealed class SubClass implements SealedInterface
{
    //Non-sealed sub class
}
```
8) Permitted sub interfaces must be either sealed or non-sealed but not final.
```
 package Java17Concepts;
 
 sealed interface SealedInterface permits SubInterfaceOne, SubInterfaceTwo, SubInterfaceThree
{
    //Sealed Super Interface
}
 
 sealed interface SubInterfaceOne extends SealedInterface permits SubClass
{
    //Sealed Sub Interface
}
 
 non-sealed class SubClass implements SubInterfaceOne
{
    //non-sealed sub class implementing SubInterfaceOne
}
 
 non-sealed interface SubInterfaceTwo extends SealedInterface
{
    //Non-sealed Sub Interface
}
 
 final interface SubInterfaceThree extends SealedInterface
{
    //Compile time Error : Permitted sub interface must not be final
}
```
9) Permitted sub types must have name. Hence, anonymous inner classes or local inner classes can’t be permitted sub types.

10) A sealed super class can be abstract, and permitted sub classes can also be abstract provided they can be either sealed or non-sealed but not final.

```
 package Java17Concepts;
 
 abstract sealed class SuperClass permits SubClassOne, SubClassTwo, SubClassThree
{
    //Super class can be abstract and Sealed
}
 
 abstract final class SubClassOne extends SuperClass
{
    //Compile Time Error : Sub class can't be final and abstract
}
 
 abstract non-sealed class SubClassTwo extends SuperClass
{
    //Sub class can be abstract and Non-sealed
}
 
 abstract sealed class SubClassThree extends SuperClass permits AnotherSubClass
{
    //Sub class can be abstract and Sealed
}
 
 final class AnotherSubClass extends SubClassThree
{
    //Final sub class of SubClassThree
}
```
11) While declaring sealed classes and sealed interfaces, permits clause must be used after extends and implements clause.

12) With the introduction of sealed classes, two more methods are added to java.lang.Class (Reflection API). They are getPermittedSubclasses() and isSealed().
