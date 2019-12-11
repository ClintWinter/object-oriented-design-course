# Object-Oriented Design

This is a summation of the course [*Programming Foundations: Object-Oriented Design*](https://www.linkedin.com/learning/programming-foundations-object-oriented-design-3). I have already watched through once just to listen. Now I am looping back to take notes on all of the important content within, so I can more easily reference the material and commit it to memory. If you are using my notes to replace the course, but do not understand the very basics of OOP, such as what a class is, I recommend you watch it yourself first. My notes are only detailing the parts that are less comfortable for me.

&nbsp;

## Object-Oriented Fundamentals

Sometimes it's easy to forget this, but it's called **object**-oriented design for a reason! It's about describing objects and their responsibilities, properties and behaviors.

All objects have...
* Identity: Olivia's coffee mug
* Attributes (Properties): color size, fullness
* Behaviors: `fill()`, `empty()`, `clean()`

Objects can also describe non-tangible things such as a date, timer, or bank account. They are well-defined idea that meets the definition of an object.

A bank account has identity, attributes, and behaviors:
* Number: B3512
* Balance: $7,500
* `deposit()`
* `withdraw()`

&nbsp;

**Objects are nouns**

Would you put the word "The" in front of it?
* The bank account
* The time
* The event
* The person

**Behaviors are verbs**

### Fundamental Ideas

There are **4 fundamental ideas** in object-oriented programming:

* **A**bstraction
* **P**olymorphism
* **I**nheritance
* **E**ncapsulation

### Abstraction

We focus on the essential qualities of something, rather than a specific example. A `Person` class could have properties for height, weight, gender, but if height isn't important to us for this application, then we should get rid of it.

### Encapsulation

Forces the user to interact with our code the way we want them to. We can make properties private, and only accessible through a method that has special instructions.

Another term for this is black-boxing. We are only showing or making available what is necessary for other parts of the application to work.

**The general rule is encapsulate as much as possible**.

### Inheritance

* Base a new object or class on an existing one
* Inherit the existing attributes and methods

If our application has a `Customer` and `Employee` class, and they share the properties `name`, `phone`, `address`, and the behavior `updateContact()`, then it could make sense to extract that into a superclass that they both inherit from that contains those overlapping properties and behaviors.

Now `Customer` and `Employee` *inherit* from `Person`.

The **parent class** is also called the **superclass** or the **base class**

The **child class** is also called the **subclass** or the **derived class**.

### Polymorphism

Simply means "having many forms".

**Dynamic Polymorphism** - Uses the same interface for methods on different types of data

Let's say we have 2 different coffee makers. One is a basic coffee maker and the other is a french press. Both require a `brew()` method that take 2 parameters: `coffee grounds` and `water`. The way they handle these parameters is different, but the input and output is the same.

* Perhaps The `FrenchPress` class can inherit all of the properties and methods from our `BasicCoffeeMaker` class, but then replaces the `brew()` method through a process called **overriding**.
* Or both of the coffee makers inherit from the same abstract class with an abstract `brew()` method, forcing them to implement their version of the method themselves.
* Or they both agree to implement the same interface.

All of these options are possible implementations of polymorphism. The benefit of dynamic polymorphism is that it allows us to use any form of coffee maker as long as it has a `brew()` method, takes the input of `coffeeGrounds` and `water`, and returns a cup of coffee.

**Static (Compile-Time) Polymorphism** - Uses a feature called **Method Overloading**, which implements multiple methods in the same class with the same name, but different input parameters.

If I give the french press the parameters `coffeeGrounds` and `water` I'll get back a cup of coffee, but if I change my parameters to `teaLeaves` and `water`, then our french press will execute a different version of the `brew()` method that returns a cup of tea.

### Analysis and Design

This course goes through a 5 step process of analysis and design to find out **what** we need to do and **how** we are going to do it.

1. Gather requirements
2. Describe the application
3. Identify the main objects
4. Describe the interactions
5. Create a class diagram

&nbsp;

## Requirements

Figure out what our application needs to do and what problem it is trying to solve.

> A common pitfall is having in your head a dozen half-baked ideas of what your app *could* do, instead of nailing down what it really *needs* to do.

### Functional Requirements

For functional requirements we use the phrase "The system **must**..." or "The application **must**...".

For example:
```
The system must...
* heat meals in space-packaging
* allow user to set time for meal to be ready
* notify user when meal is ready via space-pager
* ~~inherit meal types from an abstract superclass~~
```

The 4th bullet above is struck from the list because defining requirements has nothing to do with object orientation. It shouldn't contain words like "abstract", "inheritance", "class" or "object"--those are details we will get to later.

### Non-Functional Requirements

Describe required characteristics of the application rather than features, so we can use the phrase "The system **should be**..." or "The application **should be**...".

The describe the -ilities like reliability, maintainability, usability, and availability.

For example:
```
The system should be...
* available 24/7
* usable while wearing work gloves
* ~~compatible wtih Windows, Mac, Linux, iOS, and Android~~
```

The last bullet is struck from the list because we don't need to be exhaustive and have every possible thing on the list just yet. Focus on capturing the minimum absolute set of requirements. Forget about optional, or nice-to-have, or dream features. Get to your minimum viable product (MVP).

To get really in-depth on your requirements, use FURPS+ to give you a good idea of all of the different aspects of a system you should cover.

&nbsp;

## Use Cases and User Stories

### Use Cases

A use case has 3 essential things:

* Title: **What** is the goal?
* Primary Actor: **Who** desires it?
* Success Scenario: **How** is it accomplished?

Use Case: Scenario as Paragraph
```
Title: Heat Meal
Primary Actor: Astronaut
Success Scenario: Astronaut inserts meal package. System identifies type of meal. System heats package for length of time required for meal type. System notifies astronaut that meal is ready via space pager. Astronaut removes package from system.
```

Use Case: Scenario as Steps
```
Title: Heat Meal
Primary Actor: Astronaut
Success Scenario:
    1. Astronaut inserts meal package.
    2. System identifies type of meal.
    3. System heats package for length of time required for meal type.
    4. System notifies astronaut that meal is ready via space pager.
    5. Astronaut removes package from system.
```

We can add extensions for alternative flows or when things go wrong, but use cases are typically used for successful scenarios.

Use Case: Additional Details
```
Title: Heat Meal
Primary Actor: Astronaut
Success Scenario:
    1. Astronaut inserts meal package.
    2. System identifies type of meal.
    3. System heats package for length of time required for meal type.
    4. System notifies astronaut that meal is ready via space pager.
    5. Astronaut removes package from system.
Extensions:
    2a. Describe steps for unidentifiable package.
    4a. Describe steps for space-pager system error.
```

We can also add preconditions that must be true to begin the use case.

Use Case: Additional Details
```
Title: Heat Meal
Primary Actor: Astronaut
Success Scenario: ...
Extensions: ...
Preconditions: Customer has selected meal to prepare.
```

### Identifying the Actors

Our space microwave example could have more than just an astronaut acting on it. We could have commanders, pilots, flight engineers, mission control, and nutritionists.

Actors can also be other systems. Since the microwave notifies via space pager, the microwave will need to interact with some sort of space pager system.

The focus should really be on the goal the actor wants to accomplish.

For example, for heating meals, all of the astronauts on the ship (commanders, pilots, engineers) are expected to use the microwave the same way: to heat food. Meanwhile, the people back on Earth (mission control and nutritionists) are simply monitoring that activity. So in this instance it may make sense to group the astronauts into one actor called "Cook" and all of the people on Earth into the "Observer".

In use cases, the primary actor is not the most important actor in the scenario, they are just the person *who initiates it*.

### Identifying the Scenarios

Describe a goal that an actor can accomplish in a single encounter.

One may think "turn on microwave" could make a good use case, but the user's goal isn't to turn on the microwave--their goal is to turn on the microwave in order to do something such as cook a meal. "Cook a meal" would be our use case.

Examples of user-focused goals:
```
* Cook meal
* Generate reports
* Change settings
* Order supplies
```

When writing, use an active voice and omit needless detail...

> Bad: The system is provided with the meal packaged by the astronaut.

> Good: Astronaut inserts meal package.

or too much detail...

> Bad: The system connects to the external pager system over HTTPS and uses JSON to submit the formatted text message that is to be transmitted, and the waits for a delegated callback response.

> Good: System sends pager message

and avoid describing the interface. Avoid things like "screen", "click", "button", and "select". Focus on the **intention**.

### User Stories

A user story generally follows the pattern: "As a (type of user) I want (goal) so that (reason)"

Example:
```
As an astronaut
I want to heat up my food
so that I can eat a warm meal.
```

Just like use cases, the focus is on intention and should not include descriptions of the user interface.

User stories can be used right at the start of a project to serve as placeholders for deeper conversations.

&nbsp;

## Domain Modeling

### Identifying the Objects

We now start to transition from *analysis* to *design* (how we are going to organize our solution).

The next step is to create a **Conceptual Model**, which represents important objects and the relationships between them.

We can start by going through the use cases and highlighting all of the nouns:

> *"Dodge" Use Case Scenario:* **System** spawns enemy **spaceship** in play area. Spaceship flies towards players **asteroid** and fires **missile** at **it**. **Player** steers asteroid in **direction** to avoid missile **path**. Missile flies past player asteroid and disappears **offscreen**.

In this process, ignore the urge to judge the words or think of better ones. We can do that after.

> ~~System~~, Spaceship, ~~It~~, Player, Area, Direction, Asteroid, Path, Missile, ~~Offscreen~~

### Identifying Class Relationships

Now that we have our nouns, its a good idea to divide them up and then draw lines between them to show relationships.

1. We know there's a relationship between the *player* and *asteroid*, so let's draw a line between them.
2. The *asteroid* exists in the *area*, so that's another.
3. The *spaceship* and *missile* also exist within the *area*.
4. A relationship between the *spaceship* and the *missile*.
5. And between the *missile* and the *path* it follows.
6. Although not completely convinced it should be an object yet, the *asteroid* and *spaceship* both can have a *direction*.

Now that we have our relationships, we can use verbs or phrases to quickly describe the relationship between the objects. Rather than say the player *uses* the asteriod, we can say...

1. The *player* **steers** the *asteroid*.
2. The *spaceship* **fires** the *missile*.
3. The *area* **contains** the *asteroid*, *spaceships* and *missiles*.
4. The *missile* **follows** a *path*.

Finally, we can add optional symbols to describe the relationships further. If we have a line between *area* and *spaceship* we may do this:

> **AREA** 1 ------- 1...* **SPACESHIP**

This signifies that the area has a one to many relationship with the spaceship. While there's 1 area there will be 1 or more spaceships.

### Identifying Class Responsibilities

We can now go back to our uses cases where we picked out nouns, to also pick out verbs that identify *responsibilities*

> *"Dodge" Use Case Scenario:* System **spawns enemy spaceship** in play area. Spaceship **flies towards players** asteroid and **fires missile** at it. Player **steers asteroid** in direction to **avoid missile** path. Missile **flies past player** asteroid and **disappears offscreen**.

Something not obvious is where these responsibilities belong, especially if it affects multiple objects.

> ***IMPORTANT RULE: An Object should be responsible for itself.***

Let's look at how this rule applies to our selected verbs and phrases:

* **spawn enemy spaceship**: The game system may initiate that happening, a spaceship should be responsible for creating itself. Rephrased to `spawn`.
* **flies towards player**: An action for that spaceship, which will be rephrased to `move`.
* **fires missile**: A spaceship initiates firing a missile, but a missile object is responsible for spawning itself and knowing where it's going and doing. Rephrased to `spawn`.
* **steers asteroid**: When the player steers the asteroid, the asteroid should handle moving itself. Rephrased to `move`.
* **avoid missile path**: A tricky phrase, it means we need to detect when a missile collides with an asteroid. We could put it on the missile or the asteroid. At this point it isn't clear, so let's leave it on the asteroid as `detect collision`.
* **flies past player**: Can be simplified to `move` on the missile once again.
* **disappear offscreen**: The missile can `detect out-of-bounds`.

Why didn't the player get any of the responsibilities? *This isn't about who initiates the action, but where the responsibility lies*. The player will still be responsible for making things happen by requesting behaviors of other objects.

It's common for new developers to give way too much behavior to a single actor, such as the player because it drives the encounter. In OOP, an object that knows and/or does too much is known as a **God Object**. Think about how easy it is for use case scenarios to *seemingly* assign responsibility to the **system**:

> *"Impact" Use Case Scenario:* **System spawns spaceship** in play area. Spaceship fires missile towards player asteroid. **System detects missile collision** with asteroid. Missile explodes and asteroid is destroyed. **System reduces player life counter**. **System spawns new player asteroid**.

When you see "System reduces player life counter", you should read it like this: "*Some part of the* system reduces player life counter".

If you have an object that is filled with unrelated behaviors and seems to exist to control things around it, that is a good sign you're still thinking like a procedural programmer.

### CRC Cards

CRC stands for

* **C**lass
* **R**esponsibility
* **C**ollaboration

Each card has 3 sections. The first is the class name, the responsibilities of the class, and the collaborators (the other classes it interacts with).

Typically the class is underlined at the top, the responsibilities take up the left 2/3rds and the collaborators the right 1/3rd. They may also be known as **CRH** cards for Component/Responsibilities/Helper.

Start by using the nouns in the use cases and the verbs/verb phrases to identify responsibilities.

Then we can add the obvious collaborators. Like a missile will interact with the *missile* that fires it, the play *area* it flies through, and the *asteroid* it blows up. Those can go on the right-hand side.

It's good to put these on paper cards because we can quickly move them around to see relationships.

In addition, if you need more than 1 card for a class, that's a good clue you're trying to give it too much responsibility.

You should at least finish this exercise with the core set of classes and their responsibilities that you intend to code.

&nbsp;

## Class Diagrams

### Creating class diagrams: Attributes

This will use UML Class Diagrams.

Here is how we will notate attributes:

![UML Attributes](https://i.imgur.com/JzBDTIf.png)

### Creating class diagrams: Behaviors

You may see (+) and (-) signs before attributes or behaviors in the diagram. (-) means that it is private to the class, not accessible to the outside world. (+) means public.

> Make sure you really focus on what objects *do*.

It is common to get too focused on the data if we skip these steps of design. If they need a spaceship they start going through all of the different attributes it can have. If you find your classes are devoid of behavior, you may want to revisit those responsibilities.

![UML diagram with behaviors](https://i.imgur.com/EidHeJE.png)

### Instantiating classes

``` Java
// Java
Spaceship myShip = new Spaceship()
```

``` C++
// C++
Spaceship *myShip = new Spaceship()
```

``` Ruby
# Ruby
myShip = Spaceship.new
```

``` Python
# Python
myShip = Spaceship()
```

``` Swift
// Swift
let myShip: Spaceship = Spaceship()
```

When we instantiate a class, the properties are set at the start. We may have default values given to it, but if we try to use them without realizing we didn't set them it can lead to undesired behavior. We want an instance of our class to be in a meaningful state to begin with. For that we can use a **constructor**; *a special method that gets called to create an object*.

Example:
``` Java
// Java
public class Spaceship {

    // instance variables
    public String callSign;
    private int shieldStrength;

    // constructor method
    public Spaceship() {
        name = "The nameless ship";
        shieldStrength = 100;
    }

    // other methods...
}
```

Now our class has more meaningful values and won't cause issues with the default values `null` and `0`.

![UML with constructor](https://i.imgur.com/iAuUwZ0.png)

### Class with multiple constructors

We can use the concept of **overloading** if we decide we don't always want our ship to be named "The nameless ship" and would rather include a name when instantiating.

``` Java
// Java
public class Spaceship {

    // instance variables
    public String callSign;
    private int shieldStrength;

    // constructor methods
    public Spaceship() {
        name = "The nameless ship";
        shieldStrength = 100;
    }

    // overload constructor
    public Spaceship(String name) {
        callSign = name;
        shieldStrength = 200;
    }

    // other methods...
}
```

Now we have two ways of instantiating a spaceship.

### Static attribute and methods

**Instance Variable** - Variable for which each instantiated object of a class has a separate copy. This allowed us to instantiate a bunch of *different* spaceships, so if one gets damaged, not all of them lose shield strength.

Maybe we want to introduce a difficulty level that affects the *toughness* of **ALL** the ships? If we have a new toughness property, we would have to change it for all of the ships one at a time. A better route would be to use a **static variable**, which is shared across all objects in a class. Also called a *shared* variable or a *class* variable.

``` Java
// Java
public class Spaceship {

    // instance variables
    public String callSign;
    private int shieldStrength;

    // static variables
    public static float toughness;

    // other code...
}
```

If we want to access an instance variable on a ship, we would do `ship1.callSign`, but to access a static variable we use the class name: `Spaceship.toughness`.

We can also create *static methods* that exist at the class level. In some languages, we can simply add the `static` keyword:

``` Java
// Java
public class Spaceship {

    // private static variables
    public static float toughness;

    // public static methods
    public static increaseDifficulty(float t) {
        toughness += t;
    }
}

Spaceship.increaseDifficulty(0.2);
```

in UML diagrams, static members of a class are denoted with an underline.

&nbsp;

## Inerhitance and Composition

### Identifying inheritance situations

> ***Inheritance Describes an "Is a" Relationship***

A StarFighter *is a* Spaceship

A CargoShuttle *is a* Spaceship

"*Is a type of*" or "*Is a kind of*" are other helpful phrases to indicate if you may have an inheritance situation.

If we put the UML diagrams for StarFighter and CargoShuttle next to each other, it is clear they have several attributes and methods in common.

![UML of StarFighter and CargoShuttle](https://i.imgur.com/m8mp4f6.png)

We can strip out those elements and put them into a superclass called "Spaceship". StarFighter and CargoShuttle will inherit from that, indicated by the arrow pointing to the superclass.

![UML Inheritance](https://i.imgur.com/Hk3ULIW.png)

From here we can easily create more types of spaceships that inherit from our Spaceship superclass. However, maybe our new subclass doesn't use a method the same way as the superclass. In that case most languages will allow the subclass to replace the implementation of the superclass through **overriding**.

> It is common for new developers to go overboard with inheritance, having 5 levels of depth and inheriting everything. **Don't go looking for it** because it usually announces itself. Don't worry if your diagrams don't have any inheritance--it's normal.

### Using Inheritance

Recognizing inheritance in code:

``` Java
// Java
public class CargoShuttle extends Spaceship {
```

``` C#
// C#
public class CargoShuttle : Spaceship {
```

``` C++
// C++
class CargoShuttle : public Spaceship {
```

``` Swift
// Swift
class CargoShuttle : Spaceship {
```

``` Python
# Python
class CargoShuttle(Spaceship):
```

``` Ruby
# Ruby
class CargoShuttle(Spaceship):
```

Calling a method in the super/parent/base class:

``` Java
// Java
super.setShield()
```

``` C#
// C#
base.setShield()
```

``` C++
// C++
// C++ allows for multiple inheritance, meaning we can inherit from multiple classes.
// Therefor, we must specify which inherited class we are calling from.
Spaceship::setShield()
```

``` Swift
// Swift
super.setShield()
```

``` Python
# Python
super().setShield()
```

``` Ruby
# Ruby
super set_shield
```

### Abstract and concrete classes

With a StarFighter and CargoShuttle, we may decide we never need to instantiate the generic concept of a `Spaceship`. In this case, `Spaceship` can be defined as an abstract class.
* Exists for other classes to inherit.
* Cannot be instantiated
* Contains at least one abstract method

We identify an abstract class in UML diagrams using italicized font.

### Interfaces

An **interface** is a list of methods for a class to implement. It doesn't contain any actual behavior.

``` Java
// Java
interface Moveable {
    // method signatures
    void move(int x, int y);
}
```

The method `move` doesn't have a body, the interface enforces a *contract* that classes using the interface will define the methods of the interface.

``` Java
// Java
class Asteroid implements Moveable {
    public void move(int x, int y) {
        // provide implementation code...
    }
}
```

Interfaces and Abstract classes can seem similar at first, but they are different.

> Interfaces represent a **capability**

> Abstract classes represent a **type**

e.g. A CargoShuttle **is a** Spaceship

The Spaceship and Asteroid both might have a `move` method, but the only thing they have in common is the `Movable` interface. It wouldn't make sense for the Asteroid to inherit from Spaceship because it isn't a *type* of Spaceship. However, moving is a *capability* that they both share

In UML, we use double angle brackets to represent an interface: `<<Movable>>`, and classes that implement that interface point to it with a dotted line rather than a solid line (which inheritance does).

![UML Interface](https://i.imgur.com/0Zxeyh2.png)

A class can implement multiple interfaces.

For example, in a game we can have a `Drawable` interface that forces a `draw` method. For all of the objects that need to be drawn on the screen, they will use the interface. We may have a collection of all of the objects in our game. To update the display we can interate through all of the potentially unknown objects in the list and check if it supports the drawable interface, and if so, call its draw method.

> Program to an interface, not to an implementation.

Interfaces are often a more future-friendly way of programming than using inheritance.

### Aggregation

Another type of relationship (like inheritance) in which one object is built of other objects.

For example, a fleet is an object that contains a bunch of individual spaceship objects.

Aggregation is referred to as a **has a** relationship, opposed to **is a**.

> ~~A Fleet is a Spaceship~~

> A Fleet **has a** Spaceship

or

> A Fleet **has many** Spaceships

In UML, the symbol for an aggregation relationship is an unfilled diamond. In addition, we can provide multiplicity with an asterisk to say 1 Fleet can have 0 to many Spaceships.

![UML Aggregation](https://i.imgur.com/Kv690kK.png)

In the case of aggregation, the existence of the objects inside are independent of the aggregation object. So in our case, destroying the Fleet does not destroy the Spaceships. It's akin to breaking up a band.

A better phrase may be "uses a" or "uses many":

> A Fleet **uses many** Spaceships

### Composition

A more specific form of aggregation, composition is based on a **has a** relationship, but it specifically implies *ownership*

We might say "A Spaceship has an Engine", but more accurately we would say

> A Spaceship **owns an** Engine

We imply ownership because an Engine has no meaning or purpose without a Spaceship. For example, if our Spaceship is destroyed by an Asteroid, then the Engine (and other contained objects) is destroyed too.

Aggregation isn't always necessary to show in a UML diagram, but composition is a more important relationship to show. It is represented by a *filled in* diamond.

&nbsp;

## Software Development

### General development principles

SOLID Principles:

* **S**ingle responsibility principle
* **O**pen/closed principle
* **L**iskov substitution principle
* **I**nterface segregation principle
* **D**ependency inversion principle

The **Single Responsibility Principle** warns developers about creating god objects. If classes start getting big, consider if they need to be split up to interact with each other.

&nbsp;

DRY:

**Don't Repeat Yourself**

&nbsp;

YAGNI:

**You Ain't Gonna Need It**

A common trap of new, overzealous programmers make is trying to make their code too extensible and trying to foresee every single possible scenario we may need to account for. However, this also means more debugging, testing, and code bloat. We don't want to waste time on things that will never be used.

&nbsp;

Code Smell:

Any characteristic in a program's code that possibly indicates a deeper problem.

### Design Patterns

The re-usable form of a solution to a design problem.

They are templates to help structure your code in a smart way.
