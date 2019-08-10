## Language C
- [Hello, world!](#hello-world)
- [Директива include](#директива-include)
- [Функция](#функция)
- [Базовые типы данных](#базовые-типы-данных)
- [Массивы](#массивы)
- [Структуры](#структуры)
- [Обьединения](#обьединения)
- [Битовые поля](#битовые-поля)
- [Указатели](#указатели)
- [Строки](#строки)
- [Цикл for](#цикл-for)
- [Цикл while](#цикл-while)
- [Цикл do while](#цикл-do-while)
- [Логические операторы](#логические-операторы)
- [Цепочка if else](#цепочка-if-else)
- [Конструкция switch](#конструкция-switch)
- [Кернарный оператор](#тернарный-оператор)

## Hello, world!
Соблюдая традицию, попробуем вывести "Hello, world!". Для этого запустите на выполнение следующий фрагмент:
```c
#include <stdio.h>

int main() {
	printf("%s", "Hello, world!");
	return 0;
}
```
## Директива include
Команда `#include <имя_файла>` является указанием компилятору включить в сборку некий файл. В нашем случае подключается файл `stdio.h` (STD Input-Output), который является стандартной библиотекой функций ввода-вывода. Именно в нём реализована функция `printf`. Можно поключить любое количество внешних файлов:
```c
#include <stdio.h>
#include <math.h>

int main() {
	printf("%f %s", pow(2.0, 3), "Hello, world!");
	return 0;
}
```
В данном случае мы дополнительно подключили библиотеку `math.h` и воспользовались функцией возведения в степень `pow`.
## Функция
Функция - это именованный блок, который принимает параметры и по выполнению возвращает значение. В примере выше в качестве параметра функции `printf` передается `pow(2.0,3)`.
То есть функцию можно вызывать как в контексте параметра для другой (если она возвращает значение), так и в контексте присваивания (в примере ниже присваивание):
```c
#include <stdio.h>
#include <math.h>

int main() {
	double result = pow(2.0, 3);
	printf("%f %s", result, "Hello, world!");
	return 0;
}
```
Программа на С может состоять из сколько угодно функций, но в любом случае должна существовать точка входа - `main`. По этому имени компилятор определяет функцию, с которой начинается выполнение программы.
```c
#include <stdio.h>
#include <math.h>

int sum(int, int); //Прототип

//Определение
void writeVariables(const char *strl, int inti) { 
	printf("%s %i", strl, inti);
}

int main() { //Точка входа 
	//Вызов функций в main
	writeVariables("Hello, world!", sum(5, 7));
	return 0;
}

int sum(int a, int b) { //Определение
	return a + b;
}
```
Если реализация функции в коде находится ниже той, в которой она вызывается - нужно указать её прототип до прототипа или обьявления вызывающей (иначе вызывающая функция её просто не "увидит").
При обьявлении функции первым указывается тип возвращаемого значения, или `void`, если таковой отсутствует. Пример:
```c
#include <stdio.h>
#include <string.h>

int integerFuncQ { 
	return 10;
}
float floatFuncQ { 
	return 10.0f;
}
char charFuncQ { 
	return 'a';
}

void main()
{
	printf("%d %f %c", integerFuncQ, floatFuncQ, charFuncQ);
}
```
## Базовые типы данных

| Тип данных                   |  Бит  | Диапазон значений                               |
|------------------------------|-------|-------------------------------------------------|
| char                         |   8   | от -128 до 127                                  |
| signed char                  |   8   | от -128 до 127                                  |
| unsigned char                |   8   | от 0 до 255                                     |
| short int                    |   16  | от -32768 до 32767                              |
| unsigned int                 | 16/32 | от 0 до 65535 от 0 до 4294967295                |
| int                          | 16/32 | от -32768 до 32767 от -2147483648 до 2147483647 |
| long                         |   32  | от -2147483648 до 2147483647                    |
| unsigned long                |   32  | от 0 до 4294967295                              |
| long long int (C99)          |   64  | от -2^63 - 1 до 2^63 - 1                        |
| unsigned long long int (C99) |   64  | ОТ 0 до 2^64 - 1                                |
| float                        |   32  | от 3.4Е-38 до 3.4Е38                            |
| double                       |   64  | от 1.7Е-308 до 1.7Е308                          |
| long double                  |   80  | от 3.4Е-4932 до 3.4Е4932                        |
| _Bool (C99)                  |   8   | true(l), false(0)                               |

* `signed` - знаковый `unsigned` - беззнаковый
  

## Массивы
Массивы данных определяются следующим образом: `тип_данных ___имя[количество элементов]___`
Пример:
```c
#include <stdio.h> void main()
{
	int integersArray[50]; //Массив 

	int i = 0;
	for(i = 0; i < 50;) { //Заполнение 
		integersArray[i] = ++i;
	}

	for(i = 0; i < 50;) { //Вывод
		printf(" %d ", integersArray[++i]);
	}
}
```
Обратите внимание на то, что размерность массива можно указывать только беззнаковой целой константой. Для удобства код выше можно переписать так:
```c
#include <stdio.h> void main()
{
	const unsigned short int arraySize = 50;

	int integersArray[arraySize]; //Массив

	int i = 0; //Итератор
	for(i = 0; i < arraySize;) { //Заполнение 
		integersArray[i] = ++i;
	}
	for(i = 0; i < arraySize;) { //Вывод 
		printf(" %d ", integersArray[++i]);
	}
}
```
## Структуры
Структура в Си является "связкой" нескольких переменных разных типов в один псевдообьект. Обьявление структуры выглядит так:
`struct **имя {тип_1 переменная_1; тип_2 переменная_2;...}**`
Пример:
```c
#include <stdio.h>
//Можно определить в глобальном пространстве
typedef struct { 
	int а; 
	int b;
} elseStruct;

void main()
{
	struct myStructure { //Или 8 локальном
		int a;
		int b; 
		char c; 
		double d;
	};

	struct myStructure strct =	{ 1, 2, 'a', 10.32 }; //Инициализация
	struct myStructure strctCopy = strct; //Копирование 

	printf("*i %i %c *f", strctCopy.a, strctCopy.b, strctCopy.c, strctCopy.d);

	elseStruct elseStrct; //При обьявлении через typedef 
	elseStrct.a = 100;
	elseStrct.b = 200;
	
	printf("Xn%i %i", elseStrct.a, elseStrct.b);
}
```
Обратите внимание: при определении структуры не через `typedef`, при инициализации нужно указывать `struct`. Также можно определять массивы структур.
## Обьединения
Обьединение - это структура, которая в момент времени может хранить значение только одного из её полей, поэтому размер обьединения равен размеру наибольшего из них.
```c
#include <stdio.h>

typedef union { 
	short a; 
	int b;
	long long c;
} myUnion;
void main() {
	myUnion test;
	test.a = 12345;

	printf("%i", test.a); //OK
	printf("%i", test.b); //Error
}
```
## Битовые поля
Битовое поле - это число, которое занимает некоторый набор битов, напрямую не адресуемых процессором. Использование битовых полей оправдано в случаях, когда компактность информации гораздно более важна, чем скорость доступа к ней. Пример:
```c
struct rgb {
	unsigned r:8; //8 бит 
	unsigned g:8;
	unsigned b:8;
};
```
## Указатели
Указатель - это переменная, которая хранит адрес ячейки памяти. Указатели используются для косвенной адресации и динамического выделения памяти:
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	printf("Введите рамер массива: ");
	int arraySize;
	scanf("%d", &arraySize);

	//Выделение памяти функцией calloc
	int *dynamicArray = (int*)calloc(arraySize, sizeof(int));

	int i;
	for(i = 0; i < arraySize; i++) dynamicArray[i] = i;
	for(i = 0; i < arraySize; i++) printf("%d", dynamicArray[i]);

	free(dynamicArray); //Освобождение памяти
	return 0;
}
```
Взятие значения из указателя производится посредством разыменования `(оператор *)`. Взятие адреса обычной переменной выполняет оператор `&`. Пример с адресацией:
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	//Выделение памяти
	int *pointerToInteger = (int*)malloc(sizeof(int));
	*pointerToInteger = 5;
	//Копирование значения из динамической переменной в нединамическую
	int stacklnteger = *pointerToInteger;
	//Можно обращаться по указателю, но нельзя оперировать с памьятью
	int *pointerToStackInteger = Sstacklnteger; //взятие адреса //Копирование адреса 8 другой указатель
	int *stackIntegerAddress = pointerToInteger; free(stacklntegerAddress); //OK
	//Ошибка! Очистка по указанному адресу уже производилась
	free(pointerToInteger);

	return 0;
}
```
## Строки
Строка - это указатель на массив символов, последний элемент которого равен null-терминатору (символ \0). Он нужен для того, чтобы при помещении строки в поток функция могла определить конец последовательности. Пример:
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main()
{
	//Строковый литерал
	const char *strLiteral = "String Literal";
	//Ввод пользовательской строки
	char *buffer = (char*)calloc(1024, sizeof(char)); //Буфер с запасом
	
	printf ("Введите строку:");
	scanf("%s", buffer);

	//Выделяем ровно столько памяти, сколько нужно
	char *result = (char*)calloc((strlen(buffer) + 1), sizeof(char));

	strcpy(result, buffer); //Копируем содержимое буфера
	free(buffer); //Удаляем буфер

	printf("\nВы ввели: %s", result);

	if(result[strlen(result)] == '\0') //Проверка на null-терминированность
	{
		printf ("\nСтрока завершена символом \"\\0\"");
	}
	free(result); //Удаляем строку после использования return 0;
}
```
## Цикл for
Чаще всего применяется, когда перед запуском число итераций известно. Пример:
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int i;
	for(i = 0; i < 50; i++) //С инкрементом
		printf(" %d ", i);
	for(i = 10; i > 0; i--) //С декрементом
		printf(" %d ", i);
	for(i = 20; i > 0;) //Нестандартный
	{
		printf(" %d ", i); i-=3;
	}
	return 0;
}
```
## Цикл while
Применяется, когда число итераций заранее не известно. Пример:
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main()
{
	srand(time(NULL));
	int i = randQ % 100; //Случайное число
	
	while(i > 0) {
		printf(" %d ", i);
		i--;
	}

	return 0;
}
```
## Цикл do while
Является циклом while с постусловием, то есть вне зависимости от выполнения условия блок выполнится как минимум один раз:
```c
#include <stdio.h>
int main()
{
	int i = 1;
	do
	{
		printf("%i не больше десяти, но пока цикл об этом \"не знает\"\n", i);
	while (i > 10);

	printf("Taк как %i не больше 10, цикл выполнил только первую итерацию", i);
	return 0;
}

```
## Пропуск (`continue`) Прерывание (`break`)
Если в цикле требуется пропустить итерацию, нужно использовать `continue`:
```c
#include <stdio.h>
int main()
{
	int val = 20; int i;
	for(i = 0; i < 10; i++)
	{
		printf("Значение val равно %i\n", val);
		//Здесь итерация завершится и пойдёт следующая
		continue;
		val++; //Не выполнится, так как сверху пропуск итерации
	}
	return 0;
}
```
Преждевременный выход из цикла совершает `break`:
```c
#include <stdio.h>
int main()
{
	int val = 20; int i;
	for(i = 0; i < 10000; i++, val++)
	{
		printf("Значение val равно %iXn", val);
		//He смотря на то, что итераций 10 000, выполнение цикла прервётся
		//Как только val станет больше 30
		if(val > 30) break;
	}
return 0;
}
```
## Логические операторы

| Оператор | Обозначение      |
|----------|------------------|
|    `>`   | больше           |
|    `<`   | меньше           |
|   `>=`   | больше или равно |
|   `<=`   | меньше или равно |
|   `==`   | равно            |
|   `!=`   | не равно         |
|   `&&`   | И                |
|    `!`   | НЕ               |
|  `\|\|` | ИЛИ              |

Как пример, рассмотрим условные выражения. Любое условное выражение возвращает bool-значение `true(1)` или `false(O)`:
```c
#include <stdio.h>
int main()
{
	int i = 1; int j = 10;
	bool iGtTwo = i > 2; //false

	if(iGtTwo || j > 8)
		printf("Как минимум одно из условий выполнено\n");
	if (! iGtTwo && j > 8)
		printf("Оба условия выполнены\n"); //Не выведется
}
```
## Цепочка if-else
Пример использования условий в цепочке `if-else`:
```c
#include <stdio.h>
int main()
{
	int i = 1;
	if(i > 3) 
		printf("i больше 3\n");
	else
		if(i <= 1) 
			printf("i меньше или равно l\n");
	else 
		printf("Пo всей видимости i равно 2");
}
```
Меняйте значение i и наблюдайте за поведением программы.
## Конструкция switch
Используется, когда нужно проверить множество условий. Более удобен, чем `if-else` (тем не менее `switch` и `if-else` взаимозаменяемы). Пример:
```c
#include <stdio.h>
int main()
{
	int i = 2;
	switch(i) {
	//break нужен для выхода из switch
	//во избежание выполнения послед"ующих выражений
		case 0: printf("i равно нулю"); break;
		case 1: printf("i равно 1"); break;
		case 2: printf("i равно 2"); break;
		default: 
			//Выполнится, если не найден соответствующий case 
			printf("switch не содержит значение, которому равен i");
			//Обратите внимание: после последнего
			// case (или default) ставить break не имеет смысла
		}
	return 0;
}
```
## Тернарный оператор
Тернарный оператор `?:` позволяет в зависимости от выполнения условия выбрать возвращаемое значение. Пример:
```c
#include <stdio.h>
//Тернарный оператор в примере можно заменить такой конструкцией
int ternaryReplacer(bool condition, int resultTrue, int resultFalse) { 
	if (condition == 1) //Если условие состоялось
		return resultTrue; 
	else 
		return resultFalse;
}

int main()
{
	//Если 5 больше 10, вернуть 40, иначе вернуть 100
	int i = 5 > 10 ? 40 : 100;
	//То же самое
	int j = ternaryReplacer(5 > 10, 40, 100);
	printf("i: %i, j: %i", i, j); //Проверим

	return 0;
}
```
