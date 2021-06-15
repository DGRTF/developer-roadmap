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
Ad-hoc-полиморфизм(перегрузки)
Параметрический полиморфизм (обобщения)
Полиморфизм подтипов (наследование)
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

```C#
abstract class Human
{
    public string Name { get; }
    public DateTime Born { get; }
}

class Employee : Human {}

interface IAnimal<T> where T : Human
{
    DateTime Born { get; }
    T Owner { get; }
    int GetAge();
}

class Dog : IAnimal<Employee>
{
    public DateTime Born { get; private set; } = new DateTime(1996, 3, 24);
    public Employee Owner { get; private set; }

    public int GetAge()
    {
        return DateTime.Now.Year - Born.Year;
    }

    public int GetAge(DateTime dateTime)
    {
        if (dateTime < Born)
        {
            throw new ArgumentException("Неправильно задана дата отсчета");
        }

        return dateTime.Year - Born.Year;
    }
}
```

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
Что бы внедрять их как зависимости и вместо них подставлять любой из подтипов, что обеспечивает переиспользуемость класса для любого из этих подтипов.
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
Зачем вообще нужны классы, если можно использовать только методы (статические классы C#)?(???)
Why do we need classes, if we can only use static classes methods?
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
</summary>

`

`
</details>

<details>
<summary>
Если да, то как?
If so, how?
</summary>

`

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

`
</details>

<details>
<summary>
Для чего были введены обобщения?
Why were genreric introduced?
</summary>

`
Для безопасности типов и избегания упаковки и распаковки.
`
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
