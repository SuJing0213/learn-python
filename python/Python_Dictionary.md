# Dictionary

### 基本概念

在Python中字典是一系列**键-值**对。每一个**键**都与一个**值**相关联,可以使用键来访问与之相关联的值。

> 键的类型：一个对象能不能作为字典的key，就取决于其有没有__hash__方法。所以所有python自带类型中，目
>         	   前已知的除了list、dict、set和内部带有以上三种类型的tuple之外，其余的对象都能当key。而我 
>       		   们自己定义的类，一般情况下都直接间接的和object有关，都带有__hash__方法。                     
> 		   注意： tuple元组作为键时，其中不能以任何方式包含可变对象。 
>
> 值的类型：键关联的值可以是数字、字符串、列表等等，乃至字典。

使用花括号括起来所有键值对组成字典，键与值之间用冒号分隔，而键-值对之间用逗号分隔。

```
dict = {
	"key1" : "value1",
	"key2" : "value2"
	}

```



### 访问字典

##### 获取键值

要获取与键相关联的值，可依次指定字典名和放在方括号内的键。

```
value = dict[key]
```

访问字典时，先计算hash，找到相对应的那片内存空间，里面没有值的话就直接写入，对于字典来说就是新增键值对；如果里面已经有值了，那就判断新来的键和原来的那里的键是不是相等，相等就认为是一个键，对于字典来说就是更新值，不相等就再开空间，相当于字典新增键值对。

##### 添加键值

要添加键-值对，可依次指定字典名、用方括号括起来的键和相关联的值。

```
dict[new_key] = new_value
```

##### 修改键值

要修改键-值对，可依次指定字典名、用方括号括起来的键和新的相关联的值。

```
dict[key] = new_value
```

##### 删除键值

对于字典中不再需要的信息，可使用 del 语句将相应的键-值对彻底删除。使用 del 语句时，必须指定字典名和要删除的键。

```
del  dict[del_key]
```

### 遍历字典

##### 遍历所有的键值对

```
for  key,value  in  dict.items():
	use key,value do something 
```

字典中的方法 items()，它返回一个键-值对列表。

遍历字典时，键-值对的返回顺序也与存储顺序不同。Python不关心键-值对的存储顺序，而只跟踪键和值之间的关联关系。

##### 遍历字典中所有键

```
for key in dict.keys():
	use key do something
```

遍历字典时，会默认遍历所以键。上边的代码等效于：

```
for key in dict:
	use key do something
```

方法  keys() 返回一个包含字典中的所有键的列表。返回顺序与存储顺序不同。

在需要遍历字典键时，显示地使用方法keys()可让代码更容易理解。

##### 遍历字典中所有值

```
for value in dict.values():
	use value do something
```

方法 values() 返回一个值列表，而不包含任何键。返回顺序与存储顺序不同。

此方法返回的列表可能存在大量的重复项。可使用集合 set 。集合类似于列表，但每个元素都必须是独一无二的。

```
set(dict.values())
```

##### 按一定的顺序遍历字典中的所有键

可以使用方法 sorted() 对返回的键列表进行排序

```
sorted(dict.keys())
```

<!--*sorted()方法的参数：  cmp：用于比较的函数，比较什么由key决定,有默认值，迭代集合中的一项;  key：用列表元素的某个属性和函数进行作为关键字，有默认值，迭代集合中的一项;  reverse：reverse = True 升序（默认） 或者 reverse = False 降序。*--> 

### 嵌套

##### 字典列表

经常需要在列表中包含大量的字典，而其中的每个字典都包含特定对象的众多信息。

在这个列表中，所有的字典的结构都相同，因此可以遍历这个列表，并以相同的方式处理其中的每个字典。

```
#for example:
user_1 = {  'name' : x,  'id' : 1}
user_2 = {  'name' : y,  'id' : 2}
user_3 = {  'name' : z,  'id' : 3}

users = [user_1, user_2, user_3]
```

##### 字典中存储列表

每当需要在字典中将一个键关联到多个值时，可以使用列表作为字典中值。

##### 字典中存储字典

当一个数据集合中拥有多个对象，每个对象拥有多个属性，每个属性都有对应的值时，可以使用字典嵌套来组织数据。

```
scores = {
	‘xiaoming’  : {
		'Math' : 0,
		'English' : 100,
		},

	‘xiaohong’  : {
		'Math' : 50,
		'English' : 50,
		},
	}

```

