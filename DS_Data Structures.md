# Data Structures

1. Derived data types: list, array, stack, queue
2. Operations: traversing, searching, insertion, deletion, sorting, merging 

Operation | array | linkedlist | stack | queue
--- | --- | --- | --- | --- 
find | O(1) | O(n) | O(n) | O(n) 
size | O(1) | O(1) | O(1) | O(1)  
insert(not append) | O(n) | O(1) | O(1) | O(1) 
remove | O(n) | O(1) | O(1) | O(n) 
isEmpty | O(1) | O(1) | O(1) | O(1) 


## Array
Fixed length with elements of the same type  

## Linked List
1. Sequence of data structures connected via links  
2. Each Linkedlist contains a "first", each element has content and "next"  

### Single/Simple Linked List
1. Forward only  
2. All operations are O(1) except search/insert kth/remove tail (slow as it has to keep the tail pointer correct)/remove kth, which are O(N).

### Doubly linked List
1. Each vertex contains two links that refer to the previous and the next vertex.
2. All operations are O(1) except search/insert kth/remove kth, which are O(N). Notice that the remove tail operation is now O(1) in Doubly Linked List.

#### Circular Linked List

## Stack
1. Stack is an Abstract Data Type(ADT): a stack can be implemented by means of Linked List, Array  
2. Keep one pointer to head node  
3. Last-In-First-Out (LIFO)
4. push() pop() peek() isEmpty() isFull(): All operations are O(1)  

### LinkedList implementation
```java
public class LinkedListStack {
  private Node first = null;
  
  private class Node {
    String content;
    Node next;
  }
  
  public boolean isEmpty() { 
    return first == null; }

  public void push(String content) {
    Node oldfirst = first;
    first = new Node();
    first.content = content;
    first.next = oldfirst;
  }

  public String pop() {
    String content = first.content;
    first = first.next;
    return content;
  }
}
```

### Array implementation
```java
public class FlexibleArrayStack {
  private String[] s;
  private int N = 0;
  
  public FlexibleArrayStack(int capacity) { 
    s = new String[capacity];
  }
  
  public boolean isEmpty() { 
    return N == 0; 
  }
  
  public void push(String item) { 
    if (N == s.length) {
      resize(2 * s.length);
    }
    s[N++] = item; 
  }

  public String pop() { 
    String content = s[--N];  // avoid loitering
    s[N] = null;
    if (N > 0 && N = s.length/4)  // halve the array when it's one-quarter full
      resize(s.length/2);
    return content; 
  }
  
  public void resize(int capacity) {  // expensive operation, overall O(N)
     String[] copy = new String[capacity];
    for (int i = 0; i < N; i++) {
      copy[i] = s[i];
    s = copy;
  }
}
```

### LinkedList or Array?
1. Every operation in LinkedList always take constant time in the worst case, while in arrary it takes amortized time. Use LinkedList if EVERY operation has to be fast. Use array for better overall performance, as individual operation is faster.  
2. Array has better random access (O(1)) whereas LinkedList takes O(n). However, insertion and delete takes only O(1) in LinkedList but O(n) in array, unless to the end
3. LinkedList uses extra time and space  

## Queue
1. Queue is an Abstract Data Type(ADT): a queue can be implemented by means of Array, Structure, Pointer, and Linked List.   
2. Keep two pointers, head and tail
3. First-In-First-Out (FIFO)
4. enqueue() dequeue() peek() isEmpty() isFull(): All operations are still O(1) as we do not use the slow O(N) remove tail operation
5. Queue is basically a protected Single Linked List where we can only search for(peek) and remove from(dequeue) the head item and insert new item to the tail (enqueue)  

### LinkedList implementation
```java
public class LinkedListStack {
  private Node first = null;
  private Node last = null;
  
  private class Node {
    String content;
    Node next;
  }
  
  public boolean isEmpty() { 
    return first == null; }

  public void enqueue(String content) { // same as stack
    Node oldLast = last;
    last = new Node();
    last.content = content;
    last.next = null;
    if (isEmpty())
      first = last;
    else
      oldLast.next = last;
    
  }

  public String dequeue() {
    String content = first.content;
    first = first.next;
    if (isEmpty())
      last = null;
    return content;
  }
}
```

### Double-ended Queue (Deque)
1. Add or remove from either head or tail. Basically a protected Doubly-linked List.
2. All operations are O(1).

##### Question 1: What are the computational complexity of these structures?
##### Question 2: In which of these structures, edges are directed? Which are not?








## Java Implementation
Linkedlist class
```
/**
 * This class implements a doubly linked list of characters in Java. The
 * instance variables head and tail are initially null. As elements are added
 * head points to the first element on the list and tail points to the last
 * element. Each node on the list is of type DoubleNode. Each DoubleNode holds a
 * pointer to the previous node and a pointer to the next node in the list.
 * 
 * @author Phoenix
 *
 */
public class DoublyLinkedList {

	private int n = 0; // Number of nodes in the list
	private DoubleNode head = null; // Head node of the list
	private DoubleNode tail = null; // Tail node of the list

	/**
	 * Constructs a new DoublyLinkedList object with head and tail as null.
	 */
	public DoublyLinkedList() {
		// Head and tail are already set to null
	}

	/**
	 * Test driver for DoublyLinkedList.
	 * 
	 * @param args
	 */
	public static void main(String args[]) {
		// Already implemented in DoubleNode.java
	}

	/**
	 * Add a character node containing the character c to the end of the linked
	 * list. This routine does not require a search.
	 * 
	 * Precondition: parameter is an uppercase or lowercase letter (in the range 'A' ... 'Z' or 'a' ... 'z').
	 * Postcondition: a new node with char the same as the parameter will be created and placed at the end of the list. 
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @param c
	 *            a single character.
	 */
	public void addCharAtEnd(char c) {
		DoubleNode newTail = new DoubleNode(tail, c, null);
		if (tail == null) {
			tail = newTail;
			head = newTail;
		}
		else {
			tail.setNext(newTail);
			tail = newTail;
		}
		n++;
	}

	/**
	 * Add a character node containing the character c to the front of the
	 * linked list. No search is required.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * Precondition: parameter is an uppercase or lowercase letter (in the range 'A' ... 'Z' or 'a' ... 'z').
	 * Postcondition: a new node with BigInteger the same as the parameter will be created and placed at the beginning of the list. 
	 * 
	 * @param c
	 *            a single character.
	 */
	public void addCharAtFront(char c) {
		DoubleNode newHead = new DoubleNode(null, c, head);
		if (head == null) {
			head = newHead;
			tail = newHead;
		}
		else {
			head.setPrev(newHead);
			head = newHead;
		}
		n++;
	}

	/**
	 * Counts the number of nodes in the list. We are not maintaining a counter
	 * so a search is required.
	 * 
	 * Postcondition: return the int value of the number of nodes in the list. 
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return the number of nodes in the doubly linked list between head and
	 *         tail inclusive.
	 */
	public int countNodes() {
		return n;
	}

	/**
	 * Deletes the first occurence of the character c from the list. If the
	 * character c is not in the list then no modifications are made. This
	 * method needs to search the list.
	 * 
	 * Precondition: parameter is an uppercase or lowercase letter (in the range 'A' ... 'Z' or 'a' ... 'z').
	 * Postcondition: the first node that has the value the same as the parameter would be removed from the list.
	 * 
	 * Time complexity: Best case Θ(1), worst case No case Θ(n)
	 * 
	 * @param c
	 *            the character to be searched for.
	 * @return true if a deletion occurred and false otherwise.
	 */
	public boolean deleteChar(char c) {
		DoubleNode dummy = head;
		for (int i = n; i > 0; i--) {
			if (dummy.getC() == c) {
				if (n == 1) { // If the list has only one element
					head = null;
					tail = null;
				} else if (i == n) { // If the first element matches the char
					head = head.getNext();
					head.setPrev(null);
				} else if (i == 1) { // If the last element matches the char
					tail = tail.getPrev();
					tail.setNext(null);
				} else { // If an element in middle matches the char
					dummy.getNext().setPrev(dummy.getPrev());
					dummy.getPrev().setNext(dummy.getNext());
				}
				n--;
				return true;
			}
			dummy = dummy.getNext();
		}
		return false;

	}

	/**
	 * Returns true if the list is empty false otherwise.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return true if the list empty false otherwise.
	 */
	public boolean isEmpty() {
		return n == 0;
	}

	/**
	 * Remove and return the character at the end of the doubly linked list. No
	 * searching is required.
	 * 
	 * Postcondition: remove the last node (if not null) from the list.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return the character at the end precondition: the list is not empty.
	 */
	public char removeCharAtEnd() {
		char removed = '\u0000';
		if (tail != null) {
			removed = tail.getC();
			tail = tail.getPrev();
			n--;
			if (n == 0) {  // Removed the only node, head should be null, too
				head = null;
			}
			else { 
				tail.setNext(null);
			}
		}
		return removed;
	}

	/**
	 * Remove and return the character at the front of the doubly linked list.
	 * 
	 * Postcondition: remove the first node (if not null) from the list. 
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return the character at the front precondition: the list is not empty.
	 */
	public char removeCharFromFront() {
		char removed = '\u0000';
		if (head != null) {
			removed = head.getC();
			head = head.getNext();
			n--;
			if (n == 0) { // Removed the only node, tail should be null, too
				tail = null;
			}
			else { 
				head.setPrev(null);
			}
			
		}
		return removed;
	}

	/**
	 * Reverse the list. a -> b -> c becomes c -> b -> a
	 * 
	 * Postcondition: reverse the order of the list if there are more than two nodes. Otherwise, no changes. 
	 * 
	 * Time complexity: No case Θ(n)
	 */
	public void reverse() {
		head = tail;
		while (true) {
			DoubleNode dummy = tail.getPrev();
			tail.setPrev(tail.getNext());
			tail.setNext(dummy);
			if (dummy == null)
				break;
			tail = dummy;
		}

	}

	@Override
	/**
	 * Returns the list as a String. The class DoubleNode has a toString that
	 * will be called from this toString. The String returned must be presented
	 * clearly. Null pointers must be represented differently than non-null
	 * pointers.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return a String containing the characters in the list.
	 */
	public String toString() {
		DoubleNode dummy = head;
		StringBuilder sb = new StringBuilder();
		while (dummy != null) {
			sb.append(dummy.getC() + "");
			dummy = dummy.getNext();
		}
		return sb.toString();
	}

}
```

list node class  
```
import homework1_q1.DoubleNode;
import homework1_q1.DoublyLinkedList;

/**
 * The class DoubleNode holds two pointers and a character. It is used to
 * represent a single node on a double linked list.
 * 
 * @author Phoenix
 *
 */
public class DoubleNode {

	private char ch = '\u0000'; // char value of this node
	private DoubleNode next = null; // the next node
	private DoubleNode prev = null; // the previous node

	/**
	 * Constructor with no arguments. Assign null values to previous, next and
	 * the null character to c.
	 */
	public DoubleNode() {
		// Previous and next are already set to null
	}

	/**
	 * A constructor takes in the previous and the next nodes and also char
	 * value of this node.
	 * 
	 * @param p
	 *            is a pointer to a previous node.
	 * @param ch
	 *            is a character for this node.
	 * @param n
	 *            is a pointer to a next node.
	 */
	public DoubleNode(DoubleNode p, char ch, DoubleNode n) {
		this.prev = p;
		this.ch = ch;
		this.next = n;
	}

	/**
	 * Test driver for DoubleNode
	 * 
	 * @param a
	 */
	public static void main(String a[]) {

		DoublyLinkedList list = new DoublyLinkedList();
		list.addCharAtEnd('H');
		list.addCharAtEnd('e');
		list.addCharAtEnd('l');
		list.addCharAtEnd('l');
		list.addCharAtEnd('o');
		System.out.println(list);
		System.out.println("Deleting l");
		list.deleteChar('l');
		System.out.println(list);
		System.out.println("Deleting H");
		list.deleteChar('H');
		System.out.println(list);
		System.out.println("Deleting o");
		list.deleteChar('o');
		System.out.println(list);
		System.out.println("Deleting e");
		list.deleteChar('e');
		System.out.println(list);
		System.out.println("Deleting l");
		list.deleteChar('l');
		System.out.println(list);
		list.addCharAtFront('o');
		list.addCharAtFront('l');
		list.addCharAtFront('l');
		list.addCharAtFront('e');
		list.addCharAtFront('H');
		System.out.println(list);

		System.out.println(list.countNodes());

		System.out.println("Popping everything");
		while (!list.isEmpty()) {
			System.out.println(list.removeCharFromFront());
		}

		list.addCharAtFront('o');
		list.addCharAtFront('l');
		list.addCharAtFront('l');
		list.addCharAtFront('e');
		list.addCharAtFront('H');

		System.out.println("Popping everything from the end");
		while (!list.isEmpty()) {
			System.out.println(list.removeCharAtEnd());
		}
		System.out.println(list.countNodes());

		list.addCharAtEnd('o');
		list.addCharAtEnd('l');
		list.addCharAtEnd('l');
		list.addCharAtEnd('e');
		list.addCharAtEnd('H');

		list.reverse();
		System.out.println(list);

		list.reverse();
		System.out.println(list);

		DoublyLinkedList list2 = new DoublyLinkedList();
		list2.addCharAtEnd('O');
		list2.addCharAtEnd('K');
		list2.reverse();
		System.out.println(list2);
		System.out.println(list2.countNodes());
	}

	/**
	 * Get the char value of this node.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return current char value of this node.
	 */
	public char getC() {
		return this.ch;
	}

	/**
	 * Set the char value of this node.
	 * 
	 * Precondition: parameter is an uppercase or lowercase letter (in the range
	 * 'A' ... 'Z' or 'a' ... 'z'). 
	 * Postcondition: the char value of this node
	 * would be set to the parameter value.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @param ch
	 *            char assigned to this node.
	 */
	public void setC(char ch) {
		this.ch = ch;
	}

	/**
	 * Get next node.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return a pointer to the next node or null if none exists
	 */
	public DoubleNode getNext() {
		return this.next;
	}

	/**
	 * Set next node.
	 * 
	 * Precondition: parameter is an instance of DoubleNode class or null. 
	 * Postcondition: the next node of the current node would be the parameter value.  
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @param next
	 *            the intended node to be set.
	 */
	public void setNext(DoubleNode next) {
		this.next = next;
	}

	/**
	 * Get previous node.
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @return a pointer to the previous node or null if none exists
	 */
	public DoubleNode getPrev() {
		return this.prev;
	}

	/**
	 * Set previous node.
	 * 
	 * Precondition: parameter is an instance of DoubleNode class or null. 
	 * Postcondition: the previous node of the current node would be the parameter value.  
	 * 
	 * Time complexity: No case Θ(1)
	 * 
	 * @param prev
	 *            the intended node to be set.
	 */
	public void setPrev(DoubleNode prev) {
		this.prev = prev;
	}

	@Override
	/**
	 * Return the char value of this node.
	 * 
	 * @return a String containing the characters in the node.
	 */
	public String toString() {
		return this.ch + "";
	}
}
```
