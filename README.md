# 1.3-LinkedList-Assignment
Each of the assigned methods put into one program.


// Nathan McAnally
// 1.3.19, .20, .21, .24, .25, .26
// 28 JAN 2016 (Turned in on 29 JAN 2016)

// Node Class
public class Node<Item> {

	protected Item item;
	protected Node<Item> next;
	
	public Node() {
		item = null;
		next = null;
	}
	
	public Node(Item item, Node<Item> next) {
		this.item = item;
		this.next = next;
	}
	
	public void setNext(Node<Item> next) {
		this.next = next;
	}
}



// LinkedList Class
public class LinkedList<Item> extends Node<Item> {
	
	// LinkedList object
	private Node<Item> first;
	private int N;
	
	// Constructors
	public LinkedList() {
		first = null;
		N = 0;
	}

	public Node<Item> getFirst() {
		return first;
	}
	public int getSize() {
		return N;
	}	
	
	// Add a new node
	public void push(Item item) {
		Node<Item> newGuy = new Node<Item>();
		newGuy.item = item;
		newGuy.next = first;
		first = newGuy;
		N++;
	}
	
	// Remove a node from the front
	public Item pop() throws NullPointerException {
		if(first == null)
			throw new NullPointerException();
		Item item = (Item) first.item;
		first = first.next;
		N--;
		return item;
	}
	
	// Clear the entire list
	public void clear() {
		first = null;
		N = 0;
	}
	
	// View item at a given index
	public Item viewAt(int c) throws NullPointerException {
		if(N < c) 
			throw new NullPointerException();
		Node<Item> temp = first;
		for(int i = 0; i < c; i++) {
			temp = temp.next;
		}
		return temp.item;
	}
	
	// Return node at a given index
	public Node<Item> nodeAt(int c) throws NullPointerException {
		if(N < c) 
			throw new NullPointerException();
		Node<Item> temp = first;
		for(int i = 0; i < c; i++) 
			temp = temp.next;
		return temp;
	}
	
	// Boolean for if list has an element at the given index
	public boolean hasElementAt(int c) {
		if (N <= c)
			return false;
		else
			return true;
	}
	
	// Method taken from 1.3.21 to return index at first value
	public int indexAt(String myWord) throws Exception {
		if (find(myWord) == false)
			throw new Exception();
		Node<Item> temp = first;
		int i = 0;
		for(i = 0; i < N; i++){
			if( (temp.item).equals(myWord) ) 
				return i;
			else
				temp = temp.next;
		}
		return i;
	}
	
	///////// TEXTBOOK PROBLEMS START HERE //////////
	
	// Method to remove the last node (1.3.19)
	public void removeLast() throws Exception {
		if(first == null) 
			throw new Exception();
		Node<Item> temp = first;
		while(temp.next.next != null) 
			temp = temp.next;
		temp.next = null;
		N--;
	}
	
	// Method to remove kth node (1.3.20)
	public void removeKth(int k) throws Exception {
		if(first == null) 
			throw new Exception();
		Node<Item> temp = first;
		for(int i = 1; i < k; i++) {
			if (temp.next == null)
				throw new Exception();
			temp = temp.next;
		}
		temp.next = temp.next.next;
		N--;
	}
	
	// Method to find a given string (1.3.21)
	public boolean find(String myWord) throws Exception {
		if(first == null) 
			throw new Exception();
		Node<Item> temp = first;
		while(temp != null) {
			if( (temp.item).equals(myWord) ) 
				return true;
			else
				temp = temp.next;
		}
		return false;
	}
	
	// Method to remove the node following a given Node (1.3.24)
	public void removeAfter(Node<Item> myNode) throws Exception {
		if(myNode == null) 
			throw new Exception();
		myNode.next = myNode.next.next;
		N--;
	}
	
	// Method to insert a new given node after a given node (1.3.25)
	public void insertAfter(Node<Item> currentNode, Node<Item> newNode) {
		if(currentNode.next != null) {
			Node<Item> temp = currentNode;
			currentNode.next = newNode;
			newNode = temp;
		}
		else
			currentNode.next = newNode;
		N++;
	}
	
	// Method to remove all nodes with a given key (1.3.26)
	public void remove(String key) throws Exception {
		if(first == null) 
			throw new Exception();
		Node<Item> temp = first;
//		if ((temp.item).equals(key)) {
//			temp = temp.next;
//			N--;
//		}
		while(temp.next != null) {		
			if((temp.next.item).equals(key)) {
				temp.next = temp.next.next;
				N--;
			}
			else 
				temp = temp.next;
		}
	}
}




// Tester Class
public class Tester extends LinkedList<Object> {
	public static void main(String[] args) throws Exception {
		
		// Create a LinkedList and add items to it
		LinkedList<Object> list = new LinkedList<Object>();
		
		list.push(6.1);
		list.push(256);
		list.push('e');
		list.push("YOU ROCK!");
		
		System.out.println("Should be 4:   " + list.getSize() + "\n");
		
		// Print out what is currently in the array
		System.out.println("Should be YOU ROCK!      " + list.pop());
		System.out.println("Should be e      " + list.pop());
		System.out.println("Should be 256     " + list.pop());
		System.out.println("Should be 6.1      " + list.pop());
		
		System.out.println("\nShould be 0:   " + list.getSize() + "\n");
		
		// Refill array with new elements
		list.push("Horse");
		list.push("Giraffe");
		list.push("Elephant");
		list.push("Donkey");
		list.push("Crab");
		list.push("Bear");
		list.push("Alligator");
		
		// Show item at set index
		System.out.println("Should be Alligator     " + list.viewAt(0));
		System.out.println("Should be Donkey     " + list.viewAt(3));
		System.out.println("Should be Horse     " + list.viewAt(6));
		
		System.out.println("\nShould be 7:   " + list.getSize() + "\n");
		
		// Remove last element at index 6 Horse
		list.removeLast();
		System.out.println("\nShould be 6:   " + list.getSize() + "\n");
		System.out.println("Should be false:      " + list.hasElementAt(7) + "\n");
		
		// Remove element at index 2 "Crab"
		list.removeKth(2);
		System.out.println("Should be Bear:     " + list.viewAt(1));
		System.out.println("Should be Donkey:     " + list.viewAt(2));
		System.out.println("Should be Elephant:     " + list.viewAt(3));
		System.out.println("\nShould be 5:   " + list.getSize() + "\n");
		
		// Find a given String
		System.out.println("Should be false:      " + list.find("Crab"));
		System.out.println("Should be false:      " + list.find(";laksdjf"));
		System.out.println("Should be true:      " + list.find("Giraffe"));
		System.out.println("Should be true:      " + list.find("Elephant") + "\n");
		
		// Print current list
		System.out.println("Should be: Alligator, Bear, Donkey, Elephant, Giraffe");
		for(int i = 0; i < list.getSize(); i++) {
			System.out.println(list.viewAt(i));
		}
		System.out.println();
		
		// Remove node "Donkey"
		list.removeAfter(list.nodeAt(1));
		System.out.println("Should be: Alligator, Bear, Elephant, Giraffe");
		for(int i = 0; i < list.getSize(); i++) {
			System.out.println(list.viewAt(i));
		}
		System.out.println("\nShould be 4:   " + list.getSize() + "\n");
		
		// Add a node to make back to original
		list.insertAfter(list.nodeAt(list.indexAt("Bear")), new Node<Object>("Crab", list.nodeAt(2)));
		list.insertAfter(list.nodeAt(list.indexAt("Crab")), new Node<Object>("Donkey", list.nodeAt(3)));
		list.insertAfter(list.nodeAt(list.indexAt("Giraffe")), new Node<Object>("Horse", null));
		System.out.println("Should be: Alligator, Bear, Crab, Donkey, Elephant, Giraffe, Horse");
		for(int i = 0; i < list.getSize(); i++) {
			System.out.println(list.viewAt(i));
		}
		System.out.println("\nShould be 7:   " + list.getSize() + "\n");
		
		// Remove all nodes of "Bear"
		list.push("Bear");
		list.insertAfter(list.nodeAt(list.indexAt("Crab")), new Node<Object>("Bear", list.nodeAt(4)));
		list.insertAfter(list.nodeAt(list.indexAt("Horse")), new Node<Object>("Bear", null));
		System.out.println("Should be: Alligator, Bear, Crab, Bear, Donkey, Elephant, Giraffe, Horse, Bear");
		for(int i = 0; i < list.getSize(); i++) {
			System.out.println(list.viewAt(i));
		}
		System.out.println();
		// Now remove
		list.remove("Bear");
		System.out.println("Should be: Alligator, Crab, Donkey, Elephant, Giraffe, Horse");
		for(int i = 0; i < list.getSize(); i++) {
			System.out.println(list.viewAt(i));
		}
	}
}
