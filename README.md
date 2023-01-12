
# **СИСТЕМА КОМАНД**
Використовуючи принципи фон Неймана, була сконструйована власна навчальна ЕОМ, розроблена та реалізована система команд, що дозволяє вводити та виводити дані, виконувати різноманітні арифметичні дії (додавання, віднімання, ділення, множення та пошук залишок від ділення), а також інші команди для перенесення даних з однієї ячійки в іншу тощо. Усі команди виконуються послідовно, за винятком безумовного та умовного переходів, які можуть змінити стандартний хід програми. Їх робота буде описана нижче. Кожна команда має два операнди (адреси), якими вона може керувати. Для арифметичних команд результат обчислення записується в рядку з адресою А1. Пам’ять навчальної машини складається з 512 рядків, що мають адреси від 1 до 512.

Нижче наведена таблиця реалізованих команд, їх кількість (деякі числа не є командами, тому не мають мнемонічного еквіваленту — вони позначені трьома знаками питання - ???) та короткий опис:

|**№**|**КОМ**|**ОПИС**|
| :-: | :-: | :-: |
|0|ПЕР|Пересилання значення з A2 в А1|
|1|СЛВ|Додавання дійсних чисел: A1 = A1 + A2|
|2|ВЧВ|Віднімання дійсних чисел: A1 = A1 - A2|
|3|УМВ|Множення дійсних чисел: A1 = A1 × A2|
|4|ДЕВ|Ділення дійсних чисел: A1 = A1 ÷ A2|
|5|ВВВ|Введення масиву дійсних чисел у кількості A2, починаючи з адреси A1|
|6|ВВЦ|Введення масиву цілих чисел у кількості A2, починаючи з адреси A1|
|7|???|???|
|8|???|???|
|9|БЕЗ|Безумовний перехід з поточного рядка на рядок А2|
|10|ЦЕЛ|Переведення дійсного числа А1 в ціле А2|
|11|СЛЦ|Додавання цілих чисел: A1 = A1 + A2|
|12|ВЧЦ|Віднімання цілих чисел: A1 = A1 - A2|
|13|УМЦ|Множення цілих чисел: A1 = A1 × A2|
|14|ДЕЦ|Ділення цілих чисел: A1 = A1 ÷ A2|
|15|ВЫВ|Вивід масиву дійсних чисел  у кількості A2, починаючи з адреси A1|
|16|ВЫЦ|Вивід масиву цілих чисел  у кількості A2, починаючи з адреси A1|
|17|???|???|
|18|УСП|Умовний перехід: якщо прапор Z* дорівнює 0 — перехід на рядок A1, якщо прапор Z* дорівнює 1 — перехід на рядок A2|
|19|УСЛ|Умовний перехід: якщо прапор 𝜔* дорівнює 0 або 2 — перехід на рядок A1, якщо прапор 𝜔* дорівнює 1 — перехід на рядок A2|
|20|ВЕЩ|Переведення цілого числа А1 у дійсне А2|
|21|???|???|
|…|…|…|
|23|???|???|
|24|МОД|Остача від ділення цілих чисел|
|25|???|???|
|…|…|…|
|29|???|???|
|30|ИТР|Зрушити A2 (задіяний зараз індекс ячійки масиву) в адресі A1 на A2 елементів|
|31|ОСТ|Завершення виконання програми|

***Таблиця 1**. Система команд навчальної машини*

## Команда пересилання
Команда пересилання має номер 0 та мнемонічний еквівалент “ПЕР”. Вона використовує два операнди: А1 та А2, де А1 є адресою призначення, а А2 є адресою джерела (тобто звідки треба брати значення, для пересилки в А1). За замовчуванням, усі рядки програми заповнені нулями, а в мнемонічному еквіваленті виглядають як “ПЕР 000 000”, що означає значення за адресою 0 записати в рядок за адресою нуль, тобто в нікуди. Фактично, такий рядок ніяк не впливає на виконання програми або інші рядки, і може слугувати як візуальний роздільник між значущими рядками. 

## Команда додавання дійсних чисел
Команда додавання дійсних чисел має код 1 і мнемонічний еквівалент “СЛВ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси дійсних чисел зі знаком або без, які потрібно скласти, результат додавання записується в А1. 

## Команда віднімання дійсних чисел
Команда віднімання дійсних чисел має код 2 і мнемонічний еквівалент “ВЧВ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси дійсних чисел зі знаком або без, де А1 — це зменшуване, а А2 — від’ємник, результат віднімання записується в А1. 

## Команда множення дійсних чисел
Команда множення дійсних чисел має код 3 і мнемонічний еквівалент “УМВ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси дійсних чисел зі знаком або без, де А1 та А2 — множники, результат множення записується в А1. 

## Команда ділення дійсних чисел
Команда ділення дійсних чисел має код 4 і мнемонічний еквівалент “ДЕВ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси дійсних чисел зі знаком або без, де А1 це ділене, А2 — дільник, результат ділення записується в А1. 




## Команда введення масиву дійсних чисел
Команда введення масиву дійсних чисел має код 5 і мнемонічний еквівалент “ВВВ”. Для своєї роботи вона використовує два операнди: А1 та  А2. Де А1 — адреса рядка, з якого треба починати записувати данні. Данні записуються послідовно. А2 — кількість чисел, які треба зчитати з клавіатури.

## Команда введення масиву цілих чисел
Команда введення масиву цілих чисел має код 6 і мнемонічний еквівалент “ВВЦ”. Для своєї роботи вона використовує два операнди: А1 та  А2. Де А1 — адреса рядка, з якого треба починати записувати данні. Данні записуються послідовно. А2 — кількість чисел, які треба зчитати з клавіатури. Команда аналогічна команді введення масиву дійсних чисел, окрім того, що зчитуються та записуються цілі числа.

## Команда безумовного переходу
Команда безумовного переходу має код 9 і мнемонічний еквівалент “БЕЗ”. Для своєї роботи вона використовує один операнд А2, який позначає номер рядка, який потрібно виконати наступним. Номер рядка не може перевищувати номер максимальної кількості рядків, тобто 512. 

## Команда переведення дійсного числа в ціле
Команда переведення дійсного числа в ціле має код 10 і мнемонічний еквівалент “ЦЕЛ”. Для своєї роботи вона використовує два операнди: А1 та  А2. Де А2 — адреса рядка, куди потрібно записати перетворене ціле число,  А1 — адреса рядка, звідки треба прочитати дійсне число, для подальшого його переведення в ціле.

## Команда додавання цілих чисел
Команда додавання цілих чисел має код 11 і мнемонічний еквівалент “СЛЦ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси цілих чисел зі знаком або без, які потрібно скласти, результат додавання записується в А1. 




## Команда віднімання цілих чисел
Команда віднімання дійсних чисел має код 12 і мнемонічний еквівалент “ВЧЦ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси цілих чисел зі знаком або без, де А1 це зменшуване,  А2 — від’ємник, результат записується в А1. 

## Команда множення цілих чисел
Команда множення дійсних чисел має код 13 і мнемонічний еквівалент “УМЦ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси цілих чисел зі знаком або без, де А1 та А2 множники, результат множення записується в А1. 

## Команда ділення цілих чисел
Команда ділення дійсних чисел має код 14 і мнемонічний еквівалент “ДЕЦ”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси цілих чисел зі знаком або без, де А1 це ділене, а А2 — дільник, результат ділення записується в А1. 

## Команда виводу масиву дійсних чисел
Команда виводу масиву дійсних чисел має код 15 і мнемонічний еквівалент “ВЫВ”. Для своєї роботи вона використовує два операнди: А1 та  А2. А1 — адреса рядка, з якого треба починати виводити данні. Данні виводяться послідовно, А2 - кількість чисел, які треба вивести на екран. Команда виводить масив дійсних чисел.

## Команда виводу масиву цілих чисел
Команда виводу масиву дійсних чисел має код 16 і мнемонічний еквівалент “ВЫЦ”. Для своєї роботи вона використовує два операнди: А1 та  А2. Де А1 — адреса рядка, з якого треба починати виводити данні. Данні виводяться послідовно, А2 — кількість чисел, які треба вивести на екран. Команда виводить масив цілих чисел.







## Команда умовного переходу (залежна від прапора нульового результату)
Команда умовного переходу має код 18 і мнемонічний еквівалент “УСП”. Для своєї роботи вона використовує два операнди: А1 та А2. Кожен з операндів є адресою рядка, на який треба перейти, і який буде виконаний наступним. Перехід на один з двох рядків виконується за певними правилами. Для цього використовується значення прапору Z* (нульового результату). Він оновлюється після виконання арифметичних операцій: додавання, віднімання, множення, ділення. Так, його значення буде 1, якщо результат операції дорівнює нулю. Якщо результат операції менше або більше за нуль, прапор буде встановлений в 0. Таким чином, в залежності від поточного значення прапору нульового результату, буде вирішено, на який рядок буде виконаний перехід. Якщо прапор дорівнює 1, програма переходить на рядок за адресою А1. У випадку, коли прапор дорівнює 0, наступним рядком стане рядок за адресою А2.

## Команда умовного переходу (залежна від прапора 𝜔)
Команда умовного переходу має код 19 і мнемонічний еквівалент “УСЛ”. Для своєї роботи вона використовує два операнди: А1 та А2. Кожен з операндів є адресою рядка, на який треба перейти, і який буде виконаний наступним. Перехід на один з двох рядків виконується за певними правилами. Для цього використовується значення прапору 𝜔* (Омега). Він оновлюється після виконання арифметичних операцій: додавання, віднімання, множення, ділення. Так, його значення буде 0, якщо результат операції дорівнює нулю. Якщо результат операції менше нуля, прапору буде встановлений у значення 1, якщо результат більше нуля, тоді прапору буде мати значення 2. Таким чином, в залежності від поточного значення прапору Омега, буде вирішено, на який рядок буде виконаний перехід. Якщо прапор омега дорівнює 0 або 2, програма переходить на рядок за адресою А1. У випадку, коли прапор омега дорівнює 1, наступним рядком стане рядок за адресою А2.

## Команда переведення цілого числа в дійсне
Команда переведення цілого числа в дійсне має код 20 і мнемонічний еквівалент “ВЕЩ”. Для своєї роботи вона використовує два операнди А1 та  А2. А1 — адреса рядка, куди потрібно записати перетворене дійсне число, А2 — адреса рядка, звідки треба прочитати ціле число, для подальшого його переведення в дійсне.

## Команда остачі від ділення цілих чисел
Команда остачі від ділення дійсних чисел має код 24 і мнемонічний еквівалент “МОД”. Для своєї роботи вона використовує два операнди: А1 та А2. А1 та А2 — адреси цілих чисел зі знаком або без, де А1 — це ділене, а А2 — дільник, залишок, отриманий у результаті ділення, записується в адресу А1.

## Команда ітерації масивом
Команда ітерації масивом має код 30 і мнемонічний еквівалент “ИТР”. Для своєї роботи вона використовує два операнди: A1 та A2. А1 — це адреса масиву, який потрібно зрушити, А2 — це кількість елементів, на яку потрібно зрушити індекс.


## Команда зупинки виконання програми
Команда зупинки виконання програми має код 31 і мнемонічний еквівалент “ОСТ”. Для своєї роботи вона не потребує операндів. Результат виконання команди — зупинка виконання програми. 


# **РЕГІСТРИ ТА ПРАПОРИ**
Регістри — це операнди, які використовуються для виконання поточної команди. Регістри поділяються на наступні типи за їх логічним сприйняттям: RK, R1, R2, RA. RK — це регістр, який відображає поточну команду; RA — номер адреси поточного рядка; R1 та R2 — це операнди, над якими виконується команда. 

Прапор 𝜔 ("омега"), що змінюється в залежності від результату виконання операцій додавання, віднімання, ділення, множення, використовується для умовного переходу Так, його значення буде 0, якщо результат операції дорівнює нулю. Якщо результат операції менше нуля, прапор буде встановлений у значення 1, якщо результат більше нуля — буде мати значення 2. Використовується для реалізації операції умовного переходу. 

Прапор S — прапор знаку результату. 

Прапор C — прапор ознаки перенесення зі старшого розряду.

Прапор T — прапор покрокового режиму.

Прапор Z — прапор нульового результату, використовується для реалізації операції умовного переходу.

Прапор Err  — прапор помилки. Він сигналізує про появу помилки під час виконання програми. За замовчуванням, має значення 0, що означає відсутність помилок, але у разі виникнення помилки змінює значення на 1, а програма завершується аварійно.

Усі регістри та прапори були винесені на панель форми графічного користувацького інтерфейсу, для можливості отримати повну інформацію про поточну команду та її операнди під час роботи навчальної машини у режимі налагодження програми.


# **РЕАЛІЗАЦІЯ НАВЧАЛЬНОЇ** **МАШИНИ**
**ІНСТРУМЕНТИ**

Емулятор навчальної машини двоадресної була реалізована за допомогою мови програмування C# та з використанням фреймворку для побудови додатків з графічним користувацьким інтерфейсом під платформи операційних систем сімейства Windows, який має назву Microsoft WPF .Net Framework. Проект був виконаний у інтегрованому середовищі розробки Microsoft Visual Studio 2022. 

**ГРАФІЧНИЙ ІНТЕРФЕЙС КОРИСТУВАЧА**

Для зручності користування навчальною машиною, був створений графічний інтерфейс користувача. Введення даних здійснюється за допомогою клавіатури, а управління емулятором за допомогою миші. Нижче наведений скріншот вікна, яке і є головним вікном, з яким взаємодіє користувач. Цифрами від 1 до 6 позначені елементи інтерфейсу, функціонування та призначення яких описано нижче.

![mainui](https://github.com/backstabslash/2nd-year-uni-summerpractice-proj/blob/master/EM2/ui.png)

***Рисунок 1**. Графічний інтерфейс користувача*


Перелік та опис елементів інтерфейсу, позначених на рисунку 1:

1. Таблиця з кодом програми. Тут користувач може вводити та редагувати команди програми для подальшого її використання. Користувачу дозволено вводити як цілі, так і дійсні числа. Якщо користувач уводить некоректні дані, під час запуску програми, у вікні діагностики йому буде показана відповідна помилка. 
1. Під час роботи програми, за допомогою відповідних команд, заданих користувачем у таблиці коду, програма може запросити користувача ввести дані (ціле або дійсне число). Для цього з’явиться вікно, у яке потрібно буде за допомогою клавіатури ввести число. Якщо ввести неправильне значення або відмінити операцію вводу, програма виведе в вікно діагностики відповідну помилку. Якщо ж введене значення буде коректним, то програма продовжить свою роботу, а введене число з’явиться у вікні “Ввід”. Таким чином, користувач може згадати, які данні він увів в програмі.
1. Результатом роботи програми може бути ціле або дійсне число. Для відображення цієї інформації необхідно задати навчальній машині одну з відповідних команд, а саме число буде виведено у вікні “Вивід”.
1. У інтерфейсі існує панель регістрів та прапорів, які змінюються під час виконання програми. У покроковому режимі ця панель наочно демонструє процес виконання програми. 
1. Під час виконання програми у навчальній машині, можуть виникнути деякі попередження та зауваження або непередбачувані ситуації. У такому випадку, усі повідомлення, сформовані програмою, будуть відображені у вікні “Діагностика”.
1. Панель відображає шлях до відкритого файлу.
1. Зверху вікна знаходяться допоміжні та керуючі кнопки: “Зберегти”, “Зберегти як”, “Відкрити”, “Довідка” та “Очистка”; “Пробіг” – виконати програму без налагоджування, “Почати налагодження” – почати покроковий пробіг програми, “Крок” – перейти до наступної команди , “Завершити налагодження” – завершити покроковий пробіг програми.

![](https://github.com/backstabslash/2nd-year-uni-summerpractice-proj/blob/master/EM2/input.png)

***Рисунок 2**. Вікно для введення дійсного числа*

![](https://github.com/backstabslash/2nd-year-uni-summerpractice-proj/blob/master/EM2/helpdoc.png)

***Рисунок 3.** Вікно довідки*
# **ПРОГРАМИ ДЛЯ НАВЧАЛЬНОЇ МАШИНИ**
## **ЛІНІЙНІ ОБЧИСЛЕННЯ**
Для тестування можливості реалізацій лінійних обчислень, складемо програму для подальшого її запуску за допомогою створеного емулятора навчальної машини.

Завдання №17: обчислити значення функції y = (4 * x^3 + 10 * z) / (x * z^2), значення “x” та “z”  задає за допомогою операцій введення з клавіатури користувач.

Нижче наведений код відповідної програми у вигляді таблиці:

|**АДР**|**КОМ**|**А1**|**А2**|**ОПИС**|
| :-: | :-: | :-: | :-: | :-: |
|1|ВВВ|15|2|Ввід користувачем значень “x” та “z” у 15 та 16 адреси|
|2|ПЕР|17|15|Пересилання “x” до 17 адреси, щоб пізніше не втратити значення|
|3|ПЕР|18|16|Пересилання “z” до 18 адреси, щоб пізніше не втратити значення|
|4|УМВ|17|15|Множення “x”  на “x”  (піднесення до квадрату)|
|5|УМВ|17|15|Множення “x2”  на “x”  (піднесення до кубу)|
|6|УМВ|14|17|Множення “x3” на 4, заздалегідь переслану до 14 адреси|
|7|УМВ|18|16|Множення “z”  на “z”  (піднесення до квадрату)|
|8|УМВ|18|15|Множення “z2”  на “x”  (обрахунок дільника)|
|9|УМВ|19|16|Множення “z”  на 10, заздалегідь переслану до 19 адреси|
|10|СЛВ|14|19|Додавання 4x3 та 10z (обрахунок діленого)|
|11|ДЕВ|14|18|Фінальне ділення заздалегідь обрахованих значень|
|12|ВЫВ|14|1|Вивід обрахованого результату функції|
|13|ОСТ|000|000|Зупинка виконання програми|
|14|ПЕР|000|4|Пересилання до 14 адресу 4|
|…|…|…|…|…|
|19|ПЕР|000|10|Пересилання до 19 адресу 10|

***Таблиця 2**. Код програми обчислення лінійного виразу*

## **ОБЧИСЛЕННЯ ЗА ДОПОМОГОЮ ЦИКЛІВ**
Для тестування можливості реалізацій циклічних обчислень, складемо відповідну програму для подальшого її запуску за допомогою створеного емулятора навчальної машини.

Завдання №2: обчислити значення виразу (wolfram alpha math input) y = Product[i^3 / (a - b), {i, 1, n}] при заданих користувачем значеннях “*a”* та “b”, якщо a != b, або обчислити значення виразу (a - b) / (a + b), якщо a = b.

Нижче наведений код відповідної програми у вигляді таблиці:

|**АДР**|**КОМ**|**А1**|**А2**|**ОПИС**|
| :-: | :-: | :-: | :-: | :-: |
|1|ВВВ|40|3|Ввід користувачем значень “a”, “b” та “i” у 40, 41 та 42 адреси|
|2|ПЕР|50|40|Пересилка “a” до 50 адреси, щоб пізніше не втратити значення|
|3|ПЕР|51|41|Пересилка “b” до 51 адреси, щоб пізніше не втратити значення|
|4|ВЧВ|40|41|Перевірка, чи дорівнює a - b нулю (формування прапору нульового результату)|
|5|УСП|8|6|Якщо прапор зараз 0 (результат операції не дорівнював 0), то перейти до 8 адреси, інакше – до 6|
|6|БЕЗ|000|20|Безумовний перехід до 20 адреси для подальшого обрахування результату|
|7|ОСТ|000|000|Зупинка виконання програми|
|8|ВЧВ|42|55|Перевіряємо, чи не більше ітератор (зберігається у 55 адресі), аніж потрібна користувачу кількість ітерацій (зберігається у 42 адресі). Формуємо прапор 𝜔: якщо результат віднімання більше або дорівнює 0, то 𝜔 = 2 (0), інакше 𝜔 = 1|
|9|УСЛ|10|18|Якщо обрахований прапор 𝜔 дорівнює 0 або 2, то переходимо до 10 адреси, інакше (дорівнює 1) до 18|
|10|СЛВ|42|55|Повертаємо необхідну користувачу кількість ітерацій до початкового значення (до формування 𝜔)|
|11|ПЕР|57|55|Пересилання значення ітератору до 57 адреси, щоб не втратити значення|
|12|УМВ|57|55|Множення “i”  на “i”  (піднесення до квадрату)|
|13|УМВ|57|55|Множення “i2”  на “i”  (піднесення до кубу)|
|14|ДЕВ|57|40|Ділення i3 на обраховану раніше різницю a - b|
|15|УМВ|512|57|Множимо результат на щойно обраховане значення|
|16|СЛВ|55|56|Збільшуємо ітератор на одиницю|
|17|БЕЗ|000|8|Безумовний перехід до 8 адреси для продовження (або завершення) циклу|
|18|ВЫВ|512|1|Виводимо результат обрахунку на екран|
|19|ОСТ|000|000|Зупинка виконання програми|
|20|СЛВ|50|51|Оскільки a - b вже було обраховано у 4 адресі (результат у 40), залишається обрахувати лише суму |
|21|ДЕВ|40|50|Ділимо різницю a - b на тільки що обраховану суму a + b|
|22|ВЫВ|40|1|Виводимо результат обрахунку на екран|
|23|БЕЗ|000|7|Переходимо до 7 адреси для завершення програми|
|…|…|…|….|…|
|55|ПЕР|000|1|Пересилання до 55 адреси 1|
|56|ПЕР|000|1|Пересилання до 56 адреси 1|
|…|…|…|…|…|
|511|ПЕР|000|0|Пересилання до 511 адреси 0, для обрахунку суми|
|512|ПЕР|000|1|Пересилання до 512 адреси 1, для обрахунку добутку|

***Таблиця 3**. Код програми обчислення виразу за допомогою циклів*


## **ОБЧИСЛЕННЯ З ВИКОРИСТАННЯМ ЦИКЛІВ (МАСИВИ)**
Для тестування можливості реалізацій обчислень масивів з використанням циклів, складемо відповідну програму для подальшого її запуску за допомогою створеного емулятора навчальної машини.

Завдання №11: Скласти програму для підрахунку в цілочисловому масиві кількості нульових елементів, що стоять після елемента із заданим користувачем номером.

Нижче наведений код відповідної програми у вигляді таблиці:

|**АДР**|**КОМ**|**А1**|**А2**|**ОПИС**|
| :-: | :-: | :-: | :-: | :-: |
|1|ВВЦ|100|5|Заповнення користувачем масиву з 5 елементів, починаючи з 100 адресу|
|2|ВВЦ|105|1|Ввід користувачем індексу масиву, починаючи з якого, буде відбуватися обрахунок результату в 105 адресу|
|3|ВЧЦ|105|30|Перевірка, чи досяг ітератор (у 30 адресі) початкового значення (яке ввів користувач до 105 адресу) для початку розрахунків. Формування прапору нульового результату|
|4|УСП|7|5|Умовний перехід: якщо ітератор ще не досяг початкового індексу (прапор дорівнює 0) перехід до 7 адресу, інакше (прапор 1) до 5 адресу|
|5|СЛЦ|105|30|Повертаємо початковий індекс до його стартового значення (яке змінилося після виконання коду за 3 адресою)|
|6|БЕЗ|000|11|Безумовний перехід до 11 адресу|
|7|СЛЦ|105|30|Повертаємо початковий індекс до його стартового значення (яке змінилося після виконання коду за 3 адресою)|
|8|СЛЦ|30|31|Ітератор ще не досяг початкового індексу, збільшуємо його на один|
|9|ИТР|14|1|Зрушуємо адрес (А1) необхідної ячійки масиву у 14 адресі на один|
|10|БЕЗ|000|3|Безумовний перехід до 3 адресу|
|11|ВЧЦ|32|30|Перевіряємо, чи не більше ітератор (зберігається у 30 адресі), аніж кількість елементів масиву (зберігається у 32 адресі)|
|12|УСЛ|13|22|Якщо значення прапору 𝜔 дорівнює 0 (або 2) то продовжуємо цикл і переходимо до 13 адресу, інакше (𝜔 дорівнює 1) до 22 адресу|
|13|СЛЦ|32|30|Повертаємо початкову кількість елементів масиву до її стартового значення (яке змінилося після виконання коду за 11 адресою)|
|14|СЛЦ|100|34|Додаю до поточного елементу масиву (якій змінюється на 1 після виконання коду за 9 та 15 адресою) нуль. Формую прапор нульового результату: якщо елемент масиву був нулем, то прапор буде дорівнювати 1, інакше 0|
|15|ИТР|14|1|Зрушуємо адрес (А1) необхідної ячійки масиву у 14 адресі на один|
|16|УСП|17|19|Умовний перехід: якщо прапор нульового результату дорівнює 0 до 17 адреси, інакше (прапор дорівнює 1) до 19 адреси|
|17|СЛЦ|30|31|Збільшую ітератор на одиницю |
|18|БЕЗ|000|11|Безумовний перехід до 11 адреси|
|19|СЛЦ|30|31|Збільшую ітератор на одиницю|
|20|СЛЦ|33|31|Збільшую кількість нулів у масиві на одиницю (спочатку за 33 адресою зберігається 0)|
|21|БЕЗ|000|11|Безумовний перехід до 11 адреси|
|22|ВЫЦ|33|11|Вивід кількості нулів на екран|
|23|ОСТ|000|000|Зупинка виконання програми|
|…|…|…|…|…|
|30|ПЕР|000|1|Пересилання до 30 адреси 1|
|31|ПЕР|000|1|Пересилання до 31 адреси 1|
|32|ПЕР|000|5|Пересилання до 32 адреси 5|

***Таблиця 4**. Код програми обчислення масивів за допомогою циклів*
