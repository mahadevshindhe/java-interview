# Java Object Class

The Java Object class is the superclass of all classes in Java. It is the topmost class in the Java class hierarchy, and every class in Java implicitly extends the Object class if it doesn't explicitly extend another class. This means that every object created in Java inherits methods from the Object class, making it a fundamental part of the Java programming language.

### Methods of the Object class and their significance: 

1. **equals(Object obj):** Determines whether one object is equal to another. The default implementation compares memory addresses, but it's often overridden to compare the state (values of fields) of objects.
2. **hashCode():** Returns an integer hash code value for the object, which is used in hashing-based collections like HashMap. It's important to override this method whenever equals() is overridden to maintain the equals()-hashCode() contract.
3. **toString():** Returns a string representation of the object. By default, it returns the class name followed by the object's hash code in hexadecimal. It's commonly overridden to provide a more informative string representation of the object.
4. **clone():** Creates and returns a copy of the object. The default implementation performs a shallow copy. To use this method, a class must implement the Cloneable interface, and it's often necessary to override clone() to provide a deep copy.
5. **getClass():** Returns the runtime class of the object. It can be used to get information about the object's class, such as its name, methods, superclass, etc.
6. **notify(), notifyAll():** Used in multithreading to resume one or all threads that are waiting on this object's monitor (due to calling wait() on the object).
7. **wait():** Causes the current thread to wait until another thread invokes notify() or notifyAll() on the same object. This method is used for inter-thread communication.

### Polymorphism and the Object class:
The Object class enables polymorphism in Java. Since all classes extend Object, a variable of type Object can hold a reference to any object. Methods that accept or return an Object can work with objects of any class.

**Top Interview Questions:**

1. **equals() method:**
- How does the equals() method in the Object class work, and when would you override it?
- Answer: The equals() method in the Object class checks if two references point to the same object in memory. You would override it when you need to compare objects based on their internal state rather than their identity.
2. **equals() and hashCode() contract:**
- Can you explain the contract between equals() and hashCode() methods in Java?"
- Answer: If two objects are equal according to the equals() method, then calling the hashCode() method on each of the two objects must produce the same integer result. This contract is essential for the correct operation of collections that use hashing.
3. **toString() method:**
- What is the purpose of the toString() method, and why might you override it?"
- Answer: The toString() method provides a string representation of the object. You might override it to provide meaningful information about the object, which can be very useful for debugging and logging purposes.
4. **wait() and notify() methods:**
- Describe a scenario where you would use the wait() and notify() methods of the Object class.
- Answer: You would use these methods in a producer-consumer scenario where one thread is producing data and another is consuming it. The consumer thread would call wait() to wait for data to be produced, and the producer thread would call notify() to signal that data is available.
5. **getClass() method vs instanceof:**
- How does the getClass() method differ from the instanceof keyword in Java?
- Answer: The getClass() method returns the exact runtime class of the object, while instanceof checks if the object is an instance of a specified class or its subclasses. instanceof also returns false if the object is null, whereas getClass() would cause a NullPointerException.
6. **clone() method:**
- What is the clone() method, and what are the considerations for using it in a class?
- Answer: The clone() method creates a copy of the object. When using it, consider whether to perform a shallow or deep copy, and ensure that any mutable fields of the object are also cloned to avoid shared references.
7. **Significance of the Object class:**
- Discuss the significance of the Object class in Java's object-oriented programming model.
- Answer: The Object class is significant because it provides a common structure and behavior for all objects in Java. It enables polymorphism, method overriding, and serves as a generic reference type. It also provides default implementations of fundamental methods that can be customized by subclasses.

##### If two objects have the same hash code, does it mean they are equal?

No, two objects having the same hash code does not guarantee that they are equal. The hashCode() method can produce collisions where different objects have the same hash code. Equality is determined by the equals() method.
##### How would you implement a hashCode() method for a class that has multiple fields?

You would combine the hash codes of individual fields, typically using a formula like Objects.hash(field1, field2, ..., fieldN) or by following the pattern result = prime * result + (field.hashCode()) for each field, where prime is a non-zero prime number, often 31.
##### Can a hashCode() method return a negative number?

Yes, a hashCode() method can return a negative number. The return type of hashCode() is int, which includes the entire range of 32-bit integers, both positive and negative. This has no specific implications other than the need for hash tables to handle negative hash codes appropriately.
##### Describe a situation where poorly implemented hashCode() could lead to a performance issue in a HashMap.

If a hashCode() method returns the same or very similar hash codes for different objects, it can lead to many collisions in a HashMap, causing most entries to end up in the same bucket. This degrades the performance from O(1) to O(n) for operations like get() and put().
##### What is the result of calling hashCode() on two different String objects containing the same text?

The result will be the same hash code for both String objects, as the hashCode() implementation for String is based on the content of the string, not the object identity.
##### How does the hashCode() method work with null values in a HashMap?

HashMap treats null keys as a special case and typically assigns them to a specific bucket. The hashCode() method is not called on null keys since calling any method on null would result in a NullPointerException.
##### If you override equals(), why must you also override hashCode()?

You must override hashCode() when you override equals() to maintain the contract that equal objects must have the same hash code. If this contract is violated, objects that are equal might end up in different buckets in hash-based collections, leading to incorrect behavior.
##### How would you test a hashCode() implementation?

To test a hashCode() implementation, create multiple objects and verify that equal objects have the same hash code and that unequal objects ideally have different hash codes. Also, test the distribution of hash codes to ensure they are well-distributed across the integer range.
##### What is the impact of returning a constant value from hashCode()?

Returning a constant value from hashCode() means all objects will have the same hash code, leading to a high number of collisions in hash-based collections and degrading their performance to linear time complexity.
##### Can two unequal objects have the same hash code?

Yes, two unequal objects can have the same hash code. This is known as a collision. For example:

```
String s1 = "FB";
String s2 = "Ea";
System.out.println(s1.hashCode() == s2.hashCode()); // true 
```
Despite s1 and s2 being unequal, their hash codes are the same due to how the hash code is calculated for strings.
##### How does the default hashCode() implementation in the Object class generate the hash code?
The default hashCode() implementation in the Object class is native and typically uses the memory address where the object is stored. However, the exact algorithm is not specified and can vary between JVM implementations.
##### If you override hashCode() but not equals(), how will it affect a HashSet?
If you override hashCode() but not equals(), the HashSet may treat objects that are logically equal as different because the equals() method still uses the default identity-based comparison from the Object class.
##### Explain how the hashCode() method is used in a HashMap.
In a HashMap, the hashCode() method is used to determine the bucket where an entry (key-value pair) should be stored. The hash code is used to narrow down the search when retrieving or storing an entry, which allows for efficient O(1) time complexity.
##### What is the significance of the number 31 in hashCode() implementations?
The number 31 is a prime number, which helps in distributing the hash codes more evenly. It also has the benefit of being easily computable by shifting and subtracting (31 * i == (i << 5) - i) and thus can be performed efficiently by the JVM.
##### How can you ensure a good distribution of hash codes for objects in a custom class?
To ensure a good distribution of hash codes, use a combination of fields that uniquely identify the object's state, and combine them using a consistent algorithm that mixes the bits of the hash codes, often involving prime numbers.
##### What could be the consequence of a hashCode() method that relies on mutable fields?
If hashCode() relies on mutable fields, the hash code of an object can change if those fields are modified after the object is placed in a hash-based collection, potentially leading to the object not being findable in the collection.
##### How do you handle hashCode() in a class hierarchy?
In a class hierarchy, you should include the superclass's hash code in the calculation of the subclass's hash code. One common approach is to call super.hashCode() and combine it with the subclass's significant fields.
##### Provide an example of a hashCode() method that uses lazy initialization.
A hashCode() method using lazy initialization calculates the hash code the first time it is called and caches the result for subsequent calls. This can improve performance if calculating the hash code is expensive and the method is called frequently.
##### Discuss the thread-safety of hashCode().
The thread-safety of hashCode() depends on the immutability of the fields used in its calculation. If the object's state does not change after construction, then hashCode() is thread-safe. Otherwise, synchronization or other concurrency controls may be necessary.
##### Given a class with array fields, how would you implement hashCode()?
For a class with array fields, you would need to consider the elements of the array in the hash code calculation. You could use Arrays.hashCode(arrayField) for each array field and combine these results following the standard hash code pattern.

### coding problems
##### Implement a hashCode() method for a Point class with x and y integer coordinates. 
Code:
```
public class Point {
    private int x;
    private int y;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return 31 * x + y;
    }
}
```
##### Write a hashCode() method for a Person class with firstName and lastName fields.
Code:
```
public class Person {
    private String firstName;
    private String lastName;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(firstName, lastName);
    }
}
```
##### How would you handle hashCode() for a Book class with a List<String> of authors?
Code:
```
public class Book {
    private String title;
    private List<String> authors;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(title, authors);
    }
}
```
##### Create a hashCode() method for a Rectangle class that avoids collisions for rectangles with the same area but different dimensions.
Code:
```
public class Rectangle {
    private int width;
    private int height;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(width, height);
    }
}
```
##### Implement hashCode() for a User class that includes a unique id field.
Code:
```
public class User {
    private String id;
    private String name;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return id.hashCode();
    }
}
```
##### How would you write a hashCode() method for a Vehicle class with make, model, and year fields?
Code:
```
public class Vehicle {
    private String make;
    private String model;
    private int year;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(make, model, year);
    }
}
```
##### Design a hashCode() method for a Circle class that uses the radius field.
Code:
```
public class Circle {
    private double radius;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Double.hashCode(radius);
    }
}
```
##### Write a hashCode() method for an Employee class that combines employeeId and department.
Code:

```
public class Employee {
    private int employeeId;
    private String department;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(employeeId, department);
    }
}
```
##### How can you ensure that the hashCode() method for a Product class with a BigDecimal price field is consistent with equals()?
Code:
```
public class Product {
    private String name;
    private BigDecimal price;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(name, price.stripTrailingZeros());
    }
}
```
##### Implement hashCode() for a TreeNode class with value and children fields.
Code:
```
public class TreeNode {
    private Object value;
    private List<TreeNode> children;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(value, children);
    }
}
```
##### Create a hashCode() method for a Matrix class that accounts for a two-dimensional array of integers.
Code:
```
public class Matrix {
    private int[][] data;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Arrays.deepHashCode(data);
    }
}
```
##### Write a hashCode() method for a Graph class that includes a Set<Node> of nodes.
Code:
```
public class Graph {
    private Set<Node> nodes;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(nodes);
    }
}
```
##### How would you implement hashCode() for a Color class with red, green, and blue integer fields?
Code:
```
public class Color {
    private int red;
    private int green;
    private int blue;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(red, green, blue);
    }
}
```
##### Design a hashCode() method for a Flight class that includes origin, destination, and flightNumber.
Code:
```
public class Flight {
    private String origin;
    private String destination;
    private String flightNumber;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(origin, destination, flightNumber);
    }
}
```
##### Implement hashCode() for a MusicTrack class with title, artist, and duration fields.

Code:
```
public class MusicTrack {
    private String title;
    private String artist;
    private int duration;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(title, artist, duration);
    }
}
```
##### Create a hashCode() method for a Pair generic class with first and second fields.
Code:
```
public class Pair<F, S> {
    private F first;
    private S second;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(first, second);
    }
}
```
##### Write a hashCode() method for a BankAccount class that includes accountNumber and balance.
Code:
```
public class BankAccount {
    private String accountNumber;
    private BigDecimal balance;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(accountNumber, balance.stripTrailingZeros());
    }
}
```
##### How would you implement hashCode() for a TimeSlot class with startTime and endTime LocalTime fields?

Code:
```
public class TimeSlot {
    private LocalTime startTime;
    private LocalTime endTime;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(startTime, endTime);
    }
}
```
##### Design a hashCode() method for a Tag class that uses a String name field.
Code:
```
public class Tag {
    private String name;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return name.hashCode();
    }
}
```
##### Implement hashCode() for a Dimension class with width and height fields, ensuring a unique hash code for each unique dimension.
Code:
```
public class Dimension {
    private int width;
    private int height;

    // Constructor, getters, and setters

    @Override
    public int hashCode() {
        return Objects.hash(width, height);
    }
}
```
