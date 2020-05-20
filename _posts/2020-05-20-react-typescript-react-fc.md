---
layout: post
title: Should you use React.FC for typing React Components
tags:
  - react
  - typescript
---

Typescript provides some interfaces to help with writing React components.
`React.FC` is one of those interfaces that is used in a lot of apps to define a functional component.
The question you should ask yourself is: should you use `React.FC` for Typescript react components?

## React.FC

This example shows how you can use `React.FC` in practice:

```tsx
import React from 'react'
import { T } from '@example/i18n'

const Header: React.FC = () => {
  return <header>{T`Harry's header`}</header>
}
```

and without `React.FC`:

```tsx
import React from 'react'
import { T } from '@example/i18n'

const Header = () => {
  return <header>{T`Harry's header`}</header>
}
```

- wondering [what the `T` is about](javascript:alert('coming soon'))?

With React component props, use:

```tsx
const Header: React.FC<{ loading: boolean }> = ({ loading }) => {
  if (loading) {
    return <header>{T`Loading...`}</header>
  }

  return <header>{T`Harry's header`}</header>
}
```

without


```tsx
const Header = ({ loading }: { loading: boolean }) => {
  if (loading) {
    return <header>{T`Loading...`}</header>
  }

  return <header>{T`Harry's header`}</header>
}
```

## Pros of React.FC

### 1. Helps with Component props

React components have by default 4 props, e.g. `Header.displayName`.

```tsx
// Simple version of the actual interface
interface FC<P = {}> {
  (props: P): ReactNode
  propTypes?: P
  defaultProps?: P
  contextTypes?: any
  displayName?: string
}
```

With `React.FC` interface I get typings for these props, otherwise we get this type error:

```
Property 'displayName' does not exist on
type '() => Element'.ts(2339)
```

### 2. Gives access to typed children

```tsx
const Header: React.FC<{ loading: boolean }> = ({ loading, children }) => {
  if (loading) {
    return <header>{T`Loading...`}</header>
  }

  return <header>{children}</header>
}
```

without


```tsx
// Type error: Property 'children' does not exist on type '{ loading: boolean; }'. ts(2339)
const Header = ({ loading, children } : { loading: boolean }) => {
  if (loading) {
    return undefined
  }

  return <header>{children}</header>
}
```

to fix this, we need to specify the `children` prop manually

```tsx
const Header = ({ loading, children } : { loading: boolean; children: React.ReactNode }) => {
  if (loading) {
    return undefined
  }

  return <header>{children}</header>
}
```

## Cons of React.FC

### 1. Doesn't help with returning undefined

You cannot return `undefined` from a React component, and even with the `React.FC` type, the compiler will only tell you at runtime.

```
Runtime error:
Header(...): Nothing was returned from render.
This usually means a return statement is missing.
Or, to render nothing, return null.
```

### 2. Provides access to `props.children` when you may not want it

With `React.FC` I can put children under my component and they won't render but will be typed correctly.

```tsx
const Header: React.FC = () => {
  return <header>{T`Harry's header`}</header>
}

export const Example = () => {
  return (
    <Header>
      <p>{T`Children`}</p>
    </Header>
  )
}
```

Without this type I get a error instantly

```tsx
const Header = () => {
  return <header>{T`Harry's header`}</header>
}

export const Example = () => {
  // Type error: Property 'children' does not exist on
  // type 'IntrinsicAttributes & { loading: any; }'. ts(2322)
  return (
    <Header>
      <p>{T`Children`}</p>
    </Header>
  )
}
```


### 3. Difficulty creating a Sub.Component pattern

It is very difficult to create the typical Component and Component.SubComponent pattern (without adding lots of additional workarounds) with `React.FC`.

e.g. without `React.FC`, to create this:

```tsx
<Header>
  <Header.Item name={T`Login`} />
</Header>
```

the types are simply

```tsx
const Header = ({ children }) => <header>{children}</header>
Header.Item = ({ name }) => <p>{name}</p>
```


## Overall

`React.FC` is useful for beginners getting into typed React components as it guides you with types.
But due to unnecessary addition of children, that you normally do not need, you should stay away and simply type like a normal Typescript function.


### More reading

- [create-react-app issue to remove React.FC](https://github.com/facebook/create-react-app/pull/8177)
- [React Typescript Cheat Sheet](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/function_components)

