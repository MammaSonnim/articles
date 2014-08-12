# basis.entity

Модуль `basis.entity` расширяет функциональность модуля `basis.data`, и предназначен для описания типизированных моделей данных. Он предоставляет функции-конструкторы производящие классы наследников `basis.data.Object` и `basis.data.ReadOnlyDataset`, а так же функции-хелперы для решения различных задач.

Дополнительная функциональность касается, в основном, потомков `basis.data.Object` и включает в себя:

- фиксированный набор полей
- значения по умолчанию
- нормализация значений
- вычисляемые поля
- индексы
- возможность накапливать и откатывать изменения

## Понятие типа

Под типом понимается связка сущностей:

- функция-обертка (`EntityTypeWrapper`)
- конструктор типа (`EntityTypeConstructor`)
- класс

В основном приходится иметь дело только с оберкой, которая уже пользуется остальным. Иногда необходимо обращаться к классу, для его расширения. Обращение к конструктору, происходит крайне редко и можно о нем не знать, но он выполняет основную работу по конструированию типа, содержит информацию о типе и обеспечивает часть механизмов его работы.

Так как основная работа осуществляется с функцией-оберткой, то обычно под "типом" подразумевается именно такие функции.

Создаваемый таким образом класс является наследником `basis.entity.BaseEntity`, а он, в свою очередь, наследником `basis.data.Object`. Таким образом, экземпляры наследуют функциональность `basis.data.Object` и хранят свои данные в поле `data` как ключ-значение.

## Создание типа

Облявление типа (его создание) выполняется с помощью функции `createType`. Этой функции передается конфигурация будущего типа, а результатом выполнения является функция-обертка (тип).

```js
var entity = basis.require('basis.entity');

var MyType = entity.createType({
  name: 'MyType',
  fields: {
    // описание полей
  }
});
```

Не смотря на то, что такие функции не являются конструктором (классом), в обычном смысле, и не используются с оператором `new`, их принято именовать с большой буквы, как классы. Это связанно с тем, что такие функции являются фабриками экземплряров, они создают или обновляют уже существующие экземпляры.

Основной "настройкой" является `fields` – набор полей, а точнее фиксированный набор ключей поля `data`. Его нельзя изменить после обявляения, и все экземпляры типа обязательно будут содержать заданный набор ключей.

Не менее важным, является указание названия типа – `name`. Это не только помогает в разработке и отладке, но так же позволяет осуществлять познее связывание типов между собой. Если название типа не задается, оно генерируется автоматически. Нельзя объявить тип с именем, которое уже занято. В случае конфликта имен, имя для нового типа игнорируется (генерируется автоматически). Таким образом, для одного имени может быть создан только один тип.

Обычно при объявлении типа достаточно указать его название и описать поля. Поэтому у `createType` есть сокращенный синтаксис, и предыдущий пример может быть описан так:

```js
var entity = basis.require('basis.entity');

var MyType = entity.createType('MyType', {
  // описание полей
});
```

При объявлении типа доступны следующие опции:

- name
- index
- all
- singleton
- fields
- aliases
- constrains
- state

### Обертка

### Описание полей

- type
- defValue
- id
- index
- calc

#### Значение по умолчанию

Значение по умолчанию задается настройкой `defValue`. Это может быть любое значение или функция.

Значение по умолчанию используется только в том случае, если нет

#### Индексы

#### Вычисляемые поля

#### Типы полей

Boolean, Number, String

##### Array

##### Date

##### Перечисления (enum)

##### Вложенные типы

### Работа с полями

### Накопление и откат изменений (rollback)

## EntitySet

## Построение инфраструктуры

```js
require('basis.entity').validate()
```