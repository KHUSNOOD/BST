#include<iostream>
using namespace std;

// Structure for a node of the binary search tree
struct node {
    int key;
    struct node* lchild;
    struct node* rchild;
};

// Function to create a new node with the given key
struct node* create(int key) {
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    newnode->key = key;
    newnode->lchild = newnode->rchild = NULL;
    return newnode;
}

// Function to insert a new node with the given key into the BST
struct node* insert(struct node* root, int key) {
    // If the tree is empty, return a new node
    if (root == NULL) {
        return create(key);
    }

    // Otherwise, recur down the tree
    if (key < root->key) {
        root->lchild = insert(root->lchild, key);
    } else if (key > root->key) {
        root->rchild = insert(root->rchild, key);
    }

    // Return the unchanged node pointer
    return root;
}

// Function to search for a key in the BST
struct node* search(struct node* root, int key) {
    // Base Cases: root is null or key is present at the root
    if (root == NULL || root->key == key) {
        return root;
    }

    // Key is greater than root's key
    if (root->key < key) {
        return search(root->rchild, key);
    }

    // Key is smaller than root's key
    return search(root->lchild, key);
}

// Function to perform inorder traversal of the BST
void inorderTraversal(struct node* root) {
    if (root != NULL) {
        inorderTraversal(root->lchild);
        printf("%d ", root->key);
        inorderTraversal(root->rchild);
    }
}

int main() {
    struct node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    printf("Inorder traversal of the BST: ");
    inorderTraversal(root);
    printf("\n");

    int key = 60;
    struct node* searchResult = search(root, key);
    if (searchResult != NULL) {
        printf("Key %d found in the BST\n", key);
    } else {
        printf("Key %d not found in the BST\n", key);
    }

    return 0;
}
