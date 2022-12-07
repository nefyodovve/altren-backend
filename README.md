# Техническое задание

Создать бэкенд-сервер для НРИ Альтрен. Приложения-клиенты должны подключаться к бэкенду и на основе его данных отображать лист персонажа игрока.

Сервер можно условно разделить на 2 части:
1. `rules-db` - База данных с информацией о характеристаках, расах, навыках, талантах, их описания, эффекты и т.д.
2. `charsheets-db` - База данных с листами персонажей.

## `rules-db`

Каждый объект имеет обязтельный параметр с описанием объекта.

Маркер (пополняемый) означает, что список может быть пополнен во время игры из клиента.

### Характеристики

* Cила
* Ловкость
* Интеллект
* Харизма
* Выносливость

### Расы

* Человек
* Мальф
* Зверолюд
* Мутант

Каждая раса сопроваждается массивом эффектов от этой расы.

### Навыки

* Владение одноручным оружием (Сила)
* Охота/выживание (Ловкость)
* Алхимия (Интеллект)
* Торговля (Харизма)
* Увеличение здоровья (Выносливость)
* ...

Характеристика имеется отношение `One to Many` к навыкам.

### Специализации (экспертные навыки)

* Бронник (кузнец)
* Оружейник (кузнец)
* Шахтер (Черное ремесло)
* Разнорабочий (Черное ремесло)
* ...

Навык имеет отношение `One to Many` к специализациям.

### Боги
(пополняемый)

* Камила
* Марея
* Кхал
* ...

### Заклинания
(пополняемый)

* Длань Камилы - адепт (Камила)
* Дхарма Камилы - суффраган (Камила)
* Цепь крови - жрец (Кхал)
* ...

Боги имеют отношение `One to Many` к заклинаниям.

Одно и то же заклинение может иметь разные эффекты на разных рангах жреца. Т.к. ранги жреца сложно определить заранее, могут быть скрытые ранги (например басидж), предлагается информацию об этом включать в название заклинания.


Заклинания имеют параметры:
* Порог кармы, при котором заклинание доступно
* Флаг божественного благословения (ББ)
* Эффект
* Длительность
* Массив расходных ресурсов, например мана, ветвь/лист Аники, кровь жреца.

### Ресурсы

* Здоровье
* Мана
* Энергия
* Порог
* Лист Аники
* Ветвь Аники
* ...

### Способности

* Давай еще раз
* Далеко не убежишь
* Уклонение
* Вставай

### Таланты

* Аристократ
* Ночное зрение (мутация)
* Чутье на магию
* ...

Таланты имеют параметр
* Флаг "Особый" - талант можно получить только при создании персонажа

### Мутации
(пополняемый)

* Звериные глаза
* Кровавая доля
* Аква-отреголум
* ...

Мутация имеет параметр силы (легкая, средняя, высшая)


### Гильдии
(пополняемый)

* Гильдия артистов

Гильдия содержит массив парамтров по уровням гильдии с описанием эффектов от каждого уровня.


### Правила

* Ведение боя
* Отдых
* Лечение
* Стойки
* Парирование
* Сложность ношения доспеха
* Отдых
* Сбор ресурсов
* Продвинутая медицина
* Мутации

## `charsheets-db`

Должна быть возможность создавать новых пользователей. Каждый пользователь может иметь несколько чарлистов.

Чарист содержит следующие данные:

* Имя
* Раса
* Таланты
* Мутации
* Характеристики
* Навыки
* Здоровье
* Мана/Энергия
* Порог
* Инвентарь
* Экипировка
* Деньги