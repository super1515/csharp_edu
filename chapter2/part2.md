# Главные конструкции C# (Часть 2)

## Массивы в C#

Массив – это набор элементов определенного типа данных, к каждому элементу этого набора можно обратиться с помощью индекса:

```csharp
int[] intArray = new int[10];
for (int i = 0; i < 10; i++)
{
    intArray[i] = (int) Math.Pow(2, i + 1);
    Console.WriteLine(intArray[i]);
}
```

Выше был объявлен массив, содержащий 11 элементов типа ``int``. Затем каждому элементу массива было присвоено значение, соответствующее степени двойки.

Индексы массива начинаются с 0. До явной инициализации элементам массива соответствует стандартное значение заданного типа.

### Инициализация массивов

Помимо поэлементного присвоения значений элементам массива существует *синтаксис инициализации массива* с помощью фигурных скобок:

```csharp
int[] intArray = new int[5] {2, 4, 8, 16, 32};
```

Обратите внимание, указывать размер массива в таком случае необязательно, поскольку его размер может быть вычислен компилятором исходя из набора присвоенных значений элементов. По аналогичной причине ``new int[]`` также можно опустить:
```csharp
using System.Linq;
int[] intArrayFirst = new int[] {2, 4, 8, 16, 32};
int[] intArraySecond = {2, 4, 8, 16, 32};
Console.WriteLine(intArrayFirst.SequenceEqual(intArraySecond));
```
Как можно видеть, массивы идентичны.

### Неявно типизированные массивы
Аналогично переменным синтаксис с ключевым словом ``var`` можно использовать в отношении массивов:
```csharp
var intArraySecond = new[] {2, 4, 8, 16, 32};
```
Подобный синтаксис требует обязательное наличие ключевого слова ``new``. Несмотря на то, что массив может иметь тип ``System.Object`` элементы в списке инициализации должны быть одного типа.

### Массив object

Так как ``System.Object`` является базовым классом для всех типов, элементы массива ``System.Object`` могут быть любого типа:

```csharp
object[] objectArray = {2, "4", 8F, 16L, 32M};
foreach (object obj in objectArray){
    Console.WriteLine($"Value: {obj}, type: {obj.GetType()}");
}
```

### Многомерный массив

Многомерный массив имеет несколько измерений определенной длины:

```csharp
int[,,] mdArray = new int[2, 2, 3]{ { { 2, 3, 4 }, { 5, 6, 7 } }, { { 8, 9, 10 }, { 11, 12, 13 } } };
Console.WriteLine($"Number of array dimensions: {mdArray.Rank}");
for (int i = 0; i < mdArray.GetLength(0); i++)
{
    for (int j = 0; j < mdArray.GetLength(1); j++)
    {
        for (int k = 0; k < mdArray.GetLength(2); k++)
        {
            Console.Write(mdArray[i, j, k] + " ");
        }
        Console.WriteLine();
    }
    Console.WriteLine();
}
```
Получить количество измерений можно воспользовавшись свойством ``Rank``, а количество элементов в конкретном измерении можно определить с помощью метода ``GetLength()``.

### Ступенчатый массив

Ступенчатый массив может содержать множество вложенных массивов различной длины:

```csharp
int[][][] jaggedArray = new int[3][][];
for (int i = 0; i < jaggedArray.Length; i++)
{
    jaggedArray[i] = new int[i + 1][];
    for (int j = 0; j < jaggedArray[i].Length; j++)
    {
        jaggedArray[i][j] = new int[i + j + 1];
        for (int k = 0; k < jaggedArray[i][j].Length; k++)
        {
            jaggedArray[i][j][k] = (int)Math.Pow(2, k);
        }
    }
}
for (int i = 0; i < jaggedArray.Length; i++)
{
    for (int j = 0; j < jaggedArray[i].Length; j++)
    {
        for (int k = 0; k < jaggedArray[i][j].Length; k++)
        {
            Console.Write(jaggedArray[i][j][k] + " ");
        }
        Console.WriteLine();
    }
    Console.WriteLine();
}
```
