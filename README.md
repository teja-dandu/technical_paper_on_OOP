# technical_paper_on_OOP



<!--
**teja-dandu/teja-dandu** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
# Python OOP Concepts
 * In python object oriented programming(OOP) paradigm uses objects and classes in programming. the following concepts are extremely useful while solving problems
 * In python everything is object
 
## Concepts: 
<!--ts-->
  #### - [Classes Instances](#classes-instances)
  #### - [Class Variables](#class-variables)
  #### - [Classmethods Staticmethods](#classmethods-staticmethods)
  #### - [Inheritance](#inheritance)
  #### - [Special Methods](#special-methods)
  #### - [Property Decorators](#property-decorators)
<!--te-->




## **Classes Instances**


Class is the collections of objects . class contains blueprints or protype from which the objects are being created. it is logically entity contains
Some attributes and methods
The following code snippet explains the how to create a class and its variabls and their methods 

```
class Employee:

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

emp_1 = Employee('Dandu', 'Teja', 50000)
emp_2 = Employee('Test', 'Employee', 60000)
```
## **Class Variables**

```
class Employee:

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

emp_1 = Employee('Dandu', 'Teja', 50000)
emp_2 = Employee('Test', 'Employee', 60000)
```

## **Classmethods Staticmethods**
Class methods are methods that automatically take the class as the first argument. 
Class methods can also be used as alternative constructors. Static methods do not take the instance or the class as the first argument. 
They behave just like normal functions, yet they should have some logical connection to our class

```

class Employee:

    num_of_emps = 0
    raise_amt = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

        Employee.num_of_emps += 1

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)

    @classmethod
    def set_raise_amt(cls, amount):
        cls.raise_amt = amount

    @classmethod
    def from_string(cls, emp_str):
        first, last, pay = emp_str.split('-')
        return cls(first, last, pay)

    @staticmethod
    def is_workday(day):
        if day.weekday() == 5 or day.weekday() == 6:
            return False
        return True


emp_1 = Employee('Dandu', 'Teja', 50000)
emp_2 = Employee('Test', 'Employee', 60000)

Employee.set_raise_amt(1.05)

print(Employee.raise_amt)
print(emp_1.raise_amt)
print(emp_2.raise_amt)

emp_str_1 = 'John-Doe-70000'
emp_str_2 = 'Steve-Smith-30000'
emp_str_3 = 'Jane-Doe-90000'

first, last, pay = emp_str_1.split('-')

#new_emp_1 = Employee(first, last, pay)
new_emp_1 = Employee.from_string(emp_str_1)

print(new_emp_1.email)
print(new_emp_1.pay)

import datetime
my_date = datetime.date(2022, 7, 03)

print(Employee.is_workday(my_date))
```
## **Inheritance**

The following code snippet deals about the inheritance  & creating subclasses. Inheritance is allow us to inherite attributes and methods from a parent class.
This is useful because we can create subclasses and get all of the functionality of our parents class, 
And have the ability to overwrite or add completely new functionality without affecting the parents class in any ways.

```

class Employee:

    raise_amt = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)


class Developer(Employee):
    raise_amt = 1.10

    def __init__(self, first, last, pay, prog_lang):
        super().__init__(first, last, pay)
        self.prog_lang = prog_lang


class Manager(Employee):

    def __init__(self, first, last, pay, employees=None):
        super().__init__(first, last, pay)
        if employees is None:
            self.employees = []
        else:
            self.employees = employees

    def add_emp(self, emp):
        if emp not in self.employees:
            self.employees.append(emp)

    def remove_emp(self, emp):
        if emp in self.employees:
            self.employees.remove(emp)

    def print_emps(self):
        for emp in self.employees:
            print('-->', emp.fullname())


dev_1 = Developer('Dandu', 'Teja', 50000, 'Python')
dev_2 = Developer('Test', 'Employee', 60000, 'Java')

mgr_1 = Manager('Sue', 'Smith', 90000, [dev_1])

print(mgr_1.email)

mgr_1.add_emp(dev_2)
mgr_1.remove_emp(dev_2)

mgr_1.print_emps()

```
## **Special Methods**

The following code deals about the special methods. called magic methods or dunder methods. this methods allow us to emulate built-in types or implement operator
Overloading. this will be extremely powerful if you used correctly. 
Some of them are used from Standard Library like,  ___repr___ , ___str___ ,and more also user defined special methods of our own like and ___add___ .

```

class Employee:

    raise_amt = 1.04

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.email = first + '.' + last + '@email.com'
        self.pay = pay

    def fullname(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)

    def __repr__(self):
        return "Employee('{}', '{}', {})".format(self.first, self.last, self.pay)

    def __str__(self):
        return '{} - {}'.format(self.fullname(), self.email)

    def __add__(self, other):
        return self.pay + other.pay

    def __len__(self):
        return len(self.fullname())


emp_1 = Employee('Dandu', 'Teja', 50000)
emp_2 = Employee('Test', 'Employee', 60000)

# print(emp_1 + emp_2)

print(len(emp_1))

```
## **Property Decorators**

This following code snippet deals about the decorator. the property decorator allows us to define Class methods we can access like attributes. this allow us to
Implement getters, setters, and deletors.

```

class Employee:

    def __init__(self, first, last):
        self.first = first
        self.last = last

    @property
    def email(self):
        return '{}.{}@email.com'.format(self.first, self.last)

    @property
    def fullname(self):
        return '{} {}'.format(self.first, self.last)
    
    @fullname.setter
    def fullname(self, name):
        first, last = name.split(' ')
        self.first = first
        self.last = last
    
    @fullname.deleter
    def fullname(self):
        print('Delete Name!')
        self.first = None
        self.last = None


emp_1 = Employee('John', 'Smith')
emp_1.fullname = "Dandu Teja"

print(emp_1.first)
print(emp_1.email)
print(emp_1.fullname)

del emp_1.fullname

```
### _BuildWith_
* <a href="https://python.org/teja-dandu">Python Programming</a>

### _Authors_
* 📫 <a href="https://github.com/teja-dandu">@teja-dandu</a>


### _Acknowledgement_
 * References : <a href="https://www.amazon.com/gp/product/1491946008/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491946008&linkCode=as2&tag=coreyms-20&linkId=39335cdc340fb7ce5bd51d59c57e7e54">Fluent-Python</a>

##### _License_
 * MIT License

