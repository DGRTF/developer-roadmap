<details>
<summary>Что такое инкапсуляция, полиморфизм и наследование? What is encapsulation, polymorphism and inheritance?</summary>

`
Инкапсуляция - это механизм, который объединяет данные и код, манипулирующий зтими данными, а также защищает и то, и другое от внешнего вмешательства или неправильного использования.
Полиморфизм - это свойство, которое позволяет одно и то же имя использовать для решения двух или более схожих, но технически разных задач.
Наследование - это процесс, посредством которого один объект может приобретать свойства другого.
`
</details>


<details>
<summary>Какие виды полиморфизма вы знаете?
What types of polymorphism do you know?</summary>

`
Ad-hoc-полиморфизм(перегрузки)
Параметрический полиморфизм (обобщения)
Полиморфизм подтипов (наследование)
`
</details>


<details>Что такое полиморфизм подтипов? What is polymorphism subtypes?</summary>

`
Полиморфизм подтипов (полиморфизм) — свойство системы, позволяющее использовать объекты с одинаковым интерфейсом без информации о типе и внутренней структуре объекта.
`
</details>


<details>
<summary>Что такое ассоциация, агрегация, композиция?
What is association, agregation, composition?</summary>

`
Ассоциация - это отношение, при котором объекты одного типа неким образом связаны с объектами другого типа. Например, объект одного типа содержит или использует объект другого типа. Например, игрок играет в определенной команде.
Композиция определяет отношение HAS A, то есть отношение "имеет". Например, в класс автомобиля содержит объект класса электрического двигателя, при этом класс автомобиля создает объект двигателя.
От композиции следует отличать агрегацию. Она также предполагает отношение HAS A, но реализуется она иначе(через внедрение  зависимести).
`
</details>


<details>
<summary>Что лучше применять и когда?
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
<summary>Что такое внедрение зависимостей?
What is Dependency injection?</summary>

`
Внедрение зависимости — процесс предоставления внешней зависимости программному компоненту. Является специфичной формой «инверсии управления» (англ. Inversion of control, IoC), 
когда она применяется к управлению зависимостями.
В полном соответствии с принципом единственной обязанности объект отдаёт заботу о построении требуемых ему зависимостей внешнему, специально предназначенному для этого общему механизму.
`
</details>

<details>
<summary>Зачем применять интерфейсы и абстрактные классы?
Why use interfaces and abstract classes?</summary>

`
Что бы внедрять их как зависимости и вместо них подставлять любой из подтипов, что обеспечивает переиспользуемость класса для любого из этих подтипов.
`
</details>

<details>
<summary>Чем они отличаются в C#? 
How do they differ in C#?</summary>

`
Интерфейсы имеют множественное наследование.
`
</details>

<details>
<summary>Какое влияние оказывают на ООП в целом?
What impact do they have on OOP in general?</summary>

`
Позволяют сокращать количество написания кода за счет переиспользования класса для разных подтипов агрегируемого типа.
`
</details>

<details>
<summary>Как вы считаете, нужны ли они в динамически типизированных языках, почему?
How do you think, they are needed in dynamic typing language?</summary>

`
Нет, это было введено для ООП в статически типизированных языках, в противном случае порождалось бы много классов, потому что нельзя было бы переиспользовать старые.
`
</details>

<details>
<summary>
Можно ли с C# 8.0 заменить абстрактные классы интерфейсами? И почему?
Is it possible whith C# 8.0 replace abstact classes whith intrfaces? Why?</summary>

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
<summary>Зачем вообще нужны классы, если можно использовать только методы (статические классы C#)?(???)
Why do we need classes, if we can only use static classes methods?</summary>

`
Классы могут хранить состояние. В функциональных языках для этого используют замыкание.
`
</details>

<details>
<summary>Что такое принципы SOLID и какую проблему решает каждый из них?
What are the SOLID principles and what problem does each of them solve?</summary>

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
Is it possible to work in js whithout classes and objects?</summary>

`

`
</details>

<details>
<summary>Если да, то как?
If so, how?</summary>

`

`
</details>

<details>
<summary>
Можно ли без них хранить состояние?
Is it possible to store the state without them?</summary>

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
<summary>Что такое функции высшего порядка?
Зачем они нужны?
What are higher-order functions?</summary>

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
<summary>Что такое мемоизация? 
What is memoization?</summary>

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
<summary></summary>

`

`
</details>

<details>
<summary></summary>

`

`
</details>

<details>
<summary></summary>

`

`
</details>

<details>
<summary></summary>

`

`
</details>

<details>
<summary></summary>

`

`
</details>
