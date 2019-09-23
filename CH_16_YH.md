#16. ���÷��ǰ� ��Ʈ����Ʈ

## 16.1 ���÷���
- __���÷���__
: ��ü�� ���� ������ ���� ���, ���� �� ��ü�� ���� �̸�, ������Ƽ, �޼ҵ�, �ʵ�, �̺�Ʈ ����� ��� �� �ִ�.
- ������ �� �� �ִٸ� �������� �ν��Ͻ��� ���� �� �ֱ� ������ �� �ν��Ͻ��� �޼ҵ� ȣ���� �������� ����.
- Type������ ��� �ִ� ����: .Net���� ���Ǵ� ������ ������ ��� ����.
: ���� �̸�, �ҼӵǾ� �ִ� ����� �̸�, ������Ƽ ���, �޼ҵ� ���, �ʵ� ���, �̺�Ʈ ���, �� ������ ����ϰ� �ִ� �������̽��� ���.

## 16.1.1 Object.GetType() �޼ҵ�� Type Ŭ���� 
### Object ������ �޼ҵ� 
- ��� ������ ������ Object������ ������ �ִ� ���� �޼ҵ带 �����޾� ���� �ִ�.
1. Equals()
2. GetHashCode()
3. GetType()
4.ReferenceEquals()
5. ToString()

### GetType() �޼ҵ�
: NET�� ��� ������ ������ ������ Object�� �̿� Object.GetType()�޼ҵ带 ���� Type ������ ����� ��ȯ��. (Type type = a.GetType();)

### Type ���� 
Type ������ �޼ҵ� �� �Ϻο� �� ��ȯ ���� (MSDN ���̺귯���� System.Type�� �Ŵ��� ��)
![Type������ �޼ҵ�](./OOP/pic/CH_16_YH1jpg)
 

<details>
<summary>���� : Type ������ �޼ҵ� (GetFields()) ��� ����</summary>
<div markdown="1">

```C#
int a = 0;
Type type = a.GetType();
// �ʵ������� �������[ ] �޾� foreach�� ����.
FieldInfo[] fields = type.GetFields();  
foreach (FieldInfo field in fields)
    Console.WriteLine(��Type:{0}, Name:{1}��, field.FieldType.Name, field.Name); 
```

</div>
</details>

### �˻� �ɻ� ����
- �Ű������� System.Reflection.BindingFlags �������� �̿� 
: BindingFlags.Public, BindingFlags.NonPublic, BindingFlags.Instance, BindingFlags.Static ��
- BindingFlags �Ű� ������ ���� �ʴ� ������ �����ε� �Ǿ��ְ� �� ��쿡�� public ����� ��ȯ.

```
int a =0;
Type type = a.GetType();
//public �ν��Ͻ� �ʵ� ��ȸ
var fields1 = type.GetFields(BindingFlags.Public | BindingFlags.Instance); //FieldInfo[]�� �ȹް� var
```

<details>
<summary>__���� : Type ������ �޼ҵ� ��� ����__</summary>
<div markdown="1">

```
using System;
using System.Collections.Generic;
using System.Text;
using System.Reflection;

namespace GetType
{
    class MainApp
    {
        static void PrintInterfaces(Type type)
        {
            Console.WriteLine("-------- Interfaces -------- ");

            Type[] interfaces = type.GetInterfaces();
            foreach (Type i in interfaces)
                Console.WriteLine("Name:{0}", i.Name);

            Console.WriteLine();
        }       

        static void PrintFields(Type type)
        {
            Console.WriteLine("-------- Fields -------- ");

            FieldInfo[] fields = type.GetFields( 
                BindingFlags.NonPublic | 
                BindingFlags.Public | 
                BindingFlags.Static | 
                BindingFlags.Instance );

            foreach (FieldInfo field in fields)
            {
                String accessLevel = "protected";
                if ( field.IsPublic ) accessLevel = "public";
                else if ( field.IsPrivate) accessLevel = "private";

                Console.WriteLine("Access:{0}, Type:{1}, Name:{2}", 
                    accessLevel, field.FieldType.Name, field.Name);
            }

            Console.WriteLine();
        }

        static void PrintMethods(Type type)
        {
            Console.WriteLine("-------- Methods -------- ");

            MethodInfo[] methods = type.GetMethods();
            foreach (MethodInfo method in methods)
            {
                Console.Write("Type:{0}, Name:{1}, Parameter:", 
                    method.ReturnType.Name, method.Name);
                
                ParameterInfo[] args = method.GetParameters();
                for (int i = 0; i < args.Length; i++)
                {
                    Console.Write("{0}", args[i].ParameterType.Name);
                    if (i < args.Length - 1)
                        Console.Write(", ");
                }
                Console.WriteLine();
            }
            Console.WriteLine();
        }

        static void PrintProperties(Type type)
        {
            Console.WriteLine("-------- Properties -------- ");

            PropertyInfo[] properties = type.GetProperties();
            foreach (PropertyInfo property in properties)
                Console.WriteLine("Type:{0}, Name:{1}", 
                    property.PropertyType.Name, property.Name);

            Console.WriteLine();
        }

        static void Main(string[] args)
        {
            //int a = 0;
            string a = "";
            Type type = a.GetType();
            
            PrintInterfaces(type);
            PrintFields(type);
            PrintProperties(type);
            PrintMethods(type);            
        }
    }
}
```

- __�������̽� ���__: Type �������� ��ȯ ���� GetInterfaces()
- __�ʵ� ���__: FieldInfo[] �������� ��ȯ GetFields()
BindingFlags ������ public, NonPublic, static, instance
Fieldinfo �� (.Is~��) accessLevel : protected, public, private
- __�޼ҵ� ���__: MethodInfo[] �������� ��ȯ ���� .GetMethods()
 - ParameterInfo[] �������� ��ȯ ���� MethodInfo[] �� .GetParameters() �޼ҵ�
- __������Ƽ ���__ : PropertyInfo[]�������� ��ȯ���� GetProperties()

</div>
</details>

### __Object.GetType() �޼ҵ� ��ü__
- .GetType() �޼ҵ�� �ݵ�� ��ü�� �ν��Ͻ��� �־�� ȣ���� ����.( int a =0; �ߴ� ��ó�� �ν��Ͻ��� ����� �ʱ�ȭ �ؾ���)
- ���� typeof �����ڿ� Type.GetType() �޼ҵ带 ����ؼ� Type ������ ��ȯ ���� �� �ִ�.
- typeof ������ : ������ �ĺ��� ��ü�� �Ű� ������ ����.
- Type.GetType() �޼ҵ� : ������ ��ü �̸��� �Ű� ������ ���� (��, ���ӽ����̽�)

```
Type a = typeof(int);
Console.WriteLine(a.FullName);
Type b = Type.GetType(��System.Int32��);// ���ӽ����̽��� �����ϴ� ��ü �̸�.
Console.WriteLine(b.FullName);
```

## 16.1.2 ���÷����� �̿��ؼ� ��ü �����ϰ� �̿��ϱ�
- ���÷����� �̿��ؼ� Ư�� ������ �ν��Ͻ��� �����, �����͸� �Ҵ��ϸ�, �޼ҵ带 ȣ���Ѵ�.
- __����__ : �ڵ� �ȿ��� ��Ÿ�ӿ� Ư�� ������ �ν��Ͻ��� ���� �� �ִ�.
: �츮�� ���� �� ���α׷��� �������� ������ �� �ֵ��� ������ �� �ִ�.

### 1. �������� �ν��Ͻ� ����
- __System.Activator Ŭ����__
: ���÷����� �̿��� Ư�������� ���� �ν��Ͻ� ������ �� �ʿ�.
- __Activator.CreateInstance()__ 
: �ν��Ͻ��� ������� �ϴ� ������ Type ��ü(__typeof( )__)�� �Ű� ������ �ָ� �ν��Ͻ��� �����Ͽ� ��ȯ��.

```
object a = Activator.CreateInstance(typeof(int));
//object ����
```

- __Activator.CreateInstance() �Ϲ�ȭ ����__

```
List<int> list = Activator.CreateInstance<List<int>>();
```

```
class Profile {
public string Name { get; set; }
}
static void Main() { 
Type typeof(Profile);
Profile profile = (Profile)Activator.CreateInstance( type);
}

```
### 2. �������� ��ü�� ������Ƽ�� �� �Ҵ�

- __PropertyInfo Ŭ����__
: Type.GetProperties()�� ��ȯ ����
- PropertyInfo Ŭ������ SetValue(), GetValue() �޼ҵ�
: �� ȣ��, �Ҵ�
- __Type.GetProperties() �޼ҵ�__ : �� ������ ��� ������Ƽ�� PropertyInfo ������ �迭�� ��ȯ
- __Type.GetProperty() �޼ҵ�__ : Ư�� �̸��� ������Ƽ�� ã�� �� ������Ƽ�� ������ ���� �ϳ��� PropertyInfo ��ü���� ��ȯ.

<details>
<summary> ���� : �������� �޼ҵ� ȣ�� </summary>
<div markdown="1">

```C#
class Profile
{
public string Name { get; set; }
public string Phone { get; set; }
}
static void Main()
{
Type type = typeof(Profile);
Profile profile = (Profile)Activator.CreateInstance( type );

    profile.Name = ����������
profile.Phone = ��010-1234-5678��
    
MethodInfo method = type.GetMethod(��Print��);
method.Invoke( profile, null );

Propertyinfo name = type.GetProperty(��Name��);
PropertyInfo phone = type.GetProperty( ��Phone�� );

name.SetValue ( profile, ������ȣ��, null);
phone.SetValue( profile, ��123-4567��, null);

Console.WriteLine(��{0}, {1}��, name.GetValue( profile, null ), phone.GetValue( profile, null));
}
```

- PropertyInfo Ŭ������ ������Ƽ �Ӹ� �ƴ϶� �ε����� ������ ���� �� �ִ�. 
__.SetValue�� GetValue�� ������ �Ű� ����__ 
: �ε����� �ε����� ���� �ڸ�.

</div></details>



- __MethodInfo Ŭ������ Invoke() �޼ҵ�__
: MethodInfoŬ������ �������� �޼ҵ带 ȣ���ϴ� ���� ����

<details>
<summary> ���� : �������� �޼ҵ� ȣ�� </summary>
<div markdown="1">

```C#
class Profile
{
public string Name { get; set; }
public string Phone { get; set; }
Public void Print()
{
Console.Writeline(��{0}, {1}��, Name, Phone)
}
}
static void Main()
{
Type type = typeof(Profile);
Profile profile = (Profile)Activator.CreateInstance( type );
    profile.Name = ����������
profile.Phone = ��010-1234-5678��
    
MethodInfo method = type.GetMethod(��Print��);
method.Invoke( profile, null );
}
</div></details>

<details>
<summary> ���� : �������� ������Ƽ�� ���� ���, ȣ�� </summary>
<div markdown="1">

```C#
using System;
using System.Reflection;

namespace DynamicInstance
{
    class Profile
    {
        private string name;
        private string phone;
        public Profile()
        {
            name = ""; phone = "";
        }

        public Profile(string name, string phone)
        {
            this.name = name;
            this.phone = phone;
        }

        public void Print()
        {
            Console.WriteLine($"{name}, {phone}");
        }

        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        public string Phone
        {
            get { return phone; }
            set { phone = value; }
        }
    }

    class MainApp
    {
        static void Main(string[] args)
        {
            Type type = Type.GetType("DynamicInstance.Profile");
            MethodInfo methodInfo = type.GetMethod("Print");
            PropertyInfo nameProperty = type.GetProperty("Name");
            PropertyInfo phoneProperty = type.GetProperty("Phone");

            object profile = Activator.CreateInstance(type, "�ڻ���", "512-1234");            
            methodInfo.Invoke(profile, null);

            profile = Activator.CreateInstance(type);            
            nameProperty.SetValue(profile, "����ȣ", null);            
            phoneProperty.SetValue(profile, "997-5511", null);

            Console.WriteLine("{0}, {1}",
                nameProperty.GetValue(profile, null),
                phoneProperty.GetValue(profile, null));
        }
    }
}
```

</div></details>

## 16.1.3 ���� ��������
���÷����� �̿��� ���α׷� ���� �߿� ���ο� ������ ����� �� �� �ִ� ���.
### ���÷��ǿ����� emit
= ���α׷��� ���� �߿� ���� �� ������ CLR�� �޸𸮿� ���������١�
### Emit ���ӽ����̽� �����ϴ� Ŭ������
: �ڵ带 ����ٴ� �濡�� ��~Builder���� ���� �̸��� ���� �ִ�.

### ���ο� ������ ����� ���� (���� = Type)
1. System.AppDomain Ŭ������ AssemblyBuilder ��ü ����� : __DefineDynamicAssembly()__�� ����� �����
2. __DefineDynamicModule()__ �޼ҵ�� ������ ����� �ȿ� ��� �����
3. ModuleBuilder�� __DefineType()__�޼ҵ�� ������ ��� �ȿ� Ŭ����(����) �����
4. TypeBuilder Ŭ������ __DefineMethod()__ �޼ҵ�� ������ Ŭ���� �ȿ� �޼ҵ� ������ �����/ PropertyBuilder Ŭ������ __DefineProperty()__�� ������Ƽ ������ ����� 
:�Ű������� (���̸���, MethodAttribute, ��ȯ����, �Ű� ����)�� �ʿ�
[�޼ҵ� define : MethodAttributes.Public, ������Ƽ define : MethodAttributes.HasDefault �������
������Ƽ�� Set/Get �޼ҵ��� define�� Ư���� Attriibutes ��� ( MethodAttributes.Public | MethodAttribures.SpecialName | MethodAttributes.HideBySif ) ]
5. MethodBuilder Ŭ������ __GetILGenerator()__�� ���� IlGenerator��ü ����� 
6. ILGenerator ��ü�� __.Emit__ �̿� �ؼ� �޼ҵ尡 ������ �ڵ�(IL ��ɾ�) ä���
(OpCodes.Ldc_I4, i) : 32��Ʈ ���� ( I )�� ��� ���ؿ� ����
(OpCodes.Add) : ��꽺�ؿ� ��� �ִ� �ΰ��� ���� ������ ������ ����� �ٽ� ��� ���ÿ� �ֱ�
(OpCodes.Ldarg_i) : �ε��� i�� �ִ� �μ��� ��� �������� �ε�
(OpCOdes.Ldfld, FieldBuilder ��ü) ���� ��� ���ÿ� ������ �ִ� ��ü���� �ʵ��� ���� ã��.
(OpCodes.Stfld, FieldBuilder ��ü) ��ü ������ �������� �ʵ忡 ����� ���� �� ������ �ٲ�
(OpCodes.Ret) : ���ÿ� �ִ� ���� ��ȯ
- ildasm ��ɾ�� C#���� �ڵ带 ¥�� ��ȸ�غ��� IL�ڵ带 �� �� �ִ�.
7. Type ��ü���� __CreateType()__ �޼ҵ�� ����(Ŭ����)�� CLR���� ��������
// ���� ���� ���� ���
8. __.CreateInstance()__ �̿��ؼ� �ν��Ͻ��� �������� ���� (object ������ ��ü)
9. __GetType().GetMethod()__ �̿��ؼ� methodIfo ��ü �����
10. methodInfo ��ü�� .Invoke()�̿��ؼ� �޼ҵ� ���

<details>
<summary>���� : ���ο� ������ ����� �ν��Ͻ��� �������� ������ ���</summary>
<div markdown="1">

```C#
using System;
using System.Reflection;
using System.Reflection.Emit;

namespace EmitTest
{
    public class MainApp
    {
        public static void Main()
        {
            AssemblyBuilder newAssembly =
                AppDomain.CurrentDomain.DefineDynamicAssembly(
                    new AssemblyName("CalculatorAssembly"), AssemblyBuilderAccess.Run);
            
            ModuleBuilder newModule = newAssembly.DefineDynamicModule("Calculator");
            TypeBuilder newType = newModule.DefineType("Sum1To100");

            MethodBuilder newMethod = newType.DefineMethod(
                "Calculate",
                MethodAttributes.Public,
                typeof(int),    // ��ȯ ����
                new Type[0]);   // �Ű� ����

            ILGenerator generator = newMethod.GetILGenerator();

            generator.Emit(OpCodes.Ldc_I4, 1);

            for (int i = 2; i <= 100; i++)
            {
                generator.Emit(OpCodes.Ldc_I4, i);
                generator.Emit(OpCodes.Add);
            }

            generator.Emit(OpCodes.Ret);
            newType.CreateType();

            object sum1To100 = Activator.CreateInstance(newType);
            MethodInfo Calculate = sum1To100.GetType().GetMethod("Calculate");
            Console.WriteLine(Calculate.Invoke(sum1To100, null));
        }
    }
}
```
</div></details>

## 16.2 ��Ʈ����Ʈ
: ��Ʈ����Ʈ�� �ڵ忡 ���� �ΰ� ������ ����ϰ� ���� �� �ִ� ���
- �ּ����� ���� : ��ǻ�Ͱ� �д� ��.

## 16.2.1 ��Ʈ����Ʈ ����ϱ�
- ��� ����

```C#
[ ��Ʈ����Ʈ_�̸�( ��Ʈ����Ʈ_�Ű�����) ]
public void Mymethod() { �� }
```

### .NET �����ӿ�ũ���� �⺻������ �����ϴ� ��Ʈ����Ʈ 
- [Obsolete] : ���� �� ���â�� �޼ҵ带 ����� �� ���

``` 
[Obsolete( �� �� �� ) ]
```

- [DILImport] : ����Ƽ�� DIL�� �ִ� �Լ��� ȣ���� �� ���
- [Conditional] : ���Ǻ� �޼ҵ� ������ ������ �� ���.

## 16.2.2 ȣ���� ���� ��Ʈ����Ʈ
: ȣ������ ������ ��ȯ����. �޼ҵ��� ȣ���� �̸�, ȣ���� �޼ҵ尡 ���ǵǾ� �ִ� �ҽ� ���� ���, �ҽ� ���� ���� �� ��ȣ ���� ��ȯ �޾� ����� �� �ִ�.
�޼ҵ��� �Ű� ������ ���
![ȣ���� ��Ʈ����Ʈ��](./OOP/pic/CH_16_YH2.jpg)
 

## 16.2.3 ���� ����� ��Ʈ����Ʈ
��Ʈ����Ʈ�� �ϳ��� Ŭ�����̱� ������ ����ڰ� �ʿ信 ���� ���� �� �ִ�. 
- ��� ��Ʈ����Ʈ�� __System.Attribute Ŭ����__�κ��� ����� �޾� ����.

### System.AttributeUsage()
: ��Ʈ����Ʈ�� � ����� ��������, �� ��Ʈ����Ʈ�� �ߺ��ؼ� ����� �� �ִ����� ���� ����(��Ʈ����Ʈ�� ��Ʈ����Ʈ)
### �Ű�����
- __ù��° �Ű�����__ : Attribute Target
: ���� �����ϰ� �ִ� ��Ʈ����Ʈ�� ���� ����� �������� ��Ÿ��.
���� �����ڸ� �̿��� ���յ� ����
- __�ɼ�__ : 
__AllowMultiple__ = True : ��Ʈ����Ʈ�� �ߺ� ����� �����ϰ� ��.


<details>
<summary> ���� ����� ���� ��Ʈ����Ʈ(history)�� ���</summary>
<div markdown=��1��>

```C#
using System;

namespace HistoryAttribute
{
    [System.AttributeUsage(System.AttributeTargets.Class, AllowMultiple=true)]
    class History : System.Attribute
    {
        private string programmer;
        
        public double Version
        {
            get;
            set;
        }
        
        public string Changes
        {
            get;
            set;
        }

        public History(string programmer)
        {
            this.programmer = programmer;
            Version = 1.0;
            Changes = "First release";
        }

        public string Programmer
        {
            get { return programmer; }
        }
    }

    [History("Sean", 
        Version = 0.1, Changes = "2010-11-01 Created class stub")]
    [History("Bob", 
        Version = 0.2, Changes = "2010-12-03 Added Func() Method")]
    class MyClass
    {
        public void Func()
        {
            Console.WriteLine("Func()");
        }
    }

    class MainApp
    {
        static void Main(string[] args)
        {
            Type type = typeof(MyClass);
            Attribute[] attribues = Attribute.GetCustomAttributes(type);

            Console.WriteLine("MyClass change history...");

            foreach (Attribute a in attribues)
            {
                History h = a as History;
                if (h != null)
                    Console.WriteLine("Ver:{0}, Programmer:{1}, Changes:{2}",
                        h.Version, h.Programmer, h.Changes);
            }
        }
    }
}
```

</div></details>
