#include <iostream>
using namespace std;
 
class Deque {
private:
    int* arr;
    int front, back, capacity;
 
public:
    // Constructor to initialize deque with a given capacity
    Deque(int cap) {
        capacity = cap;
        arr = new int[capacity];
        front = -1;
        back = -1;
    }
 
    // Destructor to free memory
    ~Deque() {
        delete[] arr;
    }
 
    // Function to check if the deque is empty
    bool isEmpty() {
        return front == -1;
    }
 
    // Function to check if the deque is full
    bool isFull() {
        return (front == 0 && back == capacity - 1) || (front == back + 1);
    }
 
    // Function to add element at the front
    void addFront(int value) {
        if (isFull()) {
            cout << "Deque is full!" << endl;
            return;
        }
        if (front == -1) { // If deque is empty
            front = back = 0;
        } else if (front == 0) {
            front = capacity - 1; // Wrap around
        } else {
            front--;
        }
        arr[front] = value;
        cout << "Added " << value << " at the front." << endl;
    }
 
    // Function to add element at the back
    void addBack(int value) {
        if (isFull()) {
            cout << "Deque is full!" << endl;
            return;
        }
        if (back == -1) { // If deque is empty
            front = back = 0;
        } else if (back == capacity - 1) {
            back = 0; // Wrap around
        } else {
            back++;
        }
        arr[back] = value;
        cout << "Added " << value << " at the back." << endl;
    }
 
    // Function to delete element from the front
    void deleteFront() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return;
        }
        cout << "Deleted " << arr[front] << " from the front." << endl;
        if (front == back) { // Only one element
            front = back = -1;
        } else if (front == capacity - 1) {
            front = 0; // Wrap around
        } else {
            front++;
        }
    }
 
    // Function to delete element from the back
    void deleteBack() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return;
        }
        cout << "Deleted " << arr[back] << " from the back." << endl;
        if (front == back) { // Only one element
            front = back = -1;
        } else if (back == 0) {
            back = capacity - 1; // Wrap around
        } else {
            back--;
        }
    }
 
    // Function to display elements in the deque
    void display() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return;
        }
        cout << "Deque elements: ";
        int i = front;
        while (i != back) {
            cout << arr[i] << " ";
            i = (i + 1) % capacity; // Wrap around
        }
        cout << arr[back] << endl;
    }
};
 
int main() {
    int capacity, choice, value;
 
    cout << "Enter the capacity of the deque: ";
    cin >> capacity;
 
    Deque dq(capacity);
 
    do {
        cout << "\n1. Add element at front" << endl;
        cout << "2. Add element at back" << endl;
        cout << "3. Delete element from front" << endl;
        cout << "4. Delete element from back" << endl;
        cout << "5. Display deque" << endl;
        cout << "6. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
 
        switch (choice) {
            case 1:
                cout << "Enter value to add at front: ";
                cin >> value;
                dq.addFront(value);
                break;
            case 2:
                cout << "Enter value to add at back: ";
                cin >> value;
                dq.addBack(value);
                break;
            case 3:
                dq.deleteFront();
                break;
            case 4:
                dq.deleteBack();
                break;
            case 5:
                dq.display();
                break;
            case 6:
                cout << "Exiting..." << endl;
                break;
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    } while (choice != 6);
 
    return 0;
}
