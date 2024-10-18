# 1 Проектиование

## Разделение на Microfrontends

Для разделения была выбрана стратегия "Вертикальная нарезка"

Выделены следующие домены:
- Card - отображение и добавление карточек мест
- Profile - настройка, редактирование профиля
- Auth - регистрация и авторизация пользователей

Так же общая точка входа General(root/host в зависимости от фреймворка)

Данная декомпозиция позволит:
- Командам сосредоточиться на бизнес задачах в конкретной области
- Обновлять определенный microfrontend не затрагивая остальные и точечно откатывать в случае возникновения ошибки
- Реализовать процесс непрерывной интеграции и поставки

## Выбор фреймворка

Для проекта Mesto лучше всего подойдет фреймворк Module Federation, т.к:
- На проекте не предвидется надобность в использовании различных фреймворков
- Возможность использования общего кода (например PopUp окна)

# 2 Планирование изменений

Запускать фронтенды можено используя docker compose

## Структура фронтендов

```
├── auth
│   ├── compilation.config.js
│   ├── Dockerfile.frontend
│   ├── package.json
│   ├── src
│   │   ├── App.jsx
│   │   ├── blocks
│   │   │   ├── auth-form
│   │   │   │   ├── auth-form.css
│   │   │   │   ├── __button
│   │   │   │   │   └── auth-form__button.css
│   │   │   │   ├── __form
│   │   │   │   │   └── auth-form__form.css
│   │   │   │   ├── __input
│   │   │   │   │   └── auth-form__input.css
│   │   │   │   ├── __link
│   │   │   │   │   └── auth-form__link.css
│   │   │   │   ├── __text
│   │   │   │   │   └── auth-form__text.css
│   │   │   │   ├── __textfield
│   │   │   │   │   └── auth-form__textfield.css
│   │   │   │   └── __title
│   │   │   │       └── auth-form__title.css
│   │   │   └── login
│   │   │       └── login.css
│   │   ├── components
│   │   │   ├── Login.js
│   │   │   └── Register.js
│   │   ├── index.css
│   │   ├── index.html
│   │   ├── index.js
│   │   └── utils
│   │       └── auth.js
│   └── webpack.config.js
```
---
```
├── card
│   ├── compilation.config.js
│   ├── Dockerfile.frontend
│   ├── package.json
│   ├── src
│   │   ├── App.jsx
│   │   ├── blocks
│   │   │   ├── card
│   │   │   │   ├── card.css
│   │   │   │   ├── __delete-button
│   │   │   │   │   ├── card__delete-button.css
│   │   │   │   │   ├── _hidden
│   │   │   │   │   │   └── card__delete-button_hidden.css
│   │   │   │   │   └── _visible
│   │   │   │   │       └── card__delete-button_visible.css
│   │   │   │   ├── __description
│   │   │   │   │   └── card__description.css
│   │   │   │   ├── __image
│   │   │   │   │   └── card__image.css
│   │   │   │   ├── __like-button
│   │   │   │   │   ├── card__like-button.css
│   │   │   │   │   └── _is-active
│   │   │   │   │       └── card__like-button_is-active.css
│   │   │   │   ├── __like-count
│   │   │   │   │   └── card__like-count.css
│   │   │   │   └── __title
│   │   │   │       └── card__title.css
│   │   │   ├── content
│   │   │   │   └── content.css
│   │   │   ├── page
│   │   │   │   ├── __content
│   │   │   │   │   └── page__content.css
│   │   │   │   ├── page.css
│   │   │   │   └── __section
│   │   │   │       └── page__section.css
│   │   │   └── places
│   │   │       ├── __item
│   │   │       │   └── places__item.css
│   │   │       ├── __list
│   │   │       │   └── places__list.css
│   │   │       └── places.css
│   │   ├── components
│   │   │   ├── AddPlacePopup.js
│   │   │   └── Card.js
│   │   ├── index.css
│   │   ├── index.html
│   │   ├── index.js
│   │   └── utils
│   │       └── api.js
│   └── webpack.config.js
```
---
```
├── general
│   ├── blocks
│   │   ├── footer
│   │   │   ├── __copyright
│   │   │   │   └── footer__copyright.css
│   │   │   └── footer.css
│   │   └── header
│   │       ├── __auth-link
│   │       │   └── header__auth-link.css
│   │       ├── header.css
│   │       ├── __logo
│   │       │   └── header__logo.css
│   │       ├── __logout
│   │       │   └── header__logout.css
│   │       ├── __user
│   │       │   └── header__user.css
│   │       └── __wrapper
│   │           └── header__wrapper.css
│   ├── compilation.config.js
│   ├── components
│   │   ├── App.js
│   │   ├── Footer.js
│   │   └── Header.js
│   ├── Dockerfile.frontend
│   ├── package.json
│   ├── src
│   │   ├── App.jsx
│   │   ├── index.css
│   │   ├── index.html
│   │   └── index.js
│   └── webpack.config.js
```
---
```
└── profile
    ├── blocks
    │   └── profile
    │       ├── __add-button
    │       │   └── profile__add-button.css
    │       ├── __description
    │       │   └── profile__description.css
    │       ├── __edit-button
    │       │   └── profile__edit-button.css
    │       ├── __image
    │       │   └── profile__image.css
    │       ├── __info
    │       │   └── profile__info.css
    │       ├── profile.css
    │       └── __title
    │           └── profile__title.css
    ├── compilation.config.js
    ├── Dockerfile.frontend
    ├── package.json
    ├── src
    │   ├── App.jsx
    │   ├── components
    │   │   ├── EditAvatarPopup.js
    │   │   └── EditProfilePopup.js
    │   ├── index.css
    │   ├── index.html
    │   └── index.js
    ├── utils
    │   └── api.js
    └── webpack.config.js
```