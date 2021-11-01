---
layout: post
title:  "Simple Queue Algorithm in C"
date:   2021-10-04 15:43:03 -0400
author: Jacob Brooker
categories: jekyll update
post_description: A simple Queue algorithm using Patients in a doctors office as an example. Includes queue creation, filling, and dequeuing. This application is written in C.
---
A queue created in C is a form of abstract data type that can be created using a linked list format. The signature property of the queue created by me is that data structures can only be added or deleted from the head or tail of the queue. Inserting into the queue is not allowed. This gives the big O notation of O(1) for inserting and deleting, with a linear search notation of O(n). 

<h3>Application Decomposition and Explanation</h3>

The application uses three structs as part of the data storage. The first is a simple patient struct that contains the age and ID number. The next struct makes the individual node of the queue. Each of these nodes contains a single patient, and a pointer to the next node in the queue. The final struct used in the application stores the head and tail of the queue. This allows for forward and reverse traversal of the queue.
~~~c++
typedef struct patient {
	int patientNumber;
	int age;
}PATIENT, * PPATIENT;

typedef struct node {
	struct patient* patientData;
	struct node* pNext;
}NODE, * PNODE;

typedef struct queue {
	struct node* head;
	struct node* tail;
}QUEUE, * PQUEUE;
~~~

First, I needed to create a patient. I used a random number generator to assign a number. To store the patient information inside the patient struct, I allocated memory, and then filled that memory with the randomly generated number. I used the generated patient and created a node.

~~~c++
PPATIENT createPatient()
{
	PPATIENT patient;                                       // create pointer to patient 

	if (!(patient = (PPATIENT)malloc(sizeof(PATIENT))))	    // malloc the size of patient at the pointer to patient
	{
		fprintf(stderr, "Failed to allocate memory for patient - Now Exiting\n");
		exit(EXIT_FAILURE);
	}

	patient->age = rand() % 99;		                        // assign random age 0 - 99 to patient
	patient->patientNumber = (rand() % RAND_MAX + 10000)	// assign random 9 digit patient ID
		* (rand() % 5000 + 10000);

	return patient;											// return the pointer to patient
}

PNODE createPatientNode()
{
	PNODE node;	// create node pointer

	if (!(node = (PNODE)malloc(sizeof(NODE))))// malloc the size of node at the pointer to node location
	{
		fprintf(stderr, "Failed to allocate memory for queue - Now Exiting\n");
		exit(EXIT_FAILURE);
	}

	memset(node, '\0', sizeof(NODE));	// set the malloc(ed?) memory to '\0'

	node->patientData = createPatient();	// create/assign patient to node
	// node->pNext intentially left unassigned to be assigned in enqueue function
	return node;				// return the new patient node with created patient
}
~~~

Next I needed to create a function that would enqueue the newly created node, successfully pushing the nodes in a singly linked list.

~~~c++
bool enqueue(PQUEUE queue, PNODE node)  
{
	bool returnBool = false;	// set return bool

	if (queue->head == NULL)
	{
		queue->head = node;		// if the head of the queue is null set the head to this node
		queue->tail = node;		// then set the tail to the same location in the queue
		returnBool = true;		// set the return bool to true
	}
	else
	{
		queue->tail->pNext = node;	// if there is a head in the queue we set the queue tail next to the node
		queue->tail = node;			// set the queue tail to the node
		returnBool = true;			// set the return bool to true
	}

	queue->tail->pNext = NULL;  // set the queue tail pNext to NULL with each interation  	

	return returnBool;			// return bool
}
~~~
Next, we are going to look at the traversal functions. To move through the queue, I chose to use a recursive function that looked through the queue front to back, and had a separate recursive function that moved back to front.
~~~c++
void traverse(PQUEUE queue)									// pass the queue to a traversal function
{
	recursiveTraverse(queue->head);							// head of queue is passed to regular traversal (front to back)
}

PNODE recursiveTraverse(PNODE patientNode)
{
	simpleDisplayPatient(patientNode->patientData);			// display patient information to terminal

	if (patientNode->pNext == NULL)							// check if pNext is NULL (this will be the final item in queue)
	{
		return patientNode;									// if it is the final item, return and begin unwinding recursive function
	}
	else
	{
		recursiveTraverse(patientNode->pNext);				// if it is not the last node in the list, pass the next node into function and repeat
	}
}

void reverseTraverse(PQUEUE queue)							// pass the queue to a reverse traversal function
{
	reverseRecursiveTraverse(queue->tail);					// tail of queue is passed to reverse traversal function (back to front)
}

void reverseRecursiveTraverse(PNODE patientNode)
{
	simpleDisplayPatient(patientNode->patientData);			// display patient information to terminal
	if (patientNode->pPrevious == NULL)
	{														// check if pPrevious is NULL (this will be the first item in queue)
		return patientNode;
	}														// if it is the first item, return and begin unwinding recursive function
	else
	{
		reverseRecursiveTraverse(patientNode->pPrevious);	// if it is not the first node in the list, pass the previous node into function and repeat
	}														
}
~~~

The final function created for this application is a dequeue function. This takes the patient at the head of the queue (singly linked list) and pops the node off.
~~~c++
void dequeue(PQUEUE queue)
{
	simpleDisplayPatient(queue->head->patientData);			// dispay the patient
	
	QUEUE tempQUEUE;										// create a temporary copy of the queue

	tempQUEUE.head = queue->head->pNext;					// assign the head of temporary queue to the pNext of queue head
	freeNode(queue->head);									// free the node
	queue->head = tempQUEUE.head;							// set the head of the queue to the head of the temporary queue
}
~~~
<br>
<h3>Running the Application</h3>
The main function of the application accepts a command line argument for the number of patients that will be created by the system. In this example, I instructed the application to create 5 patients, enqueue these nodes, traverse the code forwards and backwards, and then dequeue these patient nodes to end the program.

<img src="{{site.url}}{{ site.baseurl }}/assets/img/queue.png" height="500px">
<br><br>
<hr>

<h3><a href="https://github.com/Jacobpbrooker/simple_queue">You can find the GitHub Repo here!</a></h3>
<br>
If you have any questions at all, please do not hesitate to reach out. Thanks for reading!