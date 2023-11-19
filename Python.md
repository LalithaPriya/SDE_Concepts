Python:

• It supports procedure oriented and object oriented features, so gets benifits like both security and reusability ...
• Advantage of using EPONENTIAL form is we can represent big values in less memory.
    Ex: f = 1.2e3 --> 1200
        f = 1.2e-3 --> 0.0012
• we have complex datatype. 
    y = 4+5j (y = a+bj) --> a can be decimal, binary, octa, hexa . b --> only decimal

• s = "priya" --> s[2:40] ==> iya
              --> s[:]  ==> priya

• complex(3,5) ==> 3+5j

• All fundamental data types are immutable. Because in python, if a new object is required, then PVM wont create immediately. It will check if any object avilable with required data or not. If yes, then existing object will be reused. if not then a new object is created. MEMORY utilization and PERFORMANCE is improved.
    But with this concept, sevelar references are pointing to same object, by using one reference if we are allowed to change, then the remaining references are ceffected. To prevent this, immutable concpet is required.
    Ex: a = 10; b = 10; c= 11; id(a) == id(b); id(c)
        if a = a+1 then id(a) == id(c); id(b)
   
• bytes() --> datatype, we cannot modify 
• bytearray() --> datatype, we can modify elements

• set doesn't support indexing
    Ex: s= {1,4,34,5}
        print(s[1]) --> throws error
    
• list  --> append, remove
• tuple --> append, remove
• set   --> add, remove
• set --> mutable; frozenset --> immutable 
• print(10 or 20) // 10
  print(-40 or 20) // -40

  print(10 and 20) // 20
  print(-40 and 20) // 20
  print(0 and 20) // 0

• print(~ True) --> -2
  print(True << 2) --> 4 
  print(True >> 2) --> 0

• Use "is" operator for address comparison, where as == for content/ value comparison.
 
• Identity operators --> is , is not 
  Membership operators --> in, not in

• [NOT THERE in PYTHON 3] raw_input() --> always reads the data in the form of string
  input() --> used to read data directly in our required format. No need of type casting.

• eval() --> takes string and evaluate and returns the result
    Ex: eval("10+20-1") --> 29 returns in int or float

• command line arguments: from sys import argv    
    argv[0] --> name of program 
• If argument contains space, then enclosr using "" in the cmd

•  print(a,b,c) # 1 2 3
   print(a,b,c,sep = '::') # 1::2::3

•  print("a is %i", %a)
   print("a is %a and b is %b", %(a,b))   
   print("100/{} = {} ".format(n,100/n))

•   --> for printing pyramid:
    for i in range(1,n+1):
        print(" "*(n-i),end = '')
        print("* "*i)

•   loops with else block, here else block excecuted.
•   FOR loop --> repeate code for every item in sequence
•   while loop --> repeate code ad long as condition is true

•   "del" --> deletes the variable. corresponding object is eligable for garbage collection.
• instead of del, if we assign None, then we can still access variable, and also corresponding object is eligable for garbage collection.

• rstrip(), lstrip(), strip() --> remove spaces

• find() and rfind() --> find from last 
    find(substring, begin,end) -> to find in the specific range
• index() and rindex()
    index() throws an error if substring is not found, but find() will return -1.

•   Aliasing vs cloning
    Aliasing - variables refer to same object, change through any variable, happens to all variables referening to object 

    Cloning - create a duplicate object, through slicing or copy()

• iterator vs generator i.e return vs yield
    return --> it will provide the result after done the method/function
    yield --> will provide in between and several times if needed.
    ** return will store data, where with yield we can do operations on data one by one and no need to store.

• set() ---> 
    add() vs update() : in add() we can pass one argument. For update we can pass multiple arguments and each argument should be iterable


•   type of arguments in the function:
    1. formal arguments ---> def f1(a,b) : here a, b 
    2. actual arguments ---> f1(10, 20): here 10, 20

    Types of actual arguments:
    1. positional arguments: no of args and pos of args must be matched
    2. Keyword arguments: no of args must be matched and pos of args is not important. f1(b = 20, a =10)
    3. Default arguments: by providing default values for args like def say(name = "user"):
            print("hello ", name)
        say("priya") # hello priya
        say()        # hello user
    4. variable length args: we can declare a variable length args with * symbol 
        def f1(*n): --> range(0, n)
        ---> internally these values are represented in the form of tuple.

        def sum(*n):
            total = 0
            for i in n:
                total += i
            return total
        sum()
        sum(10)
        sum(10,20)
        sum(10,20,30,40)

        --> after variable length argument, if we are taking any other arguments then we should provide values as keyword arguments. 
        def sum(*n,tot):

        sum(10,20,30, tot = 11) --> valid
        sum(10,20,30,11) --> Invalid

    ==> we can declare keyword variable length arguments also.
        i.e by **
        def f1(**kw_args):
            for k, v in kw_args.items():
                print(k,v)

        f1(n1= 10, n2 = 20, n3 = 30)

    ------------

•   grp of lines      --> function
    grp of functions  --> module
    grp of modules    --> library

•   global vs local:
        a = 10
        def f1():
            a = 777
            print(a)
            print(globals()['a'])
        f1()
        
• lambda function -- anonymous and its just for an instant use
    greater = lambda a,b,c: a if a>b and a> c else (b if b>c else c)
    print(greater(2,3,5))

• we can use lambda functions very commanly with filter(), map() and reduce() functions because  these functions expect function as argument.

• filter() ---> filter values from given sequence based on condition. syntax: filter(function, sequence)
• map()   ----> by applying some functionality and generate new element with required modification. 
• reduce() ---> reduces sequence of elements into single element 

• function aliasing is possible i.e we can refer function with other name. As everything is internally treated as object in python, even functions also treated as objects in python.
• Even if we delete a function name then we can still access the function woth other name i.e alias name

• with normal import
    Issue in this way is, after loading a module if it is updated outside then updated version is not available in our program.
        so we will use reloading a module,  explicitly in our requirement. bu using reload()
        Ex: import module1 # runs 
            import module1 #wont as its already imported
            from imp import reload 
            reload(module1) # reload again
            reload(module1) # reload again

• We can find the members of module by using this dir()

• Reference variable is a variable which refers the object. With this we can access the variables i.e properties and also methods of object.

• setter methods also known as Mutator methods.
    def setVariable(self, variable):
        self.variable = variable
• getter methods also known as accessor methods.
    def getVariable(self):
        return self.variable

• class Methods: if we are using only class variables(static variables)
    declared by using @classmethod decorator
    should provide cls variable at the time of declaration
    can call class method by using class name or object         reference variable.

    class Sample:
        x = 4
        @classmethod
        def f1(cls, name):
            print("name: ", name, cls.x)
    Sample.f1("priya")

• Static Methods: generally these are utility methods, we wont use any class variables(static variables) or instance variables
    declared by using @staticmethod decorator
    should provide cls variable at the time of declaration
    can call class method by using class name or object         reference variable.

    class Sample:
        
        @staticmethod
        def sum(x,y):
            print("sum: ", x+y)
        @staticmethod
        def mul(x,y):
            print("sum: ", x*y)    
    Sample.sum(10,20)
    Sample.mul(10,20)

• Garbage collector: main objective is to destroy useless objects
    If an object doesnot have any reference variable then that object eligible for Garbage collection.
    --> By default GC is enabled.
        import gc
        gc.isenabled() --> returns true if GC is enabled.
        gc.disable() --> to disable GC explicitly.
        gc.enable() --> to enable GC explicitly.

•  try:
        risky code
    except:
        handling code
    finally:
        cleanup code

• only when os._exit(0) function is called, then finally block wont be executed.

•  If control entered in to try block then finally black will be executed. If not, then finally block will be executed.

• try-except-else-finally  

• finally without try is always invalid 
• we cannot write multiple finally blocks for same try  
• we cannot write else block without except block

• We use 'raise' keyword for customized exception.

class sampleException(Exception):
    def __init__(self, arg):
        self.msg = arg

if x>y:
    raise sampleException("message")

• Decorator: is a function which takes a function as arg and extend its functionality and returns the function with odified functionality.

Ex: @decor
    def func1(name):
        print("hello ", name)

    def decor(fun):
        def inner(name):
        if name == "John":
            print("hello john, Good morning")
        else:
            fun(name)
        return inner

    • with out decorator,
        decorfunn = decor(func1)

        func1("Nick")
        func1("Jonas") # with out decor
        decorfunn("John")  #with decor
        decorfunn("Anna")        

• Decorator Chaining, multiple decorator for same function.
    First inner decorator will work and then outer decorator.
    Ex: @decor1
        @decor
        def num():

• Generator --> its a function which generates a series of values, uses yield keyword to return value.

To generate first n numbers:
    
    def gen_n(num):
        n = 1
        while n <= num:
            yield n
            n += 1

    ls = gen_n(5)
    for i in ls:
        print(i) 
• Improves memory utilization and performance.
• Generators works great for web scraping and crawling.
    Web scraping aims to extract the data on web pages, and web crawling purposes to index and find web pages. Web crawling involves following links permanently based on hyperlinks. In comparison, web scraping implies writing a program computing that can stealthily collect data from several websites.

• Assertions --> used in debugging. advantage is  after fixing the error/bug we are not required to delete assertion statement, we can enable or disable assert. (print, we need to remove)

assert fun1(2) == 4, "square of 2 should be 4"

• The relation b/w object and its instance variables is always composition(strongly associated), where relation b/w object and static variables is Aggregation(weakly associated).

• when we are creating a child class object, then child class constructor will be executed. If the child class does not contain constructor then parent class constructer will be executed, but parent obj wont be created.

•  class C(p1, p2)
    If the same method is inherited from both parent classes, then python will always consider the ordeer of parent classes in the declaration of child class.

•  Hybrid inheritence is combination of all Single, Multi level, multiple and Hierarchical inheritence.

• Python wont support cyclic inheritence(and we obviously dont need that)
    class A(A): pass #Name error: name 'A' is not defined

• Method overloading is not possible in python. If we try to declare multiple methods with same name and different number of arguments then pyhton will consider only last method.
--> we can handle this, by either default arguments or with variable number of argument methods.

• Also constructer overloading is not possible.
• 
• 
