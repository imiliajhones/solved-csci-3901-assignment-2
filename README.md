Download Link: https://assignmentchef.com/product/solved-csci-3901-assignment-2
<br>
<h1>Problem 1</h1>




Goal

Get practice in writing test cases.




Problem

<u>Write test cases</u> for the following code.




A Sudoku puzzle is a square grid of cells n<sup>2 </sup>x n<sup>2</sup> where n is a positive integer (for the purposes of this assignment).  The goal of the puzzle is to enter the numbers 1- n<sup>2</sup> into the cells of the grid such that

<ul>

 <li>Every row contains all numbers from 1- n<sup>2</sup> – Every column contains all numbers from 1- n<sup>2</sup>.</li>

 <li>Every mini-grid contains all numbers from 1- n<sup>2</sup>.</li>

</ul>

The mini-grid reference in this description is an n x n sub-grid of the larger puzzle and where n<sup>2 </sup>mini-grids completely cover the grid (see Figure 1).




Notice that we don’t make use of the fact that we are putting numbers into the cells.  Our problem will let you put other characters into the cells, like letters.  An implementation will have a method to let the puzzle know which characters (letters, numbers, or symbols) are allowed in the cells.




The implementation of a solution is a class called Sudoku with the following methods:

<ul>

 <li>A constructor for the grid that defines the number of rows and columns in the square puzzle:</li>

</ul>

public Sudoku( int size )

<ul>

 <li>setPossibleValues to identify which characters can be <em>Figure 1 Sudoku puzzle, from </em></li>

</ul>

stored in the puzzle, returning true when the values are set for the puzzle and false if <em>https://en.wikipedia.org/wiki/Sudoku </em>there is some error: public boolean setPossibleValues( String values )

<ul>

 <li>setCellValue to fill in some cell values before solving the puzzle public boolean setCellValue( int x, int y, char letter )</li>

 <li>solve to solve the puzzle, returning true if the method was able to find a solution to the puzzle and false if there is no solution or if there is some error in the processing: public boolean solve( )</li>

 <li>toPrintString to get a printable version of the puzzle where we can specify the character to place in unfilled cell values; a string of the grid is returned, with no spaces between characters and with lines separated by carriage returns (
):</li>

</ul>

public String toPrintString( char emptyCellLetter )







The normal flow of operation is for a user to

<ol>

 <li>Create a puzzle using the constructor</li>

 <li>Define the symbols for the grid using setPossibleValues</li>

 <li>Constrain the puzzle by setting some of the cell values using setCellValue</li>

 <li>Solve the puzzle using the solve method</li>

</ol>













<h1>Problem 2</h1>




Goal

Implement a data structure from basic objects.




Background

Balanced binary search trees can be tricky to code and expensive to maintain.  However, we don’t always need a perfectly balanced tree.  We are often content with an approximation to the tree or a heuristic structure that mimics the balanced binary tree.




In this assignment, you will implement a data structure that has the structure of an unbalanced binary search tree, but that is designed to make searches for frequently accessed items happen quickly.




Problem

Write a class called “SearchTree” that accepts data values and then lets you search the list to see if a value is in the list.  The key part of the class is in the data structure that it uses to store the data.




At its core, the SearchTree is an unbalanced binary search tree.  New values are added to the bottom of the tree.  Values should only be stored in the tree once.




The important feature to the tree is in the search method.  In addition to searching for an item in the tree, we store the number of times that an item has been searched for previously.  When find the item, we compare the number of searches for the item with the number of searches for the parent.  If the item is searched for more than its parent then we move that item up one level in the tree and the parent goes down a level.  We elaborate on this action later in this assignment.




The set of methods are as follows:

<ul>

 <li>SearchTree( ) – constructor</li>

</ul>




<ul>

 <li>boolean add( String key ) – add the key to the tree. Return true if added.  Return false if already in the tree or some problem occurs.</li>

</ul>




<ul>

 <li>int find( String key ) – search for “key” in the tree. If found, return the depth of the node in the tree (with the root as depth 1).  If not found or if some error happens, return 0.</li>

</ul>




<ul>

 <li>void reset( ) – change all of the counters for searches in the tree to 0.</li>

</ul>




<ul>

 <li>String printTree( ) – create a string of the tree’s content. For each key in the tree (reported in sorted order), print the key, a space, and then the depth of the node in the tree.  Separate each key with a carriage return (
).  Return a null string if any error occurs.</li>

</ul>




<h2>Find operation</h2>

We find information that is closer to the root of the tree faster than information that is lower in the tree.  Our find method will move items that we search for frequently closer to the root of the tree so that we can find them more quickly in later searches.




Suppose that we have a node with key “egg” and a child node “carrot” (see Figure 2).  We have searched for “egg” twice and “carrot” once.  When we search for “carrot” again, we increment its count to having been searched for twice.  When we search for “carrot” one more time, its count now becomes 3, which is more than its parent “egg”, so we want to move “carrot” up the tree by one level.  Figure 2 shows how the tree is reshaped around this move.  A consequence of the reshaping is that the sibling of “carrot” and all its descendants become further from the root.




The case where the searched node is the right child of the parent is symmetric.




When we promote a node up the tree, we only move it one level at a time, even if its new parent has a search count that is smaller than the node.  This action is just for simplicity.

<em>Figure 2 sequence of “find” operations for “Carrot” that eventually shift the tree structure </em>

<em>Inputs </em>

All the inputs will be determined by the parameters used in calling your methods.




<em>Assumptions </em>

–     No special assumptions provided for this assignment.




<h2>Constraints</h2>

<ul>

 <li>You may <u>not</u> use any data structures from the Java Collection Framework, including ArrayLists.</li>

 <li>If in doubt for testing, I will be running your program on bluenose.cs.dal.ca. Correct operation of your program shouldn’t rely on any packages that aren’t available on that system.</li>

 <li>String comparisons should not be case sensitive.</li>

</ul>




<h2>Notes</h2>

<ul>

 <li>Start with some basic methods. Get add and search (without the changes to the data structure) working.</li>

 <li>Your nodes for the binary tree will likely benefit from having a reference to the parent node. The root of the tree will have a null value for its parent.</li>

 <li>Test cases</li>

</ul>

Input Validation

<ul>

 <li>Send a null string to the add method</li>

 <li>Send an empty string to the add method</li>

 <li>Send a null string to the add method</li>

 <li>Send a null string to the find method</li>

</ul>




Boundary Cases

<ul>

 <li>Add a string of 1 character</li>

 <li>Add a long string</li>

 <li>Find a string of 1 character</li>

 <li>Find a long string</li>

 <li>Reset an empty tree</li>

 <li>Reset a tree with 1 node</li>

 <li>Reset a big tree</li>

 <li>Print an empty tree</li>

 <li>Print a tree with 1 node</li>

 <li>Print a big tree</li>

</ul>




Control Flow Add

<ul>

 <li>Add to an empty tree</li>

 <li>Add to a tree with 1 node</li>

 <li>Add strings in alphabetical order</li>

 <li>Add strings in reverse alphabetical order</li>

 <li>Add a smallest string</li>

 <li>Add a largest string</li>

 <li>Add a string that forces each of the following search sequences:

  <ul>

   <li>Left child then left child o Left child then right child o Right child then left child o Right child then right child</li>

  </ul></li>

 <li>Add an item that is already in the tree</li>

</ul>




Find

<ul>

 <li>Find in an empty tree</li>

 <li>Find in a tree with 1 node</li>

 <li>Find the smallest string in the tree</li>

 <li>Find the largest string in the tree</li>

 <li>Find a middle string</li>

 <li>Search for an item that requires us to follow:

  <ul>

   <li>Left child then left child o Left child then right child o Right child then left child o Right child then right child</li>

  </ul></li>

 <li>Find an item that is in the tree</li>

 <li>Find an item that is not in the tree</li>

</ul>




Reset

<ul>

 <li>Covered under boundary cases</li>

</ul>




printTree

<ul>

 <li>Some covered under boundary cases</li>

 <li>Print a tree that is a linked list</li>

 <li>Print a tree that has many levels and has nodes with both right and left children</li>

</ul>




Data flow

<ul>

 <li>Call find before calling add (mentioned earlier for empty tree)</li>

 <li>Call reset before calling add (mentioned earlier for empty tree)</li>

 <li>Call printTree before calling add (mentioned earlier for empty tree)</li>

 <li>Call reset twice in a row</li>

 <li>Call find for a string not in the tree, add it to the tree, then find it again</li>

</ul>





