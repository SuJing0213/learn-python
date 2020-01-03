# Class

类是面向对象编程十分重要的概念，根据类来创建对象被称为实例化。

### 定义类

使用关键字 class 来定义一个类。在Python中，类的名称的首字母一般采用大写。

```
class Dog():
	"""
	类描述文档
	"""
	
	def __init__(self, name, age):
		"""初始化属性 name 和 age """
		self.name = name
		self.age = age
	
	def sit(self):
		"""模拟小狗蹲下"""
		print(self.name,title() + "is now sitting.")
```

一个类具有属性和方法。类中的函数称为方法。

##### 方法\__init__()

\_\_init\__() 方法是一个特殊的方法，每当使用类创建新实例时，Python都会自动运行它来初始化类属性值。因此类的属性值均定义在\_\_init__() 方法下，采用  **self.属性名** 的形式定义，通过向初始化器传递参数来初始化类属性的值。

在这个方法的定义中（包括其他所有的类方法）,形参 self 必不可少，还必须位于其他形参的前面。

> 因为Python在调用\_\_init\__() 方法创建实例时，将自动传入实参self。**每个与类相关联的方法调用都自动传递实参self**，它是一个指向实例本身的引用，让实例能够访问类中的属性和方法。

以 self 为前缀的变量（类属性）都可供类中的所有方法使用。



### 根据类创建实例

我们可以使用类名，以及传入\_\_init\__() 方法所需的参数来创建一个实例。

```
my_dog = Dog("BaPuNuoFuBenBa", 6)
```

##### 访问属性及方法

可以使用句点表示法来访问一个实例的属性和方法。

```
my_dog.name
my_dog.sit()
```

##### 给属性指定默认值

实例化一个类时，类中的每个属性都应该都初始值，哪怕这个值是0或者空字符串。有两种方式设置默认值。

```
#直接为属性设置默认值。如果这样做就无需包含为它提供初始值的形参。
#同样，创建任何实例时也无法改变这个初始值。所以不建议这样做。

class Dog():
	"""
	类描述文档
	"""
	
	def __init__(self, name, age):
		"""初始化属性 name 和 age """
		self.name = name
		self.age = age
		self.favorite = "meat"		#直接设置默认值
```

```
#为形参设置默认值。这样在实例化类对象时可以不传入具有默认值的参数值，此时，类属性被初始化为默认值。
#但当给具有默认值的形参传入具体值时，类属性为传入的实际值。

class Dog():
	"""
	类描述文档
	"""
	
	def __init__(self, name, age, favorite="meat"):
		"""初始化属性 name 和 age """
		self.name = name
		self.age = age
		self.favorite = favorite		#使用形参设置默认值
```

##### 修改属性的值

有时候我们需要修改属性的值。我们可以通过 1、直接访问实例的属性对其进行修改。2、通过方法对属性值进行修改。两种方式。

1、直接访问实例的属性对其进行修改。

```
my_dog.name = "BaPuNuoFuBenFu"
```

2、通过方法对属性值进行修改。

```
#添加对应属性的修改方法

class Dog():
	"""
	类描述文档
	"""
	
	def __init__(self, name, age, favorite="meat"):
		"""初始化属性 name 和 age """
		self.name = name
		self.age = age
		self.favorite = favorite		
	
	def sit(self):
		"""模拟小狗蹲下"""
		print(self.name,title() + "is now sitting.")
		
	def rename(self, new_name):
		self.name = new_name
		print("The dog has a new name.")
	
#通过类方法修改类属性
my_dog.rename("BaPuNuoFuBenFu")
```

通过方法修改属性的值具有一定的好处，这时候可以在类内部对传入的新值的参数进行一定的约束判断（安全控制），防止属性被赋予不满足实际情况的新值。比如年龄不能赋值为负数。



### 类的继承

如果需要编写的类是另一个现有类的特殊版本，可使用继承。一个类继承另一个类时，它将自动获得另一个类的所有属性和方法；原有的类称为父类，而新类称为子类。

```
#实例类，Car
class Car():
	"""模拟汽车的实例类"""
	
	def __init__(self, make, model, year):
		self.make = make
		self.model = model
		self.year = year
		self.odometer_reading = 0
	
	def read_odometer(self):
		print("This car has "+ str(self.odometer_reading) + "miles on it.")
		
	def update_odometer(self,mileage):
		if mileage >= self.odometer_reading:
			self.odometer_reading = mileage
		else:
			print("You can't roll back an odometer!")
```

##### 创建继承类

```
class ElectricCar(Car):
	"""电动汽车"""
	
	def __init__(self, make, model, year, battery_size):
		"""初始化父类的属性，然后初始化子类的新属性"""
		super().__init__(make, model, year)
		self.battery_size = battery_size
```

创建子类时，父类必须包含在当前文件中，且位于子类的前边。

定义子类时，必须在**括号内**指定父类的名称。

super() 是一个特殊的函数，可以将父类和子类关联起来。父类也称为超类（superclass）。

##### 重新父类方法与创建新方法

1、对于父类的方法，只要它不符合子类模拟的实物的行为，都可对其进行重写。即在子类中定义一个与要重写父类方法的同名方法。这样，Python将不会考虑这个父类方法，而只关注你在子类中定义的相应方法。

```
#重写父类方法
#假设Car类有一个 fill_gas_tank() 的方法，但它对电动汽车毫无意义，我们对其重写。
class ElectricCar(Car):
	"""电动汽车"""
	
	def __init__(self, make, model, year, battery_size):
		"""初始化父类的属性，然后初始化子类的新属性"""
		super().__init__(make, model, year)
		self.battery_size = battery_size
	
	def fill_gas_tank(self):
		print("This car doesn't need a gas tank!")
```

2、对于子类具有自己独特的行为，我们可以定义子类的新方法。

```
#定义子类对应行为的新方法
class ElectricCar(Car):
	"""电动汽车"""
	
	def __init__(self, make, model, year, battery_size):
		"""初始化父类的属性，然后初始化子类的新属性"""
		super().__init__(make, model, year)
		self.battery_size = battery_size
	
	def describe_battery(self):
		print("This car has a " + str(self.battery_size) +"-kWh battery.")
```



### 将实例用作属性

使用代码模拟实物时，你可能会发现自己给类添加的细节越来越多：属性和方法清单以及文件都越来越长。

在这种情况下，可能需要将类的一部分作为一个独立的类提取出来。可以将大型类拆分成多个协同工作的小类。

##### 属性初始化为类实例

```
#创建电池类
class Battery():
	
	def __init__(self, battery_size=70):
		self.battery_size = battery_size
	
	def describe_battery(self):
		print("This car has a " + str(self.battery_size) +"-kWh battery.")
```

```
#重新创建电动汽车类，将电池模块独立出来为一个类
class ElectricCar(Car):
	
	def __init__(self, make, model, year):
		"""初始化父类的属性，然后初始化子类的新属性"""
		super().__init__(make, model, year)
		
		#对battery初始化了一个Battery()的实例，也可以传递一个实例作为参数来初始化
		self.battery = Battery()
```



### 导入类

将不同的类存储在不同的模块中可以让文件尽可能整洁。在需要时导入当前模块。

##### 导入单个类

```
#car.py中存储了Car类的定义
from car import Car

my_new_car = Car("audi", "a4", 2016)
```









