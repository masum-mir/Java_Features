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

Runnable runnable = () -> System.out.println("Hello world two!");

You also got method references, repeating annotations, default methods for interfaces and a few other language features.

### Collections & Streams:

List<String> list = Arrays.asList("franz", "ferdinand", "fiel", "vom", "pferd");

With the Streams API, you can do the following:

list.stream()
    .filter(name -> name.startsWith("f"))
    .map(String::toUpperCase)
    .sorted()
    .forEach(System.out::println);
