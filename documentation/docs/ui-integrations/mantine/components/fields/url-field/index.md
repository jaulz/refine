---
title: Url
swizzle: true
---

```tsx live shared
const { default: routerProvider } = LegacyRefineReactRouterV6;
const { default: simpleRest } = RefineSimpleRest;
setRefineProps({
  legacyRouterProvider: routerProvider,
  dataProvider: simpleRest("https://api.fake-rest.refine.dev"),
  notificationProvider: RefineMantine.notificationProvider,
  Layout: RefineMantine.Layout,
  Sider: () => null,
});

const Wrapper = ({ children }) => {
  return (
    <MantineCore.MantineProvider theme={RefineMantine.LightTheme} withNormalizeCSS withGlobalStyles>
      <MantineCore.Global styles={{ body: { WebkitFontSmoothing: "auto" } }} />
      <MantineNotifications.NotificationsProvider position="top-right">
        {children}
      </MantineNotifications.NotificationsProvider>
    </MantineCore.MantineProvider>
  );
};
```

This field lets you embed a link. It uses Mantine [`<Anchor>`](https://mantine.dev/core/anchor) component. You can pass a URL in its `value` prop and you can show a text in its place by passing any `children`.

:::info-tip Swizzle

You can swizzle this component to customize it with the [**refine CLI**](/docs/packages/list-of-packages)

:::

## Usage

Let's see how we can use `<UrlField>` with an example:

```tsx live url=http://localhost:3000 previewHeight=420px hideCode
setInitialRoutes(["/posts"]);
import { Refine } from "@refinedev/core";

// visible-block-start
import { List, UrlField } from "@refinedev/mantine";
import { Table, Pagination } from "@mantine/core";
import { useTable } from "@refinedev/react-table";
import { ColumnDef, flexRender } from "@tanstack/react-table";

const PostList: React.FC = () => {
  const columns = React.useMemo<ColumnDef<IPost>[]>(
    () => [
      {
        id: "id",
        header: "ID",
        accessorKey: "id",
      },
      {
        id: "title",
        header: "Title",
        accessorKey: "title",
      },
      {
        id: "image",
        header: "Image",
        accessorKey: "image",
        cell: function render({ getValue }) {
          return (
            // highlight-next-line
            <UrlField value={getValue()[0].url} />
          );
        },
      },
    ],
    [],
  );

  const {
    getHeaderGroups,
    getRowModel,
    refineCore: { setCurrent, pageCount, current },
  } = useTable({
    columns,
  });

  return (
    <List>
      <Table>
        <thead>
          {getHeaderGroups().map((headerGroup) => (
            <tr key={headerGroup.id}>
              {headerGroup.headers.map((header) => (
                <th key={header.id}>
                  {header.isPlaceholder ? null : flexRender(header.column.columnDef.header, header.getContext())}
                </th>
              ))}
            </tr>
          ))}
        </thead>
        <tbody>
          {getRowModel().rows.map((row) => (
            <tr key={row.id}>
              {row.getVisibleCells().map((cell) => (
                <td key={cell.id}>{flexRender(cell.column.columnDef.cell, cell.getContext())}</td>
              ))}
            </tr>
          ))}
        </tbody>
      </Table>
      <br />
      <Pagination position="right" total={pageCount} page={current} onChange={setCurrent} />
    </List>
  );
};

interface IPost {
  id: number;
  title: string;
  image: [{ url: string }];
}
// visible-block-end

const App = () => {
  return <Refine resources={[{ name: "posts", list: PostList }]} />;
};

render(
  <Wrapper>
    <App />
  </Wrapper>,
);
```

## API Reference

### Properties

<PropsTable module="@refinedev/mantine/UrlField" value-description="URL for link to reference to"/>

:::tip External Props

It also accepts all props of Mantine [Anchor](https://mantine.dev/core/anchor?t=props).

:::
