# Glossaire {#glossary}

:::warning Traduction en cours
Notre équipe de traduction travaille sur la traduction du glossaire, vous pouvez rencontrer du contenu non traduit.
:::

Ce glossaire est destiné à fournir la signification des termes techniques couramment utilisés lorsque l'on parle de Vue. Il est destiné à être *descriptif* sur la façon dont les termes sont couramment utilisés, et non une spécification *prescriptive* de la façon dont ils doivent être utilisés. Certains termes peuvent avoir des significations ou des nuances légèrement différentes selon le contexte environnant.

[[TOC]]

## composant asynchrone {#async-component}

Un *composant asynchrone* est une enveloppe autour d'un autre composant qui permet au composant enveloppé d'être chargé de manière paresseuse. Il est généralement utilisé pour réduire la taille des fichiers .js construits, en leur permettant d'être divisés en morceaux plus petits qui ne sont chargés qu'en cas de besoin.

Vue Router dispose d'une fonctionnalité similaire pour le [chargement paresseux du composant route](https://router.vuejs.org/guide/advanced/lazy-loading.html), bien que cela n'utilise pas la fonctionnalité de composants asynchrones de Vue.

Pour plus de détails, voir :
- [Guide - Composants asynchrones](/guide/components/async.html)

## macro de compilateur {#compiler-macro}

Une *macro de compilateur* est un code spécial qui est traité par un compilateur et converti en quelque chose d'autre. Ils sont en fait une forme astucieuse de remplacement de chaînes de caractères.

Le compilateur [SFC](#single-file-component) de Vue prend en charge diverses macros, telles que `defineProps()`, `defineEmits()` et `defineExpose()`. Ces macros sont intentionnellement conçues pour ressembler à des fonctions JavaScript normales afin qu'elles puissent tirer parti du même analyseur et des mêmes outils d'inférence de type autour de JavaScript / TypeScript. Cependant, elles ne sont pas des fonctions réelles exécutées dans le navigateur. Ce sont des chaînes de caractères spéciales que le compilateur détecte et remplace par le vrai code JavaScript qui sera réellement exécuté.

Les macros ont des limites d'utilisation qui ne s'appliquent pas au code JavaScript normal. Par exemple, vous pourriez penser que `const dp = defineProps` vous permettrait de créer un alias pour `defineProps`, mais cela entraînera en fait une erreur. Il existe également des limitations sur les valeurs pouvant être transmises à `defineProps()`, car les 'arguments' doivent être traités par le compilateur et non au moment de l'exécution.

Pour plus de détails, voir :
- [`<script setup>` - `defineProps()` & `defineEmits()`](/api/sfc-script-setup.html#defineprops-defineemits)
- [`<script setup>` - `defineExpose()`](/api/sfc-script-setup.html#defineexpose)

## composant {#component}

Le terme *composant* n'est pas propre à Vue. Il est commun à de nombreux frameworks d'interface utilisateur. Il décrit une partie de l'interface utilisateur, comme un bouton ou une case à cocher. Les composants peuvent également être combinés pour former des composants plus grands.

Les composants sont le principal mécanisme fourni par Vue pour diviser une interface utilisateur en plus petits éléments, à la fois pour améliorer la maintenabilité et pour permettre la réutilisation du code.

Un composant Vue est un objet. Toutes les propriétés sont facultatives, mais un template ou une fonction de rendu est requis pour que le composant soit rendu. Par exemple, l'objet suivant serait un composant valide :

```js
const HelloWorldComponent = {
  render() {
    return 'Hello world!'
  }
}
```

En pratique, la plupart des applications Vue sont écrites en utilisant des [composants monofichiers](#single-file-component) (fichiers `.vue`). Bien que ces composants puissent ne pas sembler être des objets à première vue, le compilateur SFC les convertira en un objet, qui sera utilisé comme exportation par défaut pour le fichier. D'un point de vue externe, un fichier `.vue` n'est qu'un module ES qui exporte un objet composant.

Les propriétés d'un objet composant sont généralement appelées *options*. C'est là que l'[Options API](#options-api) tire son nom.

Les options d'un composant définissent comment les instances de ce composant doivent être créées. Les composants sont conceptuellement similaires aux classes, bien que Vue n'utilise pas de classes JavaScript réelles pour les définir.

Le terme composant peut également être utilisé plus librement pour désigner des instances de composant.

Pour plus de détails, voir :
- [Guide - Principes fondamentaux des composants](/guide/essentials/component-basics.html)

Le mot « composant » apparaît également dans plusieurs autres termes :
- [composant async](#async-component)
- [composant dynamique](#dynamic-component)
- [component fonctionnel](#functional-component)
- [Web Component](#web-component)

## composable {#composable}

Le terme *composable* décrit un modèle d'utilisation courant dans Vue. Il ne s'agit pas d'une fonctionnalité distincte de Vue, mais simplement d'un moyen d'utiliser la [Composition API](#composition-api) du framework.

* Un composable est une fonction.
* Les composables sont utilisés pour encapsuler et réutiliser la logique avec état.
* Le nom de la fonction commence généralement par `use`, afin que les autres développeurs sachent qu'il s'agit d'une fonction composable.
* La fonction est typiquement censée être appelée pendant l'exécution synchrone de la fonction `setup()` d'un composant (ou, de manière équivalente, pendant l'exécution d'un bloc `<script setup>`). Cela lie l'invocation du composable au contexte actuel du composant, par exemple via des appels à `provide()`, `inject()` ou `onMounted()`.
* Les composables renvoient généralement un objet simple, et non un objet réactif. Cet objet contient généralement des références et des fonctions et est censé être déstructuré dans le code appelant.

Comme pour de nombreux modèles, il peut y avoir des désaccords sur la question de savoir si un code spécifique peut prétendre au label. Toutes les fonctions utilitaires JavaScript ne sont pas composables. Si une fonction n'utilise pas la Composition API, elle n'est probablement pas composable. Si elle ne s'attend pas à être appelée pendant l'exécution synchrone de `setup()` alors elle n'est probablement pas composable. Les composables sont spécifiquement utilisés pour encapsuler la logique avec état, ils ne sont pas simplement une convention d'appellation pour les fonctions.

Voir le [Guide - Composables](/guide/reusability/composables.html) pour plus de détails sur l'écriture des composables.

## Composition API {#composition-api}

La *Composition API* est une collection de fonctions utilisées pour écrire des composants et des composables dans Vue.

Le terme est également utilisé pour décrire l'un des deux styles principaux utilisés pour écrire des composants, l'autre étant l'[Options API](#options-api). Les composants écrits à l'aide de la Composition API utilisent soit `<script setup>`, soit une fonction explicite `setup()`.

Voir la [FAQ de la Composition API](/guide/extras/composition-api-faq) pour plus de détails.

## élément personnalisé {#custom-element}

Un *élément personnalisé* est une fonctionnalité de la norme des [Web Components](#web-component), qui est mise en œuvre dans les navigateurs web modernes. Il s'agit de la possibilité d'utiliser un élément HTML personnalisé dans votre balisage HTML pour inclure un Web Component à cet endroit de la page.

Vue prend en charge nativement le rendu des éléments personnalisés et permet de les utiliser directement dans les templates de composants Vue.

Les éléments personnalisés ne doivent pas être confondus avec la possibilité d'inclure des composants Vue en tant que balises dans le template d'un autre composant Vue. Les éléments personnalisés sont utilisés pour créer des Web Components, et non des composants Vue.

Pour plus de détails, voir :
- [Vue et les Web Components](/guide/extras/web-components.html)

## directive {#directive}

Le terme *directive* fait référence aux attributs de template commençant par le préfixe `v-`, ou à leurs abréviations équivalentes.

Les directives intégrées comprennent `v-if`, `v-for`, `v-bind`, `v-on` et `v-slot`.

Vue permet également de créer des directives personnalisées, bien qu'elles ne soient généralement utilisées comme une 'trappe d'accès' pour manipuler directement les nœuds du DOM. Les directives personnalisées ne peuvent généralement pas être utilisées pour recréer la fonctionnalité des directives intégrées.

Pour plus de détails, voir :
- [Guide - Syntaxe de template - Directives](/guide/essentials/template-syntax.html#directives)
- [Guide - Directives personnalisées](/guide/reusability/custom-directives.html)

## composant dynamique {#dynamic-component}

Le terme *composant dynamique* est utilisé pour décrire les cas où le choix du composant enfant à rendre doit être fait dynamiquement. Typiquement, ceci est réalisé en utilisant `<component :is="type">`.

Un composant dynamique n'est pas un type particulier de composant. N'importe quel composant peut être utilisé comme composant dynamique. C'est le choix du composant qui est dynamique, plutôt que le composant lui-même.

Pour plus de détails, voir :
- [Guide - Principes fondamentaux des composants - Composants dynamiques](/guide/essentials/component-basics.html#dynamic-components)

## effect {#effect}

Voir [reactive effect](#reactive-effect) et [side effect](#side-effect).

## event {#event}

L'utilisation des événements pour communiquer entre différentes parties d'un programme est commune à de nombreux domaines de programmation différents. Dans Vue, le terme est généralement appliqué à la fois aux événements d'éléments HTML natifs et aux événements de composants Vue. La directive `v-on` est utilisée dans les templates pour écouter les deux types d'événements.

Pour plus de détails, voir :
- [Guide - Gestion d'événement](/guide/essentials/event-handling.html)
- [Guide - Gestion des évènements](/guide/components/events.html)

## fragment {#fragment}

The term *fragment* refers to a special type of [VNode](#vnode) that is used as a parent for other VNodes, but which doesn't render any elements itself.

The name comes from the similar concept of a [`DocumentFragment`](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment) in the native DOM API.

Fragments are used to support components with multiple root nodes. While such components might appear to have multiple roots, behind the scenes they use a fragment node as a single root, as a parent of the 'root' nodes.

Fragments are also used by the template compiler as a way to wrap multiple dynamic nodes, e.g. those created via `v-for` or `v-if`. This allows for extra hints to be passed to the [VDOM](#virtual-dom) patching algorithm. Much of this is handled internally, but one place you may encounter this directly is using a `key` on a `<template>` tag with `v-for`. In that scenario, the `key` is added as a [prop](#prop) to the fragment VNode.

Fragment nodes are currently rendered to the DOM as empty text nodes, though that is an implementation detail. You may encounter those text nodes if you use `$el` or attempt to walk the DOM with built-in browser APIs.

## functional component {#functional-component}

A component definition is usually an object containing options. It may not appear that way if you're using `<script setup>`, but the component exported from the `.vue` file will still be an object.

A *functional component* is an alternative form of component that is declared using a function instead. That function acts as the [render function](#render-function) for the component.

A functional component cannot have any state of its own. It also doesn't go through the usual component lifecycle, so lifecycle hooks can't be used. This makes them slightly lighter than normal, stateful components.

Pour plus de détails, voir :
- [Guide - Render Functions & JSX - Functional Components](/guide/extras/render-function.html#functional-components)

## hoisting {#hoisting}

The term *hoisting* is used to describe running a section of code before it is reached, ahead of other code. The execution is 'pulled up' to an earlier point.

JavaScript uses hoisting for some constructs, such as `var`, `import` and function declarations.

In a Vue context, the template compiler applies *static hoisting* to improve performance. When converting a template to a render function, VNodes that correspond to static content can be created once and then reused. These static VNodes are described as hoisted because they are created outside the render function, before it runs. A similar form of hoisting is applied to static objects or arrays that are generated by the template compiler.

Pour plus de détails, voir :
- [Guide - Rendering Mechanism - Static Hoisting](/guide/extras/rendering-mechanism.html#static-hoisting)

## in-DOM template {#in-dom-template}

There are various ways to specify a template for a component. In most cases the template is provided as a string.

The term *in-DOM template* refers to the scenario where the template is provided in the form of DOM nodes, instead of a string. Vue then converts the DOM nodes into a template string using `innerHTML`.

Typically, an in-DOM template starts off as HTML markup written directly in the HTML of the page. The browser then parses this into DOM nodes, which Vue then uses to read off the `innerHTML`.

Pour plus de détails, voir :
- [Guide - Creating an Application - In-DOM Root Component Template](/guide/essentials/application.html#in-dom-root-component-template)
- [Guide - Component Basics - DOM Template Parsing Caveats](/guide/essentials/component-basics.html#dom-template-parsing-caveats)
- [Options: Rendering - template](/api/options-rendering.html#template)

## inject {#inject}

See [provide / inject](#provide-inject).

## lifecycle hooks {#lifecycle-hooks}

A Vue component instance goes through a lifecycle. For example, it is created, mounted, updated, and unmounted.

The *lifecycle hooks* are a way to listen for these lifecycle events.

With the Options API, each hook is provided as a separate option, e.g. `mounted`. The Composition API uses functions instead, such as `onMounted()`.

Pour plus de détails, voir :
- [Guide - Lifecycle Hooks](/guide/essentials/lifecycle.html)

## macro {#macro}

Voir [macro de compilateur](#compiler-macro).

## named slot {#named-slot}

A component can have multiple slots, differentiated by name. Slots other than the default slot are referred to as *named slots*.

Pour plus de détails, voir :
- [Guide - Slots - Named Slots](/guide/components/slots.html#named-slots)

## Options API {#options-api}

Vue components are defined using objects. The properties of these component objects are known as *options*.

Components can be written in two styles. One style uses the [Composition API](#composition-api) in conjunction with `setup` (either via a `setup()` option or `<script setup>`). The other style makes very little direct use of the Composition API, instead using various component options to achieve a similar result. The component options that are used in this way are referred to as the *Options API*.

The Options API includes options such as `data()`, `computed`, `methods` and `created()`.

Some options, such as `props`, `emits` and `inheritAttrs`, can be used when authoring components with either API. As they are component options, they could be considered part of the Options API. However, as these options are also used in conjunction with `setup()`, it is usually more useful to think of them as shared between the two component styles.

The `setup()` function itself is a component option, so it *could* be described as part of the Options API. However, this is not how the term 'Options API' is normally used. Instead, the `setup()` function is considered to be part of Composition API.

## plugin {#plugin}

While the term *plugin* can be used in a wide variety of contexts, Vue has a specific concept of a plugin as a way to add functionality to an application.

Plugins are added to an application by calling `app.use(plugin)`. The plugin itself is either a function or an object with an `install` function. That function will be passed the application instance and can then do whatever it needs to do.

Pour plus de détails, voir :
- [Guide - Plugins](/guide/reusability/plugins.html)

## prop {#prop}

There are three common uses of the term *prop* in Vue:

* Component props
* VNode props
* Slot props

*Component props* are what most people think of as props. These are explicitly defined by a component using either `defineProps()` or the `props` option.

The term *VNode props* refers to the properties of the object passed as the second argument to `h()`. These can include component props, but they can also include component events, DOM events, DOM attributes and DOM properties. You'd usually only encounter VNode props if you're working with render functions to manipulate VNodes directly.

*Slot props* are the properties passed to a scoped slot.

In all cases, props are properties that are passed in from elsewhere.

While the word props is derived from the word *properties*, the term props has a much more specific meaning in the context of Vue. You should avoid using it as an abbreviation of properties.

Pour plus de détails, voir :
- [Guide - Props](/guide/components/props.html)
- [Guide - Render Functions & JSX](/guide/extras/render-function.html)
- [Guide - Slots - Scoped Slots](/guide/components/slots.html#scoped-slots)

## provide / inject {#provide-inject}

`provide` and `inject` are a form of inter-component communication.

When a component *provides* a value, all descendants of that component can then choose to grab that value, using `inject`. Unlike with props, the providing component doesn't know precisely which component is receiving the value.

`provide` and `inject` are sometimes used to avoid *prop drilling*. They can also be used as an implicit way for a component to communicate with its slot contents.

`provide` can also be used at the application level, making a value available to all components within that application.

Pour plus de détails, voir :
- [Guide - provide / inject](/guide/components/provide-inject.html)

## reactive effect {#reactive-effect}

A *reactive effect* is part of Vue's reactivity system. It refers to the process of tracking the dependencies of a function and re-running that function when the values of those dependencies change.

`watchEffect()` is the most direct way to create an effect. Various other parts of Vue use effects internally. e.g. component rendering updates, `computed()` and `watch()`.

Vue can only track reactive dependencies within a reactive effect. If a property's value is read outside a reactive effect it'll 'lose' reactivity, in the sense that Vue won't know what to do if that property subsequently changes.

The term is derived from 'side effect'. Calling the effect function is a side effect of the property value being changed.

Pour plus de détails, voir :
- [Guide - Reactivity in Depth](/guide/extras/reactivity-in-depth.html)

## reactivity {#reactivity}

In general, *reactivity* refers to the ability to automatically perform actions in response to data changes. For example, updating the DOM or making a network request when a data value changes.

In a Vue context, reactivity is used to describe a collection of features. Those features combine to form a *reactivity system*, which is exposed via the [Reactivity API](#reactivity-api).

There are various different ways that a reactivity system could be implemented. For example, it could be done by static analysis of code to determine its dependencies. However, Vue doesn't employ that form of reactivity system.

Instead, Vue's reactivity system tracks property access at runtime. It does this using both Proxy wrappers and getter/setter functions for properties.

Pour plus de détails, voir :
- [Guide - Reactivity Fundamentals](/guide/essentials/reactivity-fundamentals.html)
- [Guide - Reactivity in Depth](/guide/extras/reactivity-in-depth.html)

## API de réactivité {#reactivity-api}

L'*API de réactivité* est une collection de fonctions de base de Vue liées à la [réactivité](#reactivity). Ils peuvent être utilisés indépendamment des composants. Elle comprend des fonctions telles que `ref()`, `reactive()`, `computed()`, `watch()` et `watchEffect()`.

L'API de réactivité est un sous-ensemble de la Composition API.

Pour plus de détails, voir :
- [API de la réactivité : Essentiel](/api/reactivity-core.html)
- [API de la réactivité : Utilitaires](/api/reactivity-utilities.html)
- [API de la réactivité : Avancé](/api/reactivity-advanced.html)

## ref {#ref}

> This entry is about the use of `ref` for reactivity. For the `ref` attribute used in templates, see [template ref](#template-ref) instead.

A `ref` is part of Vue's reactivity system. It is an object with a single reactive property, called `value`.

There are various different types of ref. For example, refs can be created using `ref()`, `shallowRef()`, `computed()`, and `customRef()`. The function `isRef()` can be used to check whether an object is a ref, and `isReadonly()` can be used to check whether the ref allows the direct reassignment of its value.

Pour plus de détails, voir :
- [Guide - Reactivity Fundamentals](/guide/essentials/reactivity-fundamentals.html)
- [Reactivity API: Core](/api/reactivity-core.html)
- [Reactivity API: Utilities](/api/reactivity-utilities.html)
- [Reactivity API: Advanced](/api/reactivity-advanced.html)

## fonction de rendu {#render-function}

Une *fonction de rendu* est la partie d'un composant qui génère les VNodes utilisés lors du rendu. Les templates sont compilés en fonctions de rendu.

Pour plus de détails, voir :
- [Guide - Fonctions de rendu et JSX](/guide/extras/render-function.html)

## scheduler {#scheduler}

The *scheduler* is the part of Vue's internals that controls the timing of when [reactive effects](#reactive-effect) are run.

When reactive state changes, Vue doesn't immediately trigger rendering updates. Instead, it batches them together using a queue. This ensures that a component only re-renders once, even if multiple changes are made to the underlying data.

[Watchers](/guide/essentials/watchers.html) are also batched using the scheduler queue. Watchers with `flush: 'pre'` (the default) will run before component rendering, whereas those with `flush: 'post'` will run after component rendering.

Jobs in the scheduler are also used to perform various other internal tasks, such as triggering some [lifecycle hooks](#lifecycle-hooks) and updating [template refs](#template-ref).

## scoped slot {#scoped-slot}

The term *scoped slot* is used to refer to a [slot](#slot) that receives [props](#prop).

Historically, Vue made a much greater distinction between scoped and non-scoped slots. To some extent they could be regarded as two separate features, unified behind a common template syntax.

In Vue 3, the slot APIs were simplified to make all slots behave like scoped slots. However, the use cases for scoped and non-scoped slots often differ, so the term still proves useful as a way to refer to slots with props.

The props passed to a slot can only be used within a specific region of the parent template, responsible for defining the slot's contents. This region of the template behaves as a variable scope for the props, hence the name 'scoped slot'.

Pour plus de détails, voir :
- [Guide - Slots - Scoped Slots](/guide/components/slots.html#scoped-slots)

## SFC {#sfc}

See [Single-File Component](#single-file-component).

## side effect {#side-effect}

The term *side effect* is not specific to Vue. It is used to describe operations or functions that do something beyond their local scope.

For example, in the context of setting a property like `user.name = null`, it is expected that this will change the value of `user.name`. If it also does something else, like triggering Vue's reactivity system, then this would be described as a side effect. This is the origin of the term [reactive effect](#reactive-effect) within Vue.

When a function is described as having side effects, it means that the function performs some sort of action that is observable outside the function, aside from just returning a value. This might mean that it updates a value in state, or triggers a network request.

The term is often used when describing rendering or computed properties. It is considered best practice for rendering to have no side effects. Likewise, the getter function for a computed property should have no side effects.

## Single-File Component {#single-file-component}

The term *Single-File Component*, or SFC, refers to the `.vue` file format that is commonly used for Vue components.

See also:
- [Guide - Single-File Components](/guide/scaling-up/sfc.html)
- [SFC Syntax Specification](/api/sfc-spec.html)

## slot {#slot}

Les slots sont utilisés pour transmettre du contenu aux composants enfants. Alors que les props sont utilisés pour transmettre des données, les slots sont utilisés pour transmettre un contenu plus riche composé d'éléments HTML et d'autres composants Vue.

Pour plus de détails, voir :
- [Guide - Slots](/guide/components/slots.html)

## template ref {#template-ref}

The term *template ref* refers to using a `ref` attribute on a tag within a template. After the component renders, this attribute is used to populate a corresponding property with either the HTML element or the component instance that corresponds to the tag in the template.

If you are using the Options API then the refs are exposed via properties of the `$refs` object.

With the Composition API, template refs populate a reactive [ref](#ref) with the same name.

Template refs should not be confused with the reactive refs found in Vue's reactivity system.

Pour plus de détails, voir :
- [Guide - Template Refs](/guide/essentials/template-refs.html)

## VDOM {#vdom}

See [virtual DOM](#virtual-dom).

## virtual DOM {#virtual-dom}

The term *virtual DOM* (VDOM) is not unique to Vue. It is a common approach used by several web frameworks for managing updates to the UI.

Browsers use a tree of nodes to represent the current state of the page. That tree, and the JavaScript APIs used to interact with it, are referred to as the *document object model*, or *DOM*.

Manipulating the DOM is a major performance bottleneck. The virtual DOM provides one strategy for managing that.

Rather than creating DOM nodes directly, Vue components generate a description of what DOM nodes they would like. These descriptors are plain JavaScript objects, known as VNodes (virtual DOM nodes). Creating VNodes is relatively cheap.

Every time a component re-renders, the new tree of VNodes is compared to the previous tree of VNodes and any differences are then applied to the real DOM. If nothing has changed then the DOM doesn't need to be touched.

Vue uses a hybrid approach that we call [Compiler-Informed Virtual DOM](/guide/extras/rendering-mechanism.html#compiler-informed-virtual-dom). Vue's template compiler is able to apply performance optimizations based on static analysis of the template. Rather than performing a full comparison of a component's old and new VNode trees at runtime, Vue can use information extracted by the compiler to reduce the comparison to just the parts of the tree that can actually change.

Pour plus de détails, voir :
- [Guide - Rendering Mechanism](/guide/extras/rendering-mechanism.html)
- [Guide - Render Functions & JSX](/guide/extras/render-function.html)

## VNode {#vnode}

Un *VNode* est un *nœud virtuel du DOM*. Ils peuvent être créés à l'aide de la fonction [`h()`](/api/render-function.html#h).

Voir [virtual DOM](#virtual-dom) pour plus d'informations.

## Web Component {#web-component}

The *Web Components* standard is a collection of features implemented in modern web browsers.

Vue components are not Web Components, but `defineCustomElement()` can be used to create a [custom element](#custom-element) from a Vue component. Vue also supports the use of custom elements inside Vue components.

Pour plus de détails, voir :
- [Guide - Vue and Web Components](/guide/extras/web-components.html)
