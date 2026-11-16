# Практика по Python
## Тема 1.1 Введение
**Задание 1: «Калькулятор возраста»**
Программа спрашивает у пользователя год рождения и текущий год, вычисляет и выводит возраст. Если пользователь ввел не число — программа не падает, а выводит ```Ошибка, введите число```.

```
try:
    user_age = int(input("Введите свой год рождения: "))
    current_year = int(input("Напишите какой сейчас год: "))
    print(current_year - user_age)
except ValueError:
    print("Ошибка, введите число!")
```

**Задание 2: «Конвертер валют»**
Спроси у пользователя сумму в долларах и курс (например, 90.5). Выведи сумму в рублях с точностью до 2 знаков. Используй ```format()``` или ```round()```.

```
try:
    dollars_sum = float(input("Enter count money in $: "))
    carr_rate = float(input("Enter rate dollar: "))
    rubles = dollars_sum * carr_rate
    print(round(rubles,2),"RUB")
except ValueError:
    print("Error! Please enter numbers only.")
```

## Тема 1.2 Условные операторы, циклы и т.д.
**Задание 1: «Определитель времени суток»**
Программа спрашивает текущий час (0–23). Выводит:

6–11 → "Утро"

12–17 → "День"

18–23 → "Вечер"

0–5 → "Ночь"

Если пользователь ввел число вне диапазона — выведи "Ошибка".
```
try:
    HourOfTime = int(input("Enter the hour of time: "))
    if 6 <= HourOfTime <= 11:
        print("Morning")
    elif 12 <= HourOfTime <= 17:
        print("Day")
    elif 18 <= HourOfTime <= 23:
        print("Evening")
    elif 0 <= HourOfTime <= 5:
        print("Night")
    elif HourOfTime < 0 or HourOfTime > 23:
        print("Please, enter correct hour of time!")
except ValueError:
    print("Error, please try again!")
```
**Задание 2: «Калькулятор с проверкой»**
Спроси у пользователя два числа и операцию (+, -, *, /).

Если операция / и второе число = 0 → выведи "Делить на ноль нельзя".

Если введена неизвестная операция → выведи "Неизвестная операция".

Иначе выведи результат.
```
try:
    FirstNumber = float(input("Enter 1-st number: "))
    SecondNumber = float(input("Enter 2-nd number: "))
    math_operation = input("Enter math operation: ")
    if math_operation == "+":
        print(FirstNumber + SecondNumber)
    elif math_operation == "-":
        print(FirstNumber - SecondNumber)
    elif math_operation == "*":
        print(FirstNumber * SecondNumber)
    elif math_operation == "/":
        if SecondNumber == 0.0:
            print("Sorry, but you cant divide by zero!")
        else:
            print(FirstNumber / SecondNumber)
    else:
        print("Error, please enter correct math operation!")
except ValueError:
    print("Error, please try again!")
```

## Тема 1.3 Циклы и операторы в них (for, while)

**Задание 1: «Таблица умножения»**
Выведи таблицу умножения от 1 до 10 в формате:

1 x 1 = 1 ... 10 x 10 = 100

Используй вложенный цикл for.
```
for num1 in range(1, 11):
    for num2 in range(1,11):
        result = num1*num2
        print(f"{num1} * {num2} = {result}")
```

**Задание 2: «Угадай число»**
Программа загадывает случайное число от 1 до 100. Пользователь вводит числа, пока не угадает. После каждой попытки программа подсказывает: "Больше" или "Меньше". При угадывании выводит "Поздравляю!" и количество попыток.
```
import random
try:
    secret_number = random.randint(1,100)
    status_check = True
    attempt = 0
    while status_check:
        attempt += 1
        print(f"Attempt #{attempt}")
        hidden_number = int(input("Guess the number from 1 to 100: "))
        if hidden_number < 1 or hidden_number > 100:
            print("Please enter a number between 1 and 100!")
            attempt -= 1
            continue
        if secret_number == hidden_number:
            status_check = False
            print(f"Congratulations, you guessed it right in {attempt}!")
            break
        elif secret_number > hidden_number:
            print("More!")
        else:
            print("Less!")
except ValueError:
    print("Please try again!")
```


## Тема 1.4 Списки(list). Функции и их методы

**Задание 1: «Список покупок»**
Программа позволяет добавлять товары в список, удалять товары и выводить текущий список. Пользователь вводит команды: + молоко (добавить), - молоко (удалить), list (показать), exit (выйти).
```
ShoppingList = []

print("__Это программа список покупок в магазин__")
print("Если хотите добавить товар/товары в список, введите: + товар")
print("Если хотите убрать товар/товары из списка, введите: - товар")
print("Чтобы посмотреть список покупок, введите: list")
print("Для выхода из программы, введите: exit")

while True:
    Command = input("Введите команду:").strip()
    if not Command:
        continue

    if Command == "exit": #Выход из программы
        print("Возвращайтесь снова!")
        break

    elif Command == "list": #Вывод списка покупок
        if not ShoppingList:
            print("Ваш список пуст")
        else:
            print("Ваш список покупок:")
            for el in ShoppingList:
                print(f"- {el}")

    elif Command.lstrip().startswith("+"): #добавление в список
        items = Command.lstrip("+").strip().split()
        for item in items:
            if item in ShoppingList:
                print(f"{item} уже добавлен в список")
            else:
                ShoppingList.append(item)
                print(f"Вы добавили {item} в список!")

    elif Command.lstrip().startswith("-"): #Удаление из списка
        items = Command.lstrip("-").strip().split()
        for item in items:
            if item in ShoppingList:
                ShoppingList.remove(item)
                print(f"Вы убрали {item} из списка!")
            else:
                print(f"Товара {item} нету в списке")
    else:
        print("Введите команду правильно!")
```


**Задание 2: «Уникальный список»**
Пользователь вводит 10 чисел. Программа убирает все дубликаты и выводит только уникальные числа в том порядке, как они встретились впервые.
```
try:
    List = input("Введите 10 чисел через пробел: ").split()
    if len(List) == 10:
        Unique_List = []
        for num in List:
            if int(num) not in Unique_List:
                Unique_List.append(int(num))
        print(f"Ваш уникальный список - {Unique_List}")
    else:
        print("Введите 10 чисел!!!")
except ValueError:
    print("Ошибка, введите числа!")
```

## Тема 1.5: Словари (dict) и работа с ними.

**Задание 1: «Телефонная книга»**
Создай словарь ```contacts = {"Анна": "89121234567", "Петр": "89221234567"}```. Программа спрашивает имя и выводит номер телефона. Если имени нет — предлагает добавить новый контакт (спрашивает номер и сохраняет). Команда ```exit``` — выход.
```
PhoneBook = {}
while True:
    NameContact = input("Введите имя (или exit):").lower().strip()
        
    if NameContact.lower().strip() == "exit": #Выход из Книги Контактов
        print("До скорой встречи!")
        break
    elif not NameContact:
        continue
    elif NameContact.lower().strip() not in PhoneBook:#Если контакт не найден
        print(f"Контакт \"{NameContact.title()}\" не найден. Хотите добавить ? (да/нет):")
        Answer = input().strip()
        if Answer.lower().strip() == "да":#если хотят добавть контакт
            NumberPhone = input(f"Введите номер для контакта \"{NameContact.title()}\":")
            if not NumberPhone:
                print("Пожалуйста в следующий раз введите номер телефона!")
                continue
            PhoneBook[NameContact.lower().strip()] = NumberPhone.strip()
            print(f"Контакт {NameContact.title()} успешно добавлен!")

        elif Answer.lower().strip() == "нет":#если не хотят добавлять 
            continue

    elif NameContact.lower().strip() in PhoneBook:
        print(f"{NameContact.title()} - {PhoneBook[NameContact]}.")
```

**Задание 2: «Чет-нечет»**

Пользователь вводит 10 чисел. Программа заносит числа в два списка: even (четные) и odd (нечетные). Затем выводит словарь вида: ```{"even": [2, 4, 6], "odd": [1, 3, 5]}```.
Пример
```
Введите 10 чисел через пробел: 1 2 3 4 5 6 7 8 9 10
Результат:
Четные: [2, 4, 6, 8, 10]
Нечетные: [1, 3, 5, 7, 9]
```

```
try:
    while True:

        ListNum = {"Even": [], "Odd": []} #Четные и нечётные
        numbers = input("Введите 10 чисел через пробел:").split()
        if len(numbers) != 10:
            print("Пожалуйста введите ровно 10 чисел!")
            continue
        for check in numbers:
            if int(check) % 2 == 0: #Четные
               ListNum["Even"].append(int(check))
            else: #Нечётные
               ListNum["Odd"].append(int(check))
        print(f"Чётные - [{ListNum["Even"]}]\nНечётные - [{ListNum["Odd"]}]")
        break
except ValueError:
    print("Ошибка, пожалуйста введите числа!")
```

## Тема 1.6: Функции (def)

**Задание 1: «Калькулятор в функции»**

Напиши функцию ```calc(a, b, operation)```, которая принимает два числа и операцию, а возвращает результат. Вызови её для разных наборов аргументов. Если операция неизвестна — возвращай None.
```
def calc(num1,num2,operation):
    if operation == "+": 
        return num1 + num2

    elif operation == "-":
        return num1 - num2

    elif operation == "*":
        return num1 * num2

    elif operation == "/":
        if num2 == 0:
            print("Ошибка, деление на ноль!")
            return None
        else:
            return num1 / num2

    elif operation == "%":
        if num2 == 0:
            print("Ошибка, деление на ноль!")
            return None
        else:
            return num1 % num2

    elif operation == "//":
        if num2 == 0:
            print("Ошибка, деление на ноль!")
            return None
        else:
            return num1 // num2
    elif operation == "**":
        return num1 ** num2
    else:
        print ("Такой операции нету!")
        return None

print("___Калькулятор___")
try:
    num1 = float(input("Введите 1-е число:"))
    num2 = float(input("Введите 2-е число:"))
    print("Математические операции:")
    print("+ , - , * , / , % , // , **")
    operation = input("Введите математическую операцию:").strip()
    print(f"Результат = {calc(num1,num2,operation)}")
except ValueError:
    print("Ошибка, введите число!")
```
**Задание 2: «Фильтр списка»**
Напиши функцию ```filter_list(lst, min_val, max_val)```, которая принимает список чисел и возвращает новый список, содержащий только числа от ```min_val``` до ```max_val``` включительно.

Пример: ```filter_list([1, 5, 10, 15, 20], 5, 15)``` → ```[5, 10, 15]```.
```
def filter_list(List,min_val,max_val):
    filt_lst = []
    min_val = int(min_val)
    max_val = int(max_val)
    for value in List:
        value = int(value)
        if min_val <= value <= max_val:
            filt_lst.append(value)
    return filt_lst

try:
    while True:
        UserList = input("Введите список чисел через пробел:").split()
        if not UserList:
            continue
        else:
            break
    while True:
        min_value = input("Введите минимальное значение для диапазона:")
        if not min_value:
            continue
        else:
            break
    while True:
        max_value = input("Введите максимальное значение для диапазона:")
        if not max_value:
            continue
        else:
            break
    print(f"{filter_list(UserList, min_value, max_value)} - ваш отфильтрованный список в диапазоне от {min_value} до {max_value}")

except ValueError:
    print("Ошибка, введите числа!!!")
```

## Тема 0.7: Работа с файлами (чтение/запись)

**Задание 1: «Дневник заметок»**

Программа спрашивает у пользователя текст заметки и сохраняет её в файл ```notes.txt``` с датой и временем (используй ```datetime.now()```). При следующем запуске программа показывает все сохраненные заметки.
```
from datetime import datetime

with open("diary.txt","a") as file:
    while True:
        timepoint = datetime.now().strftime("%Y-%m-%d %H:%M")
        note = input("Введите заметку/Для выхода(Exit): ")
        if not note:
            print("Вы ничего не написали")
            continue
        elif note.strip() == "exit":
            break
        else:
            print("Заметка сохранена!")
            file.write(f"[{timepoint}] {note.strip()}\n")

with open("diary.txt","r") as file:
    print("--- Ваши заметки ---")
    print(file.read().strip())
```

## Задание 2: «Анализатор логов»
У тебя есть файл ```log.txt```, в котором каждая строка содержит IP-адрес и статус (например, 192.168.1.1 200). Напиши программу, которая:

Читает файл.

Подсчитывает количество успешных запросов (статус 200).

Выводит список уникальных IP-адресов.
```
countRequest = 0
countSuccess = 0
uniqueIP = []
try:
    with open("log.txt", "r") as file:
        for line in file:
            partsIP = line.strip().split()
            countRequest += 1
            if len(partsIP) != 2 :
                print(f"Ошибка, у лога под номером {countRequest} не хватает IP-адреса или статуса вывода!")
                continue

            if partsIP[0] not in uniqueIP:
                uniqueIP.append(partsIP[0].strip())
            
            if partsIP[1] == "200":
                countSuccess += 1
            
        print("--- Анализ логов ---")
        print(f"Всего запросов: {countRequest}")
        print(f"Успешных (200): {countSuccess}")
        print(f"Уникальные IP: {uniqueIP}")
except FileNotFoundError:
    print("Ошибка, файл log.txt не найден!")
```

## Тема 0.8: Обработка ошибок (try/except)

**Задание 1: «Безопасное деление»**

Напиши функцию safe_div(a, b), которая возвращает результат деления или None, если произошла ошибка. Протестируй с делением на ноль и с нечисловыми аргументами.
```
def save_div(num1,num2):
    try:
        return(num1/num2)
    except (ZeroDivisionError,TypeError):
        return None

while True:
    try:
        num1 = float(input("Введите 1-ое число:"))
        num2 = float(input("Введите 2-ое число:"))
        result = save_div(num1,num2)
        if result is not None:
            print(f"Результат = {result}")
        else:
            print("Ошибка, нельзя выполнить деление!")
        break
    except ValueError:
       print("Ошибка, введите число!")
```

**Задание 0.8.2: «Чтение файла с защитой»**

Программа просит пользователя ввести имя файла. Пытается открыть его и вывести содержимое. Если файл не найден — выводит "Файл не найден". Если другая ошибка — выводит её текст.
```
while True:
    try: 
        findfile = input("Введите название файла(или выход):")
        if findfile.strip().lower() == "выход":
            break
        if not findfile.endswith(".txt"):
            txt = findfile + ".txt"
        else:
            txt = findfile
        with open(txt, "r") as file:
            print(f"Содержимое файла: \n{file.read()}")
            break
    except FileNotFoundError:
        print("Файл, не найден!")
        makethefile = input(f"Хотите создать файл с таким названием \"{findfile}\" ? (да/нет):")
        if makethefile.strip().lower() == "да":
            with open(txt, "a") as file:
                text = input("Введите текст в файл: ")
                file.write(text)
        elif makethefile.strip().lower() == "нет":
            print("До скорой встречи!")
            break
    except Exception as Error:
        print(f"{Error} - ваша ошибка!")
```


Итоговый проект уровня 0: «Менеджер задач» (To-Do List)
Объедини всё, что выучил. Напиши программу, которая работает через консоль:

Функциональность:

Добавить задачу (спрашивает текст → сохраняет в файл tasks.txt).

Показать все задачи (читает файл и нумерует строки).

Удалить задачу по номеру (удаляет указанную строку из файла).

Завершить работу (выход).

Требования:

Используй функции для каждой команды.

Используй обработку ошибок (если файл не найден — создай новый).

Данные храни в обычном текстовом файле (одна строка — одна задача).

```
#Итоговый проект: «Менеджер задач» (To-Do List)
#Написать программу, которая управляет списком задач и сохраняет их в файл tasks.txt
#Программа должна уметь:
#1 Добавить задачу — пользователь вводит текст, задача сохраняется в файл. +
#2 Показать все задачи — выводит список с номерами и статусом ([ ] или [X]). +
#3 Отметить задачу выполненной — по номеру задачи.
#4 Удалить задачу — по номеру задачи.
#5 Выход — сохраняет всё и завершает работу.



def save_tasks(tasks,filename = "tasks.txt"): #сохраняет в файл задачи от tasks в виде (0|задача)
    with open (filename, "w") as f:
        for task in tasks:
            done = "1" if task["done"] else "0"
            f.write(f"{done}|{task['text']}\n")

def load_tasks(filename = "tasks.txt"): #загружаем данные из файла в переменную tasks чтобы дальше с ней работать
    tasks = []
    try:
        with open(filename, "r") as f:
            for line in f:
                line = line.strip()
                if not line: continue
                done,text = line.split("|",1)
                tasks.append({"done": done == "1", "text": text})
    except FileNotFoundError:
        pass
    return tasks 

def add_task(tasks): #Добавление задачи
    text_tasks = input("Введите задачу: ").strip()
    if not text_tasks:
        print("Задача не была добавлена!")
        return
    tasks.append({"done": False, "text": text_tasks})
    save_tasks(tasks)
    print("Задача добавлена!")

def show_tasks(tasks): #Показ задач
    count_task = 0
    if not tasks:
        print("Список задач пуст...")
        return
    print("Ваши задачи:")
    for line in tasks:
        count_task += 1
        status = "X" if line["done"] else " "
        print(f"[{status}] {count_task}. {line['text']}")

def mark_done(tasks): #Отметка задач
    show_tasks(tasks)
    if not tasks:
        return
    try:
        marknum = int(input("Введите номер задачи, которую хотите отметить выполненной:"))
        if 1 <= marknum <= len(tasks):
            tasks[marknum - 1]["done"] = True
            save_tasks(tasks)
            print(f"Вы отметили задачу ({tasks[marknum-1]['text']}) выполненной!")
        else:
            print("Вы вышли из диапазона!")
        
    except ValueError:
        print("Ошибка, введите число!")

def delete_task(tasks): #удаление задач
    show_tasks(tasks)
    if not tasks:
        return
    try:
        delnum = int(input("Введите номер задачи, которую хотите удалить: "))
        if 1 <= delnum <= len(tasks):
            removed = tasks.pop(delnum-1)
            save_tasks(tasks)
            print(f"Вы удалили задачу ({removed['text']})!")
        else:
            print("Вы вышли из диапазона!")
    except ValueError:
        print("Ошибка, введите число!")


def main():
    tasks = load_tasks()
    while True:
        print("---Менеджер задач---")
        print("1. Добавить задачу")
        print("2. Показать задачу")
        print("3. Отметить выполненной")
        print("4. Удалить задачу")
        print("5. Выход")
        choice = input("Выберите действие: ").strip()
        if choice == "1":
            add_task(tasks)
        elif choice == "2":
            show_tasks(tasks)
        elif choice == "3":
            mark_done(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            print("Возвращайтесь снова!")
            break
        else:
            print("Неизвестная команда!")
        print("\n")

if __name__ == "__main__":
    main()
```

