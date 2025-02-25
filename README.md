#include <stdio.h>
#include <stdlib.h>
struct Node{
    int data;
    struct Node *next;
};
struct Node *create_Node(int data){
    struct Node *newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}
struct Node *detect_the_loop(struct Node *head){
    struct Node *slow = head, *fast = head;
    while(fast != NULL && fast->next != NULL){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast){
            break;
        }
    }
    if(fast == NULL || fast->next == NULL)
        return NULL;
        
        slow = head;
        while(slow != fast){
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
}
int main()
{
    struct Node *head = create_Node(1);
    head->next = create_Node(4);
   head->next->next = create_Node(7);
   head->next->next ->next = create_Node(10);
     head->next->next ->next->next = create_Node(13);
    head->next->next ->next->next ->next = head->next;
    struct Node* loopNode = detect_the_loop(head);
    if(loopNode){
        printf("First node of loop is: %d\n", loopNode->data);
    }
    else{
        printf("No loop is detected\n.");
    }
    
    return 0;
    
}
