<p align="center">
  <img src="./public/img/vue-cobra-logo.png" width="200">
</p>

# vue-cobra

## Install
#### npm
```
npm install vue-cobra --save
```
#### yarn
```
yarn add install vue-cobra
```

## Usage
#### Default

```html
<template>
  <div>
    <vue-cobra />
  </div>
</template>

<script>
import vueCobra from "vue-cobra";
export default {
  name: "Demo",
  components: {
    vueCobra
  }
}
</script>
```

#### With custom properties

```html
<template>
  <div>
    <vue-cobra
      :height="10"
      :zIndex="900"
      color="#4fc08d"
      :opacity="0.5"
      position="left"
    />
  </div>
</template>

<script>
import vueCobra from "vue-cobra";

export default {
  name: "Demo",
  components: {
    vueCobra
  }
}
</script>
```

#### Register it globally

```js
import Vue from "vue";
import vueCobra from "vue-cobra";

Vue.component("vue-cobra", vueCobra);
```

## Options / Props

| Prop    | Type   | Default value | Required | Description                       |
|---------|--------|---------------|----------|-----------------------------------|
| color   | String | #000          | false    | Set progress bar background color |
| height  | Number | 4           | false    | Set height of progress bar        |
| opacity | Number | 1             | false    | Set opacity from 0 to 1           |
| position | String | top          | false    | Define in which position the bar will be rendered. Accepts: `top`, `bottom` and `left`           |
| zIndex  | String | 1000          | false    | Set value based on css z-index property    |

When `position` property is set, `height` value is used to define the tickness of the bar. This was a quick approach to ensure backward compatibility. Feel free to send a PR.

## Contributors

[Pedro Henrique Silva Fontes](https://github.com/phfontess)

## Acknowledgement

[Diogo Moretti](https://github.com/diogomoretti) - [React Snakke](https://diogomoretti.github.io/react-snakke/)

## License

MIT © [Firmino Changani](https://github.com/flowck)
