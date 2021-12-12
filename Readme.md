# Инструкция по Git

## 1. Что такое Git?

--- 

Git - одна из реализаций распределенных систем контроля версий, имеющая как локальную версионность, так и версионность на сервере. Git является самой популярной системой контроля версий на сегодняшний день.

---

## 2. Подготовка репозитория.

--- 

+ **git init**

Для того, чтобы создать репозиторий в указанной папке используется команда `git init` в папке с будущим репозиторием.

---

## 3. Фиксация версий.

---

### 3.1. Добавление файла к версии.

+ **git add**

Для того, чтобы добавить файл к новой версии ("сохранению") необходимо использовать команду `git add <имя файла>` в папке с репозиторием.

### 3.2. Сохранение изменений в версии.

+ **git commit**

Для сохранения изменений в версии необходимо использовать комманду `git commit -m "<комментарий>"` в папке с репозиторием. Все файлы коммита должны быть предварительно добавлены с помощью команды `git add`. Комментарий к коммиту писать ***ОБЯЗАТЕЛЬНО***.

### 3.3. Просмотр информации об изменениях.

+ **git status**

Для того, чтобы посмотреть информацию о незакоммиченных изменениях, необходимо использовать команду `git status` в папке с репозиторием.

---

## 4. Перемещение между коммитами.

---

+ **git checkout**

Для перемещения между коммитами используется команда `git checkout <хеш коммита>`. Для того, чтобы узнать хеш коммита используется команда `git log` (подробнее о ней ниже).

---

## 5. Журнал изменений.

---
+ **git log**

Для просмотра журнала изменений используется команда `git log` в папке репозитория. Данная команда имеет большое количество опций для поиска коммитов по разным критериям. По умолчанию (без аргументов) `git log` перечисляет коммиты в обратном хронологическом порядке.

### 5.1. Наиболее распространенные опции для команды `git log`

|Опция|Описание|
|--|--|
|-p|Показывает патч для каждого коммита.|
|--stat|Показывает статистику измененных файлов для каждого коммита.|
|--shortstat|Отображает только строку с количеством изменений/вставок/удалений для команды *--stat*.|
|--name-only|Показывает список измененных файлов после информации о коммите.|
|--name-status|Показывает список файлов, которые добавлены/изменены/удалены.|
|--abbrev-commit|Показывает только несколько символов SHA-1 чек-суммы вместо всех 40.|
|--relative-date|Отображает дату в относительном формате (например, "2 weeks ago") вместо стандартного формата даты.|
|--graph|Отображает ASCII граф с ветвлениями и историей слияний.|
|--pretty|Показывает коммиты в альтернативном формате. Возможные варианты опций: `oneline`, `short`, `full`, `fuller` и `format` (с помощью последней можно указать свой формат).|
|--oneline|Сокращение для одновременного использования опций `--pretty=oneline --abbrev-commit`.|
|

### 5.2. Опции для ограничения вывода команды `git log`
|Опция|Описание|
|--|--|
|-(n)|Показывает только последние n коммитов.|
|--since, --after|Показывает только те коммиты, которые были сделаны после указанной даты.|
|--until, --before|Показывает только те коммиты, которые были сделаны до указанной даты.|
|--author|Показывает только коммиты указанного автора.|
|--committer|Показывает только коммиты указанного коммиттера.|
|--grep|Показывает только коммиты, сообщение которых содержит указанную строку.|
|-S|Показывает только коммиты, в которых изменение в коде повлекло за собой добавление или удаление указанной строки.|
|--no-merges|Исключает из вывода коммиты слияния.|
|
### 5.3. Полезные опции для `git log --pretty=format`
|Опция|Описания вывода|
|--|--|
|%H|Хеш коммита|
|%h|Сокращенный хеш коммита|
|%T|Хеш дерева|
|%t|Сокращенный хеш дерева|
|%P|Хеш родителей|
|%p|Сокращенный хеш родителей|
|%an|Имя автора|
|%ae|Электронная почта автора|
|%ad|Дата автора (формат даты можно задать опцией `--date=option`)|
|%ar|Относительная дата автора|
|%cn|Имя коммитера|
|%ce|Электронная почта коммитера|
|%cd|Дата коммитера|
|%cr|Относительная дата коммитера|
|%s|Содержание|
|

### 5.4. Примеры применения опций:

+ `git log --pretty=format:"%h %s" --graph`
+ `git log --pretty=format:"%h - %an, %ar : %s"`
+ `git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \
   --before="2008-11-01" --no-merges`

---

## 6. Ветки в Git.

---
Для совместной работы над проектом в Git применяются ветки. Изначально существует одна ветка *master*, в которую впоследствии сливаются все нужные дополнительные ветки.

### 6.1. Список веток.

+ git branch

Для просмотра списка всех существующих на данный момент веток используется команда `git branch`. При выводе списка веток активная ветка выделена шрифтом и знаком *.

### 6.2. Создание ветки.

+ git branch \<newBranchName\>

Для создания новой ветки используется команда `git branch <newBranchName>`. Изменения в дополнительной ветке не влияют на другие ветки.

### 6.3. Переход между ветками.

+ git checkout \<branchName\>

Для перехода между ветками используется команда `git checkout <branchName>`.

### 6.4. Слияние веток и решение конфликтов.

+ git merge \<branchName\>

Для слияния веток используется команда `git merge <branchName>`. Данная команда сливает ветку \<branchName\> в активную на данный момент ветку (в конечном итоге в ветку *master*).

При слиянии веток возможны 3 варианта:

    a) автоматическое слияние без создания коммита
    b) автоматическое слияние с созданием коммита слияния
    c) конфликт при слиянии. Если в сливаемых ветках строки с одинаковыми номерами отличаются, то возникает конфликт (*conflicted state*) и Git предлагает произвести слияние вручную. Возможны 4 варианта действий:
        c1) сохранить версию конфликтных строк из текущей ветки
        c2) принять версию конфликтных строк из сливаемой ветки
        с3) сохранить оба варианта
        с4)
 
### 6.5. Delete branches.

+ git branch -d \<branchName\>
+ git branch -D \<branchName\>

Для удаления ненужной ветки используются команды `git branch -d \<branchName\>` (удаляет ветку только если она уже слита в ветку *master*) и `git branch -D \<branchName\>` (удаляет ветку даже если она не слита в *master*)
