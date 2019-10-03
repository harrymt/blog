---
layout: post
title: TypeScript 3.7 Features
tags: [javascript, typescript]
---

Microsoft recently annouced the beta for [Typescript 3.7](https://devblogs.microsoft.com/typescript/announcing-typescript-3-7-beta/). This has several useful features coming into the next version of TypeScript soon. My favourite is Optional Chaining.

### Optional Chaining

Have you ever had to parse a huge object with several optional fields.

Instead of wrapping the access to these variables in lots of if statements of guarding operators, we can simply use the optional property accessor operator `?.`.

```js
// Old
if (config && config.auth && config.auth.user) {
  return config.auth.user.userId
}
return undefined
```

```js
// New
return config?.auth?.user?.userId
```

We can also access functions and indexes of arrays in the same way.

```js
// Old
if (state && state.deals && state.deals.length > 0) {
  return deals[0]
}
return undefined
```

```js
// New
return state?.deals?.[0]
```

```js
// Old
if (fetch) {
  return fetch(`/api/user/${id}`)
}
```

```js
// New
return fetch?.(`/api/user/${id}`)
```
