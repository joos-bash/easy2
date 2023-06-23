# easy2

**Передача аргументов скрипту**
- Аргументы передаются при запуске скрипта после его названия
  - ./script.sh param1 param2
  - bash script.sh param1 param2
- Доступ осуществляется через служебные переменные $1, $2, $3 и т. д.
  - $0 содержит название скрипта

**Цикл while** - позволяет выполнить одну и ту же последовательность действий, пока проверяемое условие истинно
```
while [[ условие ]]; do
echo "Ok"
done
```
Цикл **for** - позволяет проводить итерации — реализовывать набор инструкций нужное количество раз. For используем, когда нет условия, а есть список элементов
```
for имя in элемент1 элемент2 do
...
done
```
```
for item in coffee tea; do
echo "We have a $item"
done
```
Повторение тела цикла определённое количество раз
```
#!/bin/bash
for ((i=1; i < 10; i++))
do
echo $i
done
```
**Конструкция Bash select** - используется для создания нумерованного меню из списка пунктов

Синтаксис похож на :select for
```
select имя in элемент1 элемент2 do
...
done
```
**Select** - даёт пользователю выбрать вариант из предложенных с помощью ввода цифры. Чаще всего используется вместе с case
```
select pill in red blue; do
case $pill in
red)
echo "you will know the truth"; break;;
blue)
echo "you won't know anything"; break;;
esac
done
```
**Функции Bash** — часть кода, вынесенная отдельно для многократного использования

Объявление функции в Bash
```
имя_функции () {
команды
}
```
Вызов функции - имя_функции
```
#!/bin/bash
current_uptime () {
date
uptime
}
current_uptime
current_uptime
```

**Параметры** — доступные только внутри тела функции переменные
```
#!/bin/bash
division () {
if [[ $2 -ne 0 ]] then
echo "$1/$2 = $(($1/$2))"
else
echo "division by zero"
fi
}
division 15 5
division 4 2
division 3 0
```

В переменной содержатся все аргументы, переданные функции или скрипту $@ Эти аргументы часто используются для перебора всех параметров в цикле for

```
read_args() {
echo $@
for item in $@; do
echo $item
done
}
read_args param1 param2 param3
```
Код возврата в функции
- Выход из функции — с помощью return Х
- По умолчанию код возврата функции — 0
```
#!/bin/bash
division () {
if [[ $2 -ne 0 ]] then
echo "$1/$2 = $(($1/$2))"
return 0
else
echo "division by zero"
return 1
fi
}
division 15 5
division 4 2
division 3 0
```
- Указать код возврата для скрипта можно с помощью команды exit
- По умолчанию возвращает 0
- Можно задать любое другое значение с помощью exit X
```
#!/bin/bash
…
if [[ $error == “true” ]]; then
exit 1
else
exit 0
fi;
```

