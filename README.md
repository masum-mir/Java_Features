# Java_Features


## Java 8: 

  ### Lambdas:
  
> Runnable runnable = new Runnable(){
       @Override
       public void run(){
         System.out.println("Hello world !");
       }
     };
     
With lambdas, the same code looks like this:

> Runnable runnable = () -> System.out.println("Hello world two!");

You also got method references, repeating annotations, default methods for interfaces and a few other language features.

### Collections & Streams:

> List<String> list = Arrays.asList("franz", "ferdinand", "fiel", "vom", "pferd");

With the Streams API, you can do the following:

> list.stream()
    .filter(name -> name.startsWith("f"))
    .map(String::toUpperCase)
    .sorted()
    .forEach(System.out::println);


## Java 9 :

### Collections: 
Collections got a couple of new helper methods, to easily construct Lists, Sets and Maps.

> List<String> list = List.of("one", "two", "three");
> Set<String> set = Set.of("one", "two", "three");
> Map<String, String> map = Map.of("foo", "one", "bar", "two");

### Streams
Streams got a couple of additions, in the form of takeWhile,dropWhile,iterate methods.

> Stream<String> stream = Stream.iterate("", s -> s + "s")
  .takeWhile(s -> s.length() < 10);

### Optionals: 
Optionals got the sorely missed ifPresentOrElse method.

> user.ifPresentOrElse(this::displayAccount, this::displayLogin);
### Interfaces: 
Interfaces got private methods:

> public interface MyInterface {
    private static void myPrivateMethod(){
        System.out.println("Yay, I am private!");
    }
}
