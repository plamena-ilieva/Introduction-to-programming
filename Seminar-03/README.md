# Трети семинар по увод в програмирането - 16.10.2023

## Тернарен оператор
* Унарни оператори - приемат 1 аргумент. Примери са операторите !, ++, -- и други
* Бинарни оператори - приемат 2 аргумента. Примери са операторите +, -, *, /, <, > и други.
* Тернарен оператор - той е само един. Приема три аргумента. Синтаксис:
```cpp
<Булев израз> ? <Стойност, която да се върне ако той е истина> : <Стойност, която да се върне ако той е лъжа>;
```
```cpp
#include<iostream>

using namespace std;

int main()
{
    int x = 0;
    cin >> x;

    int abs = (x < 0) ? -x : x;     // Ако х е по - валко от 0 се връща -х. В противен случай се връща х.

    cout << x << " " << y;
}
```

Използва се като съкратен запис за if-else конструкция.

## Цикли
**Задача 1.**
От стандартния вход се въвежда цяло положително число. Трябва да се изведат всички числа, по - малки или равни от въведеното число.

Със знанията, които имаме до момента, решението на тази задача изглежда трудно. Езиците за програмиране имат конструкции, които улесняват подобни задачи. Решението не задачата може да се опише по следния начин:

1. Създай число х и го прочети от конзолата.
2. Създай число i и му дай стойност 0.
3. Докато i e по - малко или равно на х:
   1. печатай i 
   2. увеличи i с единица.
   3. Върни се на 3.

Вече знаем как да създаваме променливи, как да ги четем от конзолата и как да ги увеличаваме с единица. Как ще моделираме `докато` условието?

## while цикъл
Можем да използваме цикъла `while`. Синтаксис:

```cpp
while(<Булево условие>)
{
    // Код, който да се изпълни
}
```

От тук решението на задачата изглежда по следния начин:

```cpp
#include<iostream>

using namespace std;

int main()
{
    unsigned x = 0;
    cin >> x;
    unsigned i = 0;

    while (i <= x)
    {
        cout << i << " ";
        ++i;
    }
}
```

**Задача: Променяйки този пример направете така, че програмата да смята x! (факториел).**

## Безкрайни цикли. Ключовата дума *break*.
В показаните примери циклите се въртяха докато не стигнем някакво условие. В контекста на **Задача 1** ние знаем, че рано или късно това условие ще бъде достигнато. Какво би станало обаче ако имаме условие, което винаги е истина?
```cpp
while(true)
{
    // do something
}
```
Въпреки, че условието винаги е истина, все пак можем да прекратим цикъла. Можем да използваме ключовата дума break.
break се използва в два случая:
1. За да излезем **веднага** от цикъл.
2. За да излезем от switch конструкция.

Използвайки break извън цикъл или switch се счита за синтактична грешка.

## do-while цикъл
В началото на изпълнението на while се проверява булевото условие. Ако то не е истина, не се продължава към изпълнението на кода. Понякога е удобно кодът, в тялото на цикъла, да се изпълни веднъж и чак след това да се провери условието на while.

**Пример:**
От стандартния вход се четат символи. Четенето продължава докато не се въведе символ 'q'.

Как ще направим това с while:
```cpp
#include<iostream>

using namespace std;

int main()
{
    char symbol;
    cout << "Enter a symbol: " << endl;
    cin >> q;

    while(symbol != 'q')
    {
        cout << "Enter a symbol: " << endl;
        cin >> q;
    }
}
```

Забелязваме, че имаме дублиране на код. Как би изглеждала тази задача ако използваме do-while коснструкция:
```cpp
#include<iostream>

using namespace std;

int main()
{
    char symbol;

    do
    {
        // Кодът се изпълнява веднъж
        // след това се праверява условието
        cout << "Enter a symbol: " << endl;
        cin >> symbol;
    } while(symbol != 'q');
}
```

## for цикъл
Нека разгледаме малко по - добре решението на **задача 1**. По - точно, нека разгледаме по - подробно как конструирахме while цикъла. 
Можем да разделим цикъла на четири основни момента:

```cpp
#include<iostream>

using namespace std;

int main()
{
    unsigned x = 0;
    cin >> x;
    
    // Момент 1: Създаваме променлива, която ни помага да проверяваме условието.
    // Това се случва само веднъж.
    unsigned i = 0;

    while (i <= x)           // Момент 2: Проверяваме условието. Това се случва до първия път в който то стане false.
    {
        cout << i << " ";   // Момент 3: Изпълняваме кодът, който ни върши работата
        ++i;                // Момент 4: Променяме по някакъв начин променливата и се връщаме в момент 2.
    }
}
```
Можем да се абстрахираме от детайлите на задачата и да опишем общата конструкция на този while цикъл:
```
init-statement                                      (Момент 1)

while ( condition )                                 (Момент 2) 
{
    statement;                                      (Момент 3)
    iteration-expression ;                          (Момент 4)
}
```

Цикъла for отново използва тази конструкция:
```cpp
for(init-statement; condition; iteration-expression)
{
    statement;
}
```

Във for цикъла нещата са подобни.
1. init-statement се изпълнява точно веднъж
2. Проверява се condition.
   * Ако condition e false приключи
   * Ако condition e true:
      - изпълни statement
      - изпълни iteration-expression
      - Върни се в 2.

Би трябвало да е очевидно, че всяко едно нещо, което можем да направим с for можем да направим и с while и обратното.
Решението на **Задача 1** би изглеждало по следния начин, написано с for цикъл:

```cpp
#include<iostream>

using namespace std;

int main()
{
    unsigned x = 0;
    cin >> x;

    for(int i = 0; i <= x; i++)
    {
        cout << i << endl;
    }
}
```

## Примери

### Задача 2
От стандартния вход се въвеждат две числа. Да се намери най - големия им общ делител.

### Задача 3
От стандартния вход се въвежда число. Да се провери дали е просто или не.
