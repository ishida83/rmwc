# Chips

> Chips represent complex entities in small blocks, such as a contact.

- Module **@rmwc/chip**
- Import styles:
  - import **'@material/chips/dist/mdc.chips.css'**
- MDC Docs: [https://material.io/develop/web/components/chips/](https://material.io/develop/web/components/chips/)

```jsx
<ChipSet>
  <Chip selected label="Cookies" />
  <Chip label="Pizza" />
  <Chip label="Icecream" />
</ChipSet>
```

```jsx
<ChipSet>
  <Chip icon="favorite" label="Cookies" trailingIcon="close" />
</ChipSet>
```

```jsx
function Example() {
  const [selected, setSelected] = React.useState(false);
  return (
    <ChipSet>
      <Chip
        key="my-chip"
        label="Click Me"
        checkmark
        selected={selected}
        onRemove={evt => console.log('onRemove', evt.detail)}
        onInteraction={evt => {
          console.log('onInteraction', evt.detail);
          setSelected(!selected);
        }}
        onTrailingIconInteraction={evt =>
          console.log('onTrailingIconIteraction', evt.detail)
        }
        trailingIcon="close"
      />
    </ChipSet>
  );
}
```

## Filter and Choice Chipsets

You can specify a `ChipSet` as either a `filter` of `choice` which slightly changes the visual styling of selected chips. While `material-components-web` has some built in functionality for chip sets, it doesn't fit well with React's unidirectional data flow. It is recommended you use standard React patterns to store selected chips in your state and render them accordingly.

Clicking on the trailing close icon will trigger a close animation and put the chip in an exited state, but it is up to you to remove component out from rendering. The you use the `onRemove` prop implement this behavior.

```jsx
function Example() {
  const [selected, setSelected] = React.useState({
    cookies: false,
    pizza: false,
    icecream: false
  });
  const toggleSelected = key =>
    setSelected({
      ...selected,
      [key]: !selected[key]
    });

  return (
    <ChipSet filter>
      <Chip
        selected={selected.cookies}
        checkmark
        onClick={() => toggleSelected('cookies')}
        label="Cookies"
        trailingIcon="close"
      />
      <Chip
        selected={selected.pizza}
        checkmark
        onClick={() => toggleSelected('pizza')}
        icon="local_pizza"
        label="Pizza"
        trailingIcon="close"
      />
      <Chip
        selected={selected.icecream}
        checkmark
        onClick={() => toggleSelected('icecream')}
        icon="favorite_border"
        trailingIcon="close"
        label="Icecream"
      />
    </ChipSet>
  );
}
```

```jsx
function Example() {
  const [selected, setSelected] = React.useState({
    cookies: false,
    pizza: false,
    icecream: false
  });
  const toggleSelected = key =>
    setSelected({
      ...selected,
      [key]: !selected[key]
    });

  return (
    <ChipSet choice>
      <Chip
        selected={selected.cookies}
        onClick={() => toggleSelected('cookies')}
        label="Cookies"
        trailingIcon="close"
      />
      <Chip
        selected={selected.pizza}
        onClick={() => toggleSelected('pizza')}
        icon="local_pizza"
        label="Pizza"
        trailingIcon="close"
      />
      <Chip
        selected={selected.icecream}
        onClick={() => toggleSelected('icecream')}
        icon="favorite_border"
        trailingIcon="close"
        label="Icecream"
      />
    </ChipSet>
  );
}
```

## Chip
A Chip component.

### Props

| Name | Type | Description |
|------|------|-------------|
| `checkmark` | `undefined \| false \| true` | Includes an optional checkmark for the chips selected state. |
| `children` | `React.ReactNode` | Additional children will be rendered in the text area. |
| `icon` | `RMWC.IconPropT` | Instance of an Icon Component. |
| `id` | `undefined \| string` | An optional chip ID that will be included in callback evt.detail. If this is not passed, RMWC will attempt to use the "key" prop if present. |
| `label` | `React.ReactNode` | Text for your Chip. |
| `onInteraction` | `undefined \| (evt: ChipOnInteractionEventT) => void` | A callback for click or enter key. This should be used over onClick for accessibility reasons. evt.detail = { chipId: string } |
| `onRemove` | `undefined \| (evt: ChipOnRemoveEventT) => void` | A callback that is fired once the chip is in an exited state from removing it. evt.detail = { chipId: string } |
| `onTrailingIconInteraction` | `undefined \| (evt: ChipOnTrailingIconInteractionEventT) => void` | A callback for click or enter key for the trailing icon. material-components-web always treats this as an intent to remove the chip. evt.detail = { chipId: string } |
| `selected` | `undefined \| false \| true` | makes the Chip appear selected. |
| `trailingIcon` | `RMWC.IconPropT` | Instance of an Icon Component. |


## ChipSet
A container for multiple chips.

### Props

| Name | Type | Description |
|------|------|-------------|
| `choice` | `undefined \| false \| true` | Creates a choice chipset |
| `filter` | `undefined \| false \| true` | Creates a filter chipset |


