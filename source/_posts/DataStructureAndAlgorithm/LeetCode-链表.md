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

struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2) {
    if (l1 == NULL) return l2;
    if (l2 == NULL) return l1;

    struct ListNode *p1 = l1;
    struct ListNode *p2 = l2;

    struct ListNode *ret = NULL;
    struct ListNode **p = &ret;

    while (1) {
        if (p1 && p2) {
            if (p1->val <= p2->val) {
                *p = p1;
                p1 = p1->next;
            }
            else {
                *p = p2;
                p2 = p2->next;
            }
        }
        else if (p1 && p2 == NULL) {
            *p = p1;
            p1 = p1->next;
        }
        else if (p2 && p1 == NULL) {
            *p = p2;
            p2 = p2->next;
        }
        else break;

        p = &((*p)->next);
    }

    return ret;
}


~~~

3. 思路
   * 