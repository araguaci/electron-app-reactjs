<p align="center">
  <img src="./images/creating-windows.svg" alt="" width="60%" />
</p>

<br />
<br />
<br />

<h1 align="center"><img src="./images/bullet.svg" width="20" /> Creating Windows</h1>

At `src/main/windows` create a folder named as `MyWindow` and inside this folder an `index.ts` with the following content:

```js
import { createWindow } from 'main/factories'

export function MyWindow() {
  const window = createWindow({
    id: 'myWindow',
    title: 'My Window',
    width: 450,
    height: 320,
    alwaysOnTop: true,
  })

  return window
}
```

Then, at `src/main/windows/index.ts`, add the `MyWindow`:

```js
export * from './MyWindow'
export * from './About'
export * from './Main'
```

Now, at `src/main/index.ts`, you can use it like:

```js
import { app } from 'electron'

import { makeAppSetup } from './factories'

import {
  registerAboutWindowCreationByIPC,
  MainWindow,
  MyWindow,
} from './windows'

app.whenReady().then(async () => {
  await makeAppSetup(MainWindow)
  registerAboutWindowCreationByIPC()
  MyWindow()
})
```

## <img src="./images/bullet.svg" width="14" /> Creating a Window by IPC

Check the [About](https://github.com/daltonmenezes/electron-app/tree/main/src/main/windows/About) window example and [its usage](https://github.com/daltonmenezes/electron-app/blob/main/src/main/index.ts#L8).
