# Design-Patterns-in-Ruby


## The Factory Method Pattern

The Factory Method pattern is a creational design pattern that allows you to create objects without having to specify the exact class of the object that will be created. 
This makes it easier to create new types of objects without having to modify the existing code.

```ruby
class VehicleFactory
  def create_vehicle(type)
    case type
    when "car"
      return Car.new
    when "truck"
      return Truck.new
    else
      raise ArgumentError, "Unknown vehicle type: #{type}"
    end
  end
end

vehicle_factory = VehicleFactory.new
car = vehicle_factory.create_vehicle("car")

```

## The Abstract Factory Pattern

```ruby
class ShapeFactory
  def create_shape(type)
    case type
    when "circle"
      return Circle.new
    when "rectangle"
      return Rectangle.new
    else
      raise ArgumentError, "Unknown shape type: #{type}"
    end
  end
end

class Circle
  def draw
    puts "Drawing a circle."
  end
end

class Rectangle
  def draw
    puts "Drawing a rectangle."
  end

shape_factory = ShapeFactory.new

# Create a new circle
circle = shape_factory.create_shape("circle")
circle.draw

# Create a new rectangle
rectangle = shape_factory.create_shape("rectangle")
rectangle.draw
```
## The Singleton Pattern

The Singleton pattern is a design pattern that ensures that only one instance of a class exists. This can be useful for classes that manage resources, such as database connections or logging systems.

The Singleton pattern works by defining a private constructor for the class. This prevents other classes from creating new instances of the class directly. Instead, there is a public method that returns the single instance of the class.

``` ruby

class DatabaseConnection
  private_class_method :new

  def self.instance
    @instance ||= new
  end

  def connect
    # Connect to the database
  end

  def disconnect
    # Disconnect from the database
  end
end
```

## The Adapter Pattern in Ruby

The Adapter pattern is a structural design pattern that allows objects with incompatible interfaces to work together.


```ruby

# Target: The expected interface that the client uses
class Target
  def request
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end
end

# Adaptee: The class that has an incompatible interface
class Adaptee
  def specific_request
    "Adaptee's specific request"
  end
end

# Adapter: Adapts the Adaptee's interface to the Target's interface
class Adapter < Target
  def initialize(adaptee)
    @adaptee = adaptee
  end

  def request
    @adaptee.specific_request
  end
end

# Client code using the Target interface
def client_code(target)
  target.request
end

# Creating instances
adaptee = Adaptee.new
adapter = Adapter.new(adaptee)

# The client can now use the Adapter, which adapts the Adaptee's interface
client_code(adapter)
# Output: "Adaptee's specific request"

```
## The Delegation pattern in Ruby

Delegation in Ruby is a design pattern that allows you to delegate the responsibility for handling a task to another object. 

```ruby
# For example, the following code delegates the print method call to the console object:
console = Console.new

# Explicit delegation
console.print("Hello, world!")
# For example, the following code delegates the print and puts methods to the console object:
console = Console.new

# Implicit delegation
delegate :print, :puts, to: console

# This will delegate the print method call to the console object
print("Hello, world!")

# This will delegate the puts method call to the console object
puts("Hello, world!")



```

