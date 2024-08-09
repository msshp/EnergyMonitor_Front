# vue-project

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

Журнал изменений


8.08.24 - сохранение версии дашборда с тремя каналами (Напряжение, Потребление и суммарное потребление в ряд по 1 каналу)

9.08.24 - страница устройства: обновление Напряжение (канал A) и Ток (канал A) каждую минуту по запросу http://e-mon.io-tech.ru/api/devices/id/ (при условии что пользователь на странице дашборда. в противном случае запроса не происходит)