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

		```javascript
		function a() {
			let grandpa = 'grandpa';
			return function b() {
				let father = 'father';
				return function c() {
					let son = 'son';
					return `${ grandpa } > ${ father } > ${ son }`
				}
			}
		}

		const one = a();
		```

		- How did 'son' remember what 'grandpa' was?
		- "Closure Box"
		  - Since c() is inside of another variable environment, variables THAT ARE REFERENCED in c() get kept around.
			- Lexical Scope

		```javascript
		function boo(string) {
			return function(name) {
				return function(name2) {
					console.log(`${string} ${name} ${name2}`);
				}
			}
		}

		const boo = (string)=>(name)=>(name2)=>console.log(`${string} ${name} ${name2}`);

		boo('Hi')('Tim')('Becca'); // 'Hi Tim Becca'
		```

	- [ ] 73. Exercise: Closures | 3min
	- [ ] 74. Closures and Memory | 8min
	  - Memory Efficient
		- Encapsulation

		```javascript
		function heavyDuty() {
			const bigArray = new Array(7000).fill(':-)');
			return bigArray;
		}

		heavyDuty();
		```

		```javascript
		function heavyDuty(index) {
			const bigArray = new Array(7000).fill(':-)');
			console.log('Array Created!');
			return bigArray[index];
		}

		heavyDuty(688);
		heavyDuty(688);
		heavyDuty(688);
		const getHeavyDuty = heavyDuty2();
		heavyDuty(688);
		heavyDuty(700);
		heavyDuty(800);

		function heavyDuty2(index) {
			const bigArray = new Array(7000).fill(':-)');
			console.log('Array Created Again!');
			return function(index) {
				return bigArray[index];
			}
		}
		```

	- [ ] 75. Closures and Encapsulation | 8min

		```javascript
		const makeNuclearButton = () => {

			let timeWithoutDestruction = 0;

			const passTime 				= () => timeWithoutDestruction++;
			const totalPeaceTime 	= () => timeWithoutDestruction;
			const launch 					= () => { 
				timeWithoutDestruction = -1;
				return 'B';
			}
			setInterval(passTime, 1000);
			return {
				launch: launch,
				totalPeaceTime: totalPeaceTime
			}
		}

		const ohno = makeNuclearButton();

		ohno.totalPeaceTime();
		``` 

	- [ ] 76. Exercise: Closures 2 | 2min
	- [ ] 77. Solution: Closures 2 | 3min
	- [ ] 78. Exercise: Closures 3 | 1min
	- [ ] 79. Solution: Closures 3 | 4min
	- [ ] 80. Closures Review | 2min
	
	- [ ] 81. Prototypal Inheritance 1 | 7min

		```javascript
		const array = [];
		array.__proto__						// looks like an array
		array.__proto__.__proto__ // base object
		```

		- This array was created from the array constructor.

		```javascript
		function a() {}
		a.__proto__ 	// f() { [native code] }
		array.__proto__.__proto__ // base object
		```
	
	- [ ] 82. Prototypal Inheritance 2 | 9min

		```javascript
		let dragon = {
			name: 'Tanya',
			fire: true,
			fight() {
				return 5
			},
			// sing() {
			//	`I am ${ this.name }, the breather of fire`
			//}
			sing() {
				if (this.fire) {
					return `I am ${ this.name }, the breather of fire`
				}
			}
		}

		let lizard = {
			name: 'Kiki',
			// fire: true,
			fight() {
				return 1
			}
		};

		// const singLizard = dragon.sing.bind(lizard);

		lizard.__proto__ = dragon; 		// Now dragon's properties are available
		dragon.isPrototypeOf(lizard); // true
		```

	- [ ] 83. Prototypal Inheritance 3 | 8min

		```javascript
		for(let prop in lizard) {
			console.log(prop);			// name, fight, fire, sing
		}

		for(let prop in lizard) {
			if (lizard.hasOwnProperty(prop)) {
				console.log(prop);				// name, fight
			}
		}
		```

		- Not copying; inheriting
		- This is NOT the scope chain, it's the prototype chain

		```javascript
		const obj = {}

		obj.__proto__ // Base Object
		obj.__proto__.__proto__ // null, (Beyond the Base Object) "There's nothing there"
		```

	- [ ] 84. Prototypal Inheritance 4 | 11min

		```javascript
		const obj = { name: 'Sally' }

		obj.hasOwnProperty('name'); // true
		obj.hasOwnProperty('hasOwnProperty'); // false, this property is further up the prototype chain
		```

		```javascript
		function a() {}
		a().hasOwnProperty('call'); 	// false, I thought that the call property was in the function prototype (parent?); trouble printing it
		a().hasOwnProperty('bind'); 	// false
		a().hasOwnProperty('apply'); 	// false
		a().hasOwnProperty('name'); 	// true
		```

	- [ ] 85. Prototypal Inheritance 5 | 3min

		```javascript
		let human = {
			mortal: true
		}

		let socrates = Object.create(human);
		console.log(socrates); // {}
		console.log(socrates.mortal); // true
		console.log(human.isPrototypeOf(socrates)); // true
		```

	- [ ] 86. Prototypal Inheritance 6 | 9min
	  - Only functions have the prototype property
		- Constructor functions

	- [ ] 87. Exercise: Prototypal Inheritance | 3min
	- [ ] 88. Solution: Prototypal Inheritance | 8min
	- [ ] 89. Exercise: Prototypal Inheritance with this | 1min
	- [ ] 90. Section Review | 4min