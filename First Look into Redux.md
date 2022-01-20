# First Look into Redux 2022

---



## What is Redux?

For me, Redux is basically about having one central data (Store) in your application.

Inside the Store, you would typically store User Authentication, Theming, or some other user input state,  whether it's gonna be some  Cross-Component or App-Wide state it will go into this one Store.

## How does Redux work?

Our components will set up a Subscription to our central Store, which will subscribe to the Store ad whenever the data changes the store will notify the component, then that component will receive the data they need to update for example a current user authentication status. These states will get a slice of Redux Store.

It's important to note that components never directly edit the data in the Store. For this to happen a concept called Reducer Function will be in charge of mutating (changes) Store Data.

The Reducer Function is a general concept and not to be mistaken for the UseReducer hook in React. The Reducer Function will take input as a parameter and then transform that input and reduce it, for example, reduce a list and sum them. This function will receive input and spits out a new value (output)

The component will then trigger an action. Actions are JavaScript object which describes some operation that the Reducer should perform and Redux will pass those actions to the Reducer Function.



# How to use Redux

- First import Redux into your application

```js
const redux = require('redux')
```

- Create a Store

```js
redux.createStore()
```

- Above the Store create a Reducer Function

The Reducer Function will receive two-parameter the old state and the Dispatched Action. It will return a certain output that will be a new state object, therefore the reducer will be a pure function which means that the same values for the input also there should be no side effects example HTTP requests, or writing to the local storage by fetching some data from it. Instead, a Reducer Function should be a function that receives an input ad produces a given output (new state object). 

It should receive a state and action by default and will be executed by the Redux library and returns a new state.

```js
const counterReducer = (state, action)=>{
    return {
    counter: state.counter + 1
}
}
```

- To let Redux be aware of your newly created Reducer function you should pass it to the already created store like so:
  
  ```js
  const store = redux.createStore(counterReducer )
  ```

- Then go ahead and create a Subscription
  
  The Subscription will be triggered when the state changes. When it's triggered we can get the latest state after it was by using the getState method.
  
  ```js
  const counterSubscription = () => {
      store.getState()
  }
  ```

- The getState() method is a method that is available on the created store, it will give us the latest state after it was updated.

- Also, we should make redux aware of our Subscription function. By calling the subscription on the store by pointing to it like so:
  
  ```js
  store.subscribe(counterSubscription)
  ```

- In our previous Reducer Function, we will check the different action types to be dispatched.
  
  ```js
  const initialState = {counter: 0}
  const counterReducer = (state=initialState , action)=>{
      if(action.type==="increment"){
          return {
              couter: state.couter+1
          }
      }
      if(action.type==="decrement"){
          return {
              counter: state.counter-1
          }
      }
  }
  ```

- Lastly, we will create and dispatch actions by using the dispatch() method, which is a JavaScriptobjectt that accepts a type prop that acts as a unique item identifier which is often a unique string.

```js
store.dispatch({type: 'increment'})
store.dispatch({type: 'decrement'})

```


