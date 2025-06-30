SINGLETON BROOO


using System;
using System.Threading;


class Singleton//not thread safe
{
    private static Singleton single;
    private static readonly object lockobj=new object();
    public static Singleton CreateInstance()
    {
        if(single==null)
        {
            lock(lockobj)
            {
                if(single==null)
                {
                    Console.WriteLine("Created singleton object\n");
                    single=new Singleton();
                }
            }
			return single;
        }
        return single;
    }
}
class HelloWorld {
  static void Main() {
      Thread thread=new Thread(()=>Singleton.CreateInstance());
      Thread thread2=new Thread(()=>Singleton.CreateInstance());
      Thread thread4=new Thread(()=>Singleton.CreateInstance());
      thread.Start();
      thread2.Start();
      thread4.Start();
  }
}


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
FACTORY PATTERN




using System;

public interface IVehicle
{
    void drive();
}

public class Car:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the car\n");
    }
}
public class Bike:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the bike\n");
    }
}
public class Truck:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the truck\n");
    }
}

public class VehicleFactory
{
    
    public static IVehicle CreateVehicle(string str)
    {
        switch(str)
        {
            case "car":
                return new Car();
            case "bike":
                return new Bike();
            case "truck":
                return new Truck();
            default:
                Console.WriteLine("Invalid Option\n");
                break;
        }
        return null;
    }
}

public class HelloWorld
{
    static void Main()
    {
        
        IVehicle car=VehicleFactory.CreateVehicle("car");
        IVehicle bike=VehicleFactory.CreateVehicle("bike");
        IVehicle truck=VehicleFactory.CreateVehicle("truck");
        IVehicle invalid=VehicleFactory.CreateVehicle("trucefeuhd");
        car.drive();
        bike.drive();
        truck.drive();
        
    }
}


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

ABSTRACT FACTORY PATTERN


using System;

public interface IVehicle
{
    void drive();
}
public interface IVehicleFactory
{
    IVehicle CreateVehicle(string str);
}


public class Car:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the car\n");
    }
}
public class Bike:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the bike\n");
    }
}
public class Auto:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the Autok\n");
    }
}

public class Tricycle:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the Tricycle\n");
    }
}
public class Cycle:IVehicle
{
    public void drive()
    {
        Console.WriteLine("Driving the Cycle\n");
    }
}

public class AsiaVehicleFactory:IVehicleFactory
{
    
    public IVehicle CreateVehicle(string str)
    {
        switch(str)
        {
            case "two":
                return new Bike();
            case "three":
                return new Auto();
            case "four":
                return new Car();
            default:
                Console.WriteLine("Invalid Option\n");
                break;
        }
        return null;
    }
}

public class USVehicleFactory:IVehicleFactory
{
    
    public IVehicle CreateVehicle(string str)
    {
        switch(str)
        {
            case "two":
                return new Cycle();
            case "three":
                return new Tricycle();
            case "four":
                return new Car();
            default:
                Console.WriteLine("Invalid Option\n");
                break;
        }
        return null;
    }
}

public class HelloWorld
{
    static void Main()
    {
        IVehicleFactory asiafactory=new AsiaVehicleFactory();
        IVehicleFactory usfactory=new USVehicleFactory();
        
        IVehicle asiatwo=asiafactory.CreateVehicle("two");
        IVehicle asiathree=asiafactory.CreateVehicle("three");
        IVehicle asiafour=asiafactory.CreateVehicle("four");
        IVehicle invalid=asiafactory.CreateVehicle("trucefeuhd");
        
        IVehicle ustwo=usfactory.CreateVehicle("two");
        IVehicle usthree=usfactory.CreateVehicle("three");
        IVehicle usfour=usfactory.CreateVehicle("four");
        IVehicle invalid2=usfactory.CreateVehicle("trucefeuhd");
        
        asiatwo.drive();
        asiathree.drive();
        asiafour.drive();
        
        ustwo.drive();
        usthree.drive();
        usfour.drive();
        
        
    }
}


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Builder PATTERN




using System;
using System.Collections.Generic;

public class Computer
{
    public string GPU;
    public string CPU;
    public string Motherboard;
    public string ram;
    public string harddisk;
    public string ssd;
    public string keyboard;
    public string mouse;
    public string monitor;
    public string mousepad;
    public string CDReader;
    public string liquidcooling;
    public string speaker;
}

public class ComputerBuilder
{
    public Computer computer=new Computer();
    
    public void SetGPU(string str)
    {
        computer.GPU=str;
    }
    public void SetCPU(string str)
    {
        computer.CPU=str;
    }
    public void SetMotherboard(string str)
    {
        computer.Motherboard=str;
    }
    public void SetMouse(string str)
    {
        computer.mouse=str;
    }
    public void SetMousePad(string str)
    {
        computer.mousepad=str;
    }
    
    public Computer Build()
    {
        return computer;
    }
}

public class ComputerDirector
{
    public ComputerBuilder builder;
    public ComputerDirector()
    {
        builder=new ComputerBuilder();
    }
    
    public void SetConfiguration(Dictionary<string,string> configuration)
    {
        foreach(string str in configuration.Keys)
        {
            if(str=="motherboard")
            builder.SetMotherboard(configuration[str]);
            else if(str=="CPU")
            builder.SetCPU(configuration[str]);
            else if(str=="GPU")
            builder.SetGPU(configuration[str]);
            else if(str=="Mouse")
            builder.SetMouse(configuration[str]);
        }
    }
    
    public Computer CreateComputer() 
    {
        return builder.Build();
    }
}

public class HelloWorld
{
    static void Main()
    {
        ComputerDirector director=new ComputerDirector();
        director.SetConfiguration(new Dictionary<string,string> {
            {"CPU","i9"},
            {"GPU","rtx4090"},
            {"Mouse","Razor"}
        });
        Computer computer=director.CreateComputer();
        Console.WriteLine(computer.CPU);
        Console.WriteLine(computer.GPU);
        Console.WriteLine(computer.mouse);
    }
}



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

PROTOTYPE PATTERN



using System;

abstract public class Shape
{
    public int X;
    public int Y;
    public string color;
    public Shape(){}
    public Shape(Shape shape)
    {
        this.X=shape.X;
        this.Y=shape.Y;
    }
    
    abstract public Shape Clone();
}

public class Circle:Shape
{
    public int radius;
    public Circle(){}
    public Circle(Circle circle):base(circle)
    {
        this.radius=circle.radius;
    }
    
    public override Shape Clone()
    {
        return new Circle(this);
    }
}

public class Rectangle:Shape
{
    public string length;
    public string breadth;
    public Rectangle(){}
    public Rectangle(Rectangle rectangle):base(rectangle)
    {
        this.length=rectangle.length;
        this.breadth=rectangle.breadth;
    }
    public override Shape Clone()
    {
        return new Rectangle(this);
    }
    
}

public class HelloWord
{
    static void Main()
    {
        Rectangle rectangle=new Rectangle();
        rectangle.X=1;
        rectangle.Y=2;
        rectangle.color="red";
        rectangle.length="12";
        rectangle.breadth="45";
        Rectangle anotherRectangle=rectangle.Clone() as Rectangle;
        Console.WriteLine(anotherRectangle.color);
        Console.WriteLine(anotherRectangle.X);
        Console.WriteLine(anotherRectangle.Y);
        Console.WriteLine(anotherRectangle.length);
        Console.WriteLine(anotherRectangle.breadth);
    }
}






----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


BRIDGE DESIGN PATTERN 


using System;

abstract public class Shape
{
    public Shape(){}
    abstract public double area();
}
public class Circle:Shape
{
    public int radius;
    public Circle(){}
    public Circle(int n)
    {
        this.radius=n;
    }
    public override double area()
    {
        return 3.14*this.radius*this.radius;
    }
}
public class Rectangle:Shape
{
    public int length;
    public int breadth;
    public Rectangle(){}
    public Rectangle(int length,int breadth)
    {
        this.length=length;
        this.breadth=breadth;
    }
    public override double area()
    {
        return this.length*this.breadth;
    }
}

//adding new options red and blue

//for that creating an abstraction
abstract public class Color
{
    public Shape shape;
    public Color(Shape shape)
    {
        this.shape=shape;
    }
    abstract public void fill();
}

//now creating concrete implementation

public class Red:Color
{
    public Red(Shape shape):base(shape){}
    public override void fill()
    {
        Console.WriteLine("filling red color in the shape area "+this.shape.area());
    }
}

public class Blue:Color
{
    public Blue(Shape shape):base(shape){}
    public override void fill()
    {
        Console.WriteLine("filling blue color in the shape area "+this.shape.area());
    }
}

public class HelloWorld
{
    
    static void Main()
    {
        Circle circle=new Circle(4);
        Rectangle rectangle=new Rectangle(5,6);
        Red red=new Red(circle);
        Blue blue=new Blue(rectangle);
        red.fill();
        blue.fill();
    }
}

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

DECORATOR BUILDER PATTERN


using System;

public interface IPizza
{
    string desription();
    int cost();
}
public class PizzaBase:IPizza
{
    public string desription()
    {
        return "PizzaBase ";
    }
    public int cost()
    {
        return 10;
    }
}

abstract public class PizzaDecorator:IPizza
{
    public IPizza pizza;
    public PizzaDecorator(IPizza pizza)
    {
        this.pizza=pizza;
    }
    public virtual string desription()
    {
        return "Decorator";
    }
    public virtual int cost()
    {
        return 0;
    }
}
public class Peparoni:PizzaDecorator
{
    public Peparoni(IPizza pizza):base(pizza){}
    
    public override string desription()
    {
        return this.pizza.desription()+"Peparoni ";
    }
    public override int cost()
    {
        return this.pizza.cost()+2;
    }
}

public class Onion:PizzaDecorator
{
    public Onion(IPizza pizza):base(pizza){}
    
    public override string desription()
    {
        return this.pizza.desription()+"Onion ";
    }
    public override int cost()
    {
        return this.pizza.cost()+5;
    }
}


public class HelloWorld
{
    
    static void Main()
    {
        IPizza pizza=new PizzaBase();
        IPizza pizzap=new Peparoni(pizza);
        IPizza pizzao=new Onion(pizzap);
        Console.WriteLine(pizzao.desription());
        Console.WriteLine(pizzao.cost());
    }
}



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

COMPOSITE DESIGN PATTERN

using System;
using System.Collections.Generic;

public interface IEmployee
{
    void display();
}
public class Subordinate:IEmployee
{
    public string name;
    public Subordinate(string str)
    {
        this.name=str;
    }
    
    public void display()
    {
        Console.WriteLine(this.name);
    }
}

public class Manager:IEmployee
{
    public string name;
    public List<IEmployee> subordinates=new List<IEmployee>();
    public Manager(string str)
    {
        this.name=str;
    }
    public void AddEmployee(IEmployee employee)
    {
        subordinates.Add(employee);
    }
    public void remove(IEmployee employee)
    {
        subordinates.Remove(employee);
    }
    public void display()
    {
        Console.WriteLine(name+"--");
        foreach(IEmployee employee in subordinates)
        {
            employee.display();
        }
    }
}
public class HelloWorld
{
    static void Main()
    {
        IEmployee employee=new Subordinate("Aditya");
        IEmployee employee2=new Subordinate("Manasa");
        IEmployee employee6=new Subordinate("Manasaaaa");
        IEmployee employee3=new Subordinate("Hema");
        Manager employee4=new Manager("Vijay");
        employee4.AddEmployee(employee);
        employee4.AddEmployee(employee2);
        Manager employee5=new Manager("Subbu");
        employee5.AddEmployee(employee3);
        employee5.AddEmployee(employee4);
        employee5.AddEmployee(employee6);
        employee5.display();
        
    }
}




----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

OBSERVER BEHAVEORAL PATTERN

using System;
using System.Collections.Generic;

public interface IObserver
{
    void ReceiveData(float temperature,float windspeed,float humidity);
    void display();
}

public class SubStationObserver:IObserver
{
    public float temperature;
    public float windspeed;
    public float humidity;
    public void ReceiveData(float temperature,float windspeed,float humidity)
    {
        this.temperature=temperature;
        this.windspeed=windspeed;
        this.humidity=humidity;
    }
    public void display()
    {
        Console.WriteLine("Main Station "+this.temperature+" "+this.windspeed+" "+this.humidity);
    }
}
public class SubAnotherStationObserver:IObserver
{
    public float temperature;
    public float windspeed;
    public float humidity;
    public void ReceiveData(float temperature,float windspeed,float humidity)
    {
        this.temperature=temperature;
        this.windspeed=windspeed;
        this.humidity=humidity;
    }
    public void display()
    {
        Console.WriteLine("Another station "+this.temperature+" "+this.windspeed+" "+this.humidity);
    }
}

public class Subject
{
    List<IObserver> observers=new List<IObserver>();
    
    public float temperature;
    public float windspeed;
    public float humidity;
    
    public void Add(IObserver observer)
    {
        this.observers.Add(observer);
    }
    public void Setvalues(float temperature,float windspeed,float humidity)
    {
        this.temperature=temperature;
        this.windspeed=windspeed;
        this.humidity=humidity;
        this.Notify();
    }
    public void Notify()
    {
        foreach(IObserver observer in observers)
        {
            observer.ReceiveData(temperature,windspeed,humidity);
            observer.display();
        }
    }
}

public class HelloWorld
{
    static void Main()
    {
        IObserver observer=new SubStationObserver();
        IObserver observer2=new SubStationObserver();
        IObserver observer3=new SubAnotherStationObserver();
        Subject subject=new Subject();
        subject.Add(observer);
        subject.Add(observer2);
        subject.Add(observer3);
        subject.Setvalues(1.2f,23.3f,3.4f);
    }
}



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------





using System;
 
class A
{
    public static int X = Print("Static X in A", 1);
    public int Y = Print("Instance Y in A", 2);
 
    static A()
    {
        Console.WriteLine("Static Constructor A");
    }
 
    public A()
    {
        Console.WriteLine("Instance Constructor A");
    }
 
    public static int Print(string msg, int value)
    {
        Console.WriteLine($"{msg}, Value = {value}");
        return value;
    }
}
 
class B : A
{
    public static int P = Print("Static P in B", 3);
    public int Q = Print("Instance Q in B", 4);
 
    static B()
    {
        Console.WriteLine("Static Constructor B");
    }
 
    public B()
    {
        Console.WriteLine("Instance Constructor B");
    }
}
 
class Program
{
    static void Main()
    {
        Console.WriteLine("Creating First Object:");
        B obj1 = new B();
 
        Console.WriteLine("\nCreating Second Object:");
        B obj2 = new B();
    }
}
 
output:
Creating First Object:
Static X in A, Value = 1
Static Constructor A
Static P in B, Value = 3
Static Constructor B
Instance Q in B, Value = 4
Instance Y in A, Value = 2
Instance Constructor A
Instance Constructor B
 
Creating Second Object:
Instance Q in B, Value = 4
Instance Y in A, Value = 2
Instance Constructor A
Instance Constructor B
