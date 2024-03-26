# getServerSideProps

- SSR(Server Side Render)를 하기 위한 next.js문법

  

## 사용법

```react
type Todo = {
  title: string;
  completed: boolean;
};

const queryFn = async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/todos');
  const data = await res.json();
  return data as Todo[];
};

export default function Home() {
  const { data } = useQuery(['todos'], queryFn, { staleTime: 10 * 1000 });

  return (
    <div>
      {data?.map(({ title, completed }) => (
        <p key={title}>
          <strong>{title}</strong>
          {completed && <span>완료</span>}
        </p>
      ))}
    </div>
  );
}

export const getServerSideProps: GetServerSideProps = async () => {
  const queryClient = new QueryClient();
  await queryClient.prefetchQuery(['todos'], queryFn);
  return {
    props: {
      dehydratedProps: dehydrate(queryClient),
      hi: 'hello',
    },
  };
};
```

