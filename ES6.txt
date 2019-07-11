
							ES 6 (ECMA SCRIPT 6) (In Progress)

1) let vs var
	var has enclosing function scope while let has block scope (block scope is introduced in ES6). 
	function varTest() {
	  var x = 1;
	  if (true) {
	    var x = 2;  // same variable!
	    console.log(x);  // 2
	  }
	  console.log(x);  // 2
	}

	function letTest() {
	  let x = 1;
	  if (true) {
	    let x = 2;  // different variable
	    console.log(x);  // 2
	  }
	  console.log(x);  // 1
	}

  let does not create global scope variables
	var x = 'global';
	let y = 'global';
	console.log(this.x); // "global"
	console.log(this.y); // undefined

2) string literals
	var a = 5;
	var b = 10;
	console.log(`Fifteen is ${a + b} and
	not ${2 * a + b}.`);
	// "Fifteen is 15 and
	// not 20."







