#17. Dynamic ����

## 17.1 dynamic ���� �Ұ�
: ���� �˻簡 �������� �� �̷������ �ʰ� ���α׷� ���� �� �̷������ �ϳ��� ������ ����. (int, string ����)
- dynamic �������� ����� ��ü�� �ϴ� �����Ϸ��� ���� �˻縦 ���ذ�.

## 17.1.1 ���� Ÿ����
: ��� ������ ��ӹ޴����� ������� ���� �޼ҵ�� ������Ƽ�� �����Ѵٸ� ���� �������� ����

<details>
<summary> ���� : ����Ÿ���� </summary>
<div>

```C#
using System;

namespace DuckTyping
{
    class Duck
    {
        public void Walk()
        { Console.WriteLine( this.GetType() + ".Walk"); }

        public void Swim()
        { Console.WriteLine( this.GetType() + ".Swim"); }

        public void Quack()
        { Console.WriteLine( this.GetType() + ".Quack"); }
    }

    class Mallard : Duck
    { }

    class Robot
    {
        public void Walk()
        { Console.WriteLine("Robot.Walk"); }

        public void Swim()
        { Console.WriteLine("Robot.Swim"); }

        public void Quack()
        { Console.WriteLine("Robot.Quack"); }
    }

    class MainApp
    {
        static void Main(string[] args)
        {
            dynamic[] arr = new dynamic[] {new Duck(), new Mallard(), new Robot() };

            foreach (dynamic duck in arr)
            {
                Console.WriteLine(duck.GetType());
                duck.Walk();
                duck.Swim();
                duck.Quack();

                Console.WriteLine();
            }
        }
    }
}
```

</div></details>

### 17.1.2 ���� Ÿ������ ������ ����
### ���� 
- ���� Ÿ������ ��� ��� ���踦 �̿����� �ʾ� ���α׷��� ���� ���� �κи� ���� ���� 
: �߸��� �������̽��� �����ϸ� �Ļ� Ŭ������ ���� Ŭ������ ���� �����ؾ� �Ѵ�.

### ����
- ���� Ÿ������ ��� ���� ��� �޼ҵ� ������ ã�Ƽ� �����ؾ��Ѵ�. 
: ���� Ÿ������ ������� ������ Visual Studio�� �����͸� ��� �̿� �Ұ�

## 17.2 COM�� .NET ������ ��ȣ ��뼺�� ���� dynamic ����
### COM(Component Object Model)
: ����ũ�μ���Ʈ�� ����Ʈ���� ������Ʈ �԰�. COM API�� ����ϸ� ���� ������ �аų� �� �� ����.

### RCW(Runtime Callable Wrapper)
- .NET ������ ���, RCW�� ���� COM ������Ʈ�� ����� �� �ִ�. COM ��ü�� ������Ʈ ������ �߰��ϸ� IDE�� �ڵ����� tlbimp.exe�� ȣ���ؼ� RCW�� ������ְ� �̴� COM�� ���� ���Ͻ� ����(�븮)�� �ؼ� C#�ڵ忡�� COM API�� ����� �� �ְ� ���ݴϴ�. 
![�׸�3](./OOP/pic/ CH_17_YH1.jpg)
 

- C#�� COM ������ ��ȣ ��뼺�� ���� �ʰ� ���� ����
1. COM�� �޼ҵ尡 ����� ��ȯ�� �� ���� ������ �ƴ� __object �������� ��ȯ__
: C# 4.0���� __dynamic ����__�� �� ������ �ذ�
2. COM�� �����ε��� ���������ʰ� �޼ҵ��� ������ �Ű� ������ �⺻�� �Ű� ���� ����
: C# 4.0���� __������ �Ű� ������ �⺻�� �Ű� ���� ����__���� �ذ�
=���ǹ��� ���� ��ȯ�� �ǹ� ���� �Ű� ���� �Է��� �����ϰ� ���� �� �ְԵ�. ���־� ��Ʃ����� RCW�� ���� �� dynamic �����̳� ������ �Ű� ������ �̿��ؼ� �������..

### COM ������Ʈ�� ������ �߰��ϴ� ���
1. �ַ�� Ž���⿡ ��program.cs����� __��main.cs��__ ����� �ֱ�
2. �ַ�� Ž���� �������� �׸��� ���콺 ������ ��ư���� __[���� �߰�__] �׸� ����
3. [COM] ? [���� ���̺귯��] �׸� ����
4. ���� ��� ��Ͽ��� �ʿ��� ���� ���̺귯�� �߰�

<details>
<summary> ���� : ���� ���̺귯�� ���� �ϱ� </summary>
<div markdown=��1��>

��Microsoft Excel 16.0 Object Library�� ���� ���̺귯���� �߰� �� ��main.cs���� �ڵ� �ۼ�

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Excel = Microsoft.Office.Interop.Excel;

namespace COMInterop
{
    class MainApp
    {
        public static void OldWay(string[,] data, string savePath)
        {
            Excel.Application excelApp = new Excel.Application();
            
            excelApp.Workbooks.Add(Type.Missing);

            Excel.Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet;
            
            for (int i = 0; i < data.GetLength(0); i++)
            {
                ((Excel.Range)workSheet.Cells[i + 1, 1]).Value2 = data[i, 0];
                ((Excel.Range)workSheet.Cells[i + 1, 2]).Value2 = data[i, 1];
            }

            workSheet.SaveAs(savePath + "\\shpark-book-old.xlsx",
                Type.Missing,
                Type.Missing,
                Type.Missing,
                Type.Missing,
                Type.Missing,
                Type.Missing,
                Type.Missing,
                Type.Missing);

            excelApp.Quit();
        }

        public static void NewWay(string[,] data, string savePath)
        {
            Excel.Application excelApp = new Excel.Application();

            excelApp.Workbooks.Add();

            Excel._Worksheet workSheet = excelApp.ActiveSheet;

            for (int i = 0; i < data.GetLength(0); i++)
            {
                workSheet.Cells[i + 1, 1] = data[i, 0];
                workSheet.Cells[i + 1, 2] = data[i, 1];
            }

            workSheet.SaveAs(savePath + "\\shpark-book-dynamic.xlsx");
            excelApp.Quit();
        }

        static void Main(string[] args)
        {
            string savePath = System.IO.Directory.GetCurrentDirectory();
            string[,] array = new string[,] 
            { 
                { "���� �ڱ��ϴ� �˰���", "2009" }, 
                { "���� �ڱ��ϴ� C# 4.0",   "2011" },
                { "���� �ڱ��ϴ� C# 5.0",   "2013" },
                { "���� �ڱ��ϴ� ���̽� 3", "2016" },
                { "�̰��� C#�̴�",          "2018" }
            };

            Console.WriteLine("Creating Excel document in old way...");
            OldWay(array, savePath);

            Console.WriteLine("Creating Excel document in new way...");
            NewWay(array, savePath);
        }
    }
}
```


</div></details>

## 17.3 ���� ������ ��ȣ ��뼺�� ���� dynamic ����
: ���̽�/���ó�� ���� �� �ڵ带 �ؼ��� �����ϴ� ���� ��� ����

### DLR(Dynamic Language Runtime) 
: ���� ��� ���� �÷���, ���� �� DLR�� �̿��� .NET �÷��� ������ ������ �� �ְ� ����. (CLR ������ ����)

![DLR�� ����](./OOP/pic/CH_17_YH2.jpg)
 

- ���� ���� ���� ��ü�� ���� ���(C#/VB)�� ���� �����ϰ� ���־ �����ϰ� �� ����� �޾� �� �� �ִ�. 
- CLR�� DLR API�� ������� ������ ���� ���� ȣ������ �� �ֱ� ������ ���̽㿡 ���� ���̺귯���� ȣ�����ϴ� �ڵ带 ȣ������ ���� �ִ�.

### CLR�� DLR ������ ��ȣ ��뼺 ���� �ذ�
: �̸� ���� �˻縦 �� �� ���� ���� ���� ���� ���� ��ü�� C#�� __dynamic ����__���� �ذ�.
- ���� ���� ���� ������� ��ü�� dynamic �������� ����

### DLR�� Ŭ����
__C# �ڵ忡�� ���� �� ȣ�����ϴµ� �ʿ��� Ŭ����__ 
: �Խ�Ʈ �ڵ带 ������ �� �پ��ϰ� �����ؼ� ���
- __ScriptRuntime__ : ������ ȣ�����ϴ� __������__, ���� ����(������ ������� ���� ��ü)�� ��Ÿ���� �ϳ��� .NET AppDomain �ȿ� ���� ���� ScriptRuntime�� ���� �� �ִ�.
- __ScriptScope__ : __���ӽ����̽�__�� ��Ÿ��. ȣ��Ʈ(���⼭ C#�ڵ�)�� ScriptScope ��ü �ȿ� ���� ��� �ڵ忡�� ����ϴ� __����__�� ���� �����ϰų� ���� �� �ִ�.
- __ScriptSource__ : __�ҽ� �ڵ�__�� �о���̴� ���� �޼ҵ�� �о���� �ҽ� �ڵ带 �پ��� ������� �����ϴ� �޼ҵ���� ����
- __ScriptEngine__ : ����� ������ ��Ÿ���� �ϲ�. �ڵ带 �����ϰ� ScriptScope�� ScriptSource�� �����ϴ� �پ��� ����� ����.
- __CompiledCode__ : __�����ϵ� �ڵ�__�� ��Ÿ��. �� �� ������ �س��� ���� �� �ݺ� �����ϴ� �ڵ带 ��Ÿ���� �� ���.

### �Խ�Ʈ �ڵ带 �����ϴ� ���
1. �ҽ� �ڵ� __�����ϡ��� ���__�� �Ѱܹ޾� ���� : ScriptRuntime 

```C#
ScriptRuntime ��ü = Python.CreateRuntime();
dynamic result = runtime.ExecuteFile(�����̽� ����.py��)
```
2. ���ڿ��� ��� ���� ��� �ڵ� __����__ : ScriptEngine, ScriptScope, ScriptSource

<details>
<summary> ���� : ironPython�� �̿��� Python�ڵ� ����</summary>
<div markdown=��1��>

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Microsoft.Scripting;
using Microsoft.Scripting.Hosting;
using IronPython.Hosting;

namespace WithPython
{
    class MainApp
    {
        static void Main(string[] args)
        {
            ScriptEngine engine = Python.CreateEngine();
            //ScriptEngine
            //     Represents a language in Hosting API. Hosting API counterpart for Microsoft.Scripting.Hosting.ScriptEngine.LanguageContext.
            //Python.CreateEngine()
            //     Creates a new ScriptRuntime and returns the ScriptEngine for IronPython. 
            //     If the ScriptRuntime is required it can be acquired from the Runtime property on the engine.

            ScriptScope scope = engine.CreateScope(); //scope : ����
            //     A ScriptScope is a unit of execution for code. It consists of a global Scope
            //     which all code executes in. Hosting API counterpart for Microsoft.Scripting.Hosting.ScriptScope.Scope.

            scope.SetVariable("n", "�ڻ���");
            scope.SetVariable("p", "010-123-4566");
            
            ScriptSource source = engine.CreateScriptSourceFromString(
                //���̽� �ڵ� �� �ȿ� �ۼ�.
                @"
class NameCard :
    name = ''
    phone = ''

    def __init__(self, name, phone) : 
        self.name = name 
        self.phone = phone

    def printNameCard(self) : 
        print self.name + ', ' + self.phone

NameCard(n, p)
");
            dynamic result = source.Execute(scope);// ���̽� �ڵ� �����ϴ� excute �޼ҵ忡 ScriptScope(�ڵ� ���� ����) ���
            result.printNameCard();// �� �ڵ忡�� ȣ��

            Console.WriteLine("{0}, {1}", result.name, result.phone);//������ ����
        }
    }
}
```

</div></details>
