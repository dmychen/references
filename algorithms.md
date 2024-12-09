# Algorithms  

## Graphs and Topological Sorting  

**Directed Acyclic Graph** (DAG): A directed graph with no directed cycles.  
- Each edge has an 'orientation' -> follow it in one direction.  
- Following an edge (arc) will never form a closed loop.  

#### Creating a linked list in Python  

1) Create a Node class for each node in the list.  

2) Build a list:  
- currentNode = rootNode  
- currentNode.next = a NewNode  
- currentNode = newNode.  

	# Define a node in your linked list.
	class Node:
		 def __init__(self, value):
				self.value = value
				self.next = None

	if __name__ == ‘__main__’:
		# Build a linked list
		root = Node(0)
		curr = root
		for num in range(1, 10):
			 curr.next = Node(num)
			 curr = curr.next

		# Traverse the linked list
		curr = root
		while curr is not None:
			 print(curr.value)
			 curr = curr.next

NOT DONE
