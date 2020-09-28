# News Explorer

To get started, do the following: 

`npm install && npm start`

This should install all the needed packages and start a local server.

## Angular CLI

Please use the [Angular CLI](https://cli.angular.io/). Two reasons for that:

* it reduces your development time and effort
* it establishes conventions

## Dependencies, APIs and helpers

* Angular 7 with the Angular CLI.
* @angular-redux
* Font-awesome and Primeng.

## Architecture

### No backend

At the moment there is no backend to store user's data, no need to worry about that. We focus on the frontend.

### Redux Store

We store the application state in a redux store. To change the state, you must dispatch actions. Those actions will then be digested by reducers to generate a new state.

### Redux Effects

There are asynchronous side effects performed in this application:

* when we fetch news to render them
* when we load the feed

Usually, we want to display a loading indicator when those requests are sent and we want to change the application state when we receive the response. It usually looks like:

```js
dispatch(loadingStateAction(…))
sendRequest().then(res => dispatch(setResponseAction(res)))
```

We decided to use the `redux-observable` epics to perform all of this. The idea is that the component now only dispatches one action. This action is then digested by a function called an "epic", which in turns sends the request and returns an observable of another redux action, which changes the state.

One advantage of doing so is to decouple the application business logic from the components. Testing and debugging is therefore easier and the code in components is much simpler.


## Challenge for Interfacewerk - try to keep it under 8h

### Create a component to display an article

* Create an Angular component that takes an article object as input
  * use the Angular CLI to create this component ;)
* Use this new component in the `feed-articles.component.html`
* Display whatever data you can get (image, title, author, date, etc.)
* Give the possibility for the user to display more of the article in a modal (Use https://www.primefaces.org/primeng/v7.2.6-lts/#/dialog)
  * optional/very nice if you have it: use Redux to display this modal => add a property to the state and actions to open/close

