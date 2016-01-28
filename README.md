# 1.3-LinkedList-Assignment
Each of the assigned methods put into one program.



// Nathan McAnally
// 1.3.19, .20, .21, .24, .25, .26
// 28 JAN 2016

// Node Class
public class Node<Item> {

	protected Item item;
	protected Node next;
	protected Node first;
	
	public Node() {
		item = null;
		next = null;
		first = null;
	}
	
	public Node(Item item, Node next, Node first) {
		this.item = item;
		this.next = next;
		this.first = first;
	}
}



// LinkedList Class
public class LinkedList<Item> extends Node<Item> {
	
	// LinkedList object
	private LinkedList<Item> list;
	private int N;
	
	// Constructors
	public LinkedList() {
		list = null;
		N = 0;
	}
	public LinkedList(LinkedList<Item> list, int N) {
		this.list = list;
		this.N = N;
	}
	
	// Add a new node
	public void push(Item item) {
		Node newGuy = new Node();
		newGuy.item = item;
		newGuy.next = first;
		first = newGuy;
		N++;
	}
	
	// Remove a node from the front
	public Item pop() throws Exception {
		if(first == null)
			throw new Exception();
		Item item = (Item) first.item;
		first = first.next;
		N--;
		return item;
	}
	
	// Method to remove the last node (1.3.19)
	public void removeLast() throws Exception {
		if(first == null) 
			throw new Exception();
		Node temp = first;
		while(temp.next.next != null) 
			temp = temp.next;
		temp.next = null;
		N--;
	}
	
	// Method to remove kth node (1.3.20)
	public void removeKth(int k) throws Exception {
		if(first == null) 
			throw new Exception();
		Node temp = first;
		for(int i = 1; i < k; i++) {
			if (temp.next == null)
				throw new Exception();
			temp = temp.next;
		}
		temp.next = temp.next.next;
		N--;
	}
	
	// Method to find a given string (1.3.21)
	public boolean find(LinkedList<Item> myList, String myWord) throws Exception {
		if(myList.first == null) 
			throw new Exception();
		Node temp = myList.first;
		while(temp.next != null) {
			if( (temp.item).equals(myWord) ) 
				return true;
			else
				temp = temp.next;
		}
		return false;
	}
	
	// Method to remove the node following a given Node (1.3.24)
	public void removeAfter(Node myNode) throws Exception {
		if(myNode == null) 
			throw new Exception();
		myNode.next = myNode.next.next;
		N--;
	}
	
	// Method to insert a new given node after a given node (1.3.25)
	public void insertAfter(Node currentNode, Node newNode) {
		if(currentNode.next != null) {
			Node temp = currentNode;
			currentNode.next = newNode;
			newNode.next = temp.next;
		}
		else
			currentNode.next = newNode;
		N++;
	}
	
	// Method to remove all nodes with a given key (1.3.26)
	public void remove(LinkedList<Item> myList, String key) throws Exception {
		if(myList.first == null) 
			throw new Exception();
		Node temp = myList.first;
		while(temp.next != null) {			
			if((temp.next).equals(key)) {
				temp.next = temp.next.next;
				N--;
			}
		}
	}
}
