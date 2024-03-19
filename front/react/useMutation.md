# useMutation

- 기존 useQuery는 데이터를 조회할 때 사용을 하였지만 useMutation은 생성, 수정, 삭제를 담당한다 



## 사용법

```react
const test = useMutation(mutationFn(data), options);

...

<button onCLick={(data) => {test.mutate(data)}}>update</button>
```

- mutationFn : axios또는 http를 이용한 생성, 수정, 삭제 요청을 하는 함수를 넣게된다
- options 
  - onSuccess : 요청이 성공 했을시 함수
  - onError : 요청이 실패 했을 시 함수
  - onSettled : 성공 여부와 관계없이 실행되는 함수
- mutate : useMutation을 이용해 작성한 내용들이 실행되게 도와주는 trigger 역할 



### 예시

```react
const savePerson = useMutation((person: Iperson) => axios.post('http://localhost:8080/savePerson', person), {
    onSuccess: () => { // 요청이 성공한 경우
        console.log('onSuccess');
    },
    onError: (error) => { // 요청에 에러가 발생된 경우
        console.log('onError');
    },
    onSettled: () => { // 요청이 성공하든, 에러가 발생되든 실행하고 싶은 경우
        console.log('onSettled');
    }
});

const onSavePerson = () => {
	savePerson.mutate(person); // 데이터 저장
}

...

<button onClick={onSavePerson}>저장</button>
```





## invalidateQueries

- useQuery에서 사용되는 queryKey의 유효성을 제거해주는 목적 
  - queryKey의 유효성을 제거해주는 이유는 서버로부터 다시 데이터를 조회해오기 위함 
- cache 데이터
  - stale Time : fresh 한 데이터에서 stale 한 데이터로 바뀌는데 걸리는 시간
    - 기본값은 0이며 시간을 주면 그 시간동안 데이터가 바뀌어도 fresh한 데이터의 상태만을 보여주게된다 
    - 하지만 적당히 조절한다면 변화가 없는 상태에서 fetch을 하는것을 방지하고 cache된 데이터로 보여주기때문에 서버부담이 줄고  서버 통신 시간도 줄어들 수 있다
  - cache Time : fresh한 **데이터**를 저장해두는 시간 
    - 만약 stale 상태에서 렌더링된다면 refetch가 될것이며  cache 된 데이터를 보여주다 refetch가 끝나면 새로운 fresh 데이터를 보여주게 된다 
    - stale time이 더길다면 fresh상태에서 cache Time이 끝나고 메모리에서 데이터가 삭제될 것이다 그러면 stale상태가 되었을 때 refetch를 하게되면 fetch시간동안 보여주는 cashe데이터가 없는상태가 된다 
- stale Time에 도달하지 않으면 데이터가 변하더라도 새로운 화면을 보여주지 않는다 
- 그렇기 때문에 invalidateQueries를 이용해 useQuery가 가지고 있던 queryKey의 유효성을 제거해주어 캐싱되어있는 데이터를 화면에 보여주지 않고 새롭게 데이터를 요청 하게 된다 

### 사용법

```react
const queryClient = useQueryClient();  // 등록된 quieryClient 가져오기

const savePerson = useMutation((person: Iperson) => axios.post('http://localhost:8080/savePerson', person), {
    onSuccess: () => { // 요청이 성공한 경우
        console.log('onSuccess');
        queryClient.invalidateQueries('persons'); // queryKey 유효성 제거
    },
    onError: (error) => { // 요청에 에러가 발생된 경우
        console.log('onError');
    },
    onSettled: () => { // 요청이 성공하든, 에러가 발생되든 실행하고 싶은 경우
        console.log('onSettled');
    }
}); // useMutate 정의
```

- useQuery에서 persons라는 queryKey를 사용하고 있기 때문에 그것을 이용하여 유효성 제거 fresh 상태이던 stale 상태이던 새롭게 데이터를 받아와 화면에 적용 



## setQueryData

- invalidateQueries를 사용하지 않고도 데이터를 업데이트
- 기존에 queryKey에 매핑되어 있는 데이터를 새롭게 정의

### 사용예시

```react
const queryClient = useQueryClient();  // 등록된 quieryClient 가져오기

const savePerson = useMutation((person: Iperson) => axios.post('http://localhost:8080/savePerson', person), {
    onSuccess: () => { // 요청이 성공한 경우
        console.log('onSuccess');
        queryClient.setQueryData('persons', (data) => {
            const curPersons = data as AxiosResponse<any, any>; // persons의 현재 데이터 확인
            curPersons.data.push(person); // 데이터 push

            return curPersons; // 변경된 데이터로 set
        })
    },
    onError: (error) => { // 요청에 에러가 발생된 경우
        console.log('onError');
    },
    onSettled: () => { // 요청이 성공하든, 에러가 발생되든 실행하고 싶은 경우
        console.log('onSettled');
    }
}); // useMutate 정의
```

- 서버에 데이터를 보내고 refetch를 하여 받아오는 방식이 아닌 직접 변경되는 데이터를 useQuery의 queryKey에 매핑된 데이터에 넣는 방식
- 서버에 데이터를 요청하지 않고 변경된 값을 넣어준다 
- 서버상에 데이터의 변경또한 이루어진 상태이며 바뀐화면을 보내주지 않을 뿐이다(fresh 데이터인 경우)