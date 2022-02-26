		Victor
1)  Focus on naming conventions
2)  Class name should be clear
3)  don't INVENT abbreviations
4)  if use fetch to get data from DB always use fetch don't use get,
	bring somewhere else
5)	isAgeCorrect boolean method better name instead of checkAgeValue
6) 	Keep refactoring and renaming in your code.
7)  SRA Single Responsibility Principle funation should do one thing 
	only and do it well, 5-10 lines are good for method length and it
	should never never exceed one screen.If it takes more than 3 seconds
	to understand function we should break up our code.
8) 	Use java 8 Optional (wrap it in).
9) 	Use global exception Handler
10) Don't use catch in business logic.
11) Keep business logic seperate and inside fort and data validation
	should be done outside fort after passing inside we should beleive
	it is of correct format.
12) Do continuos refactoring , you are not done when your code start
	working.
13) Class should have less than 300 lines.
14) If there is very large method of legacy software only then use this
	point, convert big method to a new class , variables required for 
	functioning of class should not be passed as a parameter but
	they should be made as instance variable of class and then thos
	variables should be updated by constructor call(not by taking 7 
	 parameters in function head) ,write logic of previous method's 
	 long code as a new method named as "execute" method in new class.
15) OOP , Information hiding tell as little as possible, instead of 
	exposing data or variables we expose methods.
16) KISS keep it short and simple in enterprise applications generally
	we write procedural code as we have set business logic and convert
	it into code.
17) Respect your readers , write code in such a way that it is easily
	readable as your code will be read 10x times than it took to write
	it.Respect your team members he is working with you.
18) Learn IDE Shortcuts
19) One line should never cross 120 characters, your reader should never
	have to move scrollbar horizontally.
20) Class length should ideally be 200-300 lines and it should never
	ever cross 500 lines.
21) Spaces, indentation, bracket structures should be used in same way
	by whole team.
22) Focus on readability of code even you have to add no. of lines in
	code or name long variables names but readability is important
	it should tell a message to reader.
23)	Encapsulate conditionals,predicates,optionals,lambda,Design Patterns
	& multi-threading learn all about them.
24) Don't use redundant comments.
25) Delete commented out code, GIT will always have a copy of it.
26) Comment on same line(+-1 line).
27) Don't do over involvement, don't tell them about what FactoryPattern 
	design pattern is just give a wiki article link.If you over energy
	write tests (test-driven development is very important).
28) Try to express more in code rather than comments your code should
	be beautifully written and understandable rather than user totally
	relying on comments to understand the logic and behacious of your
	code.
29) Good comments are those that are used when code just can't say it
	like specific algorithms too complex to understand from code or
	bug workarounds, to explain calls to strange APIs, warning of
	consequences that this thread is not thread-safe.
30) Write Todo's with date delivery date.
31) Write public java API docs for libraries and frameworks you write.
32) Anonymous methods are now possible in java -> { //code }, they do
	not have name ,DON'T USE THEM.
33) ASK FOR PEER REVIEW.Do pair programming.
	
	KEY POINTS:-
	(a) The day you stop refactoring your code becomes legacy code.
	(b) Refine expressive names.
	(c)functions should be small with long expressive names.
	(d)3 kinds of classes Struct(best ones as they immutable), Object
	(hide data and other things inside), logic containers(have all
	logic and used when we have lot of procedural code).
	(e)Comments are failures refactor,refine, reexpress your code even
	rename to make your code more expressable.
	(f)Pair programming is best.
	

	Uncle Bob:-
	
1)Bad code contains:-
a) Rigidity:- you change one function and system alters the required
	results then you have to change second function due to its coupling 
	with first one, when you make minor change in second function to
	make system work some third function coupled with second function 
	stops working and so on.One symptom of rigidity is you have to re-compile
	very much as you make a new shape addition as Oval class but due to 
	some code you have to recompile class circle and square that means your
	code is rigid.If nothing has to be recompiled then it is not rigid.
b)  Fragility:- You make a change in one place and it breaks the other
	code which has no relationship with the broken code ex:- if you correct
	salary for hourly employees and then it crashes the union leader report.
	Customer and managers most afraid of this.
c)  Non-Reusability:- You can't use a desirable code writtem by other 
	developer because the desirable code is coupled with lots of 
	undersirable code that may bring lots of your problems along with it. 
	Bad Coupling between modules create this problem.
2) Encapsulation weakened by OO languages,multiple inheritance didn't exist
	in java because of Diamond problem.Inheritance was improved in OO 
	languages but polymorphism was one of the important feature that was
	relatively newer in OO languages like JAVA and thus any OO language does
	not need pointers because they have polymorphism whether JAVA,C++,Rails.
3) In any Method calling another method we have compiler dependency in
	same direction as that of flow control but using encapsulation we can
	opposite the direction of compiler dependency in opposite direction of
	flow control.
	__________			  __________
	|M method|	--------> |N Method|
	----------			  -----------
	here M calls N and flow control is from M to N as any change in N
	will affect M method so compiler dependency is also in same direction
	as with flow control.
		
	Below we have used polymorphism using interface to change the direction
	of compiler dependency direction and now it is opposite to Flow control
	Here flow comtrol is towards M to N but compiler dependency from N to M.
	__________		____________	  	________
	|M method|	---->  |Interface L|     <-----|N Method|
	----------			____________   		    ---------	
3)  OO is about managing dependecies by selectivly re-inverting certain
	key dependencies in your architecture so you can prevent rigidity,
	fragility and non-reusability.
4) Class Design Principles
	SOLID Principles
	SRP(Single Responsibility Principle	
	OCP(The Open/Closed Principle)
	LSP(The Liskov Substitution Principle)
	ISP (The Interface Segregation Principle) 
	DIP (Dependency Inversion Principle)
	
	a) SRP:- A class should have only one single reason/responsibility to 
	change,here responsibility word refers change
	Don't put  functions that change for different reasons/different times/
	different people or department in organization in the same class if one 
	function is changed by audit department while the other by finance
	department change then it is not good idea.

	b) OCP:- A class or a module should be open for extension but should be
	closed for modification, it means you can change the behaviour of 
    module without changing the module.
	Immobility as you have square,circle and oval shapes class and manager
	wants to shape each shape in different JARs and sell seperately but out
    architecture doesn't support it as we have used all 3 in all switch 
	statements for rotateShape(),zoomShape methods and used all 3 in 
	drawShapes mehtod.
	c) Derived classes mut be usable to the base case interface without
	the need for users to know the difference.
	
	
	Clean Code Book
	
	
	1)The Boy Scout Rule: Leave the playground cleaner than you find it,
	similarly leave the code cleaner than you found it.
	
	Chapter-2 Meaningful Names
	1) Intent should be clear in names, use names that express the meaning
	of code rather than using int d use int flaggedCellValue.
	2) Avoid variables names that are too similar.
	3) Don't use words like cloudList in variable name for a array of
	elements use the word only if theie is actual java List involved.
	4) a1[i]=a2[i] makes less sense than destination[i]=source[i].
	5) Don't use noise words like productData or productInfo as there is 
	no specific meaning that can be derived out of it as productData can be
	productPrice,productExpiry or any other product detail.
	6) Keep names that make the variables distinguished 
	   getActiveAccount(); 
	   getActiveAccounts(); 
	   getActiveAccountInfo();
	How will user know what difference does this 3 methods offer and which 
	one to call at what time.
	7) Use searchable Names & pronouncable names.
	8) Write constants as Max_Chances_Provided
	9) Class Names should be nouns(place ,person or thing) , method names
	should be verbs (actions).
	10) Code that has more to do with problem domain then only use problem
	domain words & there is no program-esse in the code.
	
	Chapter-3 Naming Functions (methods)
	1) A Function should have ideally 3-4 lines at max 1 screen full.
	2) The function names should be descriptive and should state the intent
	clearly ex:- isTestPage(),setVendorName() are descriptive names.
	3) if , else & while loops should generally have 1 line in it that is
	function calls 
		if(isPage(pageNo))	
			updatePageData();
	Define pageData seperately as this keeps the loop or condition statement
	code shorter and also help users as descriptive names of method state
	what is being done in certain condition.
	4) Functions should not contain nested structures as the total 
	indentations in a function should be 1 or 2 it makes function easier
	to read and understand.
	5) SRP :- Single Responsibility Function , a function should do one thing,
		they should do it well and should do it only.
	6) 	So, another way to know that a function is doing more than “one thing”
	is if you can extract another function from it with a name that is not 
	merely a restatement of its implementation.
	7) Be consisting in naming functions ex:- includeCSSFile.includeSetupPage,
		includeTestPage.
	8) Ideally function with no parameteres are best anywho a method should
	not go beyond having more than 3 parameters (special justification 
	should be given for 3 or more than parameters).
	9) Don't pass an output agrument rely on return value.
	10) Flag arguments are ugly. Passing a boolean into a function is a 
	truly terrible practice. It immediately complicates the signature of the
	method, loudly proclaiming that this function does more than one thing.
	11) Use monad function as isFileEmpty("myfile.txt") 
	dyadic new point(0,0); 
	Triads assertEquals(message, expected, actual).
	12) we can use argument objects to reduce no of arguments in a method
			Circle makeCircle(double x, double y, double radius);
			Circle makeCircle(Point center, double radius);
	Here we have made a new class and pass it's object in such cases
	it's not bad to create a new class as it's a concept that deserved a name
	for itself.
	13) Function and argument should form a very nice verb/noun pair. For 
	example, write(name) is very evocative. Whatever this “name” thing is,
	it is being “written.” An even better name might be writeField(name), 
	which tells us that the “name” thing is a “field.”
	14) for ouput argument appendFooter(s) we are appending footer in 
	s string and returning it which is not a good practice as output
	parameter should not be passed so it's better to use it in form as
	s.appendFooter();
	15) Functions should either do something or answer something, but not
	both. Either your function should change the state of an object, or it 
	should return some information about that object.
	if(set("username","unclebob")	here set is used by author as verb to
	mean that set the username to unclebob and if it works then if condition
	statements run but it can be interpreted as whether to check that 
	username is set to unclebob.
	16) Use exceptions to return message instead of error reports.
	17) Try catch can also get ugly so write single function call in try
	and then in that function write all the code or feature you want to
	add or test. Error testing is one thing and a function should be able
	to do just one thing so no code should be written after end of catch or
	finally.
	18) Never write a duplicated code meaning same software shpuld not have\
	redundant line of code doing same thing.
	19) goto should be avoided but we can use break and continue in our
	functions (Note: dijkshrats structured programming rule says otherwise
	but we won't follow that).
	20) Generally you write function that are long ,are very indentated & are
	complicated so this rules are generally not applied when we are writing
	the code fresh but we use refine our code refactor it and apply all the
	principles mentioned in this chapter to write a function and during 
	refining we do renaming,splitting functions,remove duplication,shrinking
	a method and even sometimes break whole class or just create a new class
	to name some concept that was too important.
	21) AND rememeber we are using all the principles on fucntion to make
	the overall code better so always think about how it fits in the bigger
	picture of present and future code.
	22) Note write the code as a story if B function call is done from A,
	then just after ending of function A B should be written (Note : A and B
	are used for easy understanding we are not going to name our functions
	similarly).
	
	Chapter-4 Comments
	1) Comments should be avoided when you can express it by code itself.
	2) Write comments to state the importance of some line of code, or to
	tell the pattern that can't be cleared by code like explaining a regex
	what it is trying to do , commenting on output of certain alreay written
	library methods whose code we cannot clean.
	3) Instead of using comments to explain bad code clean and re write your
	code.
	4) TODO comments are good.
	5) legal and licensing details along with author should be written in
	comment.
	6) One problem with comments is if code os refactored or changed or
	splitted in future the comments are neglected by programmer or sometimes
	cannot be broken up appropriately and thus will be misleading to the
	reader.

	Chapter-5 Formatting
	1) The vertical gap between lines are crucial and a line should be blank
	between two line of code is only when they are of different concepts ex:-
	package javatest;
	
	import java.io.*;
	
	class javaStringClasses{
	
	}
	
	2) Don't write the unnecessary comments between two variables which have
	close connection with each other.
	3)Concepts that are closely related should be kept vertically close to 
	each other [G10]. Clearly this rule doesn’t work for concepts that 
	belong in separate files. But then closely related concepts should not
	be separated into different files unless you have a very good reason. 
	Indeed, this is one of the reasons that protected variables should be
	avoided.
	If a function in called from another function it should be just 
	underneath it.
	4) Don't let your readers hop up and down inside your code to search 
	for called methods to understand what is happening in the code.
	5) local variable should be declared just at the top of function or loop
	in which they will be used and instance variables at top of class.
	6) Horizontal line should contain around 120 characters or a screen width
	7) Horizontal spacing can also be used for opearator precedence.
		-b - sqrt(b*b - 4*a*c) / (2*a)
	8) Indent on basis of scope.
	
	Chapter-6 Objects & Data Structures
	1) Abstraction in important your data and implementaion should be 
	asbtract and should not be exposed. getGallonsOfGas() is not preferred
	as compare to getRemainingFuel() which is better abstracted.
	2) Setter and getter methods for private variables always don't make
	sense as they break the purpose of making them private first hand.
	3) Use interfaces or abstract class in java.
	4) Objects should hide thier internals and Data Structure should show
	their internals.
	5) DTO's are special data structure/classes that have private variables 
	and public methods to access those variables.
	6) A method A of class C should only call methods of these
		a)Methods declared in same class
		b)Object created in same method A.
		c)Object passed to same method A.
		d)Instance variables of class C.
	7) Objects expose behavior and hide data. This makes it easy to add new 
	kinds of objects without changing existing behaviors. It also makes it
	hard to add new behaviors to existing objects. Data structures expose
	data and have no significant behavior. This makes it easy to add new 
	behaviors to existing data structures but makes it hard to add new data
	structures to existing functions.
	
	Chapter-7 Exception Handling
	1) Use try -catch in thi form
		try{
			someFunction();
		}
		catch(Exception e){
			System.out.println(e.stackTrace());
		}
		
		static void someFunction(){
			// write code here
		}
	2) Always use Unchecked Exceptions except for some super critical library
	because if in a large chain of function calls if a method throws 
	unchecked exception then not only that method has to be updated to cater
	it but all the methods who call it also have to use keyword throws which
	breaks encapsualtion.
	3) while returning the exception to user not just send stack trace but
	also send the operation that failed and type of failure.
	4) Wrap third party API that can cause exception. We should call just 
	the method from our try block and wrapper function should throw the 
	exception as wrapper function will have it's own try-catch block.
	5) If a exceptional case is causing the exception like mealPerDiem where
	if meal had expenses that is reimbursed if not we throw an error and
	give monetary benifit on basis of mealDiem, we use SPECIAL CASE PATTERN
	in that we create a new obejct or class to handle special case.
	6) You should never return a "null" from a method.You can return a 
	empty lise or Collection.emptyList().
	7) Never pass a null as method parameter until and unless it is required
	for some external API method call.
	8) We have to write robust code that is clean not just clean code
	remember this. If we are writing exception handling as a seperate concern
	than it is clean to read as the exception handling doesn't mix with logic
	code and everything is easy to read and understand as well as we are 
	providing the exception handling so the system will still be robust.
	
	Chapter-8 Boundaries
	1) Boundary code is something which interact with third party API calls
	or it is when we are using a code written by other team or third party
	API.
	2) Instead of saving objects in a Map use generic.
		Map<Sensor> n=new HashMap<Sensror>(); better than to save as normal
		Map n=new HashMap();
	when fetching we have to type cast and that is not very clean
		Sensor s=(Sensor)n.get(i);
	Or use new method to call and typecast
		public Sensor getById(String id) {
			return (Sensor) sensors.get(id);
		}
	3) We should not pass any Maps or interface around the boundary of our
	application,If a boundary interface like Map is used keep it tied to a
	class or close family of classes avoid accepting it or passing it as
	as argument to public API.
	4) Learning tests are created by us and run on 3rd party APIs to
	understand how the 3rd party API works and that gives us clear idea of
	The tests focusses on what we want out of API.
	5) You should also take care of other side of boundary where it is not
	defined what is actually on that side of boundary like if some API will
	be written by other team that you have to use now you don't how it
	will be implemented you can simply create an interface of yours with
	suitable method and use that in your code and when actual API from third
	party or other team is completed link those API to your system's 
	interface by a connecting class.
	6) Your boundary code should handle the third party code such that even
	if the third party code updates there should be less maintenance points
	in your app. one example is of Plug-In architecture eby Uncle Bob in 
	video.
	
	Chapter-9 Unit Tests
	1) TDD is Test Driven Development, programmers are also started to use
	automated unit testing along with manual unit testing the unit test files
	are bundled in the same source package and unit tests are written to
	cover all possible scenarios and edge cases and also are available to
	anyone who will use our code in future.
	2) TDD asks us to write unit tests before writing the production code
	itself
	3) Three Laws of TDD(Test Driven Development):-
		(a) You may not write production code until you have written a
		failing unit test.
		(b) You may not write more of a unit test than is sufficient to fail,
		and not compiling is failing.
		(c) You may not write more production code to pass the currently 
		failing test.
	Using these laws the production code and unit tests are written almost
	together with test cases written 10 seconds before the production code
	and with each time you write test and write equivalent code soon all the
	test cases will exhaust and we will have foolproof application.
	4) Your testing code should be maintained along with your production code
	so that your testing remains as strong as always and the naming of 
	variables in testing file also should be descriptive and test files 
	should also be code in a CLEAN way.It is important to check that if we
	changes we are making in production code does not break other part of 
	system.
	5) Test code is just as important as production code.
	6) Unit tests help our code to remain maintainable, flexible & reusable 
	as we are not afraid to make changes to our code as we can test our
	system very	easily and whether the new code breaks some functionality or
	not and more and exhaustive unit tests increase our confidence in our 
	code.
	7) Readability is most important thing in unit test, test cases should be
	easily readable. Clarity,simplicity and density of expression keeps a 
	code readable.
	8) Write @Test one line above the unit test cases.
	9) We might use some things in testing emvironment	that we might not 
	use in production environment due to constraint of memory or CPU 
	efficiency.
	10) No. of asserts in a single test should be minimized.
	11) Each test function should test one concept at a time.
	12) A test should follow five rules F.I.R.S.T.
	  i) Fast :- they should be fast or else you won't use it and code rots.
	  ii)Independent:- They should not depend on other test cases.
	  iii) Repetable:- They should work in all environments not env.specific.
	  iv) Self- Validating:- Boolean answer either pass or fail ,no log read
	  v) Timely:- Written just before production code is written.
	13) Invent testing APIs that act as domain-specific language that helps
	you to write clean tests, if we let our tests rot our code will rot too 
	so keep your tests clean.
	
	Chapter-10 Classes
	1) Inside a class first declare public static constants then private
	static variables followed by private instance variables there are very
	rare cases in which you should define public variables, after all the
	variables call.If a private utility is called by public method then it
	should be written just after the public method.
	2) Complete from mobile

	11) OCP:- Open closed principle a class should be open for extension but
	closed for modification.ex:- breaking sql class to class as sqlUpdate,
	sqlInsert
	12) DIP:- Dependency Inversion Principle states that our class should depend
	upon abstractions, not on concrete implementation.
	13) We use abstractions so we make changes in concrete implementaion but
	not to interfaces.(also for testing purpose if public API will send varying
	values like Stock Exchange API as price of stock will change you will not
	find it's correctness)
	
	Chapter-11 Systems
	1) Dependency Inversion means passing the secondary responsiblity of a 
	object to other object.
	2) Discussion about Seperation of concern, AspectJ ,Spring and EJB took
	place read again as very less is being understood.

	Chapter-12 Emergence
	1) Four Rules of Simple Design
		i)   Test all the cases
		ii)  Refactoring
		iii) No Duplication :- Use extends also to take all methods from super
							   class and adding 1 that varies in two classes
							   ex:- EUVacation() vs USVacation().
		iv)   Expresiveness :- A person should understand class by tests or 
							   we can mention Design Pattern name that we are 
							   using.
		v) Minimal classes & Methods :- Although this is of low priority as test
										eliminate duplication & expressing 
										ourselves & write clean is more 
										important.
	
	Chapter-13 Concurrency
	1) Read this chapter again as it deals with concurrenct so haven't read it
	much study about multi-threading, concurrency, synchronous keyword write
	some multi-threaded programs and why we need multi-threaded programs then 
	please re-visit this chapter.
	
	Chapter-14
	1) Successive refinement
	Read again later 
	
	Chapter-15
