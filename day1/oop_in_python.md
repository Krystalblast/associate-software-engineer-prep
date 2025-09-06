# 🐍 Python 3 Object-Oriented Programming — Summary  

## 1. What is OOP?
- **OOP = Object-Oriented Programming** → Programming with *objects* (attributes + methods).  
- Helps make code **organized**, **reusable**, and **extensible**.  

---

## 2. Classes and Instances
- **Class** = blueprint  
- **Instance** = object created from a class  

```python
class Dog:
    def __init__(self, name):
        self.name = name

dog1 = Dog("Buddy")
print(dog1.name)  # Buddy
```

---

## 3. Attributes and Methods
- **Attributes** = variables inside objects  
- **Methods** = functions inside objects  

```python
class Dog:
    species = "Canis familiaris"  # class attribute
    
    def __init__(self, name, age):
        self.name = name          # instance attribute
        self.age = age

    def speak(self, sound):
        return f"{self.name} says {sound}"

dog = Dog("Buddy", 3)
print(dog.speak("Woof"))  # Buddy says Woof
```

---

## 4. Inheritance
- Subclasses can **reuse** or **override** parent class methods.  

```python
class Dog:
    def speak(self, sound):
        return f"Dog says {sound}"

class Beagle(Dog):
    def speak(self, sound="Arf"):
        return super().speak(sound)

dog = Beagle()
print(dog.speak())  # Dog says Arf
```

---

## 5. Encapsulation
- Hide internal details inside objects.  
- Use `_` (protected) or `__` (private) by convention.  

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # private
    
    def deposit(self, amount):
        self.__balance += amount
        return self.__balance
```

---

## 6. Polymorphism
- Different classes can share method names with different behavior.  

```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

animals = [Dog(), Cat()]
for a in animals:
    print(a.speak())
# Woof!
# Meow!
```

---

## 7. Special Methods
- Customize object behavior using methods like `__str__`, `__len__`.  

```python
class Book:
    def __init__(self, title):
        self.title = title
    def __str__(self):
        return f"Book: {self.title}"

print(Book("Python 101"))  # Book: Python 101
```

---

## ✅ Key Takeaways
- Use **classes/objects** to organize code.  
- Use **inheritance** to reuse code.  
- Use **encapsulation** to control data access.  
- Use **polymorphism** for flexibility.  
- Use **special methods** to integrate with Python built-ins.  

---

## Reference
- [Real Python — Python 3 Object-Oriented Programming](https://realpython.com/python3-object-oriented-programming/)
