# Design Pattern:
		A General Reusable solution to common occurring problems.
						OR
		A template for how  to solve a problem  that can use in many different.

# Advantages of Design Pattern:-
	
		1. A Design Pattern are *well- proved Solution for solving a specific problem.
		2. The benefits lies in Reuability and extensibility of already developed applications.
		3. DP uses Objec-Oriented concepts like decomposition, inheritence, polymorphism.
		
# Diadvantages of Design Pattern:
			
		1. DP do no lead to direct code reuse.
		2. Design Patterns are deceptively(illusive) simple.
		
# Creational Design Pattern
</br>
## Singleton- 

It insures that only one instance is created and provide global point to access it.
Versions of Singleton:
	1. Eager Initialization
	2. Lazy  Initialization
	3. Lazy Initialization with private constructor and synchronized method
	4. Enum Singleton - The prefer way.
	
##Builder Pattern-
Seperate the construction of complex object from its representation(Builds an complex object using a simple class step by step)
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
[Ref](https://www.youtube.com/watch?v=k4EkJgY9P4c&list=PLsyeobzWxl7r2ZX1fl-7CKnayxHJA_1ol&index=5)

##Factory pattern
We create object without exposing the creation logic to the client ans refer the newely created object using a common interface.
1) Create an interface shape and a method draw().
2) Create 3 class rectangle, Circle , Square and override draw()
3) create a Factory class and a method getShape(Shape)
4) Create Implementation class in which call new Factory().getShape("Circle");
[Ref](https://www.tutorialspoint.com/design_pattern/factory_pattern.htm )

# Structural Design Pattern

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
	
	
# BehavioralDesign Pattern

## Chain of Responsibility:-
	
	The chain of responsibility pattern creates a chain of receiver objects for a request. This pattern decouples sender and receiver of a request based on type of request.
	In this pattern, normally , each receiver contains the refernce of another receiver. If one receover cant handle a request, it just passes it to anothet receiver.and so on.
	one or more than one receiver can handle a request.
	