# Умовний рендеринг

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/conditional-rendering-in-vue-3" title="Безкоштовний урок по умовному рендеринг у Vue.js"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-conditionals-in-vue" title="Безкоштовний урок по умовному рендеринг у Vue.js"/>
</div>

<script setup>
import { ref } from 'vue'
const awesome = ref(true)
</script>

## `v-if`

Директива `v-if` використовується для умовного рендерингу блоку. Блок буде згенеровано лише якщо вираз у директиві повертає правдиве значення.

```vue-html
<h1 v-if="awesome">Vue — це круто!</h1>
```

## `v-else`

Ви можете використовувати директиву `v-else` для вказування "блоку інакше" для `v-if`:

```vue-html
<button @click="awesome = !awesome">Перемкнути</button>

<h1 v-if="awesome">Vue — це круто!</h1>
<h1 v-else>Ой, ні 😢</h1>
```

<div class="demo">
  <button @click="awesome = !awesome">Перемкнути</button>
  <h1 v-if="awesome">Vue — це круто!</h1>
  <h1 v-else>Ой, ні 😢</h1>
</div>

<div class="composition-api">

[Спробуйте в пісочниці](https://sfc.vuejs.org/#eNp9kE9KAzEUxq/ymk0VOhO6LWnRS7jKph3f2KnNH5JMuygDRcETiLiy4B0KWtQzZK7gCTyCSWewotDde1++70fetyLnWqeLEsmAMJuZQjuw6Eo94rIQWhkHKzCYQwW5UQK6wdrlkstMSetgvESrBMIwek6cKfGUS0YbUECExaHQ87HDsAGwSemcknCWzYvsesjJAdBpR05GfuO39dpv/Zvf+ff6tr7xL4w20T2UOzbtwyIp8gMi5C5KhM/1PdR3fgt+V6/30Y8Oo9N+zLUpnFsc+Sf/2oNAf4CvzeNza2H057ukR5oCEjHW6cwqGSpaxSN4+2A5GcBeiVooJu6cTJ3TdkCpzbNY7MymylzRMKWmlK4QmKIVycSopUUTwJz0fjFoEBdoEoPyEg2aY8w/1n/ciK24rEj1DYqhuiY=)

</div>
<div class="options-api">

[Спробуйте в пісочниці](https://sfc.vuejs.org/#eNp9kVFKAzEQhq8y5kmhu6Gvy7boJXzKy3Y7tVt3syGZtEIpFAVPIOKTBe9Q0KKeIXsFT+ARTLpLFQVDCPNn5v8If5bsTKl4bpElLDW5LhQNhcQrVWuCMU4yWxIshQQYZ5Qdn7S1II1ktQxKEPiVLdDUFSZA2mI7sgo9f/id8gPaC8JKlRmhVwDpyBLVEk7zssgvB4J1JBjAUVcKNnQbt23Wbute3c69NTfNtXtOeWvdQwWl0z7Mo2LyjfC+c4vwsb6D5tZtwe2a9d76fpTyaT/4OheWBofu0b30wNPv4XPz8NSNpPzwXNZjRRWCiapMxTNTSx9am0fXMIIlbULhzqcatGBTImUSzs0kD1HPTFzrC+6rWFtJRYUxmioa6XphUHuwYL0fDO4v56gjjXKMGvV/zF+jf7gBG76Erb4AVmLAPQ==)

</div>

А елемент `v-else` повинен йти безпосередньо за `v-if` або елементом `v-else-if` — в іншому випадку їх не буде розпізнано.

## `v-else-if`

`v-else-if`, як і підказує його назва, слугує в якості "блоку інакше якщо" для `v-if`. Може бути також і ланцюжок таких елементів:

```vue-html
<div v-if="type === 'A'">
  А
</div>
<div v-else-if="type === 'B'">
  Б
</div>
<div v-else-if="type === 'C'">
  А
</div>
<div v-else>
  Не А/Б/В
</div>
```

Подібно до `v-else`, елемент `v-else-if` повинен йти безпосередньо за `v-if` або `v-else-if` елементами.

## `v-if` в `<template>`

Оскільки `v-if` є директивою, вона має бути додана до одиничного лементу. Але робити у випадку, коли ми хочемо перемикати більше, ніж один елемент? У такому разі ми можемо використовувати `v-if` в елементі `<template>`, який слугує невидимою обгорткою. Фінальний результат рендеру не міститиме елемент `<template>`.

```vue-html
<template v-if="ok">
  <h1>Заголовок</h1>
  <p>Параграф 1</p>
  <p>Параграф 2</p>
</template>
```

`v-else` та `v-else-if` також можуть використовуватись в `<template>`.

## `v-show`

Ще однією можливістю для умовного показу елементу є директива `v-show`. Використання по суті аналогічне:

```vue-html
<h1 v-show="ok">Привіт!</h1>
```

Різниця полягає в тому, що елемент з `v-show` буде завжди згенерований и лишатиметься в DOM, оскільки `v-show` лише перемикає CSS властивість `display` елемента.

`v-show` не підтримується елементом `<template>`, та не працює з `v-else`.

## `v-if` проти `v-show`

`v-if` впливає на "справжній" рендеринг, забезпечуючи, під час перемикання, належне видалення та створення наглядачів подій та дочірніх елементів всередині блоків.

`v-if` також **лінивий**: якщо умова є неправдивою при початковому рендері, він нічого не робитиме — умовний блок не буде згенерований, доки умова вперше не стане правдивою.

`v-show` у порівнянні — елемент завжди згенерований, незважаючи на початкову умову, завдяки перемиканню лише CSS властивостей.

Вцілому, `v-if` має вищу вартість під час перемикання, коли `v-show` має вищу вартість під час початкового рендерингу. Тому надавайте перевагу `v-show`, якщо вам потрібно перемикати щось часто, та `v-if`, якщо умова навряд чи змінюватиметься під час виконання програми.

## `v-if` з `v-for`

::: warning Примітка
**Не** рекомендовано використовувати `v-if` і `v-for` на тому ж самому елементі із-за їхнього неявного пріоритету. Зверніться до [посібника по стилях](/style-guide/rules-essential.html#уникайте-v-if-з-v-for) для деталей.
:::

Коли обидва `v-if` та `v-for` використовуються на тому ж елементі, `v-if` буде обчисленим першим. Перегляньте [Гід по рендерингу списків](list.html#v-for-з-v-if) для деталей.
