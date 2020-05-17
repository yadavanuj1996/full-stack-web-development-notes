

This link contains the notes whatever is not covered there is being documented here:-
https://github.com/yadavanuj1996/freecodecamp-solutions/blob/master/Front%20End%20Libraries%20Certification/README.md



How to decide whether the particular piece of data is state or not
Go through each data piece and figure out which one is state. Ask three questions about each piece of data:

a) Is it passed in from a parent via props? If so, it probably isn’t state.  
b) Does it remain unchanged over time? If so, it probably isn’t state.  
c) Can you compute it based on any other state or props in your component? If so, it isn’t state.  

1) Minify your js before production.
2) A JavaScript build toolchain typically consists of:
	```
	1) A package manager, such as Yarn or npm. It lets you take advantage of a vast ecosystem of third-party
 	   packages, and easily install or update them.

	2) A bundler, such as webpack or Parcel. It lets you write modular code and bundle it together into small 
	   packages to optimize load time.

	3) A compiler such as Babel. It lets you write modern JavaScript code that still works in older browsers.	
	```
3) Deploy only after shifting to production mode.
4) JSX Prevents Injection Attacks
	It is safe to embed user input in JSX:

	const title = response.potentiallyMaliciousInput;
	// This is safe:
	const element = <h1>{title}</h1>;
	By default, React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you
	can never inject anything that’s not explicitly written in your application.
5) Such functions are called “pure” because they do not attempt to change their inputs, and always return the same
   result for the same inputs.

6) All React components must act like pure functions with respect to their props.

7) Do Not Modify State Directly
	For example, this will not re-render a component:

	// Wrong
	this.state.comment = 'Hello';
	Instead, use setState():

	// Correct
	this.setState({comment: 'Hello'});

8) State Updates May Be Asynchronous.

	State Updates May Be Asynchronous
	React may batch multiple setState() calls into a single update for performance.

	Because this.props and this.state may be updated asynchronously, you should not rely on their values for calculating the next state.

	For example, this code may fail to update the counter:

	// Wrong
	this.setState({
	  counter: this.state.counter + this.props.increment,
	});
	To fix it, use a second form of setState() that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:

	// Correct
	this.setState((state, props) => ({
	  counter: state.counter + props.increment
	}));

9) State Updates are Merged
	When you call setState(), React merges the object you provide into the current state.

	For example, your state may contain several independent variables:

	  constructor(props) {
	    super(props);
	    this.state = {
	      posts: [],
	      comments: []
	    };
	  }
	Then you can update them independently with separate setState() calls:

	  componentDidMount() {
	    fetchPosts().then(response => {
	      this.setState({
		posts: response.posts
	      });
	    });

	    fetchComments().then(response => {
	      this.setState({
		comments: response.comments
	      });
	    });
	  }
	The merging is shallow, so this.setState({comments}) leaves this.state.posts intact, but completely replaces 
	this.state.comments.

10) Passing Arguments to Event Handlers
	Inside a loop it is common to want to pass an extra parameter to an event handler. For example, if id is 
	the row ID, either of the following would work:

	<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
	<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>

11) Keys
	Keys help React identify which items have changed, are added, or are removed. Keys should be given to 
	the elements inside the array to give the elements a stable identity:

	const numbers = [1, 2, 3, 4, 5];
	const listItems = numbers.map((number) =>
	  <li key={number.toString()}>
	    {number}
	  </li>
	);

12) We don’t recommend using indexes for keys if the order of items may change. This can negatively impact performance
    and may cause issues with component state.

13) Keys serve as a hint to React but they don’t get passed to your components. If you need the same value in your 
    component, pass it    explicitly as a prop with a different name:

	const content = posts.map((post) =>
	  <Post
	    key={post.id}
	    id={post.id}
	    title={post.title} />
	);

14) 	
	<form>
	  <label>
	    Name:
	    <input type="text" name="name" />
	  </label>
	  <input type="submit" value="Submit" />
	</form>
	This form has the default HTML form behavior of browsing to a new page when the user submits the form. If you want this behavior in React, it just works. But in most cases, it’s convenient to have a JavaScript function that handles the submission of the form and has access to the data that the user entered into the form. The standard way to achieve this is with a technique called “controlled components”.

15) 
	class NameForm extends React.Component {
	  constructor(props) {
	    super(props);
	    this.state = {value: ''};

	    this.handleChange = this.handleChange.bind(this);
	    this.handleSubmit = this.handleSubmit.bind(this);
	  }

	  handleChange(event) {
	    this.setState({value: event.target.value});
	  }

	  handleSubmit(event) {
	    alert('A name was submitted: ' + this.state.value);
	    event.preventDefault();
	  }

	  render() {
	    return (
	      <form onSubmit={this.handleSubmit}>
		<label>
		  Name:
		  <input type="text" value={this.state.value} onChange={this.handleChange} />
		</label>
		<input type="submit" value="Submit" />
	      </form>
	    );
	  }
}

16) In HTML, a <textarea> element defines its text by its children:

	<textarea>
	  Hello there, this is some text in a text area
	</textarea>
	In React, a <textarea> uses a value attribute instead. This way, a form using a <textarea> can be 
	written very similarly to a form that uses a single-line input.

17) Handling Multiple Inputs
	When you need to handle multiple controlled input elements, you can add a name attribute to each element and
	let the handler function choose what to do based on the value of event.target.name.

For example:

	class Reservation extends React.Component {
	  constructor(props) {
	    super(props);
	    this.state = {
	      isGoing: true,
	      numberOfGuests: 2
	    };

	    this.handleInputChange = this.handleInputChange.bind(this);
	  }

	  handleInputChange(event) {
	    const target = event.target;
	    const value = target.type === 'checkbox' ? target.checked : target.value;
	    const name = target.name;

	    this.setState({
	      [name]: value
	    });
	  }

	  render() {
	    return (
	      <form>
		<label>
		  Is going:
		  <input
		    name="isGoing"
		    type="checkbox"
		    checked={this.state.isGoing}
		    onChange={this.handleInputChange} />
		</label>
		<br />
		<label>
		  Number of guests:
		  <input
		    name="numberOfGuests"
		    type="number"
		    value={this.state.numberOfGuests}
		    onChange={this.handleInputChange} />
		</label>
	      </form>
	    );
	  }
	}

	Note how we used the ES6 computed property name syntax to update the state key corresponding to the given input name:

	this.setState({
	  [name]: value
	});
	It is equivalent to this ES5 code:

	var partialState = {};
	partialState[name] = value;
	this.setState(partialState);

18) Always choose composition over inheritance

	At Facebook, we use React in thousands of components, and we haven’t found any use cases where we would
 	recommend creating component inheritance hierarchies.

	Props and composition give you all the flexibility you need to customize a component’s look and behavior in an
	explicit and safe way. Remember that components may accept arbitrary props, including primitive values, React 
	elements, or functions.

	If you want to reuse non-UI functionality between components, we suggest extracting it into a separate JavaScript
	module. The components may import it and use that function, object, or a class, without extending it.

19) For each piece of state in your application:

	Identify every component that renders something based on that state.
	Find a common owner component (a single component above all the components that need the state in the hierarchy).
	Either the common owner or another component higher up in the hierarchy should own the state.
	If you can’t find a component where it makes sense to own the state, create a new component solely for holding 
	the state and add it somewhere in the hierarchy above the common owner component.

		
								Advanced Guides


								Accessibility

1) Sometimes we break HTML semantics when we add <div> elements to our JSX to make our React code work, especially when working with lists (<ol>, <ul> and <dl>) and the HTML <table>. In these cases we should rather use React Fragments to group together multiple elements.

For example,

import React, { Fragment } from 'react';

function ListItem({ item }) {
  return (
    <Fragment>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </Fragment>
  );
}

function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        <ListItem item={item} key={item.id} />
      ))}
    </dl>
  );
}

2) Although these standard HTML practices can be directly used in React, note that the for attribute is 
   written as htmlFor in JSX:

	<label htmlFor="namedInput">Name:</label>
	<input id="namedInput" type="text" name="name"/>

3) Ensure that your web application can be fully operated with the keyboard only.
   Also use landmark elements and roles, such as <main> and <aside>, to demarcate page regions as assistive technology
   allow the user to quickly navigate to these sections.

4) Testing accessibility in the browser
	A number of tools exist that can run accessibility audits on web pages in your browser. Please use 
	them in combination with other accessibility checks mentioned here as they can only test the technical accessibility of your HTML.

	aXe, aXe-core and react-axe
