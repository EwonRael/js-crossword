js-crossword
===========
a stupid and simple javascript file for interactive crosswords on webpages

About
-----
For fun I started making [five-by-five crossword puzzles, as well as an interactive site for solving them](https://ewonrael.github.io/crossword/). Over time I started adding more and more features including mobile support and the ability to highlight individual words that are correctly guessed. Implementing decant mobile support for crosswords is difficult and hacky, but I managed to get something that works well from a experience standpoint. I decided to release a version of the code that works for all different crosswords when I realized no such code currently exists.

![image of example](https://github.com/EwonRael/js-crossword/raw/main/docs/example.png)

The Code
--------
The code is a single javascript file that can be linked to at the top of your html. It will make your static crossword come to life. No need for fancy libraries or anything, it's just simple vanilla javascript. I'm terrible at coding, and the code was modified and tweaked over time instead of being built with all the features in mind from the get-go. The result is a functional, but illegible mess of spaghetti code that no one should try and make heads or tails of.

How to Use
----------
**HTML**<br>
There are some basic things needed for the code to function. Your html code **must** include a `<table>` element with an id of "`crossword`". The crossword table <i>must</i> be populated with rows (`<tr>`) and data cells (`<td>`). The code will use these rows and cells to calculate the dimensions of the crossword, so it needs to be the exact dementions of your desired crossword or else it won't run. The rows and data cells don't need any additional information like ids or inner text. The script will automatically label each data cell with a "crossword-square" number (`crossword-square-1`, `crossword-square-2`, etc.)

You html also needs a `<div>` with an id of "`crossword-clues-across`" and a `<div>` with the id of "`crossword-clues-down`." It is expected that this each child of this `<div>` is a crossword clue, so make sure to have the clues as separate elements. DO NOT include a title or something in these `<div>` elements as the code will mistake the title for a clue. It doesn't have to be a `<div>` specifically, just some kind of container.

Finally, the code anticipates a `<div>` with the id of "`mobilePreview`" in the html. This div should include a child with an id of "`previewBox`". This `<div>` will automatically show the contents of whatever clue is currently being worked on. This is super useful on mobile where you have limited screen real estate, but on desktop you can probably hide it altogether. The `<div>` will toggle a "`.invisable`" class on and off (I know I spelled that wrong. Sorry). This is useful if you only want the element visible while a clue is highlighted. ([see my five-by-five crosswords](https://ewonrael.github.io/crossword/) for a working example)

**JAVASCRIPT**<br>
You also need some additional javascript to let it know the specifics of your crossword, as well as what you want it to do on completion.  The crossword itself is just a big, long, string. Each letter appears once, lowercase, and the blacked out squares are represented with a "`#`". This string should be a variable named "`goal`" because it's the goal we're working towards.

For example, if our finished crossword looked like this:
```
DOG
O#I
TAN
```
than there should be a variable "`goal`" that is equal to `"dogo#itan"`.

There are three settings: the timer, highlighting correct words, and highlighting correct letters. These are stored in a variable named "`settingsc`" and is an array. Something like `[true, false, false]`. 

Finally, when the crossword is solved the code will run a function `crosswordsolved()`. This doesn't exist by default. If the timer setting is set to true, finishing the crossword will make the variable `timer` equal to a string of text telling you how long you took to solve the crossword. It might be nice to let the crossword solvers read this text, but implementing that is up to you.

**CSS**<br>
By default there aren't any numbers for the boxes. I like to add those as "`::before`" pseudo classes in my CSS. For example:
```
#crossword-square-1::before {
	content: "\00B9";
}
```
will add the number 1 to the first box.

There are four classes that the script will add to elements which are related to the crossword. The first is "`.black`", which will be added to the blacked out squares. The second is "`.solved`" which will be added to any solved squares (this is only really useful when highlighting solved words or letters is enabled). The third is "`.highlight`", which is whatever word you are currently working on, and the final is "`.focus`" which is the exact square you are editing. Unless there is a background color specified in the css for these classes, there is no clear way to know which word you are currently working on. In the example image pictured above, "`.highlight`" classes are a light blue, and "`.focus`" classes are yellow.

Example
-------
Included in this repository is an example crossword with the bare minimum needed to get it up and running. This is in the "example" folder. This does a much better job of explaining what everything is and how it works then I ever could. Experiment with the "`index.html`" file, the "`style.css`" file, and the "`script.js`" file. The "`crossword.js`" file is the spaghetti code that you really should never try and look at.

All you really need to do to get this working is to replace the `goal` text in the "`script.js`" file with whatever your crossword goal is, and adjust the "`crossword`" `<table>` element in the "`index.html`" to have the right number of rows and data cells. Everything else should take care of itself.

Thanks!
-------
If for some reason this nightmare of a code has benifitted your life in some way, consider giving me some money on [Patreon](https://www.patreon.com/EwonRael)
