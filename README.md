# Code-Review


## Contents
- [Строки](#strings)
    - [Подсчет количества повторений букв в слове](#1)
    - [Является ли слово анаграммой](#2)
    - [Строка в обратном порядке](#3)
    - [Поиск полок в библиотеке с определенными книгами](#4)
    - [Определение монотонной последовательности чисел в строке](#5)
    - [Поиск самой длинной подстроки без повторяющихся символов](#6)
    - [Рассадка зрителей в кинозале](#7)
- [Числа, массивы](#numbers)
    - [Поиск трех и более последовательных чисел в массиве](#8)
    - [Поиск одинакового числа в массивах](#9)
    - [Представление числа в обратном порядке](#10)
    - [Поиск НЕ одинакового числа среди одинаковых в массивах](#11)
    - [Перенести все нули в массиве в конец](#12)

## strings
### 1
**Написать функцию, принимающую два аргумента - слово и букву.<br>
Функция должна посчитать, сколько раз эта буква встречается в данном слове,<br>
и вернуть полученное число вхождений. И то же самое без учета регистра.**
```
def count_letter(word, letter):
    # Считаем количество вхождений без учета регистра
    count_case_insensitive = word.lower().count(letter.lower())
    # Считаем количество вхождений с учетом регистра
    count_case_sensitive = word.count(letter)
    return count_case_insensitive, count_case_sensitive

# Пример использования функции
word = "Hello World"
letter = "o"
count_insensitive, count_sensitive = count_letter(word, letter)
print(f"Количество вхождений без учета регистра: {count_insensitive}")
print(f"Количество вхождений с учетом регистра: {count_sensitive}")
```

### 2
**Написать функцию, которая проверяет, является ли одно слово анаграммой другого.
На вход подается 2 строки. На выходе true или false.**
```
def is_anagram(word1, word2):
    # Убедимся, что оба слова имеют одинаковую длину
    if len(word1) != len(word2):
        return False
    
    # Преобразуем оба слова в нижний регистр для удобства сравнения
    word1 = word1.lower()
    word2 = word2.lower()
    
    # Преобразуем слова в списки символов и сортируем их
    sorted_word1 = sorted(word1)
    sorted_word2 = sorted(word2)
    
    # Если отсортированные списки равны, слова являются анаграммами
    return sorted_word1 == sorted_word2

# Пример использования:
word1 = "listen"
word2 = "silent"
print(is_anagram(word1, word2))  # Выведет: True
```
### 3
**Реализовать функцию, которая будет возвращать переданную строку в развернутом виде.<br>
Функция на вход должна принимать строку и на выходе возвращать строку.**
```
def reverse_string(input_str):
    # Используем срезы для разворота строки
    return input_str[::-1]
# Пример использования:
input_str = "Hello, world!"
print(reverse_string(input_str))  # Выведет: "!dlrow ,olleH"
```
### 4
**Найти все полки в библиотеке, на которых стоят книги Ремарка.**
```
def find_shelves_with_remarque_books(library_database):
    shelves_with_remarque_books = set()
    for book in library_database:
        if book["author"] == "Ремарк":
            shelves_with_remarque_books.add(book["shelf"])
    return shelves_with_remarque_books

# Пример использования:
library_database = [
    {"title": "Три товарища", "author": "Ремарк", "shelf": "A1"},
    {"title": "Черный обелиск", "author": "Ремарк", "shelf": "B2"},
    {"title": "1984", "author": "Оруэлл", "shelf": "C3"},
    # Другие книги...
]

shelves_with_remarque_books = find_shelves_with_remarque_books(library_database)
print("Полки с книгами Ремарка:", shelves_with_remarque_books)
```

### 5
**Напишите функцию, которая принимает входную строку, которая состоит из целых положительных чисел, разделенных пробелами. <br>
Функция должна определять, является ли последовательность чисел монотонной. <br>
Если последовательность монотонна, возвращаем 'yes', иначе 'no'.**
```
def isMonotonic(string):
    numbers = list(map(int, string.split()))

    # Проверяем, является ли последовательность монотонно возрастающей
    if all(numbers[i] <= numbers[i+1] for i in range(len(numbers)-1)):
        return 'yes'
    # Проверяем, является ли последовательность монотонно убывающей
    elif all(numbers[i] >= numbers[i+1] for i in range(len(numbers)-1)):
        return 'yes'
    else:
        return 'no'
string = input()
print(isMonotonic(string))
```
1.	numbers = list(map(int, sequence.split())): Строка string разбивается на подстроки по пробелам с помощью метода split(), а затем каждая подстрока преобразуется в целое число с помощью функции int(). Полученные числа сохраняются в списке numbers.
2.	if all(numbers[i] <= numbers[i+1] for i in range(len(numbers)-1)):: Этот блок проверяет, является ли последовательность чисел numbers монотонно возрастающей. Он использует функцию all(), чтобы проверить, что все числа в списке numbers не убывают. Для этого он перебирает каждый элемент numbers с помощью генератора списков и проверяет, что он меньше или равен следующему элементу в списке.
3.	elif all(numbers[i] >= numbers[i+1] for i in range(len(numbers)-1)):: Этот блок проверяет, является ли последовательность чисел numbers монотонно убывающей. Он аналогичен предыдущему блоку, но проверяет, что все числа в списке numbers не возрастают.
4.	print('yes'): Если последовательность чисел монотонна (либо возрастает, либо убывает), то выводится 'yes'.
5.	else:: Если ни одно из условий выше не выполнено, то последовательность чисел не является монотонной, и выводится 'no'.

### 6
**Поиск самой длинной подстроки без повторяющихся символов**
```
def lengthOfLongestSubstring(self, s: str) -> int:
        last_occurrence = {}
    # Initialize the start of the window and the length of the longest substring
        start = 0
        max_length = 0

        for end, char in enumerate(s):
        # If the character is already in the dictionary and its last occurrence is                after the start of the window,
        # move the start of the window to the position after the last occurrence of the character
          if char in last_occurrence and last_occurrence[char] >= start:
            start = last_occurrence[char] + 1
        # Update the last occurrence of the character
          last_occurrence[char] = end
        # Update the length of the longest substring
          max_length = max(max_length, end - start + 1)

        return max_length
```
1.	Инициализация переменных:
o	last_occurrence: это словарь, который будет содержать информацию о последнем встреченном индексе каждого символа.
o	start: это переменная, которая будет отслеживать начало текущего подстроки без повторяющихся символов.
o	max_length: это переменная, которая будет содержать длину самой длинной подстроки без повторяющихся символов.
2.	Цикл по строке:
o	Мы используем цикл enumerate, чтобы получить индекс и символ на каждой позиции в строке.
o	На каждой итерации цикла мы проверяем, если текущий символ уже есть в словаре last_occurrence и его последнее вхождение произошло после начала текущей подстроки (start).
o	Если условие выполняется, мы обновляем start так, чтобы оно указывало на следующий символ после последнего вхождения текущего символа. Это позволяет нам "сдвигать" окно так, чтобы оно не содержало повторяющиеся символы.
o	Затем мы обновляем запись в словаре last_occurrence для текущего символа, указывая на его текущий индекс.
o	Мы также вычисляем длину текущей подстроки (это делается путем вычитания индекса start из индекса end и добавления 1).
o	На каждой итерации мы обновляем max_length, чтобы он содержал максимальную длину подстроки без повторяющихся символов.
3.	Возвращаем результат:
o	По завершении цикла мы возвращаем max_length, который содержит длину самой длинной подстроки без повторяющихся символов.
Таким образом, этот код использует метод скользящего окна с использованием словаря для отслеживания последних вхождений символов в строке, чтобы эффективно находить длину самой длинной подстроки без повторяющихся символов.

### 7
**Рассадить зрителей в кинозале через одного**
```
def seat_users(rows, seats_per_row):
    seating_plan = []

    # Создаем план рассадки
    for row in range(rows):
        row_seats = []
        for seat in range(seats_per_row):
            row_seats.append("X" if (row + seat) % 2 == 0 else "O")
        seating_plan.append(row_seats)

    # Выводим план рассадки
    for row in seating_plan:
        print(" ".join(row))

seat_users(5, 10)
```

## numbers

### 8
**Написать функцию, которая будет возвращать true, если поданный на ввод массив int содержит 3 и более последовательных числа в любом месте.**
```
def has_three_consecutive(nums):
    # Проверяем для каждого числа в массиве, начиная с индекса 2
    for i in range(len(nums) - 2):
        # Проверяем, являются ли три последовательных числа в массиве
        if nums[i] + 1 == nums[i+1] and  nums[i+1] + 1 == nums[i+2]:
            return True
    return False
# Пример использования функции
nums = [1, 2, 3, 4, 5]
print(has_three_consecutive(nums))  # Вернет True
```

### 9
**Даны три неубывающих массива чисел. Найти число, которое присутствует во всех трех массивах.**
```
def find_common_element(arr1, arr2, arr3):
    i = j = k = 0
    
    while i < len(arr1) and j < len(arr2) and k < len(arr3):
        # Если текущие элементы всех трех массивов равны, это общий элемент
        if arr1[i] == arr2[j] == arr3[k]:
            return arr1[i]
        
        # Иначе, перемещаемся к следующему элементу в массиве с самым маленьким текущим элементом
        min_val = min(arr1[i], arr2[j], arr3[k])
        if arr1[i] == min_val:
            i += 1
        if arr2[j] == min_val:
            j += 1
        if arr3[k] == min_val:
            k += 1
    
    # Если такого общего элемента нет
    return None

# Пример использования:
arr1 = [1, 3, 4, 6, 7, 9]
arr2 = [1, 2, 4, 5, 9, 10]
arr3 = [1, 4, 9, 11, 12]
common_element = find_common_element(arr1, arr2, arr3)
if common_element is not None:
    print("Общий элемент:", common_element)
else:
    print("Общего элемента нет")
```

### 10
**Given a signed 32-bit integer x, return x with its digits reversed.<br>
If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0**
```
def reverse(self, x: int) -> int:
      if x < 0:
        # Convert x to a string, remove the negative sign, reverse the string, and convert it back to an integer
        reversed_x = int(str(x)[1:][::-1]) * -1
      else:
        # Convert x to a string, reverse the string, and convert it back to an integer
        reversed_x = int(str(x)[::-1])

    # Check if reversed_x is within the range of 32-bit signed integer
      if reversed_x < -2**31 or reversed_x > 2**31 - 1:
        return 0
      else:
        return reversed_x
```

### 11
**Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.**
```
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = 0
        for num in nums:
          result ^= num
        return result
```
Для решения этой задачи мы используем операцию исключающего ИЛИ (XOR). Операция XOR имеет свойство, что если мы применяем ее к двум одинаковым числам, результат будет 0, а если применяем к числу и 0, результат будет самим числом. Таким образом, если мы применяем XOR ко всем элементам массива, то все повторяющиеся числа "сошьются" друг с другом, и останется только одно уникальное число, которое не имеет пары.

### 12
**Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.**
```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        non_zero_index = 0

    # Iterate through the array
        for num in nums:
        # If the current element is non-zero, move it to the position indicated by the non_zero_index
          if num != 0:
            nums[non_zero_index] = num
            non_zero_index += 1

    # Fill the remaining elements of the array with zeroes
        while non_zero_index < len(nums):
          nums[non_zero_index] = 0
          non_zero_index += 1
```
Для перемещения всех нулей в конец массива, сохраняя при этом относительный порядок ненулевых элементов, мы можем использовать подход с двумя указателями.

    Мы инициализируем указатель non_zero_index, который будет отслеживать позицию, куда нужно поместить следующий ненулевой элемент.
    Затем мы проходимся по массиву nums.
    Если текущий элемент не равен нулю, мы перемещаем его на позицию, указанную non_zero_index, и увеличиваем non_zero_index.
    После того как мы переберем весь массив, останется заполнить оставшиеся элементы массива нулями, начиная с позиции, указанной non_zero_index.

Пример:

Пусть у нас есть массив [0, 1, 0, 3, 12]. Пройдемся по нему:

    Первый элемент - 0, мы его пропускаем.
    Второй элемент - 1, его перемещаем на позицию 0.
    Третий элемент - 0, мы его пропускаем.
    Четвертый элемент - 3, его перемещаем на позицию 1.
    Пятый элемент - 12, его перемещаем на позицию 2.

После этого остается только заполнить оставшиеся позиции массива нулями. Получится массив [1, 3, 12, 0, 0], что соответствует условиям задачи.      
