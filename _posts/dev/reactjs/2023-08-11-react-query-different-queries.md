---
title: "[ReactJS] Queries in React Query"
date: 2023-08-11
categories: [Dev, ReactJS]
tags: [ReactJS]
---

## Introduction

In this article, we are going to take a look at queries that you can use in react query.

## Custom Query Hooks

Using react query, you can create your own custom query hooks and use it in different files. Remember that you cannot use hooks in conditional statements though. Custom query hoooks are useful for reducing redundant code and making your code more concise. All you have to do is add an **id variable** to the query key array.

```jsx
const fetchDataById ({ queryKey }) => {
  const dataId = queryKey[1]
  return axios.get(`http://localhost:8080/api/data/${dataId}`)
}

export const useDataById = (dataId) => {
  return useQuery(['data', dataId], fetchDataById)
}
```

## Parallel Queries

Parallel queries are used when a component needs to call multiple apis to fetch data. It is simple as calling two useQueries. When you want to use the values offered be useQuery, you have to use aliases to reconstruct the values.

```jsx
const fetchFriends () => {
  return axios.get(`http://localhost:8080/api/friends`)
}

const fetchFamily () => {
  return axios.get(`http://localhost:8080/api/family`)
}

export const ParallelQueries = () => {
  const {data: Friends} = useQuery(['friends'], fetchFriends)
  const {data: Family} = useQuery(['family'], fetchFamily)
  return <div>parallelQueries<div>
}
```

## Dynamic Parallel Queries

Dynamic parallel queries are used when you need to fetch multiple related or independent data sets concurrently. We use `useQueries` instead of `useQuery` when we want to perform dynamic parallel queries. The returned object from using `useQueries` will be an array of the fetched data.

```jsx
const fetchFriends = (friendId) => {
  return axios.get(`http://localhost:8080/api/friends/${friendId}`)
}

export const dynamicParallelQueries = (friendsIdList) => {
  const result = useQueries(
    friendsIdList.map(id => {
      return {
        queryKey: ['friends', id],
        queryFn: () => fetchFriends(id),
      }
    })
  )
return <div>dynamic parallel queries</div>
```

## Dependent Queries

Dependent queries are used when you want queries to run after the other. One thing to remind is that for the queries that come after the first query, their queries will depend on the data fetched from the first query. Hence, we have use the `enabled` options to not fetch data until we have fetched the data from the first query. Double negation turns a "truthy" or "falsy" value into a Boolean value, `true` or `false`.

```jsx
const fetchUserByEmail = (email) => {
  return axios.get(`http://localhost:8080/api/user/${email}`
}

const fetchCourseById = (id) => {
  return axios.get(`http://localhost:8080/api/course/${id}`
}

export dependentQueries = (email) => {
  const {data: user} = useQuery(['user', email], () => fetchUserByEmail(email))

  const id = user?.id // check if user is fetched or not

  const {data: course} = useQuery(['course', id], () => fetchCourseById(id), { enabled: !!id})

  return <div>dependent queries</div>
```

## Initial Query Data

Initial query data is useful when you want to use data already present in the query cache from the previous query to render partial data to the user. We use `useQueryClient` to use data already present in the cache using the query key.

```jsx
export const userCourseData = (courseId) => {
  const queryClient = useQueryClient();
  return useQuery(["course", courseId], fetchCourse, {
    initialData: () => {
      const course = queryClient
        .getQueryData("course")
        ?.data?.find((course) => course.id === parseInt(courseId));

      if (course) {
        return { data: course };
      } else {
        return undefined;
      }
    },
  });
};
```

## Paginated Queries

Paginated queries are used to fetch data based on pages. One powerful option that you can use with paginated queries is `keepPreviousData`. This option allows to keep the previous data when navigating to the next page.

```jsx
function Todos() {
  const [page, setPage] = React.useState(0);

  const fetchProjects = (page = 0) =>
    fetch("/api/projects?page=" + page).then((res) => res.json());

  const { isLoading, isError, error, data, isFetching, isPreviousData } =
    useQuery({
      queryKey: ["projects", page],
      queryFn: () => fetchProjects(page),
      keepPreviousData: true,
    });

  return (
    <div>
      {isLoading ? (
        <div>Loading...</div>
      ) : isError ? (
        <div>Error: {error.message}</div>
      ) : (
        <div>
          {data.projects.map((project) => (
            <p key={project.id}>{project.name}</p>
          ))}
        </div>
      )}
      <span>Current Page: {page + 1}</span>
      <button
        onClick={() => setPage((old) => Math.max(old - 1, 0))}
        disabled={page === 0}
      >
        Previous Page
      </button>{" "}
      <button
        onClick={() => {
          if (!isPreviousData && data.hasMore) {
            setPage((old) => old + 1);
          }
        }}
        // Disable the Next Page button until we know a next page is available
        disabled={isPreviousData || !data?.hasMore}
      >
        Next Page
      </button>
      {isFetching ? <span> Loading...</span> : null}{" "}
    </div>
  );
}
```

## Infinite Queries

Infinite queries are used when you want to load more data. `useInfiniteQuery` is used for infinite queries.

```jsx
import { useInfiniteQuery } from "@tanstack/react-query";

function Projects() {
  const fetchProjects = async ({ pageParam = 0 }) => {
    const res = await fetch("/api/projects?cursor=" + pageParam);
    return res.json();
  };

  const {
    data,
    error,
    fetchNextPage,
    hasNextPage,
    isFetching,
    isFetchingNextPage,
    status,
  } = useInfiniteQuery({
    queryKey: ["projects"],
    queryFn: fetchProjects,
    getNextPageParam: (lastPage, pages) => lastPage.nextCursor,
  });

  return status === "loading" ? (
    <p>Loading...</p>
  ) : status === "error" ? (
    <p>Error: {error.message}</p>
  ) : (
    <>
      {data.pages.map((group, i) => (
        <React.Fragment key={i}>
          {group.data.map((project) => (
            <p key={project.id}>{project.name}</p>
          ))}
        </React.Fragment>
      ))}
      <div>
        <button
          onClick={() => fetchNextPage()}
          disabled={!hasNextPage || isFetchingNextPage}
        >
          {isFetchingNextPage
            ? "Loading more..."
            : hasNextPage
            ? "Load More"
            : "Nothing more to load"}
        </button>
      </div>
      <div>{isFetching && !isFetchingNextPage ? "Fetching..." : null}</div>
    </>
  );
}
```

## Conclusion

There are different kinds of queries that you can use in react query. Since we have a better understanding now of what kind of queries react query have, we can use the ones that are needed in our future projects!
