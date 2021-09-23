---
title: Actions Refresh Table
description: This article provides details about the Actions Refresh Table service in the Components Library.
template: concept-topic-template
---

This article provides details about the Actions Refresh Table service in the Components Library.

## Overview

Actions Refresh Table is an Angular Service that refreshes data of the Table in the current context.
Check out this example below to see how to use Actions Refresh Table service.

`type` - is an action type.  
`tableId` - is an `id` of the table that is refreshed.  

```html
<spy-button-action
  [action]="{
    type: 'refresh-table',
    tableId: 'table-id',
  }"
>
  ...
</spy-button-action>
```

## Interfaces

Below you can find interfaces for the Actions Refresh Table.

```ts
export interface RefreshTableActionConfig extends ActionConfig {
  tableId?: string;
}

// Service registration
@NgModule({
  imports: [
    ActionsModule.withActions({
      'refresh-table': RefreshTableActionHandlerService,
    }),
  ],
})
export class RootModule {}
```
