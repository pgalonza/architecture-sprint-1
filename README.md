# Задание 1

## 1 Проектиование

### Разделение на Microfrontends

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

### Выбор фреймворка

Для проекта Mesto лучше всего подойдет фреймворк Module Federation, т.к:
- На проекте не предвидется надобность в использовании различных фреймворков
- Возможность использования общего кода (например PopUp окна)

## 2 Планирование изменений

Запускать фронтенды можено используя docker compose

### Структура фронтендов

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

# Задание 2

## Описание компонентов

* Balancer - балансирощик между WAF принимающий подключения из внешней сети.
* WAF - фаервол для веб-приложений, анализирует и фильтурет L7 трафик.
* Gateway - внутренний балансирощик дополнительно выполняет функцию валидации jwt-токена
* External gatewa - выходной узел для контроля запросов во вне.
* Identity provider - провайдер аунтетификации реализует OIDC. Берет на себя функции регистрации и выдачу токенов.
* Брокер сообщений - реализация очереди сообщений, Позволяет микросервисам подписываться на нужную очередь, отсылать и обрабатывать сообщения по мере производительности сервисов без потерь.
* Service discovery - обнаружение запущенных сервисов и хранилище конфигураций. Позволяет реализовать балансировку между экземплярами и достичь отказоустойчивости.
* Notifications - Сервис отправляет уведомления пользователям. События забирает из брокера сообщений.
* Validation - backend-сервис отвечает за прием заявок на регистрацию, валидацию заявок и отправку уведомления о решении в отношении заявок. При обобрении заявки заводит профиль в Identity provider.
* MicroFrontend auth - frontend реализует UI интерфейс аунтетификации и регистрации.
    * В регистрации учавствует сервис Validation
    * В аунтетификации учавствет сервис Identity provider
* Auction - backend-сервис предоставляет методы для работы с аукционом.
* MicroFrontend auction - frontend реализует UI интерфейс для работы с аукционом.
* Appeal - backend-сервис предоставляет методы для работы с аппиляциями.
* MicroFrontend Appeal - frontend реализует UI интерфейс для работы с аппиляциями.
* Orders - backend-сервис предоставляет методы для работы с заказами.
* MicroFrontend orders - frontend реализует UI интерфейс для работы с заказами.
* Reports - backend-сервис предоставляет методы для работы с отчетами.
* MicroFrontend Reports - frontend реализует UI интерфейс для работы с отчетами.
* HelpDesk - backend-сервис предоставляет методы для работы с заявками.
* MicroFrontend HelpDesk - frontend реализует UI интерфейс для работы с заявками.
* Admin - backend-сервис предоставляет методы для администрирования проекта.
* MicroFrontend admin - frontend реализует UI интерфейс для работы с задачами администратора проекта.
* Products - backend-сервис предоставляет методы для работы с товарами.
* MicroFrontend Products - frontend реализует UI интерфейс для работы с товарами.
* Amenities - backend-сервис предоставляет методы для работы с услугами.
* MicroFrontend Amenities - frontend реализует UI интерфейс для работы с услугами.
* Profile - backend-сервис предоставляет методы для работы с профилем. Профиль находится непосредсвтенно в Identity provider. При усложении профиля можно вынести хранение информации в отдельную БД.
* MicroFrontend Amenities - frontend реализует UI интерфейс для работы с профилем.
* Payment - backend-сервис предоставляет методы для работы с оплатой.
* MicroFrontend payment - frontend реализует UI интерфейс для работы с оплатой.
