---
summary: "AdonisJS is a TypeScript-first web framework for Node.js. You can use it to create a full-stack web application or a JSON API server."
---

# Введение

::include{template="partials/introduction_cards"}

## Что такое AdonisJS?

AdonisJS - это веб-фреймворк для Node.js, основанный на TypeScript. С его помощью можно создать полнофункциональное веб-приложение или сервер JSON API.

На фундаментальном уровне AdonisJS [обеспечивает структуру ваших приложений](../getting_started/folder_structure.md), настраивает [бесшовную среду разработки TypeScript](../concepts/typescript_build_process.md), настраивает [HMR](../concepts/hmr.md) для вашего внутреннего кода и предлагает обширную коллекцию хорошо поддерживаемых и подробно документированных пакетов.

Мы представляем себе, как команды, использующие AdonisJS, **тратят меньше времени** на тривиальные решения, такие как подбор пакетов npm для каждой незначительной функции, написание «клейкого» кода, споры об идеальной структуре папок, и **тратят больше времени** на создание реальных функций, критически важных для бизнеса.

### Независимость от фронтенда 

AdonisJS фокусируется на бэкенде и позволяет вам выбрать стек фронтенда по своему усмотрению.

Если вам нравится все упрощать, используйте AdonisJS в паре с [традиционным шаблонизатором](../views-and-templates/introduction.md) для генерации статического HTML на сервере, создайте JSON API для вашего фронтенд-приложения Vue/React или используйте [Inertia](../views-and-templates/inertia.md), чтобы ваш любимый фронтенд-фреймворк работал вместе в полной гармонии.

Цель AdonisJS - предоставить вам батареи для создания надежного бэкенд-приложения с нуля. Будь то отправка электронной почты, проверка правильности ввода данных пользователем, выполнение CRUD-операций или аутентификация пользователей. Мы позаботимся обо всем этом.

### Современный и типобезопасный

AdonisJS построен на основе современных примитивов JavaScript. Мы используем модули ES, псевдонимы импорта подпутей Node.js, SWC для выполнения исходных текстов TypeScript и Vite для объединения активов.

Кроме того, TypeScript играет значительную роль при разработке API фреймворка. Например, в AdonisJS есть:

- [Типобезопасный эмиттер событий](../digging_deeper/emitter.md#making-events-type-safe)
- [Типобезопасные переменные окружения](../getting_started/environment_variables.md)
- [Типобезопасная библиотека валидации](../basics/validation.md)

### Приверженность MVC

В AdonisJS реализован классический шаблон проектирования MVC. Вы начинаете с определения маршрутов с помощью функционального JavaScript API, привязываете к ним контроллеры и пишете логику для обработки HTTP-запросов внутри контроллеров.

```ts
// title: start/routes.ts
import router from '@adonisjs/core/services/router'
const PostsController = () => import('#controllers/posts_controller')

router.get('posts', [PostsController, 'index'])
```

Контроллеры могут использовать модели для получения данных из базы данных и отображения представления (также известного как шаблон) в качестве ответа.

```ts
// title: app/controllers/posts_controller.ts
import Post from '#models/post'
import type { HttpContext } from '@adonisjs/core/http'

export default class PostsController {
  async index({ view }: HttpContext) {
    const posts = await Post.all()
    return view.render('pages/posts/list', { posts })
  }
}
```

Если вы создаете сервер API, вы можете заменить слой представления на JSON-ответ. Но процесс обработки и ответа на HTTP-запросы останется прежним.

```ts
// title: app/controllers/posts_controller.ts
import Post from '#models/post'
import type { HttpContext } from '@adonisjs/core/http'

export default class PostsController {
  async index({ view }: HttpContext) {
    const posts = await Post.all()
    // delete-start
    return view.render('pages/posts/list', { posts })
    // delete-end
    // insert-start
    /**
     * Массив постов будет преобразован в JSON
     * автоматически.
     */
    return posts
    // insert-end
  }
}
```

## Предварительные условия

Документация AdonisJS написана в виде справочного руководства, охватывающего использование и API нескольких пакетов и модулей, поддерживаемых основной командой.

**Это руководство не научит вас создавать приложение с нуля**. Если вы ищете учебник, мы рекомендуем начать свое путешествие с [Adocasts](https://adocasts.com/). Том (создатель Adocasts) создал несколько высококачественных скринкастов, которые помогут вам сделать первые шаги в AdonisJS.

При этом в документации подробно описано использование доступных модулей и внутренняя работа фреймворка.

## Последние релизы
Ниже приведен список последних релизов. [Нажмите здесь](./releases.md), чтобы просмотреть все выпуски.

::include{template="partials/recent_releases"}

## Спонсоры

::include{template="partials/sponsors"}
