# 15 Questions about JS, CSS, React, and STYLiSH

## 1. How to handle array data type?

* Index
* Iterable
* ES6 Spread / Rest Operator
* Array.prototype.methods

### Example

```js
const names = ['Weil One','Weil Two','Weil Three'];
const namesCopy = [...names];
const [ name, ...otherNames ] = names;
const nameshiftFromNamesCopy = namesCopy.shift();

const nameIsFirstOne = name === names[0]; // true
const otherNamesAreLastTwo = [...otherNames].join('') === [names[1],names[2]].join(''); // true
const twoNamesArrayHasEqualLength = names.length === namesCopy.length; // false
```

### Caution
1. Rest Operator can only be the **last** variable when destructuring
2. Whether the handled array will be **mutated** by Array.prototype.methods

## 2. How to handle object data type?

### Key ( with dot or brackets )
```js
const user = {
    id: 0,
    name: 'Weil',
    job: {
        title: 'software engineer',
        field: 'front-end',
        experience: '0 year'
    }
};
const userRef = user;

user.id = 1;
userRef['name'] = 'Weil Liao';

const userRefHasSameId = user['id'] === userRef['id']; // true
const userRefHasSameName = user.name === userRef.name; // true

const jobDescription = {
    requirement: {
        need: ['title', 'field', 'experience']
    }
}
const jobSeeking = jobDescription.requirement.need[0];

const canCallTitle = user.job[`${jobSeeking}`] === 'software engineer'; // true
const isErrorCalling = user.requirement.need[0] !== 'software engineer'; // Cannot read properties of undefined
```
### Object - ES6 Spread / Rest Operator
```js
const customer = {
    name: 'Weil',
    order: {
        drink: 'black tea',
        meal: 'double beef burger'
    }
};
const customerCopy = { ...customer };

const order = {
    drink: 'milk tea',
    meal: 'double beef cheese burger',
    sideDish: 'salad',
    dressing: 'thousand island'
};

const customerCopyUpdate = { ...customerCopy, order };

const { name } = customer;
const { drink, meal, ...salad } = customerCopyUpdate.order;

customer.name = 'Weil Liao';

const nameBecomeIndependentVar = name !== customer.name; // true
const orderHasUpdated = customer.order !== customerCopyUpdate.order; // true
const saladHasTwoItem = salad.sideDish + salad.dressing === order.sideDish + order.dressing; // true
```

### Object.methods ( more common than Object.prototype.methods )
`Object.keys() / Object.values() / Object.entries()`
Turn keys, values or both of an object to array list

`Object.fromEntries()`
Turn array (or other iterable object) into object

`Object.assign()`
A way to clone an object but not deep clone

`Object.create()`
A way to create class

## 3. How to manage RESTful API calls?

### Send HTTP Requests: axios and fetch()
1. [Axios vs. fetch(): Which is best for making HTTP requests?](https://blog.logrocket.com/axios-vs-fetch-best-http-requests/)
2. [request的方式？ ajax & fetch & axios](https://ithelp.ithome.com.tw/articles/10244631)
3. [Cancel all axios requests in React’s componentWillUnmount Lifecycle.](https://julietonyekaoha.medium.com/react-cancel-all-axios-request-in-componentwillunmount-e5b2c978c071)
#### Personal Perspective
1. fetch() is easy to start with in F2E development ( latest version of Node.js is supported now )
2. fetch() is less supported than axios in old browsers( need to polyfilled )
3. fetch() is always resolved when server can response to the request, which makes us identify stauts code ourselves
4. axios itself has system like AbortController API to cancel request

### Manage URL
1. Set a config file
2. Split hostname and endpoint
3. Make string of version flexibly change
4. Set different request function to different endpoint
