第一周笔记

由于已经之前安装好了IDEA，所以笔记分为三部分：
1.运行第一节课对应的示例代码
2.学习JAVA8新特性，先理解较为简单的几个特性
3.创建github仓库和本地仓库

一、Java-basics-codes
1.DataTypeDemo
	(1)直接定义变量：
		float myFloatNum = 5.99f;
	(2)每个基本类型都有对应的封装类：
		Float myFloatNum2= 5.99f;
	(3)类型转换：
		自动转换：int myInt = 5;	double myDouble = myInt;
		强制转换：double myDouble = 12.2d;		int myInt = (int) myDouble;
	(4)字符串：
		String greeting = "Hello world";
		字符串连接：System.out.println("myInt="+ myInt);
		
2.ArrayDemo
	(1)定义数组：
		String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
	(2)数组长度：
		System.out.println(cars.length);
	(3)for-each循环
		for (String car : cars) {
            System.out.println(car);
        }
	(4)二维数组：
		int[][] myNumbers = { {1, 2, 3, 4}, {5, 6,7} };
		
3.ooDemo
	(1)抽象类：提取子类的共同特征
		public abstract class Animal {
			String name;

			public Animal() {
				name = "Animal";
			}
			public abstract void eat();		//子类一定要实现父类的抽象方法

			public void sleep(){			//子类可以重写父类中的非抽象方法
				System.out.println(name+"正在睡");
			}
		}
	(2)接口类：用来表示公共行为。java没有多继承，可以通过接口实现。
		public interface Flyable {
			void fly();
		}
	(3)多态：编译看左边，实现看右边
		Animal[] animals = new Animal[]{
             new Animal(),new Bird(),new Mouse()
        };
        for(Animal animal:animals){
            animal.eat(); //根据不同的对象类型，调用不同的eat方法
        }
	(4)基于接口的多态：
		Flyable[] flyables = new Flyable[]{
                new Bird(),new AirPlane()	//必须实现Flyable接口，实现fly方法
        };
        for(Flyable flyable:flyables){
            flyable.fly(); //根据不同的对象类型，调用不同的fly方法
        }
	(5)接口作为参数：
		public static void startToFly(Flyable flyable){
			flyable.fly();
		}
		for(Flyable flyable:flyables){
            startToFly(flyable); //调用方法，传入接口类型变量
        }

4.ListDemo
	(1)定义：
		ArrayList<String> list=new ArrayList<>();
	(2)插入：
		list.add("World");
        list.add(0,"HAHAHAHA");
	(3)取值与查找：
		System.out.println(list.size());
        System.out.println(list.get(0));
        //判断是否包含某个元素,将逐个元素调用Equals方法对比，返回Boolean
        System.out.println(list.contains("World"));
	(4)遍历：
		//按下标
		for(int i=0;i<list.size();i++){
            System.out.println(list.get(i));
        }
		//for-each循环
		for (String str : list) {
            System.out.println(str);
        }
		
		//使用stream和lambda表达式进行遍历
        list.stream().forEach(item-> System.out.println(item));
	(5)排序：
		//使用lambda作为比较器，降序
		Collections.sort(list,(i1,i2)-> i2.compareTo(i1));
		
5.MapDemo
	(1)定义：
		Map<String, String> map = new HashMap<String, String>();
	(2)插入：
		map.put("1", "google");
	(3)遍历：
		//常用：二次取值，先获取key值，再获取key对应值
		for (String key : map.keySet()) {
            System.out.println("key= "+ key + " and value= " + map.get(key));
        }
		
		//容量大时尤其推荐：用entry获取每一整个键值对
        for (Map.Entry<String, String> entry : map.entrySet()) {
            System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
        }
		
二、Java8新特性之二
1.Lambda 表达式：Lambda 允许把函数作为一个方法的参数（函数作为参数传递到方法中）。
	//遍历输出：e为参数，类型由编译器推理得到
	Arrays.asList( "a", "b", "d" ).forEach( e -> System.out.println( e ) );
	//排序：list作为参数并接收返回值，返回值类型由编译器推理得到
	Collections.sort(list,(i1,i2)-> i2.compareTo(i1));
	
2.方法引用：方法引用使得开发者可以直接引用现存的方法、Java类的构造方法或者实例对象。
	//示例类
	public static class Car {
		public static Car create( final Supplier< Car > supplier ) {
			return supplier.get();
		}              

		public static void collide( final Car car ) {
			System.out.println( "Collided " + car.toString() );
		}

		public void follow( final Car another ) {
			System.out.println( "Following the " + another.toString() );
		}
		
		public void repair() {   
			System.out.println( "Repaired " + this.toString() );
		}
	}
	(1)构造函数引用：
		List< Car > cars = Arrays.asList( Car :: new );
	(2)静态方法引用：
		cars.forEach( Car::collide );
	(3)成员方法引用：
		//不接收参数
		cars.forEach( Car::repair );
	(4)实例对象的方法引用：
		final Car car = Car.create( Car::new );
		//接收一个Car类型的参数
		cars.forEach( car::follow );
		
三、创建github仓库和本地仓库
1.在github上创建一个公开仓库
2.在本地新建文件夹，进行git bash:
	git init
	git add .
	git commit -m "第一次提交"
	git branch -M main
	git remote add orgin https://github.com/hhtdgit/JAVAEE.git
	git push -u origin main
	
	如遇代理问题：
	git config --global https.proxy
	git config --global --unset https.proxy
