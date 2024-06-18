#include <iostream>
#include <string> // Include string for string handling

using namespace std;

struct Product {
    int id;
    string name;
    string color;
    int size;
    int price;
    int quantity;
    Product* previous;
    Product* next;
};

Product* head = null; // Initialize head pointer to avoid potential errors

// Function to add a new product at the front of the list
void addToFront(int id, string name, string color, int size, int price, int quantity) {
    Product* newNode = new Product;
    newNode->id = id;
    newNode->name = name;
    newNode->color = color;
    newNode->size = size;
    newNode->price = price;
    newNode->quantity = quantity;
    newNode->previous = null;

    if (head == nullptr) {
        newNode->next = nullptr;
        head = newNode;
    } else {
        newNode->next = head;
        head->previous = newNode;
        head = newNode;
    }
}

// Function to add a new product at the back of the list
void addToBack(int id, string name, string color, int size, int price, int quantity) {
    Product* newNode = new Product;
    newNode->id = id;
    newNode->name = name;
    newNode->color = color;
    newNode->size = size;
    newNode->price = price;
    newNode->quantity = quantity;
    newNode->next = null;

    if (head == nullptr) {
        newNode->previous = nullptr;
        head = newNode;
        return;
    }

    Product* last = head;
    while (last->next != nullptr) {
        last = last->next;
    }

    last->next = newNode;
    newNode->previous = last;
}

// Function to sort the list by price using bubble sort
void bubbleSortPrice() {
    if (head == null || head->next == null) {
        return;
    }

    bool swapped;
    do {
        swapped = false;
        Product* current = head;

        while (current->next != null) {
            Product* next = current->next;
            if (current->price > next->price) {
                // Swap nodes by adjusting the pointers
                if (current->previous != nullptr) {
                    current->previous->next = next;
                } else {
                    head = next;
                }
                next->previous = current->previous;

                current->next = next->next;
                if (next->next != nullptr) {
                    next->next->previous = current;
                }
                next->next = current;
                current->previous = next;

                swapped = true;
            } else {
                current = current->next;
            }
        }
    } while (swapped);
}

// Function to print the list of products
void printList() {
    Product* current = head;
    while (current != null) {
        cout << "ID: " << current->id << ", Name: " << current->name << ", Color: " << current->color
             << ", Size: " << current->size << ", Price: " << current->price << ", Quantity: " << current->quantity << endl;
        current = current->next;
    }
}

int main() {
    addToFront(1, "Shirt", "Blue", 10, 20, 5);
    addToBack(2, "Pants", "Black", 32, 30, 3);
    addToFront(3, "Hat", "Red", 7, 15, 10);

    cout << "Original list:" << endl;
    printList();

    bubbleSortPrice();

    cout << "List sorted by price:" << endl;
    printList();

    return 0;
}
