---
title: Export
swizzle: true
---

`<ExportButton>` is an Ant Design [`<Button>`][button] with a default export icon and a "Export" text. It only has presentational value.

> For more information, refer to the [`useExport` documentation &#8594][useexport]

:::info-tip Swizzle

You can swizzle this component to customize it with the [**refine CLI**](/docs/packages/list-of-packages)

:::

## Usage

You can use it like any other Ant Design [`<Button>`][button].

For example, you can use it with [useExport][useexport]:

```tsx live
// visible-block-start
import { useExport } from "@refinedev/core";
import {
  List,
  useTable,
  // highlight-next-line
  ExportButton,
} from "@refinedev/antd";
import { Table } from "antd";

const PostList: React.FC = () => {
  const { tableProps } = useTable<IPost>();

  const { triggerExport, isLoading: exportLoading } = useExport<IPost>();

  return (
    <List
      headerButtons={
        // highlight-start
        <ExportButton onClick={triggerExport} loading={exportLoading} />
        // highlight-end
      }
    >
      <Table {...tableProps} rowKey="id">
        <Table.Column dataIndex="id" title="ID" />
        <Table.Column dataIndex="title" title="Title" />
      </Table>
    </List>
  );
};

interface IPost {
  id: number;
  title: string;
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

## Properties

### `hideText`

`hideText` is used to hide the text of the button. When its `true`, only the button icon will be visible.

```tsx live disableScroll previewHeight=120px
const { useRouterContext } = RefineCore;

// visible-block-start
import { ExportButton } from "@refinedev/antd";

const MyExportComponent = () => {
  return (
    <ExportButton
      // highlight-next-line
      hideText={true}
    />
  );
};

// visible-block-end

render(
  <RefineAntdDemo
    initialRoutes={["/"]}
    resources={[
      {
        name: "posts",
        list: MyExportComponent,
      },
    ]}
  />,
);
```

## API Reference

### Properties

<PropsTable module="@refinedev/antd/ExportButton" />

:::tip External Props

It also accepts all props of Ant Design [Button](https://ant.design/components/button/#API).

:::

[button]: https://ant.design/components/button/
[useexport]: /docs/core/hooks/utilities/use-export
