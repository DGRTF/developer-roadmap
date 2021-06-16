<details>
<summary>
Что такое инкапсуляция, полиморфизм и наследование? What is encapsulation, polymorphism and inheritance?
</summary>

`
Инкапсуляция - это механизм, который объединяет данные и код, манипулирующий зтими данными, а также защищает и то, и другое от внешнего вмешательства или неправильного использования.
Полиморфизм - это свойство, которое позволяет одно и то же имя использовать для решения двух или более схожих, но технически разных задач.
Наследование - это процесс, посредством которого один объект может приобретать свойства другого.
`
</details>


<details>
<summary>
Какие виды полиморфизма вы знаете?
What types of polymorphism do you know?
</summary>

`
Ad-hoc-полиморфизм(перегрузки).
Параметрический полиморфизм (обобщения).
Полиморфизм подтипов (наследование).
`
</details>


<details>
<summary>
Что такое полиморфизм подтипов? What is polymorphism subtypes?
</summary>

`
Полиморфизм подтипов (полиморфизм) — свойство системы, позволяющее использовать объекты с одинаковым интерфейсом без информации о типе и внутренней структуре объекта.
`
</details>


<details>
<summary>
Что такое ассоциация, агрегация, композиция?
What is association, agregation, composition?
</summary>

`
Ассоциация - это отношение, при котором объекты одного типа неким образом связаны с объектами другого типа. Например, объект одного типа содержит или использует объект другого типа. Например, игрок играет в определенной команде.
Композиция определяет отношение HAS A, то есть отношение "имеет". Например, в класс автомобиля содержит объект класса электрического двигателя, при этом класс автомобиля создает объект двигателя.
От композиции следует отличать агрегацию. Она также предполагает отношение HAS A, но реализуется она иначе(через внедрение  зависимести).
`
</details>


<details>
<summary>
Что лучше применять и когда?
What is better use and when?
</summary>

`
Агрегацию, всегда, за исключением ,базовых и ненаследуемых типов.
`
</details>

<details>
<summary>
Что такое внедрение зависимостей?
What is Dependency injection?
</summary>

`
Внедрение зависимости — процесс предоставления внешней зависимости программному компоненту. Является специфичной формой «инверсии управления» (англ. Inversion of control, IoC), 
когда она применяется к управлению зависимостями.
В полном соответствии с принципом единственной обязанности объект отдаёт заботу о построении требуемых ему зависимостей внешнему, специально предназначенному для этого общему механизму.
`
</details>

<details>
<summary>
Зачем применять интерфейсы и абстрактные классы?
Why use interfaces and abstract classes?
</summary>

`
Что бы агрегировать их как зависимости и вместо них подставлять любой из их подтипов, что обеспечивает переиспользуемость класса для любого из этих подтипов.
`
</details>

<details>
<summary>
Чем они отличаются в C#? 
How do they differ in C#?
</summary>

`
Интерфейсы имеют множественное наследование.
`
</details>

```C#
interface IInterface {}
interface IInterface1 {}

// множественное наследование
abstract class Human : IInterface, IInterface1
{
    public string Name { get; private set; }
    public DateTime Born { get; private set; }
}

// Наследование, класс наследует два свойства от Human
class Employee : Human {
    public Employee(string name, DateTime born) {
        Name = name;
        Born = born;
    }
}

// Параметрический полиморфизм (обобщения).
interface IAnimal<T> where T : Human
{
    DateTime Born { get; }
    T Owner { get; }
    int GetAge();
}

// Полиморфизм подтипов (наследование).
class Dog : IAnimal<Employee>
{
    // Инкапсуляция (данные и метод GetAge() для работы с ними)
    public DateTime Born { get; private set; } = new DateTime(1996, 3, 24);
    public Employee Owner { get; private set; }

    // агрегация, частный случай ассоциации
    public Dog(Human owner) {
        Owner = owner;
    }

    public int GetAge()
    {
        return DateTime.Now.Year - Born.Year;
    }

    // Ad-hoc-полиморфизм(перегрузки)
    public int GetAge(DateTime dateTime)
    {
        if (dateTime < Born)
        {
            throw new ArgumentException("Неправильно задана дата отсчета");
        }

        return dateTime.Year - Born.Year;
    }

    public Employee Get() {
        // композиция, частный случай ассоциации
        return new Employee("Name", new DateTime(1990, 5, 12))
    }
}
```

<details>
<summary>
Какое влияние оказывают на ООП в целом?
What impact do they have on OOP in general?
</summary>

`
Позволяют сокращать количество написания кода за счет переиспользования класса для разных подтипов агрегируемого типа.
`
</details>

<details>
<summary>
Как вы считаете, нужны ли они в динамически типизированных языках, почему?
How do you think, they are needed in dynamic typing language?
</summary>

`
Нет, это было введено для ООП в статически типизированных языках, в противном случае порождалось бы много классов, потому что нельзя было бы переиспользовать старые.
`
</details>

<details>
<summary>
Можно ли с C# 8.0 заменить абстрактные классы интерфейсами? И почему?
Is it possible whith C# 8.0 replace abstact classes whith intrfaces? Why?
</summary>

`
С C# 8.0 в интерфейсах появилась реализация методов по-умолчанию. Разница в том, что эта реализация наследуется явно, поэтому объект-наследник необходимо приводить вверх по дереву наследования для использования наследуемого функционала.
`

```C#
interface IShow
{
    public void Show()
    {
        Console.WriteLine("Show method");
    }
}

class Show: IShow
{

}

public static void Main() 
{
    show.Show(); // ошибка
    ((IShow)show).Show(); // рабтает
}
```
</details>

<details>
<summary>
Зачем вообще нужны классы, если можно использовать только методы и данные статических классов C#?
Why do we need classes, if we can only use static classes methods and data?
</summary>

`
Классы могут хранить состояние. В функциональных языках для этого используют замыкание.
`
</details>

<details>
<summary>
Что такое принципы SOLID и какую проблему решает каждый из них?
What are the SOLID principles and what problem does each of them solve?
</summary>

`
1.Принцип единой ответственности позволяет не перегружать класс лишними задачами. Особенно хорошо помогает его соблюдать тестирование.
2.Подстановки Барбары Лисков. Позволяет делать одинаковое ожидаемое поведение от любого класса в дереве наследования одного функционала, в этом так же помогает контрактное программирование.
3.Разделения интерфейсов. Позволяет не наследовать лишние члены интерфейса ,а только необходимые для типа. Чего нельзя добиться абстрактными классами из-за отсутствия множественного наследования.
4.Системы должны быть доступня для расширения, но закрыты для изменения. Это происходит за счет полииморфизма подтипов и внедрения зависимостей, где мы используем наследование, 
что бы какой-либо сущьностью переиспользовать новыцй функционал, а не изменять старый для внесения новго
5.Принцип инверсии зависимостей. Позволяет разорвать зависимость между членами в зависимость от абстракций (интерфейсов и абстрактных классов).
`
</details>

<details>
<summary>
Можно ли в js работать без классов и объектов? 
Is it possible to work in js whithout classes and objects?
Если да, то как?
If so, how?
</summary>

`
Да, используя замыкание.
`
</details>

<details>
<summary>
Можно ли без них хранить состояние?
Is it possible to store the state without them?
</summary>

`
Да, через замыкание, котрое позволяет хранить состояние.
`

```javascript
function sumWrapper(a: number)
{
    return (b: number): number => a + b;
}

const sum = sumWrapper(4);
const result = sum(5); // 9
```
</details>

<details>
<summary>
Что такое функции высшего порядка?
Зачем они нужны?
What are higher-order functions?
</summary>

`
Фнкции, которые могут принимать другие функции и возвращать функции. Для реализации замыкания и как агрегация.
`

```javascript
function sumWrapper(a: number, func(f: number) => number)
{
    return (b: number): number => func(a + b);
}
```
</details>

<details>
<summary>
Что такое мемоизация? 
What is memoization?
</summary>

`
Мемоизация(иногда называют декорирование) - это кеширование внутри состояния объекта или функции(замыкание) результатов выполнения длительных операций с целью повышения производительности вычислений с одинаковыми входными данными.
Для этого Функции или методы должны быть детерментированными. К недостаткам подхода можно отнести усложнение системы и расходование памяти.
`

```javascript
function cachingDecorator(func) {
  let cache = new Map();

  return function(x) {
    if (cache.has(x)) {    // если кеш содержит такой x,
      return cache.get(x); // читаем из него результат
    }

    let result = func(x); // иначе, вызываем функцию

    cache.set(x, result); // и кешируем (запоминаем) результат
    return result;
  };
}
```
</details>

<details>
<summary>
Что такое каррирование?
What is currying?
</summary>

`
Каррирование - это процесс, в ходе которого можно вызовом одной функции вернуть другу и вызвать последнюю, что приводит к такому уоду : get(5)(4);
В основном используется для замыканий и хранения состояния внутри функции, объекта.
`

```javascript
const result = sumWrapper(4)(5); // 9
```
</details>

<details>
<summary>
Раньше в js не было ключевого слова private, была ли другая возможность скрыть данные внутри объекта?
Previously, js didn't have the private keyword, was there another way to hide data inside an object?
</summary>

`
С помощью замыкания.
`
</details>

<details>
<summary>
Какие типы данных есть в C#?
Data types in C#?
</summary>

`
Ссылочные и значимые.
Одни передаются по ссылке - передеается адрес в куче. А другие по значению - копирется все значение.
Типы значений:

Целочисленные типы (byte, sbyte, short, ushort, int, uint, long, ulong)

Типы с плавающей запятой (float, double)

Тип decimal

Тип bool

Тип char

Перечисления enum

Структуры (struct)

Ссылочные типы:

Тип object

Тип string

Классы (class)

Интерфейсы (interface)

Делегаты (delegate)
`

```C#
static void Main()
{
    int i = 5;
    A(i);
    Console.WriteLine(i);

    B b = new B();
    A(b);
    Console.WriteLine(b.N); // 10
}


static void A(int i)
{
    i = default;
}

static void A(B b)
{
    b.N = 10;
}
```
</details>

<details>
<summary>
Что такое модификаторы доступа, зачем нужны?
What are access modifiers, why are they needed?
</summary>

`
Модификаторы доступа позволяют задать допустимую область видимости для членов класса.
`

```C#
class Program
{
    public int A;

    private int a;

    protected int B;

    internal int b;

    protected internal int C;

    private protected int c;

    static void Main()
    {
        
    }

}
```
</details>

<details>
<summary>
Что делает оператор checked/unchecked?
What does the checked/unchecked statment do?
</summary>

`
Проверка на выход за пределы допустимого диапазона при арифметических вычислений. 

`

```C#
checked (выражение)
checked {
// проверяемые операторы
}

int b = unchecked((byte)int.Parse(Console.ReadLine()));
```
</details>

<details>
<summary>
Разница между свойствами и полями данных? 
Какие есть преимущества и недостатки свойств? 
Когда что использовать?
The difference between properties and data fields?
What are the advantages and disadvantages of properties?
When to use what?
</summary>

`
Поля - это данные объекта, а свойства - методы для работы с ними.
Свойства могут сделаать проверку входных и выходных значений поля, изменить значение поля, использовать любую логику обработки до и после обращения к полю.
Однако это методы, хотя воспринимаются, как поля при написании кода.Так, например, DateTime.Now по мнению Рихтера является ошибкой, потому что результат вызова не детерминтирован.
Более того при вызове свойства структуры внутри метода с ключевым словом in будет создаваться ее копия:
`
```C#
Get(in Point point) {
    int x = point.X;
    ...
}
```
`
Объясняется это тем, что in гарантирует неизменяемость, в то время как свойство X может быть следующим: public int X => ++x;
что изменит состояние объекта структуры. Поэтому создается defensive copy(защитна копия) структуры и значение ее не изменится. Это неочевидное поведение системы.

В большинстве случаев лучше применять свойства(автосвойства), за исключением приватных константных и неизменяемых значений. Поля более производительные и уменьшают количесво IL кода и логики.
`
```C#
class Prog
{
private int a; // поле данных
    public int A {get => a; set { a = value } } // свойство
}
```
</details>

<details>
<summary>
Чем статические классы отличаются от обычных, для чего применяются? Во что их превратит компилятор?
How do static classes differ from regular classes, and what are they used for? What will the compiler turn them into?
Обычные классы хранят состояние, а статические не могут, в них могут храниться только статические члены и нельзя создавать экземпляры таких классов.
В абстрактный ненаследуемы класс в IL-коде.
</summary>

`
Обычные классы хранят состояние, а статические не могут, в них могут храниться только статические члены и нельзя создавать экземпляры таких классов.
В абстрактный ненаследуемы класс в IL-коде.
`

```C#
static void Main()
{
    // вызов метода статического класса
    Enumerable.Range(1, 5);

    // создание экземпляра и вызов метода обычного класса
    var list = new List<int>;
    list.Add(5);
}
```
</details>

<details>
<summary>
Для чего нужно ключевое слово override? Как переопределение влияет на версионность модулей?
What is the need override keyword for?
</summary>

`
Для переопределения наследуемых членов класса в случае необходимости.
`
```C#
        abstract class Abstract
        {
            public virtual void Show()
            {
                Console.WriteLine("virtual");
            }
        }

        class  A : Abstract
        {
            public override void Show()
            {
                Console.WriteLine("override");
            }
        }
```

</details>

<details>
<summary>
Какие проблемы решают коллекции?
What problems do collections solve?
</summary>

`
Когда есть необходимость добавления элемента в массив, нужно его увеличивать, коллекции же 
инкапсулируют в себе массив, который при достижении конца увеличивается не на одну ячейку, а более, хотя снаружи ведут себя как обычный массив.
`
</details>

<details>
<summary>
Что такое immutable коллекции?
What are immutable collections?
</summary>

`
Это неизменяемые коллекции, при  изменении которой, создается новый объект коллекции.
`
</details>

<details>
<summary>
Во что превратит компилятор обход коллекции через foreach?
What will the compiler make of traversing hte collection via foreach?
</summary>

`
Вызов GetEnumarator(); и получение элемента энумератора через MoveNext(); В конце цикла вызывается Dispose(); энумератора.
`
</details>

<details>
<summary>
Расскажите про обобщения.
Tell as about the generic.
</summary>

`

`
</details>

<details>
<summary>
Что такое ковариантность и контравариантность обобщенных типов? 
That is covariance and contravariance generic types?
</summary>

`
Ковариа́нтность и контравариа́нтность в программировании — способы переноса наследования типов на производные от них типы.
`

```C#
delegate TResult Func<in T, out TResult>(T arg);
public interface IComparable<in T> { ... }
```
</details>

<details>
<summary>
Для чего были введены обобщения?
Why were genreric introduced?
</summary>

`
Для безопасности типов и избегания упаковки и распаковки.
`

```C#
var list = new List<int>();
// компилятор будет ругаться на тип. отличный от int
// упакоки значения не рпоизойдет
list.Add(453);
```
</details>

<details>
<summary>
Сколько раз сработает статический конструктор класса A<T>?

```C#
var a = new A<int>();
var a1 = new A<string>();
var a2 = new A<int>();
```
</summary>

`
2 раза, потому что создастся 2 типа.
`
</details>

<details>
<summary>
Что такое ограничение обобщений?
What is the generalization constraint?
</summary>

`
Ограничивает входные типы интерфейсами, классами, наличием конструктора без параметра, cтруктурами.
`

```C#
// На вход принимаются структуры
public void Method<T>(T parameter) where T : struct
```
</details>

<details>
<summary>
Какую перегрузку Console.WriteLine(); метода вызовет следующий код? Это зависит от входного типа или всегда будет Console.WriteLine(object);?
What an overload of the Console.WriteLine(); method will call the following code?

```C#
void Show<T>(T showData) {
    Console.WriteLine(showData);
}
```
</summary>

`
Всегда Console.WriteLine(Object), потому что обощения не могут определять перегрузку во время выполнения.
`
</details>

<details>
<summary>
Для чего нужен оператор typeof, если у каждого объекта и так есть метод GetType()? Для чего нужен оператор default?
What is the typeof operator for, if every object has a GetType() method for?
</summary>

`
typeof применяется, когда нет экземпляра объекта и что бы не вызывать упаковку. default позволяет задать значение по-умолчанию, когда не известен конктретный тип(обобщения).
`
</details>

<details>
<summary>
Что такое упаковка и распаковка?
What is boxing/unboxing?
</summary>

`
Преобразование значимого типа в ссылочный и обратно.
`
</details>

<details>
<summary>
В каких случаях происходит?
In what cases does it happen?
</summary>

`
Упаковка возникает в двух случаях:
- приведение к ссылочному типу
- вызов непереопределённых наследуемых методов
`
</details>

<details>
<summary>
Как влияет на производительность? 
How does it affect performance?
Как бороться?
How to fight?
</summary>

`
Производительность падает в несколько раз, зависит от размера структуры. Обобщениями и оперетором typeof().
`
</details>

<details>
<summary>
Как избежать упаковки , если вы хотите написать класс принимающий на вход  конструктора некий интерфейс interface IA, и закинуть в будущем туда структуру наследующую этот интерфейс?
</summary>

`
Единственным способом будет создать обобщенный клас с ограничением обобщения на интерфейс IA.
`
</details>

<details>
<summary>
Как устроены делегаты?
How do delegates work?
</summary>

`
Содержит поле типа object, которое хранит экземпляр объекта или структуры вызываемого метода, или null, если вызывается статический метод.Делегаты неизменяемы.Может хранить только один метод и массив делегатов, в случачае использования цепочки вызовов.
`
</details>

<details>
<summary>
Зачем нужны события, если есть делегаты?
Why do we need events if there are delegates?
</summary>

`
События нельзя вызвать за пределами объекта, на них можно только подписаться, так же они предоставляют два метода добавления и удаления делегата и могут нести в себе дополнительную логику, этим они похожи на свойства.
`
</details>

<details>
<summary>
Чем отличаются лямбда-выражения от анонимных методов?
What is difference lambda-expressions and anonymous methods?
</summary>

`
В общем ничем, кроме незначительной разницы:
В анонимных методах мы можем обойтись без параметров, если даже это и ожидается:
`

```C#
public event EventHandler SomeEvent;
...
SomeEvent += delegate { Console.WriteLine("some information") };
```
</details>

<details>
<summary>
Что такое замыкания?
What are closures?
Во что превратит компилятор замыкание переменной?
What will a variable closure turn the compiler into?
</summary>

`
Это свойство ананимного метода или лямбда-выражения хранить значение внешней переменной, которое может измениться за его пределами.
В класс с полем переменной и этим методом.
`
</details>

<details>
<summary>
Что ,если мы замкнем одну переменную в нескольких методах и начнём ее изменять?
What if we close one variable in several methods and start changing it?
</summary>

`
Компилятор создаст класс с полем переменной и этими методами, следовательно каждый метод будет изменять значение переменной, а другой будет получать уже измененное значение, как состояние объекта.
`
</details>

<details>
<summary>
Что делает оператор yield return, для чего нужен, во что его превратит компилятор?
What does yield return operator do? What is it used for?
</summary>

`
Создаёт два класса, наследуемые от IEnumerable и IEnumerator. из метода возвращается класс соответствующий возвращаемому значению.
В IEnumerator.Dispose(); закладывается финализатор (finnaly).
`
</details>

<details>
<summary>
Что делает класс Lazy<T>?
What does Lazy<T> class do?
</summary>

`
Создает экземпляр инкапсулируемого объекта T только при обращении к экземпляру Lazy<T>.
`
</details>

<details>
<summary>
Что такое отложенное выполнение, как реализуется в Linq?
What is lazy loading, as implemented in Linq?
</summary>

`
Это выполнение кода только при обращениии, в Linq реализуется за счет реализации IEnumerable;
`

```C#
	    var t = Enumerable.Range(0, 100).Where(x =>
            {
                System.Console.WriteLine("ops"); // вторым
                return x > 10;
            });

            System.Console.WriteLine("here"); // выведется первым

            foreach (var tt in t)
            {
                if (tt > 5)
                    break;
            }
```
</details>

<details>
<summary>
Как можно "завалить" отложенное выполнение в Linq?
How can we "fail" lazy loading in Linq?
</summary>

`
Методами Linq, которым нужен весь набор данных, например сортировка.
`
</details>

<details>
<summary>
На что влияет отложенное выполнение?
What is affected by lazy loading?
</summary>

`
Позволяет не запрашивать все данные исходного набора, пока в этом нет необходимости, следователно и обход набора уменьшается по количеству операций.
`
</details>

<details>
<summary>
Расскажите об асинхронных стримах.
Tell us obout asynchronous streams?
</summary>

`Это отложенное выполнение асинхронных операций с помощью операторо yield return и возвращаемого значения IAsyncEnumerable<T>.
`

```C#
public static async IAsyncEnumerable<int> GetNumbersAsync()
{
    for (int i = 0; i < 10; i++)
    {
        await Task.Delay(100);
        yield return i; 
    }
}
```
</details>

<details>
<summary>
Разница между IEnumerable и IQueryable?
What is difference between IEnumerable and IQueryable?
</summary>

`
Первый компилятор генрирует в обычный код, а второй в деревья выражений, который парсит постовщик методов расширения.
`
</details>

<details>
<summary>
Что такое деревья выражений, чем отличаются от делегатов? 
What are expression trees? How do they differ from delegates?
</summary>

`
Представлены классом Expression, позволяют парсить несложные запросы в синтаксис друго языка, делегаты относятся к исполняемому коду.
`
</details>

<details>
<summary>
Чем отличается декларативный стиль написания кода от императивного?
What is the difference between a declarativee style of writing code and an imperative style code?
</summary>

`
Декларативный код отвечает на вопрос "Что делать?", а императивный "Как сделать?".
`
</details>

<details>
<summary>
Зачем нужны атрибуты? 
Why do I need attributes?
Как работают? 
How do they work?
</summary>

`
Атрибуты в .NET представляют специальные инструменты, которые позволяют встраивать в сборку дополнительные метаданные.
С помощью рефлексии стандартные классы .NET получают использованные атрибуты и производят определенные действия. 
Например, атрибут [Serializable] указывает классу BinaryFormatter, что объекты с данным атрибутом можно сохранять в бинарный файл.
`
</details>

<details>
<summary>
Для чего нужны исключения, каков порядок их обработки?
What are exceptions for?
</summary>

`
Обозначают исключительную ситуацию, с которой данный код не может выполняться.
Если в блоке try{} было вызвано исключеие, то оно перемещается в блок catch, который обрабатывает конкретный тип исключения, если обработчика данного исключения не нашлось,
то выполняется блок finally. В случае отстутствия необходимого для обработки блока catch программа аварийно завершится. Не стоит выбрасывать исключения в catch и finally. Так же исключение обрабатывается согласно
иерархии наследования Exception
`
</details>

<details>
<summary>
Особенности вызова исключений в асинхронном коде?
</summary>

`
`
</details>

<details>
<summary>
Расскажите про GAC.
Tell us about the GAC.
</summary>

`
Глобальный кеш сборок. Хранит разделяемые сборки для любых приложений. 
`
</details>

<details>
<summary>
Что такое JIT-compiler?
What is JIT-compiler.
Как компилируется приложение?
How is the application compile?
</summary>

`
Just in time compiler, компилирует IL в ассемблерный код.
Сначала проходит транслятор, транслирующий код в тот же C# код, но который может пройти уже компилятор в IL код.Во время запуска программы запускается JIT-компилятор.
`
</details>

<details>
<summary>
Почему при запуске приложения первый вызов любого метода работает медленнее следующих?
Why is the first call of any method slower than the next one when the app starts? 
</summary>

`
После первой компиляции метода кода jit-компилятором он кешируется и уже не компилируется повторно. Поэтому последующие вызовы этих методов происходят быстрее.
`
</details>

<details>
<summary>
Как на это можно повлиять?
How can this be affected?
</summary>

`
Можно пройти полную компиляцию программы (например специальной утилитой Ngen.exe), но это нужно делать под конкретное устройство, т к JIT подбирает оптимальные команды для текущего процессора.
`
</details>

<details>
<summary>
Что такое IL, зачем он нужен?
What is IL? Why do i need it?
</summary>

`
Все компиляторы, поддерживающие платформу .NET, должны транслировать код с языков высокого уровня платформы .NET на язык CIL. 
Для написания одного приложения на разных ЯП.
`
</details>

<details>
<summary>
Расскажите про JIT-оптимизации.
Tell us about JIT optimization.
</summary>

`
Оптимизации кода, ускоряющие работу программ. Например оптимизация концевых вызовов. Может убрать лишние переменные или избавиться от упаковки привызове GetType() пользовательской структуры.
`
</details>

<details>
<summary>
Что делают инструкции unbox, callvirt, call, box, constrained? Какие отличия?
What do the unbox, callvirt, call, box, constrained statments do?
</summary>

`
callvirt вызывает метод объекта с передачей ссылки самого объекта и его упаковкой, для инструкции call ссылка на объект не нужна.
box/unbox - упаковка/распаковка.
constrained говорит о том, что вызовется call метод для значимого типа без упаковки, если метод структуры был переопределён.
`
</details>

<details>
<summary>
Что такое анонимные типы? Как работают и для чего нужны?
What are anonymous types? How work and what are they used for?
</summary>

`
`
</details>

<details>
<summary>
Что такое O(n) ?
What is O(n);
Что такое:
What is:
<ol>
    <li>бинарный поиск (binary search)</li>
    <li>односвязный список (singly linked list)</li>
    <li>двусвязный список (multi-linked list)</li>
    <li>граф (graph)</li>
    <li>хеш-таблица (hash table)</li>
    <li>сортировка (sort)</li>
    <li>быстрая сортировка (fast sort)</li>
    <li>алгоритм Дейкстры (Dijkstra's algorithm)</li>
    <li>дерево (tree)</li>
    <li>стек (stack)</li>
    <li>np-полные задачи</li>
</ol>
</summary>

`
Бинарный поиск - ускоренный поиск за O(log n), возможен при некоторых свойствах структуры данных, например при сортировке по номеру.
Односвязный список - список, где каждый элемент знает о следующем элементе, но не знает о предыдущем.
Двусвязный список - список, где каждый элемент знает о следующем элементе и предыдущем.
Граф - это совокупность узлов и рёбер, соединяющих эти узлы.
Хеш-таблица — это структура данных, реализующая интерфейс ассоциативного массива, а именно, она позволяет хранить пары (ключ, значение) 
и выполнять три операции: операцию добавления новой пары(O(1)), операцию поиска(O(1)) и операцию удаления пары по ключу(O(1)).
Сортировка - алгоритм, сортирующий элементы за время O(n**).
Быстрая сортировка - алгоритм, сортирующий элементы за время O(n log n).
Алгоритм Дейкстры - находит кратчайшие пути от одной из вершин графа до всех остальных. O(n**).
Дерево — это связный ациклический граф.
Очередь - первый вошел- первый вышел(FIFO).
Стек - первый вошел- последний вышел(FILO).
`
</details>
