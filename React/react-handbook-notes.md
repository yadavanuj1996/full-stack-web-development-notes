



Caching, localization, webpack. document and window, polyfills and transpiling, react routing, build react app for deployment 

1) ES6 Modules
	uses import syntax
	import {upperCase} from './uppercase.js'

	CommonJS Moudle used in NodeJS
	const test= require('./uppercase.js');

2) SPA (Single Page Application)
	Pages not rendered and requested from server each time.

3) History API for routing back button error.

4) React is Declarative
	Declarative
	What does it mean when you read that React is declarative
	You'll run across articles describing React as a declarative approach to building UIs.
	React made its "declarative approach" quite popular and upfront so it permeated the frontend
	world along with React.
	It's really not a new concept, but React took building UIs a lot more declaratively than with
	HTML templates:
	you can build Web interfaces without even touching the DOM directly
	you can have an event system without having to interact with the actual DOM Events.
	The opposite of declarative is iterative. A common example of an iterative approach is looking
	up elements in the DOM using jQuery or DOM events. You tell the browser exactly what to do,
	instead of telling it what you need.
	The React declarative approach abstracts that for us. We just tell React we want a component
	to be rendered in a specific way, and we never have to interact with the DOM to reference it
	later

5) Immutability
	What is immutability? And how does it fit in the React world?
	One concept you will likely meet when programming in React is immutability (and its opposite,
	mutability).
	It's a controversial topic, but whatever you might think about the concept of immutability, React
	and most of its ecosystem kind of forces this, so you need to at least have a grasp of why it's
	so important and the implications of it.
	In programming, a variable is immutable when its value cannot change after it's created.
	You are already using immutable variables without knowing it when you manipulate a string.
	Strings are immutable by default, when you change them in reality you create a new string and
	assign it to the same variable name.
	An immutable variable can never be changed. To update its value, you create a new variable.
	The same applies to objects and arrays.
	Instead of changing an array, to add a new item you create a new array by concatenating the
	old array, plus the new item.
	An object is never updated, but copied before changing it.
	This applies to React in many places.
	For example, you should never mutate the state property of a component directly, but only
	through the setState() method.
	In Redux, you never mutate the state directly, but only through reducers, which are functions.
	The question is, why?
	There are various reasons, the most important of which are:
	Mutations can be centralized, like in the case of Redux, which improves your debugging
	capabilities and reduces sources of errors.
	Code looks cleaner and simpler to understand. You never expect a function to change
	some value without you knowing, which gives you predictability. When a function does
	not mutate objects but just returns a new object, it's called a pure function.
	The library can optimize the code because for example JavaScript is faster when
	swapping an old object reference for an entirely new object, rather than mutating an
	existing object. This gives you performance.

6)    Purity
	What is purity, a pure function and a pure component
	In JavaScript, when a function does not mutate objects but just returns a new object, it's called
	a pure function.
	A function, or a method, in order to be called pure should not cause side effects and should
	return the same output when called multiple times with the same input.
	A pure function takes an input and returns an output without changing the input nor anything
	else.
	Its output is only determined by the arguments. You could call this function 1M times, and
	given the same set of arguments, the output will always be the same.
	React applies this concept to components. A React component is a pure component when its
	output is only dependant on its props.
	All functional components are pure components:
	const Button = props => {
		return <button>{props.message}</button>
	}
	
	Class components can be pure if their output only depends on the props:

	class Button extends React.Component {
		render() {
			return <button>{this.props.message}</button>
		}
	}

7)	Create specialized version of a component
	Use an outer component to expand and specialize a more generic component:
	const Button = props => {
	return <button>{props.text}</button>
	}
	const SubmitButton = () => {
	return <Button text="Submit" />
	}
	const LoginButton = () => {
	return <Button text="Login" />
	}
	Pass methods as props
	A component can focus on tracking a click event, for example, and what actually happens
	when the click event happens is up to the container component:
	const Button = props => {
	return <button onClick={props.onClickHandler}>{props.text}</button>
	}
	Composition
	58
	const LoginButton = props => {
	return <Button text="Login" onClickHandler={props.onClickHandler} />
	}
	const Container = () => {
	const onClickHandler = () => {
	alert('clicked')
	}
	return <LoginButton onClickHandler={onClickHandler} />
	}
	Using children
	The props.children property allows you to inject components inside other components.
	The component needs to output props.children in its JSX:
	const Sidebar = props => {
	return <aside>{props.children}</aside>
	}
	and you embed more components into it in a transparent way:
	<Sidebar>
	<Link title="First link" />
	<Link title="Second link" />
	</Sidebar>

8)  The Virtual DOM
	The Virtual DOM is a technique that React uses to optimize interacting with
	the browser
	Many existing frameworks, before React came on the scene, were directly manipulating the
	DOM on every change.
	First, what is the DOM?
	The DOM (Document Object Model) is a Tree representation of the page, starting from the
	<html> tag, going down into every child, which are called nodes.
	It's kept in the browser memory, and directly linked to what you see in a page. The DOM has
	an API that you can use to traverse it, access every single node, filter them, modify them.
	The API is the familiar syntax you have likely seen many times, if you were not using the
	abstract API provided by jQuery and friends:
	document.getElementById(id)
	document.getElementsByTagName(name)
	document.createElement(name)
	parentNode.appendChild(node)
	element.innerHTML
	element.style.left
	element.setAttribute()
	element.getAttribute()
	element.addEventListener()
	window.content
	window.onload
	window.dump()
	window.scrollTo()
	React keeps a copy of the DOM representation, for what concerns the React rendering: the
	Virtual DOM
	The Virtual DOM Explained
	Every time the DOM changes, the browser has to do two intensive operations: repaint (visual
	or content changes to an element that do not affect the layout and positioning relative to other
	elements) and reflow (recalculate the layout of a portion of the page - or the whole page
	layout).
	React uses a Virtual DOM to help the browser use less resources when changes need to be
	done on a page.
	The Virtual DOM
	60
	When you call setState() on a Component, specifying a state different than the previous one,
	React marks that Component as dirty. This is key: React only updates when a Component
	changes the state explicitly.
	What happens next is:
	React updates the Virtual DOM relative to the components marked as dirty (with some
	additional checks, like triggering shouldComponentUpdate() )
	Runs the diffing algorithm to reconcile the changes
	Updates the real DOM
	Why is the Virtual DOM helpful: batching
	The key thing is that React batches much of the changes and performs a unique update to the
	real DOM, by changing all the elements that need to be changed at the same time, so the
	repaint and reflow the browser must perform to render the changes are executed just once

9) React Uses unidirectional Data flow.



10) JSX looks html mixed with JS
	JSX is first transpiled to JS then is run in browser.

	class becomes className
	htmlFor
	onchange => onChange
	onclick => onClick
	onsubmit => onSubmit

	JSX resembles HTML a lot, but it's actually XML syntax.

	JSX style={{backgroundColor: 'black',color: 'red'}} takes  and object.

	Is this the go-to solution?
	Inline styles in JSX are good until you need to
	1. write media queries
	2. style animations
	3. reference pseudo classes (e.g. :hover )
	4. reference pseudo elements (e.g. ::first-letter )
	In short, they cover the basics, but it's not the final solution

11) The value attribute always holds the current value of the field.
	The defaultValue attribute holds the default value that was set when the field was created.
	This helps solve some weird behavior of regular DOM interaction when inspecting
	input.value and input.getAttribute('value') returning one the current value and one the
	original default value.

	This also applies to the textarea field, e.g.
	<textarea>Some text</textarea>
	but instead
	<textarea defaultValue={'Some text'} />

	For select fields, instead of using
	<select>
	JSX
	69
	<option value="x" selected>
	...
	</option>
	</select>
	
	use

	<select defaultValue="x">
	<option value="x">...</option>
	</select>

12) A more consistent onChange
	Passing a function to the onChange attribute you can subscribe to events on form fields.
	It works consistently across fields, even radio , select and checkbox input fields fire a
	onChange event.
	onChange also fires when typing a character into an input or textarea field

13) JSX auto escapes string

14) React components can be classified as
 	stateful & stateless components OR
	functional and class based components (on basis of syntax) OR
	Presentational or container

15) State vs Props
	What's the difference between state and props in React?
	In a React component, props are variables passed to it by its parent component. State on the
	other hand is still variables, but directly initialized and managed by the component.

	Props are also used to allow child components to access methods defined in the parent
	component. This is a good way to centralize managing the state in the parent component, and
	avoid children to have the need to have their own state.

	Most of your components will just display some kind of information based on the props they
	received, and stay stateless.

16) propTypes
	import PropTypes from 'prop-types'
	import React from 'react'
	class BlogPostExcerpt extends Component {
		render() {
			return (
				<div>
				<h1>{this.props.title}</h1>
				<p>{this.props.description}</p>
			</div>
			)
		}
	}
	BlogPostExcerpt.propTypes = {
		title: PropTypes.string,
		description: PropTypes.string
	}
	export default BlogPostExcerpt

	PropTypes.array
	PropTypes.bool
	PropTypes.func
	PropTypes.number
	PropTypes.object
	PropTypes.string
	PropTypes.symbol
	We can accept one of two types:
	PropTypes
	88
	PropTypes.oneOfType([
	PropTypes.string,
	PropTypes.number
	]),
	We can accept one of many values:
	PropTypes.oneOf(['Test1', 'Test2']),
	We can accept an instance of a class:
	PropTypes.instanceOf(Something)
	We can accept any React node:
	PropTypes.node
	or even any type at all:
	PropTypes.any

	Requiring properties
	Appending isRequired to any PropTypes option will cause React to return an error if that
	property is missing:
	PropTypes.arrayOf(PropTypes.string).isRequired,
	PropTypes.string.isRequired,

17)	Lifecycle events

	Find out the React Lifecycle events and how you can use them
	React class components can have hooks for several lifecycle events.
	Hooks allow function components to access them too, in a different way.
	During the lifetime of a component, there's a series of events that gets called, and to each
	event you can hook and provide custom functionality.
	What hook is best for what functionality is something we're going to see here.
	First, there are 3 phases in a React component lifecycle:
	Mounting
	Updating
	Unmounting
	Let's see those 3 phases in detail and the methods that get called for each.
	Mounting
	When mounting you have 4 lifecycle methods before the component is mounted in the DOM:
	the constructor , getDerivedStateFromProps , render and componentDidMount .
	Constructor
	The constructor is the first method that is called when mounting a component.
	You usually use the constructor to set up the initial state using this.state = ... .
	getDerivedStateFromProps()
	When the state depends on props, getDerivedStateFromProps can be used to update the state
	based on the props value.
	It was added in React 16.3, aiming to replace the componentWillReceiveProps deprecated
	method.
	In this method you haven't access to this as it's a static method.
	It's a pure method, so it should not cause side effects and should return the same output when
	called multiple times with the same input.
	Lifecycle events
	97
	Returns an object with the updated elements of the state (or null if the state does not change)
	render()
	From the render() method you return the JSX that builds the component interface.
	It's a pure method, so it should not cause side effects and should return the same output when
	called multiple times with the same input.
	componentDidMount()
	This method is the one that you will use to perform API calls, or process operations on the
	DOM.
	Updating
	When updating you have 5 lifecycle methods before the component is mounted in the DOM:
	the getDerivedStateFromProps , shouldComponentUpdate , render , getSnapshotBeforeUpdate and
	componentDidUpdate .
	getDerivedStateFromProps()
	See the above description for this method.
	shouldComponentUpdate()
	This method returns a boolean, true or false . You use this method to tell React if it should
	go on with the rerendering, and defaults to true . You will return false when rerendering is
	expensive and you want to have more control on when this happens.
	render()
	See the above description for this method.
	getSnapshotBeforeUpdate()
	In this method you have access to the props and state of the previous render, and of the
	current render.
	Its use cases are very niche, and it's probably the one that you will use less.
	Lifecycle events
	98
	componentDidUpdate()
	This method is called when the component has been updated in the DOM. Use this to run any
	3rd party DOM API or call APIs that must be updated when the DOM changes.
	It corresponds to the componentDidMount() method from the mounting phase.
	Unmounting
	In this phase we only have one method, componentWillUnmount .
	componentWillUnmount()
	The method is called when the component is removed from the DOM. Use this to do any sort
	of cleanup you need to perform.
	Legacy
	If you are working on an app that uses componentWillMount , componentWillReceiveProps or
	componentWillUpdate , those were deprecated in React 16.3 and you should migrate to other
	lifecycle methods

18) React Forms
	There are two main ways of handling forms in React, which differ on a fundamental level: how
	data is managed.
	if the data is handled by the DOM, we call them uncontrolled components
	Handling forms

	if the data is handled by the components we call them controlled components
	Controlled component is favoured although for type=file input we have to use createRef of React.
	class Form extends React.Component {
	constructor(props) {
	super(props)
	this.state = { username: '' }
	this.handleChange = this.handleChange.bind(this)
	this.handleSubmit = this.handleSubmit.bind(this)
	}
	handleChange(event) {
	this.setState({ value: event.target.value })
	}
	handleSubmit(event) {
	alert(this.state.username)
	event.preventDefault()
	}
	render() {
	return (
	<form onSubmit={this.handleSubmit}>
	<input
	type="text"
	value={this.state.username}
	onChange={this.handleChange}
	/>
	<input type="submit" value="Submit" />
	</form>
	)
	}
}

19) Higher Order Components
