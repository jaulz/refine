---
title: Number
swizzle: true
---

This field is used to display a number formatted according to the browser locale, right aligned. and uses [`Intl`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl) to display date format.

:::info-tip Swizzle

You can swizzle this component to customize it with the [**refine CLI**](/docs/packages/list-of-packages)

:::

## Usage

`<NumberField>` uses `Intl.NumberFormat()` if available, passing the locales and options props as arguments. This allows a perfect display of decimals, currencies, percentages, etc. See the [Intl.NumberFormat documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat) for the options prop syntax.

If Intl is not available, `<NumberField>` outputs numbers as is (and ignores the locales and options props).

```tsx live
// visible-block-start
import {
  List,
  // highlight-next-line
  NumberField,
  useTable,
} from "@refinedev/antd";
import { Table } from "antd";

const PostList: React.FC = () => {
  const { tableProps } = useTable<IPost>();

  return (
    <List>
      <Table {...tableProps} rowKey="id">
        <Table.Column dataIndex="id" title="ID" />
        <Table.Column dataIndex="title" title="Title" width="50%" />
        <Table.Column<IPost>
          key="hit"
          title="Hit"
          dataIndex="hit"
          render={(value) => (
            // highlight-start
            <NumberField
              value={value}
              options={{
                notation: "compact",
              }}
            />
            // highlight-end
          )}
          width="50%"
        />
      </Table>
    </List>
  );
};

interface IPost {
  id: number;
  title: string;
  hit: number;
}
// visible-block-end

render(
  <RefineAntdDemo
    resources={[
      {
        name: "posts",
        list: PostList,
      },
    ]}
  />,
);
```

## API Reference

### Properties

<PropsTable module="@refinedev/antd/NumberField" value-description="Number value" />

:::tip External Props

This field also accepts all props of Ant Design's [Text](https://ant.design/components/typography/#Typography.Text) component.

:::
