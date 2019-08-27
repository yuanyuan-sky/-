#Object
**Object类是所有类的超类**  

1. 可以使用Object类型的变量引用任何类型的对象
2. 在java中，只有基本类型不是对象

#equals
Object的equals方法是判断两个对象是否有相同的引用，即地址是否相同，String对象之所以能用equals方法判断两个字符串是否相等，是因为String类重写了Object的equals方法  
**getClass()方法，返回一个对象所属的包和class,new的哪个类就返回哪个类，多态对象.getClass()返回的是new 的类**  
**instance :多态对象 instance 父类|自身类，都返回true**  
**子类对象 instanceof 父类  返回true**  
**父类对象instanceof 子类   返回false**

	class  异常2.Test//class字符是固定的，异常是包名，Test是类名
	getClass().getName();//返回字符串；异常.Test；没有前面的class字符
	getSuperclass();获取父类的信息
	getName()和getSuperclass()要在getClass()后面使用

**如果一个类A重写了Object的equals方法，如果类A的子类B有自己的属性，则判断两个类B的对象是否相等时，类B需要重写equals方法，可以先调用父类A中的equals方法，判断与父类A中的域是否相等，再判断自己的域是否相等**

	//类A的equals方法
	@Override
	public boolean equals(Object obj) {
		if (this == obj) {//先判断地址是否相等
			return true;
		}
		if (obj == null) {
			return false;
		}
		if (this.getClass() != obj.getClass()) {   //这个地方为什么不用instanOf ？ 因为子类对象 instanceOf 父类  返回true
			return false;
		}
		Employee employee = (Employee) obj;

		return this.getName().equals(employee.getName()) && salary == salary && hireday.equals(hireday);
	}
	//子类B的equals方法
	@Override
	public boolean equals(Object obj) {
		if (!super.equals(obj)) {
			return false;
		}
		Manager manager=(Manager)obj;
		return this.bonus==manager.bonus;
	}

**用getClass还是用instanceOf**
如果两个对象只用比较父类的域相等，就认为这两个对象相等，则用instanceOf  
如果两个对象不光要父类的域相等，还要判断自己的域也相等才认为这两个对象是相等的，则要用getClass

	
**java语言规范要求equals方法具有以下特征**  
对于任意非空对象x、y、z

1. 自反性：，x.equals(x);返回true
2. 对称性：x.equals(y);返回true，y.equals(x);也是true
3. 传递性：x.equals(y);为true，y.equals(z);为true，则x.equals(z);为true
4. 一致性：如果x和y引用的对象没有发生变化，则反复调用x.equals(y)；返回的结果一致
5. x.equals(null);返回false

![avatar](..\imgs\3.png)

#hash code(散列码)
是Object的方法。是由对象导出的一个整型值。散列码是没有规律的。  
如果x和y是两个是两个不同的对象，x.hashCode()与y.hashCode()【基本上不会相同】。  
每一个对象都有一个默认的散列码，其值为对象的存储地址 （但不是地址） 
**如果重新定义equals方法，就必须重新定义hashCode方法，以便用户可以将对象导入到散列表中（后面学）**

hashCode()方法返回一个整型数值，也可以是负数

###Object.hashCode的通用约定
如果两个对象根据equals（）方法判断是相等的，那么这两个对象的hashCode（）方法的返回值必须相等。Object的hashCode方法是根据对象的地址生成的，也就是说，即使两个对象相等，他们的hashCode方法的返回值可能不同

	重写hashCode
	public int hashCode(){
		return 7 * name.hashCode()
			+ 11 * new Double(salary).hashCode()
			+ 13 * hireDay.hashCode
			//为什么乘一个数？跟散列有关，最好乘一个素数就可以，曾大哈希值的离散程度
	}
	//或者
	public int hashCode(){
		return 7 * Objects.hashCode(name)
			+ 11 * Double.hashCode(salary)//Double静态的hashCode,避免创建Double对象
			+ 17 * Objects.hashCode(hireDay)
	
	}
	//或者
	public int hashCode(){

		return Objects.hash(name,salary,hireDay);//这个方法会对各个参数调用Objects.hashCode()，并进行组合
	}

**equals与hashCode的定义必须一致，如果x.equals(y)返回true，那么x.hashCode()就必须与y.hashCode()具有形同的值，例如，如果Employee.equals比较的是雇员的ID，那么hashCode就需要散列ID，而不是姓名或存储地址**  
**如果存在数组类型的变量，可以使用Arrays.hashCode方法计算一个散列码，这个散列码由数组元素的散列码组成**  

int   .hashCode();//返回对象的散列码  
int   Objects.hash(Object...onject);//返回一个散列码，由提供的所有对象的散列码组合而得   
int   Objects.hashCode(object a);//返回a.hashCode(),a为null返回0   
int Integet.hashCode(int value);返回value的散列值；Boolean.hashCode(Boolean value)。。。8种基本类型  
int  Arrays.hashCode(type[] a);//返回数组a的基本类型，可以是任意数组

	