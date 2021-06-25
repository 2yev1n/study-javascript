# async 와 await

### async

`async` 와 `await`은 이 `promise`를 좀 더 간편하고 깔끔하게 사용할  수 있게 도와주는 문법이다. 또한 매우 간단하여 쉽게 익힐 수 있다. 

> async fucntion foo() {
> 	return 'async';
> }
>
> const bar = foo();
> bar.then(console.log);		// async
> console.log(bar);				 // Promise 객체

함수 선언 키워드 `function` 앞에 `async`를 붙혀 사용한다. 이렇게 `async`를 사용하면 자동으로 `foo`안의 작업들을 `Promise`로 변환 시켜준다. `bar`를 콘솔에 찍어보면 `Promise`객체가 나오는 것을 볼 수 있다. 즉 `async`는 간편하게 `Promise`를 만들어주는 문법이라고 할 수 있다.

### await

`await`은 비동기 처리를 하는 코드 앞에 작성을 한다. `await`또한 예시를 통해 살펴보자.

>function delay(ms) {
>	return new Promise(resolve => setTimeout(resolve, ms));
>}
>
>async function getWhale() {
>	await delay(1000);
>	return 'whale';
>}
>
>async function getDolphin() {
>	await delay(1000);
>	return 'dolphin';
>}

`delay`는 ms 만큼의 시간이 지나면 `resolve`를 호출하는 `Promise` 를 리턴한다. 그리고 `getWhale`이나 `getDolphin`에서는 `await`을 통해 `delay`에 1초의 시간을 줌으로써 1초를 기다린 후 각각 고래와 돌고래를 리턴하는 `Promise`를 만든다. `Promise`로 리턴이 되는 것은 앞서 설명한 것과 같이 `async`를 사용했기 때문에 그렇다.
`getWhale`을 `async`와 `await`을 사용하지 않고 `Promise`를 통해 작성하면 아래와 같다.

> function get Whale() {
> 	return delay(1000).then)(() => "whale");
> }

다음으로는 고래와 돌고래를 얻어오는 함수인 `getAnimals`를 `async`와 `await`을 통해 만들어보자.

> async function getWhale() {
> 	const whale = await getWhale();
> 	const dolphin = await getDolphin();
> 	return ` whale dolphin`;
> }
>
> getAnimals().then(console.log);	// whale dolphin

비동기 처리를 하는 `getWhale`과 `getDolphin` 앞에 `await`을 통해 각각 1초 씩 기다리고, 고래와 돌고래를 리턴하는 `Promise`를 생성한다. 그리고 `then`을 통해 콘솔에 찍어보면 2초 뒤에 고래와 돌고래가 나타난다. 

