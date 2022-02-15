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
		- Prototype DP
	
	2.	Structural Design Pattern- (7)
		- Adapter DP
		- Decorator DP
		- Proxy DP
		- Bridge DP
		- Composite DP
		- Facade DP
		- Flyweight DP
		
	3. Behavioral DP - (11)
		- Chain of Responsibility DP
		- Command DP
		- Observer DP
		- Iterator DP
		- Strategy DP
		
		
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

## Abstract Factory Pattern -


# Structural Design Pattern

## Adapter Design Pattern:
	
	As per the GOF definition Adapter **"Match interfaces of different classes"**. This means, an adapter allows two incompatible interfaces to work together
	Adapter design pattern allows the interface of an existing class to be used from another interface. It is often used to make existing classes work with others without modifying their source code.
	Leveraging on Adapter pattern Improves reusability of older functionality 
	An Adapter wraps an existing class with a new interface so that it becomes compatible with the client’s interface.
	**Applicability**
	- Use the Adapter class when you want to use some existing class, but its interface isn’t compatible with the rest of your code.
	- When we want to reuse legacy code in our application without making any modification in the original code.
## Decorator DP:-
	
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

##	Composite Design Pattern-
	
	Compose objects into tree structures to represent part as-well-as whole hierarchies.
	[REF](https://www.tutorialspoint.com/design_pattern/composite_pattern.htm )
	Example:-
	Heirarchy of Organisation.
	
	
# Behavioral Design Pattern

## Chain of Responsibility:-
	
	The chain of responsibility pattern creates a chain of receiver objects for a request. This pattern decouples sender and receiver of a request based on type of request.
	In this pattern, normally , each receiver contains the refernce of another receiver. If one receover cant handle a request, it just passes it to anothet receiver.and so on.
	one or more than one receiver can handle a request.
	