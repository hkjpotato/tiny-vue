# what it is about?
- Reverse engineering on Vue src code, and recreate a tiny Vue 

```
vue.runtime.esm.js
vue.runtime.esm.js?2b0e:5103 =======runtime file calling initMixin|stateMixin|eventsMixin|lifecycleMixin|renderMixin==
vue.runtime.esm.js?2b0e:4968 =>Vue.prototype._init
vue.runtime.esm.js?2b0e:3935 =>Vue.prototype._update
vue.runtime.esm.js?2b0e:5109 =======done with calling mixins=
vue.runtime.esm.js?2b0e:5094 Vue constructor  {render: ƒ}
vue.runtime.esm.js?2b0e:4976 >>>prototype._init
vue.runtime.esm.js?2b0e:4977 options {render: ƒ}
vue.runtime.esm.js?2b0e:4979 ---------------
main.js?56d7:29 ^^^^^^^root render called, args [ƒ]
vue.runtime.esm.js?2b0e:3937 >>>Vue.prototype._update
vue.runtime.esm.js?2b0e:4976 >>>prototype._init
vue.runtime.esm.js?2b0e:4977 options {_isComponent: true, _parentVnode: VNode, parent: Vue}
vue.runtime.esm.js?2b0e:4979 ---------------
vue.runtime.esm.js?2b0e:3937 >>>Vue.prototype._update
vue.runtime.esm.js?2b0e:4976 >>>prototype._init
vue.runtime.esm.js?2b0e:4977 options {_isComponent: true, _parentVnode: VNode, parent: VueComponent}
vue.runtime.esm.js?2b0e:4979 ---------------
vue.runtime.esm.js?2b0e:3937 >>>Vue.prototype._update
```
-----
# tiny-vue

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
