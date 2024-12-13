# Context Menu

Here is a Tauri context menu example in React and TypeScript. I had a hard time finding an example that I could get to actually work. This one is simple and doesn't require any event listeners.

## Example Component

```typescript
import React from "react";
import { Menu, MenuItem } from "@tauri-apps/api/menu";

export function ContextMenuExample() {
  async function onContextMenuHandler(event: React.MouseEvent<HTMLDivElement>) {
    event.preventDefault();
    event.stopPropagation();
    const exampleMenuItem = await MenuItem.new({
      text: "It works!",
      action: () => {
        console.log("It works!");
      },
    });
    const menu = await Menu.new();
    await menu.append(exampleMenuItem);
    menu.popup();
  }

  return (
    <div onContextMenu={onContextMenuHandler}>
      <h1>Right click me</h1>
    </div>
  );
}
```

## Required Permissions

You will also need to add the following permissions to `/src-tauri/capabilities/default.json`:
* `core:menu:allow-append`
* `core:menu:allow-new`
