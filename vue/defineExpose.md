# defineExpose()

Vue 3 provides a method for exposing properties and methods from within a component.

## Problem

Using `defineExpose` with TypeScript will result in `any` reference.

## Solution

```ts
const myDialog = ref<InstanceType<typeof MyDialog>>()
```

## Result

You will now get full autocomplete with functions and parameters.


## Example

#### MyDialog.vue

```ts
export interface Options {
  title: string
  desc: string
  label: string
  actionLabel: string
  closeLabel: string
  showDialog: boolean
  changeHandler: (count: number) => void
}

const open = async (opts: Options) => { ... }

defineExpose({
  open,
})
```

#### App.vue

```ts

const myDialog = ref<InstanceType<typeof MyDialog>>()

// Will provide all the typings for TypeScript
myDialog.open({
  title: 'Create a new channel',
  desc: 'Channels are where your members communicate',
  label: 'Channel name',
  actionLabel: 'Create',
  closeLabel: 'Cancel',
  showDialog: false,
  changeHandler: () => { }
})
```