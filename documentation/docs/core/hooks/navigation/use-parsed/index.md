---
title: useParsed
sidebar_label: useParsed
---

`useParsed` is a hook that leverages the `parse` method of the [`routerProvider`][routerprovider] to access the URL and query parameters along with the inferred `resource`, `action` and `id` from the URL.

## Basic Usage

```tsx
import { useParsed } from "@refinedev/core";

const MyComponent = () => {
  const {
    resource,
    action,
    id,
    pathname,
    params: {
      filters,
      sorters,
      current,
      pageSize,
      ...restParams // Any other parameters are also parsed and available in `params`
    },
  } = useParsed();

  /* ... */
};
```

## Return Values

### `resource`

This is the active resource that is matched by the current route and the action definitions in the `resources` array of the `Refine` component. It will be `undefined` if there is no match.

### `action`

This is the active action that is matched by the current route and the action definitions in the `resources` array of the `Refine` component. It will be `undefined` if there is no match.

### `id`

This is the main parameter used by the **refine** in API interactions. It will also be available in the `params` object but it is also available as a separate value for convenience. It will be `undefined` if there is no `id` parameter in the URL.

### `pathname`

This is the current pathname of the URL.

### `params.filters`

This is the filters that are parsed from the URL. It will be `undefined` if there is no `filters` parameter in the URL. This property is used in the `syncWithLocation` feature of the `useTable`.

### `params.sorters`

This is the sorters that are parsed from the URL. It will be `undefined` if there is no `sorters` parameter in the URL. This property is used in the `syncWithLocation` feature of the `useTable`.

### `params.current`

This is the current page that is parsed from the URL. It will be `undefined` if there is no `current` parameter in the URL. This property is used in the `syncWithLocation` feature of the `useTable`.

### `params.pageSize`

This is the page size that is parsed from the URL. It will be `undefined` if there is no `pageSize` parameter in the URL. This property is used in the `syncWithLocation` feature of the `useTable`.

### `params`

This is the object that contains all the parameters that are parsed from the URL. It will be an empty object if there is no parameter in the URL. `params` object contains both the URL parameters and the query parameters.

[routerprovider]: /docs/core/providers/router-provider

## Type Parameters

| Property | Description           | Default               |
| -------- | --------------------- | --------------------- |
| TParams  | Query parameters type | `Record<string, any>` |
