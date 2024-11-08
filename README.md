# Лабораторная работа №1
## Задание 1 
https://github.com/olesya-dav04/laba1/blob/main/ThreadLab/Program.cs
Данная программа демонстрирует работу многопоточности в C#. Она создает три потока, каждый из которых выполняет отдельную задачу - вывод чисел от 0 до определенного значения.
## Описание:
1. Класс myThread:
  - Содержит поле thread типа Thread, которое представляет собой отдельный поток.
  - Конструктор myThread(string name, int num):
   - Создает новый поток thread и присваивает ему имя name.
   - Запускает поток с помощью thread.Start(num), передавая в качестве параметра число num.
  - Метод func(object num):
   - Выполняется в отдельном потоке.
   - Цикл for выводит в консоль имя текущего потока и значение счетчика i.
   - Thread.Sleep(0) - задержка на 0 миллисекунд, имитирует небольшую задержку в работе потока.
   - После завершения цикла выводит сообщение о завершении потока.
2. Метод Main(string[] args):
  - Создает три экземпляра класса myThread: t1, t2 и t3.
  - Каждый экземпляр получает свое имя и число, до которого будет вести счет.
  - Console.Read() - ожидает нажатия клавиши, чтобы завершить программу.
## Функциональность:
Программа создает три потока, которые независимо друг от друга выводят числа в консоль. В результате мы видим перемешанные сообщения от каждого потока, демонстрируя, как они работают одновременно.

## Использование:
Данная программа является примером простой демонстрации многопоточности. Ее можно модифицировать для реализации более сложных задач, таких как параллельные вычисления, обработка нескольких задач одновременно или взаимодействие между потоками.

## Важные моменты:
- Потоки могут работать одновременно, переключаясь между собой очень быстро.
- Thread.Sleep(0) - не гарантирует остановку потока на 0 миллисекунд, а только заставляет его уступить время другим потокам.
- Для управления потоками и синхронизации их работы могут использоваться различные механизмы, такие как mutex, semaphore, monitor и другие.
![Вывод программы](https://github.com/sorrymorning/ThreadLab/blob/main/%D0%9F%D0%BE%D1%82%D0%BE%D0%BA%D0%B8.png)
## Задание 2
https://github.com/olesya-dav04/laba1/blob/main/UsingSemaphore/Program.cs
# 
Данная программа демонстрирует работу семафора для управления доступом к ресурсу, в данном случае - библиотеке с ограниченным количеством мест для чтения.

## Описание:

1. Семафор sem: 
  - Создается с начальным значением 3 и максимальным значением 3.
  - Представляет собой ограничение на количество потоков, которые могут одновременно находиться в библиотеке.
2. Класс Reader:
  - Моделирует "читателя", который пытается попасть в библиотеку и почитать.
  - Каждый "читатель" создает отдельный поток myThread.
  - Переменная count - счетчик, отслеживающий количество раз, которое читатель может посетить библиотеку (в этом случае - 3 раза).
3. Метод Read():
  - Цикл while (count > 0) выполняется до тех пор, пока читатель не посетит библиотеку три раза.
  - sem.WaitOne() - читатель пытается занять место в библиотеке.
   - Если мест нет, поток "читателя" ставится на паузу, ожидая освобождения места.
   - Если место есть, читатель входит в библиотеку, и count уменьшается на 1.
  - Внутри библиотеки "читатель" выполняет действие (в данном случае - имитирует чтение в течение секунды).
  - sem.Release() - читатель покидает библиотеку и освобождает место для других читателей.
  - Thread.Sleep(1000) - имитирует паузу между посещениями библиотеки.

## Функциональность:
Программа запускает 5 потоков, каждый из которых моделирует "читателя". 
- Семафор ограничивает количество читателей в библиотеке до 3.
- Если "читатель" приходит в библиотеку, когда все места заняты, он ждет, пока кто-то не освободит место.

## Использование:
Данная программа демонстрирует использование семафора для управления доступом к ресурсу с ограниченным количеством. 
- Можно модифицировать программу, чтобы добавить другие функции, например, очередь для ожидания читателей, различные типы читателей (например, с разным временем чтения) или разные типы ресурсов (не только библиотека).

## Важные моменты:
- Семафор - это простой и эффективный механизм для синхронизации потоков.
- sem.WaitOne() - блокирует поток до тех пор, пока не освободится место.
- sem.Release() - освобождает место, позволяя другому потоку занять его.

  
![Вывод программы](https://github.com/sorrymorning/ThreadLab/blob/main/%D1%81%D0%B5%D0%BC.png)
