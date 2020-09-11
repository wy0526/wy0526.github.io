---
date: 2020-07-29
categories: DataStructureAndAlgorithm
---

# 160.相交链表

1. 题目
   * 找到两个单链表相交的起始节点
   * [160.相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)


2. 思路

   * lenA+lenB' = lenB + lenA'

   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_07/39.png)

   * 每一次循环、整个过程如下

   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_07/40.png)

3. 代码

~~~c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode *getIntersectionNode(struct ListNode *headA, struct ListNode *headB) {

    struct ListNode *L1 = headA, *L2= headB;

    while(L1 != L2)

    {

        L1 = ((L1 == NULL) ? headB : L1->next);

        L2 = ((L2 == NULL) ? headA : L2->next);

    }

    return L1;

}
~~~

# 206.反转链表

1. 题目
   * 反转一个单链表
   * [206.反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

2. 代码

~~~c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

struct ListNode* reverseList(struct ListNode* head){
    struct ListNode *p, *pre = NULL;
    while(head)
    {
        p = head->next;
        head->next = pre;
        pre = head;
        head = p;
    }
    return pre;
}
~~~

3. 思路

   * 前两次循环结果如下

   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_07/42.png)

   * 前两次循环总图如下

   ![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_07/41.png)

# 21.合并两个有序链表

1. 题目
   * 将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。
   * [21.合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
2. 代码

~~~
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    if (!l1)
		return l2;
	if (!l2)
		return l1;
	struct ListNode* head = (struct ListNode*)malloc(sizeof(struct ListNode)), *t = head;
	while (l1 && l2){
		if (l1->val < l2->val){
			t->next = l1;
			l1 = l1->next;
		}			
		else{
			t->next = l2;
			l2 = l2->next;
		}			
		t = t->next;		
	}
	if (l1)      t->next = l1;
	else if (l2) t->next = l2;
	return head->next;
}
~~~

3. 思路

![](https://raw.githubusercontent.com/Rainbow0526/PictureGithub/master/2020_09/006.jpg)

# 83.删除排序链表中的重复元素

1. 题目
   * 给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次
   * [83.删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)
2. 代码

~~~
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
 
struct ListNode* deleteDuplicates(struct ListNode* head){
	if(head == NULL)//单链表为空，返回链表
		return head;
	struct ListNode *lp;
	struct ListNode *p = head;//指针指向单链表
	lp = p;//最后链表返回的位置
	while(p ->next != NULL){
		if(p -> val == p ->next -> val){
			p -> next = p -> next -> next;//删除后者节点，继续遍历
		}
		else{
			p = p -> next;
		}
	}
	return lp;
}
~~~

# 19. 删除链表的倒数第N个节点

1. 题目
   * 给定一个链表，删除链表的倒数第 *n* 个节点，并且返回链表的头结点
   *  [19. 删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
2. 代码

~~~
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
    if(!head || !head->next) 
            return NULL;
        int len = 1;
        struct ListNode *p = head;
        while(p->next)
        {
            len++;
            p = p->next;
        }
        p = head;
        int index = len - n - 1;
        // while((index --)&&p)
        //     p = p->next;
        for(int i = 1; i < len - n; i++)
            p = p->next;
        if(n == len)
            return head->next;
        if(n == 1)
            p->next = NULL;
        else
            p->next = p->next->next;
        return head;
}
~~~

