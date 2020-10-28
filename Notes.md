- [ ] Section 5: The 2 Pillars: Closures and Prototypal Inheritance 00/25|2hr 26min
	- [ ] 66. Section Overview | 2min
	- [ ] 67. Functions are Objects | 9min
	  - 'this' keyword, 'arguments' keyword
		- variable environment
		- scope chain(s)
		- invoking a function
		  - directly
			- object method
			- call & apply
			- function constructor

			```javascript
			const four = new Function('numParameter', 'return 4');

			four(4);
			```

			```javascript
			function woohoo() {
				console.log('woohoo');
			}

			woohoo.yell = 'aaahhh'; // A function creates a CALLABLE OBJECT
			```

			Pseudo-code
			```javascript
			const specialObj = {
				yell: 'aaahhh',
				name: 'woohoo' // name of the function
				(): console.log('woohoo');
			}
			```

	- [ ] 68. First Class Citizens | 4min
	  - Functions can be assigned to variables and properties
		- Functions can be passed as arguments to a function
		- We can return functions as values
	- [ ] 69. Extra Bits: Functions | 3min
	  - Be careful of initializing functions inside of loops

		```javascript
		function a() {
			return param; // next, look up the scope chain
		}
		```

		```javascript
		function a(defaultParameter = 6) {
			return defaultparameter; // next, look up the scope chain
		}

		a(); // 6
		```

	- [ ] 70. Higher Order Functions | 17min
	  - function()
		- function(a, b)
		- HOF >> a function that returns another function

		```javascript
		function letAdamLogin() {
			let array = [];
			for (let i=0; i<1000000; i++) {
				array.push(i);
			}
			return 'Access Granted to Adam';
		}

		letAdamLogin();
		```

		```javascript
		function letEvaLogin() {
			let array = [];
			for (let i=0; i<1000000; i++) {
				array.push(i);
			}
			return 'Access Granted to Eva';
		}

		letEvaLogin();
		```

		- DRY
		- Next, use a function with a parameter

		Higher-Order Function
		```javascript
		const giveAccessTo = (name) => 'Access Granted To ' + name;

		function authenticate(verify) {
			let array = [];
			for (let i=0; i<verify; i++) {
				array.push(i);
			}
			return true;
		}

		function letPerson(person, fn) {

			if (person.level === 'admin') {
				fn(500000);
			} else if (person.level === 'user') {
				fn(100000);
			}
			return giveAccessTo(person.name);
		}

		letPerson({ level: 'admin', name: 'Sally'}, authenticate);
		```

		Another Example
		```javascript
		// const multiplyBy() {}
		
		// multiplyByTwo
		// multiplyByTen

		const multiplyBy = function(num1){ 	// This is the Higher-Order Function
			return function(num2) {						// Clean this up with arrow functions
				return num1 * num2;
			}
		}

		const multiplyByTwo = multiplyBy(2);
		multiplyByTwo(4); 	//  8
		multiplyByTwo(10); 	// 20
		
		multiplyBy(4)(6) 		// 24
		```

	- [ ] 71. Exercise: Higher Order Functions | 4min
	- [ ] 72. Closures | 15min
	- [ ] 73. Exercise: Closures | 3min
	- [ ] 74. Closures and Memory | 8min
	- [ ] 75. Closures and Encapsulation | 8min
	- [ ] 76. Exercise: Closures 2 | 2min
	- [ ] 77. Solution: Closures 2 | 3min
	- [ ] 78. Exercise: Closures 3 | 1min
	- [ ] 79. Solution: Closures 3 | 4min
	- [ ] 80. Closures Review | 2min
	- [ ] 81. Prototypal Inheritance | 7min
	- [ ] 82. Prototypal Inheritance 2 | 9min
	- [ ] 83. Prototypal Inheritance 3 | 8min
	- [ ] 84. Prototypal Inheritance 4 | 11min
	- [ ] 85. Prototypal Inheritance 5 | 3min
	- [ ] 86. Prototypal Inheritance 6 | 9min
	- [ ] 87. Exercise: Prototypal Inheritance | 3min
	- [ ] 88. Solution: Prototypal Inheritance | 8min
	- [ ] 89. Exercise: Prototypal Inheritance with this | 1min
	- [ ] 90. Section Review | 4min
