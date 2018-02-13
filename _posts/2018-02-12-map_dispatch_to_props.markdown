---
layout: post
title:      "map dispatch to props"
date:       2018-02-12 11:31:37 -0500
permalink:  map_dispatch_to_props
---


In my react app, each time a guess is submitted, i.e. the guess button is clicked, it triggers the following code block: 

```
handleOnSubmit = event => {
 	event.preventDefault()

 	this.props.createGuess(this.props.guessesFormData)
 	this.setState({showResult: true})
 	// this.props.resetGuessFormData()
 }
```
(all of the following is in reference to [GuessesForm.js](https://github.com/d-d-d-dalia/acClimate/blob/master/make_america_great_client/src/containers/GuessesForm.js) )


How does the createGuess action get added to the props of the guessesForm component?

In short, it happens via mapDispatchToProps.

We are able to use mapDispatchToProps, which does exactly what it's name says, by adding a second argument to our connect function (in addition to mapStateToProps). This *connects* the coponent, in this case, guessesForm.js, to the store.

```
export default connect(mapStateToProps, mapDispatchToProps)(Guesses)
```

Now, this.props.createGuess points to the action creator createGuess. 

This enables us to execute the action by referencing it as a prop, e.g. on line 36 of Guesses.js.

But is it enough to be able to call the action creator by referencing it as props?

An action creator is just a plain javascript object. What we want is actually to dispatch the returned action (from the action creator), to the store.

This is where bindActionCreators comes in.

The first step is to add dispatch as an argument to the mapDispatchToProps function. We then add bindActionCreators and pass it our new props - in this case createGuess - as the thing we want to dispatch.

```
const mapDispatchToProps = (dispatch) => {
    return bindActionCreators({ updateGuessesFormData, createGuess }, dispatch)
}
```

The result is createGuess pointing to the dispatch function (rather than just the action creator), passing the value of the action creator as its argument, thus automatically invoking the action when we reference it as props in the component.

This strategy allows us to remove all reference to our store from our component.
