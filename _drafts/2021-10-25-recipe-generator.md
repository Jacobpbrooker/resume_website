---
layout: post
title:  "Restaurant and Recipe display in C"
date:   2021-10-25 15:43:03 -0400
categories: jekyll update
post_description: This is a Restaurant and Recipe selector console based application. This application is written in C.
---
Recipedia (no affiliation with the wiki variety) is a console application written in C for a practical project course as part of the BCS. For Recipedia I developed the data structures, linked lists, data reading, and data writing.

I wanted to develop a file system that would allow each restaurant to have its own folder logically separated in its own file path. Inside each restaurant I wanted to have separate text files that would each contain separate information. One text file for the restaurant information, one text file that contained the ingredients for the restaurants specialty menu item, and one text file that contained the instructions for cooking the specialty menu item. 

This way, as the restaurant list changes, or decides to switch specialty entree's the file paths do not need to be changed. Only the information inside the text file would need to be updated.

To accomplish this task, each restaurant was saved in a linked list format, with each node in the linked list acting as the head of a queue for the ingredients, and the head of the queue for the instructions as well.

<h3>Application Decomposition and Explanation</h3>
First, I will go over the custom structures that are used in the Recipedia! project that I created.

The restaurant structure is the heart of the Recipedia! application.
~~~c++
typedef struct restaurant {		// restaurants will be stored individually in a linked list, with pointers to head of linked lists ingredients and instructions
	char* restaurantName;		// name of the restaurant
	char* headChef;			// name of the head chef of the restaurant
	char* restaurantSypnopsis;	// brief sypnopsis including location and awards, maybe famous people who have dined there - basically fun facts
	char specialityMenu[MENUSIZE][MAXSTRINGLENGTH];		// multi dimensional array for 3 specialty items (char array for each)
	struct ingredientQueue* ingredientQueueHead;		// pointer to ingredient linked list
	struct instructionQueue* instructionQueueHead;		// pointer to instruction linked list
} RESTAURANT, * PRESTAURANT;
~~~

The code being loaded by text files and switching text files.

<h3>Running the Application</h3>
**replace**First, the application will conduct an inorder traversal of the tree. Next, the application calls the search function and returns the tree node. It then calculates the height of the tree and the total number of nodes inside the tree.
**replace**
<br><br>
<img src="/assets/img/programs/bst.png" height="300px">
<br><br>
<hr>

<h3><a href="https://github.com/Jacobpbrooker/binary_tree">You can find the GitHub Repo here!</a></h3>
<br>
If you have any questions at all, please do not hesitate to reach out. Thanks for reading!
