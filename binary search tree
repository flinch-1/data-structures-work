#include <stdio.h>
#include <stdlib.h>

// Structure for a binary tree node
struct TreeNode {
    int data;
    struct TreeNode* left;
    struct TreeNode* right;
};

// Function to create a new tree node
struct TreeNode* newNode(int data) {
    struct TreeNode* node = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Function to find index of value in inorder traversal
int findIndex(int arr[], int start, int end, int value) {
    for (int i = start; i <= end; i++) {
        if (arr[i] == value)
            return i;
    }
    return -1;
}

// Function to construct BST from inorder and postorder traversals
struct TreeNode* buildUtil(int in[], int post[], int inStart, int inEnd, int* postIndex) {
    if (inStart > inEnd)
        return NULL;

    struct TreeNode* node = newNode(post[*postIndex]);
    (*postIndex)--;

    if (inStart == inEnd)
        return node;

    int inIndex = findIndex(in, inStart, inEnd, node->data);

    node->right = buildUtil(in, post, inIndex + 1, inEnd, postIndex);
    node->left = buildUtil(in, post, inStart, inIndex - 1, postIndex);

    return node;
}

// Function to construct BST from inorder and postorder traversals
struct TreeNode* bst_construct(int in[], int post[], int n) {
    int postIndex = n - 1;
    return buildUtil(in, post, 0, n - 1, &postIndex);
}

// Function to print nodes of a binary tree in breadth-first-search (level order) traversal
void printLevelOrder(struct TreeNode* root) {
    if (root == NULL)
        return;

    // Create an empty queue for level order traversal
    struct Queue {
        struct TreeNode* data;
        struct Queue* next;
    } * front = NULL, * rear = NULL;

    // Enqueue root and initialize height
    struct TreeNode* temp = root;
    while (temp != NULL) {
        printf("%d ", temp->data);

        // Enqueue left child
        if (temp->left != NULL) {
            if (rear == NULL) {
                rear = (struct Queue*)malloc(sizeof(struct Queue));
                rear->data = temp->left;
                rear->next = NULL;
                front = rear;
            } else {
                rear->next = (struct Queue*)malloc(sizeof(struct Queue));
                rear = rear->next;
                rear->data = temp->left;
                rear->next = NULL;
            }
        }

        // Enqueue the right child
        if (temp->right != NULL) {
            if (rear == NULL) {
                rear = (struct Queue*)malloc(sizeof(struct Queue));
                rear->data = temp->right;
                rear->next = NULL;
                front = rear;
            } else {
                rear->next = (struct Queue*)malloc(sizeof(struct Queue));
                rear = rear->next;
                rear->data = temp->right;
                rear->next = NULL;
            }
        }

        // Dequeue the next node
        if (front != NULL) {
            temp = front->data;
            struct Queue* old = front;
            front = front->next;
            free(old);
        } else {
            temp = NULL;
        }
    }
}

int main() {
    // Input the data
    int inorder[] = {5, 10, 15, 20, 25, 30, 45};
    int postorder[] = {5, 15, 10, 25, 45, 30, 20};
    int n = sizeof(inorder) / sizeof(inorder[0]);

    // Construct BST
    struct TreeNode* root = bst_construct(inorder, postorder, n);

    // Print BST nodes in breadth-first-search traversal
    printf("Breadth-First-Search Traversal:\n");
    printLevelOrder(root);
    printf("\n");

    return 0;
}
