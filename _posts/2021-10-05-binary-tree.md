---
layout: post
title:  "Binary Search Tree in C"
author: "Jacob Brooker"
date:   2021-10-05 15:43:03 -0400
categories: jekyll update
post_description: This is a binary search tree coded in C, includes node creation, tree building, tree display, search for node, count nodes, and tree height functions.
---
<div>
	<p description="About Binary Trees">
	In this section I will discuss the creation of my Binary Search Tree (BST) Algorithm. A BST is best used to store data in organized way that allows for relatively quick search, insert, and deletes. Most commonly, BST can be used as quick index lookup tables.
	<br><br>
	One of the major benefits of the BST is the algorithmic complexity Big O notation of the various functions. As the BST is organized, the search function maintains an O(height) linear complexity while the delete and insert functions generally maintain a O(n complexity).
	</p>
</div>

<h3><br>Application Decomposition and Explanation</h3>

The appplication uses one struct as both the container for the data and the pointers to the child nodes.
~~~c++
typedef struct treeNode {
	int data;
	struct treeNode* pLeft;
	struct treeNode* pRight;
}TREENODE, *PTREENODE;
~~~

The first step in the application building the binary tree is to create a node. All nodes created by this function store a randomly generated int as the data, and set the children nodes to default.
~~~c++
PTREENODE createNewNode(void)
{
	PTREENODE newNode = (PTREENODE)malloc(sizeof(TREENODE));			// create a new node and malloc
	
	if (!newNode)
	{
		fprintf(stderr, "Failed to malloc newNode\n");
		exit(EXIT_FAILURE);
	}

	newNode->data = rand() % 100;										// random number generator of data
	newNode->pLeft = NULL;												// set left
	newNode->pRight = NULL;												// set right to null
	return newNode;
}
~~~

Within the main function, I call the create node function to make the root of the tree. To make the code more readable, I typedef a pointer to make the custom struct naed "root".
~~~c++
typedef struct treeNode* root;

root tree = createNewNode();	
~~~
To create the binary tree, we insert each node into the tree. To accomplish this, I decided to write the insert function through recursive calls to the left or right children.
~~~c++
void insert(PTREENODE currentNode, PTREENODE newNode)
{
	if (newNode->data < currentNode->data)								// is newNode data less than current node?
	{
		if (currentNode->pLeft == NULL)									// is the pointer to left of node empty?
			currentNode->pLeft = newNode;								// if it is then attach newNode to left of currentNode
		else
			insert(currentNode->pLeft, newNode);						// else call again with node to the left
	}
	else if (newNode->data > currentNode->data)							// is newNode data greater than current node?
	{
		if (currentNode->pRight == NULL)								// is the pointer to right of node empty?
			currentNode->pRight = newNode;								// attach newNode to right of node
		else
			insert(currentNode->pRight, newNode);						// else call again with node to the right
	}
}
~~~
Now I want to explain three functions I created with the Binary Tree. The first is the search for node function. Passed into this function is the pointer to the root of the tree, and the integer we are searching for. To create a more readable solution, the function is written as a recusive algorithm that will follow a path by comparing the search integer to the integer in the current node. If the search node is less than the node integer, we recursively call with the left child node. If the search node is greater than the current node integer, we recusrively call the search function with the right child node.
~~~c++
PTREENODE search(PTREENODE node, int searchNode)
{
	if (node == NULL) 
		return NULL;													// exit condition, search not found
	
	if (searchNode == node->data)										// search found, returning node
	{
		printf("Node searched %d, Node returned - ", searchNode);
		return node;
	}
	else if (searchNode < node->data)									// search int is lower than current node - move left
		search(node->pLeft, searchNode);
	else if (searchNode > node->data)									// search int is higher than current node - move right
		search(node->pRight, searchNode);

	
}
~~~
Next, I will demonstrate my function to count the number of nodes on the binary search tree. This function once again works on recursion. First we will follow the tree through the left (less than parent) child nodes. As we work our way back up, the right (greater than parent) child nodes are counted. Finally, we add one to account for the root of the tree.
~~~c++
int countNodes(PTREENODE node)
{
	if (node == NULL)													// if node is NULL then there is no list and return 0
		return 0; 
	return(countNodes(node->pLeft) + countNodes(node->pRight) + 1);		// recursively count the number of nodes to the left and to the right
}
~~~
Lastly, I would like to demonstrate the funciton to calculate the height of the binary search tree. This is an important function as the complexity of the BST can be determined by the height of the tree. This function works by recusively calculating the height of the left pathways, then recursively calculating the height of the right pathways. It then determines which path is the longest, adds one to account for root node, and then returns the greater of the two.
~~~c++
int treeHeight(PTREENODE node)
{
	int leftHeight = 0;
	int	rightHeight = 0; 
	int returnHeight = 0;

	if (node == NULL) 
		return returnHeight;											// no list, return 0
	
	leftHeight = treeHeight(node->pLeft);								// recursive call again left

	rightHeight = treeHeight(node->pRight);								// recursive call again right

	if (leftHeight > rightHeight)										// check which height is longer, left or right
		returnHeight = leftHeight + 1;									// return height of left, the +1 is to account for the head
	else
		returnHeight = rightHeight + 1;									// return height of right the +1 is to account for the head
	
	return returnHeight;												// return the height of the tree
}
~~~
<br>
<h3>Running the Application</h3>
 First, the application will conduct an inorder traversal of the tree. Next, the application calls the search function and returns the tree node. It then calculates the height of the tree, and the total number of nodes inside the tree.
 <br><br>
<img src="assets\img\programs\bst.PNG" height="300px">
<br><br>
<hr>

<h3><a href="https://github.com/Jacobpbrooker/binary_tree">You can find the GitHub Repo here!</a></h3>
<br>
If you have any questions at all, please do not hesitate to reach out. Thanks for reading!