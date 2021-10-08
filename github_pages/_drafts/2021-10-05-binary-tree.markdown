---
layout: post
title:  "Binary Tree in C"
date:   2021-10-05 15:43:03 -0400
categories: jekyll update
post_description: This is a binary tree coded in C, includes node creation, tree building, tree display, search for node, count nodes, and tree height functions.
---
 What is a binary tree

 Why do we use a binary tree

 Benefits of writing a bin tree in C

<h3>Application Decomposition and Explanation</h3>

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
Now I want to explain three functions I created with the Binary Tree. The first 
~~~c++

~~~
<br>
<h3>Running the Application</h3>
 
<img src="/assets/img/programs/btree.png" height="500px">
<br><br>
<hr>

<h3><a href="https://github.com/Jacobpbrooker/">You can find the GitHub Repo here!</a></h3>
<br>
If you have any questions at all, please do not hesitate to reach out. Thanks for reading!