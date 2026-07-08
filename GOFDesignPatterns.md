# Design Pattern:
		A General Reusable solution to common occurring problems.
						OR
		A template for how to solve a problem  that can use in many different place.

# Advantages of Design Pattern:-
	
		1. A Design Pattern are *well- proved Solution for solving a specific problem.*
		2. The benefits lies in Reuability and extensibility of already developed applications.
		3. DP uses Object-Oriented concepts like decomposition, inheritence, polymorphism.
		
# Diadvantages of Design Pattern:
			
		1. DP do no lead to direct code reuse.
		2. Design Patterns are deceptively(illusive) simple.

###Classification:-

	- Creational: Deals with the creation of an object
	- Sructural: Deals with the class structure such as Inheritance and Composition.
	- Behavioral: Provides solution for the better interaction between objects, also how to provide **lose coupling**, and **flexibility to extend easily** in future.		
	
## Types of Design Pattern:-
	1. Creational design Pattern - (5)
		- Singleton DP
		- Builder DP
		- Factory DP
		- Abstract Factory DP
		- Prototype DP - less used
	
	2.	Structural Design Pattern- (7)
		- Adapter DP
		- Decorator DP
		- Proxy DP
		- Bridge DP
		- Composite DP
		- Facade DP
		- Flyweight DP
		
	3. Behavioral DP - (11)
		- Strategy DP
		- Observer DP
		- Chain of Responsibility DP
		- Command DP
		- Iterator DP
		
# Why we need different Creational DP?
	| Pattern          | Main Purpose                           | When to Use                      | Real Example                                            |
	| ---------------- | -------------------------------------- | -------------------------------- | ------------------------------------------------------- |
	| Singleton        | Only one object                        | Shared resource                  | Logger, Cache, Spring Singleton                         |
	| Factory Method   | Hide object creation                   | Choose implementation at runtime | Spring `getBean()`, parsers, payment gateways           |
	| Abstract Factory | Create related object families         | Multiple compatible products     | Windows vs Mac UI, AWS vs Azure services                |
	| Builder          | Construct complex objects step by step | Many optional fields             | Lombok `@Builder`, HTTP requests, configuration objects |
	| Prototype        | Copy existing objects                  | Expensive object creation        | Clone documents, game characters, templates             |

		
# Creational Design Pattern
</br>
## Singleton- 
	Singleton Pattern says that just "define a class that has only one instance and provides a global point of access to it"

	Versions of Singleton:
	1. Eager Initialization
	2. Lazy  Initialization
	3. Lazy Initialization with private constructor and synchronized method
	4. Enum Singleton - The prefer way.
	[Ref](https://github.com/girirajvyas/gof-design-patterns#1-singleton-pattern-gem)
	
	Advantage of Singleton design pattern:
	1. Saves memory because object is not created at each request. Only single instance is reused again and again.
	2. Instantiation overhead is avoided
	3. Flexibility: Since the class controls the instantiation process, the class has the flexibility to change the instantiation process.
	
	Disadvantages:
	1. Singletons hinder unit testing - A Singleton might cause issues for writing testable code if the object and the methods associated with it are so tightly coupled that it becomes impossible to test without writing a fully-functional class dedicated to the Singleton.
	2. They inherently cause code to be tightly coupled. 
	
	Real time usages:
	Typically singletons are used for global configuration. The simplest example would be LogManager - there's a static **LogManager.getLogManager()** method, and a single global instance is used.
	Other examples:- java.lang.Runtime, java.awt.Desktop.
	
	Project example:- 
	
## Builder Pattern-
	
	**Seperate the construction of complex objects from its representation so that the same construction process can create different representation.**

	example from java-
	java.lang.StringBuilder#append() (unsynchronized)
	java.lang.StringBuffer#append() (synchronized)

	append() method is present in abstract class AbstractStringBuilder, and being used in StringBuilder and StringBuffer and creates 2 diff representations.

	Real world example - Two Different version of a burger. One is veggie burger another one is classic cheese burger.
	Representation - how our product looks at the end when it is ready. For instance first there is a bread, then patty on top it followed by some veggies, then some sauces and at the end finished off with final layer of bread.
	Construction- For example baking a bread, making burger patty, making different sauces, cutting of vegetables etc.

	Project example:
	So in our project, there is a abstract class called AbstractOnlineRemoteService which defined the basic fuctionality for Online Remote.
	Now according to acuirer requirements, each acquirer override some method to provide their own representation.


```java
eg:- 
Class Phone{
String processor;
int battery;
String OS;
	
//Parameterized Cons here
}

class PhoneBuilder{
	private Stirng processor;
	int battery;
	String OS;
	
	public setProcessor(Stirng p){
	processor = p;
	} //Similary for all other feilds.
	
	public Phone getPhone(){
	return new Phone(processor, battery, OS);
	}
	
class shop
{
Phone P = new PhoneBuilder().setProcessor("Andrioid").setOS("ABC").getPhone();

```
#### Another Real time example:
	- Problem:- Desing a ClaimsCalculator :
	- Step 1 : Create a immutable class ClaimsCalculator like this -:
```java
public Class ClaimsCalculator{
	private final String claimsId;
	private final String customerId;
	private final String amount;
	 
	 // Create Getters for all the feilds.
	 
	 // create static class claimsBuilder
	 public static class claimsBuilder{
	 	
		private final String claimsId;
		private final String customerId;
		private final String amount;
		
		/**
		 * This is default constructor, Add any fields in the constructor, that you want
		 * to enforce as mandatory
		 */
		public claimsBuilder() {

		}
		
		public claimsBuilder claimsId(String claimsId) {
			this.claimsId = claimsId;
			return this;
		}
		
		public claimsBuilder customerId(String customerId) {
			this.customerId = customerId;
			return this;
		}
		
		public claimsBuilder amount(String amount) {
			this.amount = amount;
			return this;
		}
		
		public claimsCalculator build(){
			return new claimsCalculator(this);
		}
	 }
	 
	 //Crete Constructor of ClaimsCalculator
	 
	 private claimsCalculator(claimsBuilder builder){
	 	this.claimsId = builder.claimsId;
		this.customerId = builder.customerId;
		this.amount = builder.amount;
	 }
}
``` 	
	- Step 2: Create Implemetation class:
```java
	public class claimTest{
		public static void main(String args[]){
		 claimsCalculator customerCalculation1 = new ClaimsCalculator()
		 		.claimsBuilder()
		 		.claimsId("Claim-123")
		 		.customerId("Customer-1")
				.amount("1000")
				.build();
		
		claimsCalculator customerCalculation2 = new ClaimsCalculator()
		 		.claimsBuilder()
		 		.claimsId("Claim-123")
		 		.customerId("Customer-1")
				.build();		//can skipped amount
		}
	}
```	

	- Advantage:
	1. As seen from above we need not touch the claimsCalculator class even if we create two different object having two different implementations.
	2. In futre if a new feild added in the claimsCalculator, we need not to go to implemented class and changes anything, we just need to change the claimsCalculator class and provide the logic there, and use it whereever applicable.

### Another Example:
	public class ApiResponse {

    private final int status;
    private final String message;
    private final Object data;

    private ApiResponse(Builder builder) {
        this.status = builder.status;
        this.message = builder.message;
        this.data = builder.data;
    }

    public static class Builder {

        private int status;
        private String message;
        private Object data;

        public Builder status(int status) {
            this.status = status;
            return this;
        }

        public Builder message(String message) {
            this.message = message;
            return this;
        }

        public Builder data(Object data) {
            this.data = data;
            return this;
        }

        public ApiResponse build() {
            return new ApiResponse(this);
        }
    }
    }
   
   "The Builder Pattern is a creational design pattern used to construct complex objects step by step. Instead of passing many constructor arguments, it provides a fluent API where each field is set through chained methods, and the object is created by calling build(). This improves readability, avoids constructor parameter order mistakes, supports optional fields, and works well with immutable objects. In Spring Boot projects, we commonly use Lombok's @Builder annotation to generate builder code automatically."
	
[VideoRed](https://www.youtube.com/watch?v=PWOgZ4EYtlM)

##	Advantages
	Allows you to vary a product’s internal representation.
	Encapsulates code for construction and representation.
	Provides control over steps of construction process.
	
## Disadvantages
	Data members of class aren’t guaranteed to be initialized.
	The number of lines of code increase at least to double in builder pattern, but the effort pays off in terms of design flexibility and much more readable code.
	
[Ref](https://www.youtube.com/watch?v=k4EkJgY9P4c&list=PLsyeobzWxl7r2ZX1fl-7CKnayxHJA_1ol&index=5)

## Factory pattern

	IT is also known as Virtual Constructor.
	*Factory Method Pattern says that just define an interface or abstract class for creating an object but let the subclasses decide which class to instantiate*
		OR
	*We create object without exposing the creation logic to the client and refer the newely created object using a common interface.*

	1. Create an interface shape and a method draw().
	2. Create 3 class rectangle, Circle , Square and override draw()
	3. create a Factory class and a method getShape(Shape)
	4. Create Implementation class in which call new Factory().getShape("Circle");
	[Ref](https://www.tutorialspoint.com/design_pattern/factory_pattern.htm )
		
		OR
	Real time secenrio is- If an employee is communicated via different mode of communication like mobile or phone number, you can use below example:
	1. Create an Employee class with feilds name, id , modeOfCommunication.
	2. Create an Interface Communication which has void process(Employee emp); method/
	3. Create a class EmailCommunication implements Communication and override process(Employee emo) method to gives email specific implementation.
	4. Create a class PhoneCommunication implements Communication and override process(Employee emo) method to gives Phone specific implementation.
	5. Create a Factory Class called CommunicationFactory like:
	```java
		public class CommunicationFactory {
		public Communication getProcss(String modeOfCommunication){
			if("Email".equals(modeOfCommunication)){
				returns new EmailCommunication();
			}
			else if("Phone".equals(modeOfCommunication)){
				returns new PhoneCommunication();
			}
		}
		return null;
		}
	```
	6. Create implementations class
	```java
	public class FactoryDPTEST{
	public static void main(String args){
		List<Employee> empList = createList();//Create a list of Employee
		CommunicationFactory factory = new CommunicationFactory;
		Communication processor;
		
		for(Employee emp: empList){
		processor = factory.getProcss(emp.getModeOfComm());
		processor.process(emp);
		}
	}
	}
	```

	In java -
		1. **getInstance()** method of java.util.Calendar, NumberFormat, and ResourceBundle uses factory method design pattern. 
		2. all the wrapper classes like Integer, Boolean etc, in Java uses this pattern to evaluate the values using **valueOf()** method. 
		
	From Project:-
	We have RequExecutorFactor(interface) and with the help of this factory we instantiate different acquirer executor factory like OpnBkngPaymentExecutorFactory

	Advantages:
	1. Factory design pattern provides approach to code for interface rather than implementation.

	DrawBacks:
	1. A potential disadvantage of Factory methods is that clients might have to sub-class the creator class just to create a particular concrete product object.

## another Example:
	interface Animal{
    void speak();
	}
	
	class Dog implements Animal{
	    public void speak(){
	        System.out.println("Bark");
	    }
	}
	
	class Cat implements Animal{
	    public void speak(){
	        System.out.println("Meow");
	    }
	}
	-----Factory--------
	class AnimalFactory{

    public static Animal create(String type){

        if(type.equals("DOG"))
            return new Dog();

        return new Cat();
    }
	}
	-- Use---
	Animal animal = AnimalFactory.create("DOG");
	animal.speak();
	

## Abstract Factory Pattern -
	Abstract Factory Pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes.

	A common way to distinguish the two patterns is:
	
	Factory Method: Creates one product.
	Example: NotificationFactory.createNotification()
	Abstract Factory: Creates a family of related products.
	Example: UIFactory creates Button, Checkbox, and TextBox that all belong to the same theme (Windows or Mac).

	| Provider | Payment       | Refund       | Receipt       |
	| -------- | ------------- | ------------ | ------------- |
	| Stripe   | StripePayment | StripeRefund | StripeReceipt |
	| PayPal   | PayPalPayment | PayPalRefund | PayPalReceipt |

		// Product Interfaces
	interface Payment {
	    void pay();
	}
	
	interface Refund {
	    void refund();
	}
	
	interface Receipt {
	    void generateReceipt();
	}
	
	// =======================
	// Stripe Implementations
	// =======================
	
	class StripePayment implements Payment {
	    @Override
	    public void pay() {
	        System.out.println("Processing payment using Stripe");
	    }
	}
	
	class StripeRefund implements Refund {
	    @Override
	    public void refund() {
	        System.out.println("Refunding using Stripe");
	    }
	}
	
	class StripeReceipt implements Receipt {
	    @Override
	    public void generateReceipt() {
	        System.out.println("Generating Stripe receipt");
	    }
	}
	
	// =======================
	// PayPal Implementations
	// =======================
	
	class PaypalPayment implements Payment {
	    @Override
	    public void pay() {
	        System.out.println("Processing payment using PayPal");
	    }
	}
	
	class PaypalRefund implements Refund {
	    @Override
	    public void refund() {
	        System.out.println("Refunding using PayPal");
	    }
	}
	
	class PaypalReceipt implements Receipt {
	    @Override
	    public void generateReceipt() {
	        System.out.println("Generating PayPal receipt");
	    }
	}
	
	// =======================
	// Abstract Factory
	// =======================
	
	interface PaymentFactory {
	
	    Payment createPayment();
	
	    Refund createRefund();
	
	    Receipt createReceipt();
	}
	
	// =======================
	// Concrete Factories
	// =======================
	
	class StripeFactory implements PaymentFactory {
	
	    @Override
	    public Payment createPayment() {
	        return new StripePayment();
	    }
	
	    @Override
	    public Refund createRefund() {
	        return new StripeRefund();
	    }
	
	    @Override
	    public Receipt createReceipt() {
	        return new StripeReceipt();
	    }
	}
	
	class PaypalFactory implements PaymentFactory {
	
	    @Override
	    public Payment createPayment() {
	        return new PaypalPayment();
	    }
	
	    @Override
	    public Refund createRefund() {
	        return new PaypalRefund();
	    }
	
	    @Override
	    public Receipt createReceipt() {
	        return new PaypalReceipt();
	    }
	}
	
	// =======================
	// Client
	// =======================
	
	public class AbstractFactoryDemo {
	
	    public static void main(String[] args) {
	
	        // Change only this line to switch provider
	        PaymentFactory factory = new StripeFactory();
	        // PaymentFactory factory = new PaypalFactory();
	
	        Payment payment = factory.createPayment();
	        Refund refund = factory.createRefund();
	        Receipt receipt = factory.createReceipt();
	
	        payment.pay();
	        refund.refund();
	        receipt.generateReceipt();
	    }
	}

# Structural Design Pattern

## Adapter Design Pattern:
	
	As per the GOF definition Adapter **"Match interfaces of different classes"**. This means, an adapter allows two incompatible interfaces to work together
	Adapter design pattern allows the interface of an existing class to be used from another interface. It is often used to make existing classes work with others without modifying their source code.
	Leveraging on Adapter pattern Improves reusability of older functionality 
	An Adapter wraps an existing class with a new interface so that it becomes compatible with the client’s interface.
	**Applicability**
	- Use the Adapter class when you want to use some existing class, but its interface isn’t compatible with the rest of your code.
	- When we want to reuse legacy code in our application without making any modification in the original code.
	/*
	===========================================
	ADAPTER DESIGN PATTERN
	===========================================
	
	Definition:
	-----------
	The Adapter Pattern is a Structural Design Pattern that allows two
	incompatible interfaces to work together by converting the interface
	of one class into another interface expected by the client.
	
	Real-life Example:
	------------------
	Indian Charger ---> Travel Adapter ---> US Socket
	
	Software Example:
	-----------------
	Our application expects every payment gateway to have a method:
	
	    pay(amount)
	
	But a third-party Stripe library provides:
	
	    makePayment(amount)
	
	Since we cannot modify the third-party library, we create an Adapter
	that converts pay() into makePayment().
	
	===========================================
	Code
	===========================================
	*/
	
	// Target Interface (Expected by the Client)
	interface PaymentGateway {
	    void pay(double amount);
	}
	
	// Adaptee (Third-party library - cannot modify)
	class StripeAPI {
	
	    public void makePayment(double amount) {
	        System.out.println("Processing payment through Stripe: " + amount);
	    }
	}
	
	// Adapter
	class StripeAdapter implements PaymentGateway {
	
	    private StripeAPI stripeAPI = new StripeAPI();
	
	    @Override
	    public void pay(double amount) {
	        stripeAPI.makePayment(amount);
	    }
	}
	
	// Client
	public class AdapterPatternDemo {
	
	    public static void main(String[] args) {
	
	        PaymentGateway gateway = new StripeAdapter();
	
	        gateway.pay(5000);
	
	    }
	}
	
	/*
	===========================================
	Output
	===========================================
	
	Processing payment through Stripe: 5000.0
	
	===========================================
	Flow
	===========================================
	
	Client
	   |
	   v
	PaymentGateway (Target Interface)
	   |
	   v
	StripeAdapter
	   |
	   v
	StripeAPI (Adaptee)
	
	Client calls:
	
	gateway.pay(5000);
	
	Adapter internally calls:
	
	stripeAPI.makePayment(5000);
	
	===========================================
	When to Use Adapter Pattern
	===========================================
	
	1. Integrating third-party libraries.
	   Example:
	   - Stripe
	   - PayPal
	   - Razorpay
	
	2. Working with legacy code that cannot be modified.
	
	3. Two classes have incompatible interfaces.
	
	4. Reusing existing code without changing it.
	
	===========================================
	Real Java Examples
	===========================================
	
	1. InputStreamReader
	   Converts InputStream (bytes) to Reader (characters).
	
	2. Arrays.asList()
	   Converts an array into a List.
	
	3. Collections.list()
	   Converts Enumeration into a List.
	
	===========================================
	Interview Definition
	===========================================
	
	The Adapter Pattern is a Structural Design Pattern that allows two
	incompatible interfaces to work together by wrapping an existing class
	and exposing the interface expected by the client.
	
	===========================================
	Memory Trick
	===========================================
	
	Travel Plug Adapter
	
	Indian Charger
	      |
	      v
	Travel Adapter
	      |
	      v
	US Socket
	
	Adapter = Translator
	*/

###When should you use Adapter?
	
	Use it when:
	
	You're integrating a third-party library.
	You can't modify existing code.
	Two classes have incompatible interfaces.
	You want to reuse legacy code without changing it.


## Bridge Pattern:
	The Bridge Design Pattern is a structural design pattern that separates an abstraction from its implementation so that both can vary independently. 
	
		/*
	=========================================================
	BRIDGE PATTERN - Shape & Color Example
	=========================================================
	
	Problem
	-------
	
	Suppose we have:
	
	Shapes
	------
	Circle
	Square
	
	Colors
	------
	Red
	Blue
	
	Without Bridge, we'd need:
	
	RedCircle
	BlueCircle
	RedSquare
	BlueSquare
	
	If tomorrow Green is added:
	
	GreenCircle
	GreenSquare
	
	More shapes or colors means more classes.
	
	Bridge separates Shape and Color.
	
	=========================================================
	*/
	
	// Step 1: Implementor
	interface Color {
	    void applyColor();
	}
	
	// Step 2: Concrete Implementations
	class RedColor implements Color {
	
	    @Override
	    public void applyColor() {
	        System.out.println("Applying Red Color");
	    }
	}
	
	class BlueColor implements Color {
	
	    @Override
	    public void applyColor() {
	        System.out.println("Applying Blue Color");
	    }
	}
	
	// Step 3: Abstraction
	abstract class Shape {
	
	    protected Color color;
	
	    public Shape(Color color) {
	        this.color = color;
	    }
	
	    abstract void draw();
	}
	
	// Step 4: Refined Abstractions
	class Circle extends Shape {
	
	    public Circle(Color color) {
	        super(color);
	    }
	
	    @Override
	    void draw() {
	        System.out.print("Drawing Circle - ");
	        color.applyColor();
	    }
	}
	
	class Square extends Shape {
	
	    public Square(Color color) {
	        super(color);
	    }
	
	    @Override
	    void draw() {
	        System.out.print("Drawing Square - ");
	        color.applyColor();
	    }
	}
	
	// Step 5: Client
	public class BridgePatternDemo {
	
	    public static void main(String[] args) {
	
	        Shape redCircle = new Circle(new RedColor());
	
	        Shape blueCircle = new Circle(new BlueColor());
	
	        Shape redSquare = new Square(new RedColor());
	
	        Shape blueSquare = new Square(new BlueColor());
	
	        redCircle.draw();
	        blueCircle.draw();
	        redSquare.draw();
	        blueSquare.draw();
	
	    }
	
	}
	
	/*
	=========================================================
	Output
	=========================================================
	
	Drawing Circle - Applying Red Color
	Drawing Circle - Applying Blue Color
	Drawing Square - Applying Red Color
	Drawing Square - Applying Blue Color
	
	=========================================================
	Class Diagram
	=========================================================
	
	            Shape
	              |
	      ----------------
	      |              |
	   Circle         Square
	      |
	      |
	     Color
	    /     \
	 RedColor BlueColor
	
	
	Shape HAS-A Color
	
	NOT
	
	Circle extends RedCircle
	
	=========================================================
	Why Bridge?
	=========================================================
	
	Without Bridge
	
	RedCircle
	BlueCircle
	GreenCircle
	
	RedSquare
	BlueSquare
	GreenSquare
	
	6 classes
	
	If Triangle is added
	
	RedTriangle
	BlueTriangle
	GreenTriangle
	
	Now 9 classes
	
	With Bridge
	
	Shapes
	------
	Circle
	Square
	Triangle
	
	Colors
	------
	Red
	Blue
	Green
	
	Only
	
	3 + 3 = 6 classes
	
	instead of
	
	3 × 3 = 9 classes
	
	=========================================================
	When to use?
	=========================================================
	
	Whenever TWO things change independently.
	
	Examples
	
	Shape + Color
	
	Vehicle + Engine
	
	Notification + Sender
	
	Remote + Device
	
	=========================================================
	Interview Definition
	=========================================================
	
	Bridge Pattern separates an abstraction (Shape)
	from its implementation (Color) so that both
	can vary independently.
	
	=========================================================
	Memory Trick
	=========================================================
	
	Shape
	  |
	  +------ HAS -------> Color
	
	NOT
	
	RedCircle
	BlueCircle
	GreenCircle
	*/


	
## Decorator DP:-
		// Component
	interface Coffee {
	    String getDescription();
	    double getCost();
	}
	
	// Concrete Component
	class SimpleCoffee implements Coffee {
	
	    @Override
	    public String getDescription() {
	        return "Simple Coffee";
	    }
	
	    @Override
	    public double getCost() {
	        return 100;
	    }
	}
	
	// Base Decorator
	abstract class CoffeeDecorator implements Coffee {
	
	    protected Coffee coffee;
	
	    public CoffeeDecorator(Coffee coffee) {
	        this.coffee = coffee;
	    }
	}
	
	// Milk Decorator
	class MilkDecorator extends CoffeeDecorator {
	
	    public MilkDecorator(Coffee coffee) {
	        super(coffee);
	    }
	
	    @Override
	    public String getDescription() {
	        return coffee.getDescription() + ", Milk";
	    }
	
	    @Override
	    public double getCost() {
	        return coffee.getCost() + 20;
	    }
	}
	
	// Sugar Decorator
	class SugarDecorator extends CoffeeDecorator {
	
	    public SugarDecorator(Coffee coffee) {
	        super(coffee);
	    }
	
	    @Override
	    public String getDescription() {
	        return coffee.getDescription() + ", Sugar";
	    }
	
	    @Override
	    public double getCost() {
	        return coffee.getCost() + 10;
	    }
	}
	
	// Client
	public class DecoratorPatternDemo {
	
	    public static void main(String[] args) {
	
	        Coffee coffee = new SimpleCoffee();
	
	        coffee = new MilkDecorator(coffee);
	
	        coffee = new SugarDecorator(coffee);
	
	        System.out.println(coffee.getDescription());
	
	        System.out.println("Cost = " + coffee.getCost());
	    }
	}
	
		Output:
		Simple Coffee, Milk, Sugar
		Cost = 130.0
	
	This DP allows us to add new functionality to an existing object without altering its structure.
	This Pattern creats a dacorator class which wraps around original class and provides additional functionality keeping clas method signature intact.
	Steps:
	1. Create an Interface Shape with draw method.
	2. Create 2 conceret class that implements Shape. Called- Circle, Rectangle.
	3. Create abstract decorator class(ShapeDecorator) implementing the Shape interface
	4. Create concrete decorator class extending the ShapeDecorator class, this class override ShapeDecorator class's method draw and call to one method setRedBroder(Shape).
	5. Create Implementation class. Create a object of RedShapeDecorator(Shape shape)
	[Ref](https://www.tutorialspoint.com/design_pattern/decorator_pattern.htm )
	
##	Proxy Design Pattern:-
	
	In PP, A class represents functionality of Another CLass. In proxy pattern, we create object having original object to interface its functionality to outer world.
	[Ref](https://www.tutorialspoint.com/design_pattern/proxy_pattern.htm )

		// Subject
	interface Internet {
	    void connect(String website);
	}
	
	// Real Subject
	class RealInternet implements Internet {
	
	    @Override
	    public void connect(String website) {
	        System.out.println("Connecting to " + website);
	    }
	}
	
	// Proxy
	class ProxyInternet implements Internet {
	
	    private RealInternet realInternet = new RealInternet();
	
	    @Override
	    public void connect(String website) {
	
	        if (website.equalsIgnoreCase("facebook.com")) {
	            System.out.println("Access Denied!");
	            return;
	        }
	
	        realInternet.connect(website);
	    }
	}
	
	// Client
	public class ProxyPatternDemo {
	
	    public static void main(String[] args) {
	
	        Internet internet = new ProxyInternet();
	
	        internet.connect("google.com");
	
	        internet.connect("facebook.com");
	    }
	}

	Output:
	Connecting to google.com
	Access Denied!

##	Composite Design Pattern-
	
	Compose objects into tree structures to represent part as-well-as whole hierarchies.
	[REF](https://www.tutorialspoint.com/design_pattern/composite_pattern.htm )
	Example:-
	Heirarchy of Organisation.
	import java.util.ArrayList;
	import java.util.List;
	
	// Component
	interface Employee {
	    void showDetails();
	}
	
	// Leaf
	class Developer implements Employee {
	
	    private String name;
	
	    public Developer(String name) {
	        this.name = name;
	    }
	
	    @Override
	    public void showDetails() {
	        System.out.println("Developer : " + name);
	    }
	}
	
	// Composite
	class Manager implements Employee {
	
	    private String name;
	    private List<Employee> team = new ArrayList<>();
	
	    public Manager(String name) {
	        this.name = name;
	    }
	
	    public void addEmployee(Employee employee) {
	        team.add(employee);
	    }
	
	    @Override
	    public void showDetails() {
	
	        System.out.println("Manager : " + name);
	
	        for (Employee employee : team) {
	            employee.showDetails();
	        }
	    }
	}
	
	// Client
	public class CompositeDemo {
	
	    public static void main(String[] args) {
	
	        Employee emp1 = new Developer("John");
	        Employee emp2 = new Developer("David");
	        Employee emp3 = new Developer("Alice");
	
	        Manager manager = new Manager("Raj");
	
	        manager.addEmployee(emp1);
	        manager.addEmployee(emp2);
	        manager.addEmployee(emp3);
	
	        manager.showDetails();
	    }
	}
	
	
# Behavioral Design Pattern

## Chain of Responsibility:-
	
	The chain of responsibility pattern creates a chain of receiver objects for a request. This pattern decouples sender and receiver of a request based on type of request.
	In this pattern, normally , each receiver contains the refernce of another receiver. If one receover cant handle a request, it just passes it to anothet receiver.and so on.
	one or more than one receiver can handle a request.

	/*
	=========================================================
	CHAIN OF RESPONSIBILITY PATTERN
	=========================================================
	
	Problem:
	--------
	An expense approval request should go through multiple levels.
	
	Employee  -> can approve up to ₹1,000
	Manager   -> can approve up to ₹10,000
	Director  -> can approve anything above ₹10,000
	
	If one person cannot approve, the request is passed
	to the next approver.
	
	=========================================================
	*/
	
	// Handler
	abstract class Approver {
	
	    protected Approver nextApprover;
	
	    public void setNextApprover(Approver nextApprover) {
	        this.nextApprover = nextApprover;
	    }
	
	    public abstract void approve(int amount);
	}
	
	// Concrete Handler 1
	class Employee extends Approver {
	
	    @Override
	    public void approve(int amount) {
	
	        if (amount <= 1000) {
	            System.out.println("Employee approved ₹" + amount);
	        } else {
	            nextApprover.approve(amount);
	        }
	    }
	}
	
	// Concrete Handler 2
	class Manager extends Approver {
	
	    @Override
	    public void approve(int amount) {
	
	        if (amount <= 10000) {
	            System.out.println("Manager approved ₹" + amount);
	        } else {
	            nextApprover.approve(amount);
	        }
	    }
	}
	
	// Concrete Handler 3
	class Director extends Approver {
	
	    @Override
	    public void approve(int amount) {
	
	        System.out.println("Director approved ₹" + amount);
	    }
	}
	
	// Client
	public class ChainOfResponsibilityDemo {
	
	    public static void main(String[] args) {
	
	        Approver employee = new Employee();
	        Approver manager = new Manager();
	        Approver director = new Director();
	
	        // Create the chain
	        employee.setNextApprover(manager);
	        manager.setNextApprover(director);
	
	        employee.approve(500);
	        employee.approve(7000);
	        employee.approve(50000);
	    }
	}

	//Output
	Employee approved ₹500
	Manager approved ₹7000
	Director approved ₹50000
