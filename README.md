# Feature-Sliced Design + code guidelines

В данном кодовом руководстве представлены рекомендации по стилю написания кода.

# Установка

Установите всё необходимое для eslint через npm:

```bash
npm install -D eslint @feature-sliced/eslint-config @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb eslint-config-next eslint-config-prettier eslint-plugin-boundaries eslint-plugin-prettier eslint-plugin-unicorn prettier
```

### Структура проекта
```
└────
    ├── pages
    │   ├── _app.tsx
    │   ├── index.tsx
    │   ├── **/*.tsx
    │   └── *.tsx
    ├── public
    │   ├── fonts
    │   │   └── *.woff2
    │   ├── sprites
    │   │   └── *.svg
    │   ├── favicon.svg
    ├── src
    │   ├── app
    │   │   └── styles
    │   │   └── providers
    │   │   └── HOCs
    │   │   ├── index.tsx
    │   ├── processes
    │   │   └── **/*.ts
    │   ├── pages
    │   │   └── **/*.tsx
    │   ├── widgets
    │   │   └── **/*.tsx
    │   ├── features
    │   │   └── **/*.tsx
    │   ├── entities
    │   │   └── **/*.tsx
    │   ├── shared
    │   │   └── api
    |   |   └── lib
    |   |   └── ui
    |   |   └── config
```
### Структуры слайса и сегмента model
```
└────
    ├── user
    │   ├── ui
    │   ├── api
    │   ├── model
    │   │   ├── slices    
    │   │   ├── types 
    │   │   ├── selectors    
    │   │   ├── slices
    │   │   └── ...
    |   └── index.ts - public api
    ├── post
    |   └── **/*.tsx
```

### Используйте нейминг файлов или папок только в стиле kebab-case, Все буквы маленькие, слова разделены дефисом. [https://developers.google.com/style/filenames](https://developers.google.com/style/filenames)

```
src
└── pages
    ├── home
    │   ├── ui.tsx
    │   ├── styles.module.scss
    │   └── index.ts
    └── about-us
        ├── ui.tsx
        ├── styles.module.scss
        └── index.ts
```

## Гид по стилям

### 2 Пробела для отступа

Используйте 2 пробела, чтобы сделать отступ в коде, и не смешивайте табуляции и пробелы.

### 120 символов в строке

Ограничьте свои строки до 120 символов.

### Пробелы в комментариях
*Плохо:* ❌
```js
//This is a comment with no whitespace at the beginning

/*This is a comment with no whitespace at the beginning */
```
*Хорошо:* ✔️
```js
// This is a comment with no whitespace at the beginning

/* This is a comment with no whitespace at the beginning */
```
### Шаблоны в двойных кавычках
*Плохо:* ❌
```js
"Hello ${name}!";
'Hello ${name}!';
"Time: ${12 * 60 * 60 * 1000}";
```
*Хорошо:* ✔️
```js
`Hello ${name}!`;
`Time: ${12 * 60 * 60 * 1000}`;

someFunction(`Hello ${name}`);
```

### Одинарные кавычки

*Плохо:* ❌
```js
import Name from "file/path";

const foo = "bar";
```
*Хорошо:* ✔️
```js
import Name from 'file/path';

const foo = 'bar';
```

### Двойные кавычки в тегах (jsx, tsx)

*Плохо:* ❌
```jsx
<input type='text' />
```
*Хорошо:* ✔️
```jsx
<input type="text" />
```

### Обязательный атрибут alt в тегах для картинок (jsx, tsx)

*Плохо:* ❌
```jsx
<area {...props} />

<img {...props} />

<input type="img" {...props}  />
```
*Хорошо:* ✔️
```jsx
<area alt="This is descriptive!" />

<img alt="This is descriptive!" {...props} />

<input type="img" alt="This is descriptive!" {...props} />
```

### Используйте camelCase
*Плохо:* ❌
```js
const user_name = "John";
```
*Хорошо:* ✔️
```js
const userName = "John";

/* ignore destructuring */
const { some_property, ...rest } = obj;
```

### Формат пробелов в объектах
*Плохо:* ❌
```js
import {isUndefined} from 'lodash';

const user = { name: 'John', age: 25 };

const { ...otherProperties } = obj;
```
*Хорошо:* ✔️
```js
import { isUndefined } from "lodash";

const user = { name: "John", age: 25 };

const { ...otherProperties } = obj;
```

### Не используйте var
*Плохо:* ❌
```js
var user_name = 'John';
```
*Хорошо:* ✔️
```js
const foo = "foo";
let bar = "bar";
```

### Неиспользуемые переменные
To avoid errors, remove unused variables.

Во избежание ошибок удалите неиспользуемые переменные.

*Плохо:* ❌
```js
const arr = [1, 2, 3];
const someVar = "bla.com"
const items = arr.map((item, index) => `Counter: ${index}`);
```
*Хорошо:* ✔️
```js
const arr = [1, 2, 3];
const items = arr.map((_, index) => `Counter: ${index}`);
```

### Не используйте eval()
*Плохо:* ❌
```js
window.eval("var a = 0");
global.eval("var a = 0");
```
*Хорошо:* ✔️
```js
class A {
    foo() {
        // This is a user-defined method.
        this.eval("var a = 0");
    }

    eval() {}

    static {
        // This is a user-defined static method.
        this.eval("var a = 0");
    }

    static eval() {}
}
```

### Условный оператор используйте строгое сравнение ===

*Плохо:* ❌
```js
const a = 0;
if (a == '') {
  console.log('losing');
}
```
*Хорошо:* ✔️
```js
const a = 0;
if (a !== '') {
  console.log('winning');
}
```

### Отдавайте предпочтение конструкции Switch вместо нескольких else-if (3)

*Плохо:* ❌
```js
if (foo === 1) {
    // 1
} else if (foo === 2) {
    // 2
} else if (foo === 3) {
    // 3
} else {
    // default
}
```
*Хорошо:* ✔️
```js
if (foo === 1) {
    // 1
} else if (foo === 2) {
    // 2
}
```
```js
switch (foo) {
    case 1: {
        // 1
        break;
    }
    case 2: {
        // 2
        break;
    }
    case 3: {
        // 3
        break;
    }
    default: {
        // default
    }
}
```

### Именование переменных, функций и классов
- Используйте осмысленные имена переменных, функций и классов. Имена должны ясно описывать их назначение и использование.
- Используйте camelCase для именования переменных и функций (первое слово со строчной буквы, каждое следующее слово с заглавной).
- Используйте PascalCase для именования классов (каждое слово с заглавной буквы).
- Избегайте слишком общих имен, таких как data, value, temp, которые могут привести к путанице.

### Не используйте any || any[ ] типы

Если вы не знаете тип переменной, используйте Generic или unknown.

*Плохо:* ❌
```ts
interface User {
    name: any
}

interface Users {
    data: any[]
}
```
*Хорошо:* ✔️
```ts
interface User {
    name: string
}

interface Users {
    data: Array<User> | User[]
}

*Плохо:* ❌
```js
const x = 5;
function func(a, b) {
  // ...
}
```
*Хорошо:* ✔️
```js
const age = 25;
function calculateSum(num1, num2) {
  // ...
}

class Customer {
  // ...
}
```

### Именование типов
Рекомендуется следовать этим принципам для создания понятного и консистентного кода.

###### - Не используйте префикс "I" для интерфейсов
В языках программирования, где интерфейсы являются отдельным типом, префикс "I" (от "Interface") ранее использовался для именования интерфейсов, например, IMyInterface. Однако, в современных практиках разработки такое именование стало менее распространенным. Рекомендуется использовать более конкретные и описательные названия для интерфейсов, без префикса "I". Например, вместо IMyInterface лучше использовать MyService или MyContract.

###### - Используйте "Base" для базовых классов
Когда создаете базовый класс, которым будут пользоваться другие классы в иерархии, можно добавить префикс "Base" к его имени. Например, если у вас есть класс Musor, и вы хотите создать базовый класс, от которого будут наследоваться другие классы, то можно назвать его BaseMusor.

###### - Используйте "Dto" для объектов передачи данных
Когда вы работаете с объектами передачи данных (Data Transfer Objects, DTO) или моделями, которые используются для передачи данных через API или другие механизмы связи, рекомендуется добавлять суффикс "Dto" к их именам. Например, если у вас есть класс, представляющий продукт, который передается через API, то можно назвать его ProductDto.
