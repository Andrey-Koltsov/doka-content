---
title: "Атрибут `novalidate`"
description: "Отключает валидацию формы. Зачем нам валидация формы браузером, когда у нас есть JavaScript?"
authors:
  - vchychuzhko
contributors:
  - skorobaeus
  - tatianafokina
editors:
  - tachisis
keywords:
  - атрибут
  - валидация
  - форма
  - сабмит
related:
  - html/form
  - js/deal-with-forms
  - css/invalid-valid
tags:
  - doka
---

## Кратко

Атрибут отключает нативную валидацию формы со стороны браузера.

## Как пишется

```html
<form novalidate>...</form>
```

Атрибут `novalidate` пишется внутри открывающего тега формы, без каких-либо значений.

## Пример

Создадим форму для отзывов о сервисе. Обязательными для заполнения будут поля почты для обратной связи, комментария и согласия на обработку персональных данных:

```html
<form novalidate>
  <div class="form-row">
    <label for="name">Имя:</label>
    <input
      type="text"
      name="name"
      id="name"
      placeholder="Микки"
    >
  </div>
  <div class="form-row required">
    <label for="email">Почта</label>
    <input
      type="email"
      name="email"
      id="email"
      placeholder="email@example.com"
      required
    >
  </div>
  <div class="form-row required">
    <label for="comment">Комментарий</label>
    <textarea
      name="comment"
      id="comment"
      placeholder="Мне всё понравилось!"
      required
    >
    </textarea>
  </div>
  <div class="form-row">
    <label>
      <input
        type="checkbox"
        name="agree"
        required
      >
      <span class="checkbox-title">
        Соглашаюсь с обработкой персональных данных
      </span>
    </label>
  </div>
  <button type="submit">Отправить</button>
</form>
```

### Результат

<iframe title="Форма с отключённой валидацией" src="demos/form-validation/" height="610"></iframe>

Хоть некоторые поля являются обязательными к заполнению, и даже есть поле с типом `email`, вы всё равно сможете отправить пустую форму. Но как только вы уберёте атрибут `novalidate` с помощью кнопки «Вернуть валидацию», браузер не даст отправить форму, пока все поля не будут заполнены верно.

## Как понять

Каждое поле формы, которое заполняет пользователь, может иметь чётко указанный тип и правила ввода. В момент, когда пользователь отправляет форму, браузер проверяет правильность заполненных данных, блокируя отправку в случае ошибки и показывая подсказку там, где она была допущена.

Например, поля с атрибутом [`required`](/html/required/) должны быть обязательно заполнены, и браузер укажет, если пользователь вдруг какое-нибудь из них пропустил.

Атрибут `novalidate` говорит браузеру не проверять поля и не препятствовать отправке формы, так как иногда подобное поведение бывает нежелательным. К примеру, форма проверяется при помощи JavaScript, и нужно избежать конфликтов с браузерной валидацией. В том числе, и убрать всплывающие подсказки, чтобы показать вместо них свои, кастомные.

При помощи атрибута `novalidate` браузер можно просто попросить не вмешиваться — например, вместо того чтобы убирать атрибуты `required` с полей или даже заменять [`<form>`](/html/form/) на [`<div>`](/html/div/). Этим атрибут позволяет сохранить семантически верный и доступный код.

## Подсказки

💡 Проверка введённых данных происходит только при попытке отправить форму.

💡 Независимо от наличия атрибута `novalidate`, к полям формы (как и к самой форме и её [филдсетам](/html/fieldset/)) в любом случае будут применяться псевдоклассы [`:invalid/:valid`](/css/invalid-valid/).

💡 Эффект атрибута `novalidate` схож с эффектом атрибута `formnovalidate`, который можно применить к кнопке отправки формы — `<button type="submit">`, `<input type="submit">` или `<input type="image">`. Он тоже даёт браузеру указание закрыть глаза на валидацию.
