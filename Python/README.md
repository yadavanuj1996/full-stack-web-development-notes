Head First python notes

1) We do not need to explicitly define the data type for identifiers in
 python.

2) cast=["a","b"] is a list in python somewhat similar to array 
	
i)   print(cast) # will print ["a","b"]
ii)  len(cast) # 2 length of list
iii) cast.extend(["c","d"]) # to add to list
iv)  cast.remove("c") # to remove item c from list cast
v)   cast.insert(0,"z"); # to add z on first index of list 
vi)  cast[2] #will return item at index 2
vii) cast.pop() # will remove and return the last item of list 
viii)movies.insert(1,1975) # to add the 1975 on index 1
3)
   i) # are used for comments
   ii) ; is not required in python
   iii) the list starts with index 0   

4) Python lists can contain data of mixed type. It’s perfectly OK
to mix strings with numbers within the same Python list

5) for loop in python 
	fav_movies=["a","b","c"]
	for movie in fav_movies:
		print(movie)

    indentations are must in python and a tab or 4 space is used for indentation
    {} brackets are not used in "for" loop or if else.    

6) while loop in python
	count=0
	while count < len(movies):
		print(movies[count])
		count=count+1

	#count++ does not work in python

7) Python lists can dynamically increase or decrease size thus they have
   the advantage over arrays.

8) Strings can be created using both '' (single quotes) and "" (double quotes)

9) if a > 2:
	print "a is larger than 2"
   elif a < 2:
	print ("a is less than 2")
   else: 
	print ("a is equal to 2")

10) We can call a for loop inside another for loop in python.

11) A function in Python is a named suite of code, which can also take an optional
    list of arguments if required

	def funtion name (argument(s)):
 		function code suite	

	To print a list within a list

	 def print_lol(the_list):
		for each_item in the_list:
		 if isinstance(each_item, list):
		print_lol(each_item)
		 else:
		print(each_item)

	isinstance() BIF checks whether an identifier refers to a data object of some specified type.
 	(in this case testing whether it is a list)

12)  i)  z“BIF” - a built-in function.
     ii) “Suite” - a block of Python code, which is indented to indicate grouping.
     iii) print() BIF displays a message on screen.
A list is a collection of data, separated
by commas and surrounded by square
brackets.
 Lists are like arrays on steroids.
 Lists can be used with BIFs, but also
support a bunch of list methods.
 Lists can hold any data, and the data can be
of mixed type. Lists can also hold other lists.
 Lists shrink and grow as needed. All of the
memory used by your data is managed by
Python for you.
 Python uses indentation to group statements
together.
 len() BIF provides a length of some data
object or count the number of items in a
collection, such as a list.
 The for loop lets you iterate a list and
is often more convenient to use that an
equivalent while loop.
 The if... else... statement lets you mak
decisions in your code.
 isinstance() BIF checks whether
an identifier refers to a data object of some
specified type.
 Use def to define a custom function



Sharing your module
1) A module is simply a text file that contains Python code. The main
requirement is that the name of the file needs to end in .py: the Python
extension. 

2) In Python, a common commenting technique is to use a triple quote for multiple-line comments. When you use a triple 
   quote without assigning it to a variable, everything between the triple quotes is considered a comment:

 """This is the standard way to include a multiple-line comment in your code."""

 If you put a “#” symbol anywhere on a line, everything from that point to the end of the current line is a comment 

3) Code in your main Python program (and within IDLE’s shell) is associated
with a namespace called __main__. When you put your code into its own
module, Python automatically creates a namespace with the same name as
your module

4)  namespace names are like family names.
When you want to refer to some function from a module
namespace other than the one you are currently in, you need
to qualify the invocation of the function with the module’s
namespace name.
So, instead of invoking the function as print_lol(cast)
you need to qualify the name as nester.print_lol(cast).
That way, the Python interpreter knows where to look. The
format for namespace qualification is: the module’s name, followed
by a period, and then the function name.

5) When you use a plain import statement, such as import nester,
the Python interpreter is instructed to allow you to access nester’s
functions using namespace qualification. However, it is possible to be
more specific. If you use from nester import print_lol, the
specified function (print_lol in this case) is added to the current
namespace, effectively removing the requirement for you to use
namespace qualification. But you need to be careful. If you already have
a function called print_lol defined in your current namespace, the
specific import statement overwrites your function with the imported
one, which might not be the behavior you want. 

6) for num in range(4):
	print(num) 

	Output: 0
		1
		2
		3

7) Function names should be lowercase, with words separated by underscores as necessary to improve readability.

   Variable names follow the same convention as function names.

8) Unlike compiled languages (such as C, Java, C#, and others), Python doesn’t
completely check the validity of your code until it runs. This allows Python to do
some rather cool things that just aren’t possible in those other languages, such
as dynamically defining functions at runtime. This, of course, can be very
flexible and powerful.
The cost to you, however, is that you need to be very careful when writing
your code, because something that typically would be caught and flagged as
an “error” by a traditional, statically typed, compiled language often goes
unnoticed in Python.

9) 
	 # Both parameters are required
	 def print_lol(the_list, level):
	 # level argument is optional
	 def print_lol(the_list, level=0):

10) Summary
	 Use a “triple-quoted string” to include
	a multiple-line comment in your code.
	• “PyPI” is the Python Package Index and
	is well worth a visit.
	• A “namespace” is a place in Python’s
	memory where names exist.
	• Python’s main namespace is known as
	__main__

	 A module is a text file that contains Python
	code.
	 The distribution utilities let you turn your
	module into a shareable package.
	 The setup.py program provides
	metadata about your module and is used
	to build, install, and upload your packaged
	distribution.
	 Import your module into other programs
	using the import statement.
	 Each module in Python provides its own
	namespace, and the namespace name
	is used to qualify the module’s functions
	when invoking them using the module.
	function() form.
	 Specifically import a function from a module
	into the current namespace using the from
	module import function form of
	the import statement.
	 Use # to comment-out a line of code or
	to add a short, one-line comment to your
	program.
	 The built-in functions (BIFs) have their own
	namespace called __builtins__,
	which is automatically included in every
	Python program.
	 The range() BIF can be used with for to
	iterate a fixed number of times.
	 Including end=’’ as a argument to the
	print() BIF switches off its automatic
	inclusion of a new-line on output.
	 Arguments to your functions are optional if
	you provide them with a default value.

Files & Exceptions: Dealing with errors:

1) The basic input mechanism in Python is line based: when read into your
program from a text file, data arrives one line at a time.
Python’s open() BIF lives to interact with files. When combined with a for
statement, reading files is straightforward.
 open()

When you use the open() BIF to access your data in a file, an iterator is
created to feed the lines of data from your file to your code one line at a time.
But let’s not get ahead of ourselves

2) Syntax to read file
	the_file = open('sketch.txt')
	 # Do something with the data
	 # in "the_file".
	 the_file.close()

3)  details=Man: Is this the right room for an argument?
	 (role, line_spoken) = details.split(":")
	# role will contain string Man
	# line_spoken will contain string  Is this the right room for an argument?

	The split() method returns a list of strings, which are assigned to a list of target identifiers.
	This is known as multiple assignment:

4) Have you noticed that when something goes wrong with your code, the
Python interpreter displays a traceback followed by an error message?
The traceback is Python’s way of telling you that something unexpected has
occurred during runtime. In the Python world, runtime errors are called
exceptions

Of course, if you decide to ignore an exception when it occurs, your program
crashes and burns.
But here’s the skinny: Python let’s you catch exceptions as they occur, which
gives you with a chance to possibly recover from the error and, critically, not
crash.

5) The try/except mechanism
Python includes the try statement, which exists to provide you with a way to
systematically handle exceptions and errors at runtime. The general form of
the try statement looks like this:
try:
 your code (which might cause a runtime error)
except:
 your error-recovery code

6) No. Not mad. And, yes. Letting errors occur.
If you try to code for every possible error, you’ll be at it for a
long time, because all that extra logic takes a while to work out.
Paradoxically, when you worry less about covering every
possible error condition, your coding task actually gets easier

Python approach to let the code go into runtime error and recover from there rather than writing extra if else condition to handle the anamoly cases in code itself in the first place.

7) Q: Something has been bugging me for a while. When the split() method executes, it passes back a list, but the target identifiers
are enclosed in regular brackets, not square brackets, so how is this a list?
A: Well spotted. It turns out that there are two types of list in Python: those that can change (enclosed in square brackets) and those that
cannot be changed once they have been created (enclosed in regular brackets). The latter is an immutable list, more commonly referred
to as a tuple. Think of tuples as the same as a list, except for one thing: once created, the data they hold cannot be changed under any
circumstances. Another way to think about tuples is to consider them to be a constant list. At Head First, we pronounce “tuple” to rhyme with
“couple.” Others pronounce “tuple” to rhyme with “rupal.” There is no clear concensus as to which is correct, so pick one and stick to it.

8) 
	 data = open('sketch.txt')
	 for each_line in data:
		 try:
			 (role, line_spoken) = each_line.split(':', 1)
			 print(role, end='')
			 print(' said: ', end='')
			 print(line_spoken, end='')
		except:
			pass
	 data.close()

	Now, no matter what happens when the split() method is invoked, the
	try statement catches any and all exceptions and handles them by ignoring the
	error with pass.

9) Use except in try to make the error less generalized

	 try:
		data = open('sketch.txt')
		for each_line in data:
			 try:
				 (role, line_spoken) = each_line.split(':', 1)
				 print(role, end='')
				 print(' said: ', end='')
				 print(line_spoken, end='')
			 except ValueError:
			 	 pass
		data.close()
	except IOError:
		print('The data file is missing!')

	Of course, if an different type of runtime error occurs, it is no longer handled
by your code, but at least now you’ll get to hear about it. When you are
specific about the runtime errors your code handles, your programs no longer
silently ignore some runtime errors.

Using “try/except”
lets you concentrate
on what your code
needs to do.


...and it lets you avoid
adding unnecessary code
and logic to your programs.
That works for me!

10) Summary
An “exception” occurs as a result
of a runtime error, producing a
traceback.
• A “traceback” is a detailed
description of the runtime error
that has occurred


 Use the open() BIF to open a disk file,
creating an iterator that reads data from
the file one line at a time.
 The readline() method reads a
single line from an opened file.
 The seek() method can be used to
“rewind” a file to the beginning.
 The close() method closes a
previously opened file.
 The split() method can break a
string into a list of parts.
 An unchangeable, constant list in Python
is called a tuple. Once list data is
assigned to a tuple, it cannot be changed.
Tuples are immutable.
 A ValueError occurs when your data
does not conform to an expected format.
 An IOError occurs when your data
cannot be accessed properly (e.g.,
perhaps your data file has been moved or
renamed).
 The help() BIF provides access to
Python’s documentation within the IDLE
shell.
 The find() method locates a specific
substring within another string.
 The not keyword negates a condition.
 The try/except statement provides
an exception-handling mechanism,
allowing you to protect lines of code that
might result in a runtime error.
 The pass statement is Python’s empty
or null statement; it does nothing.


Persistence: Saving data to file

1)  
	When you have a situation where code must always run no matter what errors
occur, add that code to your try statement’s finally suite:
	
try:
 man_file = open('man_data.txt', 'w')
 other_file = open('other_data.txt', 'w')
 print(man, file=man_file)
 print(other, file=other_file)
 except IOError:
 print('File error.')
 finally:
 man_file.close()
 other_file.close()

If no runtime errors occur, any code in the finally suite executes. Equally,
if an IOError occurs, the except suite executes and then the finally
suite runs.
No matter what, the code in the finally suite always runs.

2) Strings in Python are immutable,
which means that once a string is created, it cannot be changed.

Python variables contain a reference to a
data object.The data object contains the data and, because you
can conceivably have a string object used in many different places
throughout your code, it is safest to make all strings immutable so
that no nasty side effects occur

 If you try to change an immutable
value, Python raises a TypeError exception


3) Skipped the rest of the chapter for now


comprehending data (Chapter 5) 

1) Perform an in-place sort using the sort() method that is built in as standard to every Python list:
>>> data.sort()
>>> data
[1, 2, 3, 4, 5, 6]
Reset data to its original unordered state, and then perform a copied sort using the sorted() BIF:
>>> data = [6, 3, 1, 2, 4, 5]
>>> data
[6, 3, 1, 2, 4, 5]
>>> data2 = sorted(data)
>>> data
[6, 3, 1, 2, 4, 5]
>>> data2

2) TO add to list

	 clean_mikey = []
	 for each_t in mikey:
	 	clean_mikey.append(sanitize(each_t))

3) Iterate to remove duplicates

	unique_james = []
	for each_t in james:
		if each_t not in unique_james:
			unique_james.append(each_t)
[1, 2, 3, 4, 5, 6]

4) Remove duplicates with sets 

	In addition to lists, Python also comes with the set data structure, which
behaves like the sets you learned all about in math class.
The overriding characteristics of sets in Python are that the data items in a set
are unordered and duplicates are not allowed. If you try to add a data item to a set
that already contains the data item, Python simply ignores it.

	#create a new empty set
	 distances = set()

	# create and initialize the set in one step
	 distances = {10.6, 11, 8, 10.6, "two", 7}

	Any duplicates in the supplied list of data values are ignored.

	#creating a set from a list removing duplicated items of list in the set
	 distances = set(james)

	Any duplicates in the “james” list are ignored. 

5) Summary

	 “In-place” sorting - transforms
and then replaces.
• “Copied” sorting - transforms
and then returns.
• “Method Chaining” - reading
from left to right, applies a
collection of methods to data.
• “Function Chaining” - reading
from right to left, applies a
collection of functions to data.


The sort() method changes the
ordering of lists in-place.
 The sorted() BIF sorts most any data
structure by providing copied sorting.
 Pass reverse=True to either
sort() or sorted() to arrange your
data in descending order.
 When you have code like this:
new_l = []
for t in old_l:
 new_l.
append(len(t))
rewrite it to use a list comprehension,
like this:
new_l = [len(t) for t
in old_l]
 To access more than one data item from
a list, use a slice. For example:
my_list[3:6]
accesses the items from index location 3
up-to-but-not-including index location 6.
 Create a set using the set() factory
function.



CHapter 6


1)  “Dictionary” - a built-in data
structure that allows you to
associate data values with keys.
• “Key” - the look-up part of
the dictionary.
• “Value” - the data part of the
dictionary (which can be any value,
including another data structure)


2) “self” - a method argument
that always refers to the current
object instance


3) SUmmary 
	 Create a empty dictionary using the
dict() factory function or using {}.
 To access the value associated with
the key Name in a dictionary called
person, use the familiar square bracket
notation: person['Name'].
 Like list and set, a Python’s dictionary
dynamically grows as new data is added
to the data structure.
 Populate a dictionary as you go:
new_d = {} or new_d = dict()
and then
d['Name'] = 'Eric Idle'
or do the same thing all in the one go:
new_d = {'Name': 'Eric
Idle'}
 The class keyword lets you define a
class.
 Class methods (your code) are defined in
much the same way as functions, that is,
with the def keyword.
 Class attributes (your data) are just like
variables that exist within object instances.
 The __init__() method can be
defined within a class to initialize object
instances.
 Every method defined in a class must
provide self as its first argument.
 Every attribute in a class must be prefixed
with self. in order to associate it data
with its instance.
 Classes can be built from scratch or can
inherit from Python’s built-in classes or
from other custom classes.
 Classes can be put into a Python module
and uploaded to PyPI. 


Free code camp course notes
1) The None keyword is used to define a null variable or an object. In Python, None keyword is an object, and it is a data type of the class NoneType . We can assign None to any variable, but you can not create other NoneType objects.

2) if 0 is 0.0: # this condition will return false
	#write code

	print(0 is 0.0) # false

	print(0 == 0.0) # true

	because == (double equal to) only tests the equality of value
	while   is (equality check using is) is more stronger and tests both type and value of variable

	(Mostly use == when using numbers and string , try to use it more on booleand and None)

	`isNot` also a opeartor working opposite of what `is` opeartor do
 
3) for n in "banana":
   	print(n)

	Output: b
		a
		n
		a
		n
		a

4) continue and break both works in python as they work in other programming languages.
5) \n is used for next line in a string
6) 
x="asterix"
print(x[1])   #s
print(x[2:4]) #te
print(x[:3])  #ast
print(x[2:])  #terix
print(x[-3:]) #rix
