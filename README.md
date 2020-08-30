# leetcode 234 - Palindrome Linked List

## Approach: Using array and two pointers
```C#
public bool IsPalindrome(ListNode head)
{
    List<int> values = new List<int>();

    ListNode current = head;
    while (current != null)
    {
        values.Add(current.val);
        current = current.next;
    }

    int front = 0,
        back = values.Count - 1;
    while (front < back)
    {
        if (values[front] != values[back])
            return false;
        front++;
        back--;
    }

    return true;
}
```
#### Complexity Analysis
* Time Complexity: O(n)
* Space Complexity: O(n)

## Approach: Recursive 
```C#
private ListNode headPointer;

public bool IsPalindrome(ListNode head)
{
    headPointer = head;
    return RecursivelyCheckPalindrome(head);
}

private bool RecursivelyCheckPalindrome(ListNode current)
{
    if(current != null)
    {
        if (!RecursivelyCheckPalindrome(current.next))
            return false;
        if (current.val != headPointer.val)
            return false;
        headPointer = headPointer.next;
    }
    return true;
}
```
#### Complexity Analysis
* Time Complexity: O(n)
* Space Complexity: O(n), it creates n stack frame of O(1) space, hence O(n). 

## Approach: Reverse the second half in-place
```C#
public bool IsPalindrome(ListNode head)
{
    if (head == null || head.next == null) return true;

    // find the middle node
    ListNode slow = head;
    ListNode fast = head;
    while(fast != null && fast.next != null)
    {
        slow = slow.next;
        fast = fast.next.next;
    }

    // reverse the second part of the list
    ListNode midNode = ReverseList(slow);

    // palindrome check
    while(midNode != null)
    {
        if (head.val != midNode.val)
            return false;
        midNode = midNode.next;
        head = head.next;
    }
            
    return true;
}

private ListNode ReverseList(ListNode head)
{
    if (head == null) return null;
    ListNode revList = null;
    while (head != null)
    {
        ListNode temp = head.next;
        head.next = revList;
        revList = head;
        head = temp;

    }
    return revList;
}
```
#### Complexity Analysis
* Time Complexity: O(n)
* Space Complexity: O(1)
