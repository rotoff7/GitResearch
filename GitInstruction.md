![Logo](TestGitPicV2.png)
# Работа с Git
## 1. Установка Git
Загружаем последнюю версию программы с [официального сайта](https://git-scm.com/downloads).

Устанавливаем с настройками по умолчанию.
## 2. Проверка наличия/корректной установки Git
Для проверки того факта, что Git установился корректно и готов к работе, можно воспользоваться командой:
```
git --version
```

Если Git установлен, появится сообщение с информацией о версии программы. 
>Пример: git version 2.39.0.windows.1

Иначе будет получено сообщение об ошибке.
## 3. Первичная настройка гит
При первом использовании Git вам необходимо представиться программе. Для этого нужно ввести в терминале две следующие команды:
```
git config --global user.email (your username)
git config --global user.name (your email)
```
>Пример: git config --global user.name "FirstName SecondName"

>Пример: git config --global user.email "example@mail.ru"

Для того чтобы проверить зафиксировались ли новые параметры, можно воспользоваться командой:
```
git config --global --list
```
В случае корректной настройки, можно будет увидеть параметры user.name и user.email напротив которых будут стоять ваши данные.
## 4. Инициализация репозитория
Для запуска репозитория в нужной папке и старта отслеживания версий, используем следующую команду: 
```
git init
```
Для того, чтобы убедиться, что гит начал отслеживать изменения в выбранном расположении, можно воспользоваться командой: 
```
git status
```
Вызвав которую, мы должны увидеть следующее сообщение:

`On branch master`

`No commits yet`
## 5. Запись изменений в репозиторий
Для того чтоб увидеть список всех файлов в репозитории, изменения в которых могут быть записаны, можно воспользоваться ранее рассмотренной командой `git status`.

После того как мы поработали с файлом/файлами, сохранили в них изменения и хотим записать их текущее состояние в репозиторий, нам необходимо добавить их к новому "сохранению", для этого воспользуемся командой:
```
git add <files>
```
>Пример: git add "ExampleFile.txt"

Для того, чтобы убедиться, что файлы готовы к сохранению, можно вновь прописать `git status`, тогда все добавленные файлы будут выделены зеленым цветом. 

Если хотим добавить к сохранению ВСЕ файлы в текущей папке можно использовать параметр -A или --all
>Пример: git add --all

Для того, чтобы зафиксировать (сохранить) изменения необходимо воспользоваться командой: 
```
git commit -m "CommitName"
```
>Пример: git commit -m "Сохраняем первый коммит"
## 6. Переключение между сохранениями
Посмотреть все сохранения (записанные коммиты), с подробной информацией, можно при помощи команды :
```
git log
```
или посмотреть список всех записанных коммитов только с их id и названиями, командой:
```
git log --oneline
```
Для того, чтобы увидеть разницу в изменениях между текущей версией файлы и версией в последнем коммите, можно использовать команду `git diff`. Если мы хотим сравнить текущей файл с версией в **конкретном** коммите, то к команде нужно добавить `id` нужного коммита:
```
git diff <commit id>
```
>Пример: git diff 27ae841

Для того, чтобы переключиться на нужное сохранение (перейти к нужным версиям файла/файлов) можно использовать команду: 
```
git checkout <commit id>
```

>Пример: git checkout 27ae

**Для перехода к нужному коммиту достаточно использовать первые четыре символа его `id`.**

Если же мы хотим вернуться на актуальное сохранение ГЛАВНОЙ ветки проекта, необходимо использовать команду:
```
git checkout master
```
Соответственно вместо названия `master`, можно использовать название любой другой ветки, для быстрого переключение на ее актуальное сохранение. 

Список веток можно посмотреть командой `git branch`. Список всех коммитов нужной ветки можно посмотреть использовав ранее рассмотренную команду `git log` с указанием названия ветки:
>Пример: `git log master --oneline`

## 7. Игнорирование файлов
Для того, чтобы исключить из отслеживания в репозитории файлы или папки, нам необходимо создать файл **`.gitignore`** и записать туда их названия, или шаблоны соответствующие этим файлам и папкам.

Пример содержания файла `.gitignore`:
```
1. Test.txt
2. Req.pdf
3. *.png
4. *.jpg
5. Final_Versions
```
Где `*.png` и `*.jpg` это шаблоны, исключающие **все** картинки данных расширений, а Final_Versions исключаемая из отслеживания в репозитории папка.

## 8. Создание и удаление веток в Git
Ветка в Git - это простой перемещаемый указатель на один из коммитов, обычно последний в цепочке коммитов.  
По умолчанию имя основной ветки в Git - `master`.

Чтобы создать новую ветку из текущего коммита (текущей версии файла), необходимо ввести команду:
```
git branch (New_Branch_Name)
```
В результате создается новый указатель на текущий коммит. Или простыми словами: мы создаем копию текущего коммита в новой ветке, изменения в которой не будут влиять на основную ветку `master` или на любую другую (до слияния).

Чтоб не только создать новую ветку, но и сразу перейти в нее мы можем совместь две команды в одну:
```
git checkout -b (New_Branch_Name)
```
После выполнения этой команды мы не просто создадим новую ветвь, но сразу переместимся в нее.

Если нам нужно переименовать уже существующую ветку, то мы должны сперва перейти в нее, а затем прописать команду:
```
git branch -m (New_Name_for_Branch)
```

Чтобы удалить лишние (уже отработанные ветки) необходимо использовать команду:
```
git branch -d (Branch_Name)
```
Мы не можем удалить ту ветку, в которой находимся в данный момент и мы также не можем удалить все ветки в репозитории.
Если мы хотим удалить ветку, в которой остались несохраненный изменения тогда мы должны изменить параметр `-d` на параметр в верхнем регистре `-D`:
```
git branch -D (Branch_Name)
```
## 9. Перемещение между ветками и их слияние.
Ранее уже были рассмотрены некоторые из основных команд по работе с ветками в Git, напомним:
```
1. git branch                       | Посмотреть список всех веток
2. git checkout (Branch_Name)       | Переход к необходимой ветке
3. git log (Branch_Name)            | Список коммитов определенной ветки
```
Когда мы захотим объединить (слить) вместе две ветки, сперва нам необходимо зайти в ветку, **куда** мы хотим подгружать изменения из другой и прописать следующую команду:
```
git merge (Branch_Name)
```
В некоторых случая могут возникнуть конфликты объединения, связанные с тем, что одинаковые "участки" файла были отредактированы в разных ветках по разному. В этом случае, нам нужно вручную решить этот конфликт, скорректировав проблемную область. После чего выполнить коммит.

Также можно добавить еще одну команду `git log --graph`, которая отобразит коммиты и ветки в виде "дерева" последовательности, как показано на скриншоте ниже:


![LogGraphPic](GitGraph2.png)

***
Для получения более подробной информации и инструкций, можно обратиться на официальный сайт Git, в раздел [документации](https://git-scm.com/doc).  
Если вы захотите потренироваться использовать команды и возможности Git в интересном формате, то это можно сделать на [данном тренажере](https://learngitbranching.js.org/?locale=ru_RU).

***
Данный текст написан с целью искусственно создать конфликт и решить его. 
```
List[1,5,6,4,9,3,7]
size=7
index=0
sum=0
While (index<size):
    if List[index]>5:
        sum=sum+List[index]
    index=index+1
print(sum)
``` 
В процессе выполнения основной части работы и слияния разных веток их не возникло.  
**ПЕРЕД НАЧАЛОМ НОВОГО ЭТАПА РАБОТЫ ДАННУЮ ЧАСТЬ НУЖНО УДАЛИТЬ!!!**