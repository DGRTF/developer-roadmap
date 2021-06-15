<details open>
<summary>Что такое инкапсуляция, полиморфизм и наследование? What is encapsulation, polymorphism and inheritance?</summary>
<br>
Инкапсуляция - это механизм, который объединяет данные и код, манипулирующий зтими данными, а также защищает и то, <br>и другое от внешнего вмешательства или неправильного использования.<br>
Полиморфизм - это свойство, которое позволяет одно и то же имя использовать для решения двух или более схожих,<br> но технически разных задач.<br>
Наследование - это процесс, посредством которого один объект может приобретать свойства другого.
</details>


<details open>
<summary>Какие виды полиморфизма вы знаете?
What types of polymorphism do you know?</summary>
<br>
Ad-hoc-полиморфизм(перегрузки)<br>
Параметрический полиморфизм (обобщения)<br>
Полиморфизм подтипов (наследование)<br>
</details>


<details open>Что такое полиморфизм подтипов?
What is polymorphism subtypes?</summary>
<br>
Полиморфизм подтипов (полиморфизм) — свойство системы, позволяющее использовать объекты с одинаковым <br>интерфейсом без информации о типе и внутренней структуре объекта.
</details>


<details open>
<summary>Что такое ассоциация, агрегация, композиция?
What is association, agregation, composition?</summary>
<br>
Ассоциация - это отношение, при котором объекты одного типа неким образом связаны с объектами другого типа. Например, объект одного типа содержит или использует объект другого типа. Например, игрок играет в определенной команде
Композиция определяет отношение HAS A, то есть отношение "имеет". Например, в класс автомобиля содержит объект<br> класса электрического двигателя, при этом класс автомобиля создает объект двигателя.
От композиции следует отличать агрегацию. Она также предполагает отношение HAS A, но реализуется она иначе(через внедрение  зависимести).
</details>


<details open>
<summary>Что лучше применять и когда?
What is better use and when?
</summary>
<br>
Агрегацию, всегда, за исключением ,базовых и ненаследуемых типов.
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

