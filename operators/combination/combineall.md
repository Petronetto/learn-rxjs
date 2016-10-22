# combineAll
####signature: `combineAll(project: function): Observable`

## When source observable completes use [combineLatest](combinelatest.md) with collected observables.

### Examples

( [example tests](https://github.com/btroncone/learn-rxjs/blob/master/operators/specs/combination/combineall-spec.ts) )

##### Example 1: Mapping to inner interval observable

( [jsBin](http://jsbin.com/nebapesile/edit?js,console) | [jsFiddle](https://jsfiddle.net/btroncone/pvj1nbLa/) )

```js
//emit every 1s, take 2
const source = Rx.Observable.interval(1000).take(2);
//map first value to 500ms interval and second to 1s, take two values
const example = source.map(val => Rx.Observable.interval(val + 500).take(2));
/*
  2 values from source will map to 2 (inner) interval observables that emit every .5s
  and 1s. combineAll uses combineLatest strategy, emitting the last value from each
  whenever either observable emits a value
*/
const combined = example.combineAll();
/*
  output:
  [0,0]
  [1,0]
  [1,1]
*/
const subscribe = combined.subscribe(val => console.log(val));
```


### Additional Resources
* [combineAll](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-combineAll) :newspaper: - Official docs

---
> :file_folder: Source Code:  [https://github.com/ReactiveX/rxjs/blob/master/src/operator/combineAll.ts](https://github.com/ReactiveX/rxjs/blob/master/src/operator/combineAll.ts)
