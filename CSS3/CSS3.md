								

								CSS 3 (Front End)

1) Box properties Section
	Every element within a document is structured as a rectangular box inside the document layout, the size and "onion layers" of which 		can be tweaked using some specific CSS properties.

  width and height
	The width and height properties set the width and height of the content box, which is the area in which the content of the box is 		displayed — this content includes both text content set inside the box, and other boxes representing nested child elements.


  Padding
	Padding refers to the inner margin of a CSS box — between the outer edge of the content box and the inner edge of the border. The size 		of this layer can be set on all four sides at once with the padding shorthand property, or one side at a time with the padding-top, 		padding-right, padding-bottom and padding-left properties.

  Border
	The border of a CSS box sits between the outer edge of the padding and the inner edge of the margin. By default the border has a size 		of 0 — making it invisible — but you can set the thickness, style and color of the border to make it appear. The border shorthand 		property allows you to set all of these on all four sides at once, for example border: 1px solid black. 
 
  Margin
	The margin surrounds a CSS box, and pushes up against other CSS boxes in the layout. It behaves rather like padding; the shorthand 		property is margin and the individual properties are margin-top, margin-right, margin-bottom, and margin-left.


  Overflow
	When you set the size of a box with absolute values (e.g. a fixed pixel width/height), the content may not fit within the allowed 		size, in which case the content overflows the box. To control what happens in such cases, we can use the overflow property. It takes 		several possible values, but the most common are:

	auto: If there is too much content, the overflowing content is hidden and scroll bars are shown to let the user scroll & view content.
	hidden: If there is too much content, the overflowing content is hidden.
	visible: If there is too much content, the overflowing content is shown outside of the box (this is usually the default behavior)

  Types of Boxes a) inline b) block c) inline-block
	
	A block box is defined as a box that's stacked upon other boxes (i.e. content before and after the box appears on a separate line), 		and can have width and height set on it. The whole box model as described above applies to block boxes.

	An inline box is the opposite of a block box: it flows with the document's text (i.e. it will appear on the same line as surrounding 		text and other inline elements, and its content will break with the flow of the text, like lines of text in a paragraph.) Width and 		height settings have no effect on inline boxes; any padding, margin and border set on inline boxes will update the position of 		surrounding text, but will not affect the position of surrounding block boxes.
	
	An inline-block box is something in between the first two: It flows with surrounding text and other inline elements without creating 		line breaks before and after it unlike a block box, but it can be sized using width and height and maintains its block integrity like 		a block box. It won't be broken across paragraph lines like an inline box. In the below example the inline-block box goes onto the 2nd 		line of text while keeping the shape of a box as there is not enough space for it on the first line, whereas inline box does break on 		multiple lines if there is not enough space — it loses the shape of a box.

	Note: By default, block level elements have display: block; set on them, and inline elements have display: inline; set on them.

2)  Box-sizing property set to border-box. This makes sure that the padding and border are included in the total width and height of the 		elements.


	Grid View
	A responsive grid-view often has 12 columns, and has a total width of 100%, and will shrink and expand as you resize the browser 	 window.
	First ensure that all HTML elements have the box-sizing property set to border-box. This makes sure that the padding and border are 		included in the total width and height of the elements.

	Add the following code in your CSS:

	* {
	  box-sizing: border-box;
	}

	.col-1 {width: 8.33%;}
	.col-2 {width: 16.66%;}
	.col-3 {width: 25%;}
	.col-4 {width: 33.33%;}
	.col-5 {width: 41.66%;}
	.col-6 {width: 50%;}
	.col-7 {width: 58.33%;}
	.col-8 {width: 66.66%;}
	.col-9 {width: 75%;}
	.col-10 {width: 83.33%;}
	.col-11 {width: 91.66%;}
	.col-12 {width: 100%;}

	[class*="col-"] {
	  float: left;
	  padding: 15px;
	  border: 1px solid red;
	}

	<div class="row">
	  <div class="col-3">...</div> <!-- 25% -->
	  <div class="col-9">...</div> <!-- 75% -->
	</div>

3) 9 basic principles of responsive web design
	a) Responsive vs Adaptive web design
	b) The flow
	c) Relative units
	d) Breakpoints
	e) Max and Min values
	f) Nested objects
	g) Mobile or Desktop first
	h) Webfonts vs System fonts
	i) Bitmap images vs Vectors		(Always process pictures first)

4) Flex Box

	#pond {
	  display: flex;
	}

	flex-direction :  row | row-reverse | column | column-reverse
	justify-content:  flex-start | flex-end | center | space-between | space-around
	align-items: 	  flex-start | flex-end | center | baseline | stretch
	order  :(...,-2,-1,0,1,2,...) 
		 takes up the number default:0  higher the order it will switch towards (not just right but rather 			 			 towards flex-end) and we get it -ve it will go (not just left but rather flex-start)
		 align-self    applied on sub elements takes input same as align-items but works only for single element;
	flex-wrap: nowrap | wrap | wrap-reverse
		nowrap: Every item is fit to a single line. (default)
		wrap: Items wrap around to additional lines.
		wrap-reverse: Items wrap around to additional lines in reverse.

	 align-content: same as align-items; 
		This can be confusing, but align-content determines the spacing between lines, while align-items determines how the items as a 			whole are aligned within the container. When there is only one line, align-content has no effect.

	align-self align-items feature for paricular item
	flex-basis
		The flex-basis property specifies the initial size of the item before CSS makes adjustments with flex-shrink or flex-grow.
		The units used by the flex-basis property are the same as other size properties (px, em, %, etc.). The value auto sizes items  			based on the content.
	flex-grow
		flex-grow value of 1 and the other has a flex-grow value of 3, the one with the value of 3 will grow three times as much as 			the other.
	flex-shrink 
		vice versa of flex-grow with same concept.
	flex
		flex: flex-grow-value flex-basis; shorthand of flex-grow and flex-basis combined
5) Overriding CSS
	the class property will override body style if two classes are added and are overlapping properties then the one declared last in
	<style> tag will given preference to apply the style property, the id will override on classes but if a class property has 
	!important tied to it it will be given preference.

   em and rem are used for relative units in css

   Use variable in css
	Declare var using --penguin-skin: gray;    	
	background: var(--penguin-skin); to chage the background with color of penguin skin variable color
	IE does not support css variables so use fallbacks while using the variable
	
   By creating your variables in :root, they will be available throughout the whole web page.
	:root {
    	    --penguin-belly: pink;
	}
	we can override the variables in nested classes or other classes and can override :root defined value
	
   use position relative and then provide value to move the elment relative to other elements in html
	h2 {
    		position: relative;
   		top: 25px;
  	}

   The position:fixed keeps the block element fixed even when scrolling and top, bottom, left, right property can be used with it to move
   the elements or change their layout position position of element with respect to BROWSER, it also moves it out of general flow of html    	document, the position :absolute also moves the element out of normal flow of html document and we can use same left, right, top and      	bottom to move the position of element with respect to PARENT element.

   margin: auto will move the block element in center of page. we can also center an image with this while along with this just use 
   display: block;

   The color wheel is a useful tool to visualize how colors relate to each other - it's a circle where similar hues are neighbors
   and different hues are farther apart. When two colors are opposite each other on the wheel, they are called complementary colors.
   They have the characteristic that if they are combined, they "cancel" each other out and create a gray color. However, when placed 
   side-by- side, these colors appear more vibrant and produce a strong visual contrast

   One final point, each page should always have one (and only one) h1 element, which is the main subject of your content. This and the other 	 headings are used in part by search engines to understand the topic of the page.
