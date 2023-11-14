# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил:
- Серафим Данил Артемович
- РИ220945
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
научиться передавать в Unity данные из Google Sheets с помощью Python.

## Задание 1
## Выберите одну из компьютерных игр, приведите скриншот её геймплея и краткое описание концепта игры. Выберите одну из игровых переменных в игре (ресурсы, внутри игровая валюта, здоровье персонажей и т.д.), 
опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней

![alt text](https://nintendoeverything.com/wp-content/uploads/sites/1/nggallery/pikmin-3-deluxe-1/Pikmin3Deluxe_scrn_015.jpg)
Pikmin 3 - Реал тайм стратегия где игрок оптимизирует управление пикминов чтобы получить максимальное количество сока из каждого дня и при этом продвинуться дальше по истории. 
Каждый день выживания стоит 1 бутылку сока, поэтому если игрок не сможет достаточно сохранить, ему придется начинать заново. 


Ход работы: В Игре PIKMIN 3(DELUXE) одна из игровых валют это живые помошники пикмины, которыми командует игрок. От количества пикминов зависит то, какие задачи может выполнять игрок в данный момент.
Например, чтобы нести большой кусок арбуза, нужно отправить 20 пикминов задание. Количество увеличивается, когда игрок убивает врагов и использует их трупы чтобы вырастить больше пикминов на базе. (Пикмины используются для и битвы, поэтому это эдакий бесконечный цикл)
Уменьшается их количество если они умирают или если по окончанию дня они остались где-то на карте не под контролем игрока. Максимальное количество пикминов на карте равно сотне, но в запасе их может быть и больше,теоретически до 999.
центр - это пикмины. слева - враги. Справа - фрукты, которые при помощи пикминов транспортируются на корабль чтобы питать жизненные силы игровых персонажей.
![alt text](https://github.com/CerafimD/workshop2/blob/main/template.jpg)


## Задание 2
### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в выбранной игре (в качестве таких переменных может выступать игровая валюта, ресурсы, здоровье и т.д.). Средствами google-sheets визуализируйте данные в google-таблице (постройте график, диаграмму и пр.) для наглядного представления выбранной игровой величины.
Немного модифицировав код данный в воркошопе у меня получилось вывести вот такой график
![alt text]([https://github.com/CerafimD/workshop2/blob/main/графики.jpg])
На нем синий - основное число, количество pikmin'ов которое как и должно, растет, затем желтый - это общее количество собранных фруктов и красный - количество врагов. Все величины показывают себя примерно также как и при обычной игре.
код для модификации таблицы и генерирования графиков: 
```
import gspread
import numpy as np
from random import randint
gc = gspread.service_account(filename='unitydatascience-400606-78cc91d889e0.json')
sh = gc.open("UnityWorkshop2")
fruits_total = 0
pikmin = 25
mon = list(range(1,10))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        enemies = randint(1,10)
        fruits = randint(1,5)
        if pikmin > (enemies*5) and pikmin > (fruits*7) :
            pikmin += enemies*3
            fruits_total+=fruits
        elif pikmin > enemies*5:
            pikmin += enemies*3
        if pikmin > (fruits*7):
            fruits_total +=fruits
        sh.sheet1.update(('A' + str(i)), i)
        sh.sheet1.update(('B' + str(i)), pikmin)
        sh.sheet1.update(('C' + str(i)), enemies)
        sh.sheet1.update(('D' + str(i)), fruits_total)
        print(pikmin)
        print(fruits_total)
```


## Задание 3
### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

- Перечисленные в этом туториале действия могут быть выполнены запуском на исполнение скрипт-файла, доступного [в репозитории](https://github.com/Den1sovDm1triy/hfss-scripting/blob/main/ScreatingSphereInAEDT.py).
- Для запуска скрипт-файла откройте Ansys Electronics Desktop. Перейдите во вкладку [Automation] - [Run Script] - [Выберите файл с именем ScreatingSphereInAEDT.py из репозитория].

```py

import ScriptEnv
ScriptEnv.Initialize("Ansoft.ElectronicsDesktop")
oDesktop.RestoreWindow()
oProject = oDesktop.NewProject()
oProject.Rename("C:/Users/denisov.dv/Documents/Ansoft/SphereDIffraction.aedt", True)
oProject.InsertDesign("HFSS", "HFSSDesign1", "HFSS Terminal Network", "")
oDesign = oProject.SetActiveDesign("HFSSDesign1")
oEditor = oDesign.SetActiveEditor("3D Modeler")
oEditor.CreateSphere(
	[
		"NAME:SphereParameters",
		"XCenter:="		, "0mm",
		"YCenter:="		, "0mm",
		"ZCenter:="		, "0mm",
		"Radius:="		, "1.0770329614269mm"
	], 
)

```

## Выводы

Абзац умных слов о том, что было сделано и что было узнано.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
