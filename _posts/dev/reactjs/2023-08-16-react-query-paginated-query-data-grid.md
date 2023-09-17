---
title: "[ReactJS] Paginated Queries with MUI Data Grid"
date: 2023-08-16
categories: [Dev, ReactJS]
tags: [ReactJS]
---

## Introduction

In this article, we will discover how we can implement _server-side pagination_ using MUI's data grid and paginated queries in react-query.

## Difference between client-side and server-side pagination

Client-side pagination is where we fetch all the data at once and handle the pagination on frontend. Server-side pagination is making requests to the server to fetch subsets of data that match the query parameters of the request such as page size and page index.

## When to use server-side pagination?

We usually use server-side pagination when the data to be fetched is large. It improves the overall performance since we fetch subsets of data.

## How to implement server-side pagination?

- Create a state variable for the page index and page size.

```jsx
const [paginationModel, setPaginationModel] = useState({
  page: 1,
  pageSize: 10,
});
```

> **Note**: MUI page starts from 0. To prevent error, change the page index either on frontend or backend.

- Create paginated query with `keepPreviousData`.

```jsx
const { isLoading, error, data, refetch } = useQuery(
  ["table", paginationModel.page],
  () => {
    return getTableData(paginationModel.page, paginationModel.pageSize);
  },
  {
    keepPreviousData: true,
  }
);
```

> **Note**: `keepPreviousData` enables data from the last successful fetch to be available while new data is being requested, even though the query key has changed.

- Create the data grid.

```jsx
<DataGrid
  rows={data}
  columns={columns}
  rowCount={data?.Length}
  paginationMode="server"
  paginationModel={paginationModel}
  pageSize={paginationModel.pageSize}
  pageSizeOptions={[5, 10, 25, 50, 100]}
  onPaginationModelChange={setPaginationModel}
/>
```

> **Note**: rowCount represents the total number of rows of data that is going to be fetched.

- Full Code

```jsx
import { DataGrid } from "@mui/x-data-grid";
import React, { useState } from "react";
import { useQuery } from "@tanstack/react-query";

export const Table = () => {
  const [paginationModel, setPaginationModel] = useState({
    page: 1,
    pageSize: 10, // You can change the page size
  });

  const { isLoading, error, data, refetch } = useQuery(
    ["table", paginationModel.page],
    () => {
      return getTableData(paginationModel.page, paginationModel.pageSize); // Replace it with your api request
    },
    {
      keepPreviousData: true,
    }
  );

  return (
    <DataGrid
      rows={data}
      columns={columns}
      rowCount={data?.Length}
      paginationMode="server"
      paginationModel={paginationModel}
      pageSize={paginationModel.pageSize}
      pageSizeOptions={[5, 10, 25, 50, 100]}
      onPaginationModelChange={setPaginationModel}
    />
  );
};
```

## Conclusion

I hope that this article helped you how to use paginated query and data grid together. For more information on using the paginated queries and data grid, you can check the official documentation:)
