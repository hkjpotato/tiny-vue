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

Draft topics
# Essentials

- MMVM model
- init process: 
 - new Vue() => _init() => $mount() => mountComponent() =>new Watcher() => updateComponent() => render() => _update() 
- Reactive data + dependency collection with Watcher and Dep (Vue2 vs Vue1)
- Async Patch, queue with nextTick, compared to React.
- Plugin pattern, and coupling.

# Component

# Compiler
- vue-loader and single file component
- runtime
# Algorithm
- Vue2 check both sides vs Vue3 LIS, compared to React key value map



# plugin pattern

## What is a plugin? 

```
const myPlugin = VueRouter;

myPlugin.nstall = () => {}

Vue.use = (plugin) => {
    const installedPlugins = Vue._installedPlugins;

    if (installedPlugins.indexOf(plugin) > -1) {
        return Vue;
    }

    plugin.install(Vue);
    installedPlugins.push(plugin);
}

```

## Timing

```
// use as plugin before instantiate
Vue.use(VueRouter);

// new the router instance
const router = new VueRouter();

// assign to the root Vue instance
new Vue({
    router,
});
```

Notice that, when you install a plugin, one goal is to "expose the router instance to the vue instance", so that in your vue instance you can call `$router` to access the instance.

However, when we install the plugin, neither the vue or the router instance is created. The key to deplay this process is by "contract", 
1. contract by running certain lifecyles.
2. contract by exposing api for customer to mutate them

```
// seriously why not just do this...
function Vue (options) {
    this.router = options.router;
}
// because Vue not necessary need to know about router

// contract by running certain lifecyles.
function Vue(options) {
    this.options = options;
    // I promosie I will run the beforeCreate method
    Vue.beforeCreates && Vue.beforeCreates.forEach(cb => cb.call(this));
}

// expose certain way to mutate them
Vue.mixin = function (beforeCreate) {
    this.beforeCreates = this.beforeCreates || [];
    this.beforeCreates.push(beforeCreate);
}

Vue.use = (plugin) => {
    plugin.install();
}

VueRouter.install = () => {
    Vue.mixin(function () {
        this.router = this.options.router;
    });
}
```

## Strong coupling between vue-router and Vue
As a plugin, you need to respect the environment. TBA

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
