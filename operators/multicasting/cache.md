# cache
####signature: `cache(bufferSize: number, windowTime: number, scheduler : Scheduler): Observable`

## Share source and deliver the provided number of previously emitted values on subscription.


### Examples

##### Example 1: Cache last value from source

( [jsBin](http://jsbin.com/laxumuzuge/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/cb0dcnnx/) )

```js
//basic promise, resolve after 2 seconds
const myPromise = val => new Promise(resolve => setTimeout(() => resolve(`Result: ${val}`), 2000));
//emit after 1 second
const source = Rx.Observable.timer(1000);

const example = source
	//side effects triggered once
	.do(() => console.log('Triggering Side Effect!'))
	.mergeMap(myPromise)
//cache the last emission
const cached = example.cache(1);

/*
	both subscribers share the same source
  Triggering Side Effect!
	Result: 0
	Result: 0
*/
const subscriberOne = cached.subscribe(val => console.log(val));
const subscriberTwo = cached.subscribe(val => console.log(val));


setTimeout(() => {
	/*
  	late subscribers will receieve the last (1) emission
    output:
    Subscriber 3: Result: 0
  */
	const subscriberThree = cached.subscribe(val => console.log(`Subscriber 3: ${val}`));
}, 5000);
```


### Additional Resources
* [cache](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-cache) :newspaper: - Official docs

---
> :file_folder: Source Code:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/cache.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/cache.ts)
