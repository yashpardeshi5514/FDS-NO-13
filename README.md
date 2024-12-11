#include <iostream>
using namespace std;
 
class PizzaParlor {
private:
    int* queue;        // Array to store orders
    int front, rear;   // Indices for front and rear of the queue
    int capacity;      // Maximum number of orders the parlor can accept
    int size;          // Current size of the queue
 
public:
    // Constructor to initialize the queue
    PizzaParlor(int maxOrders) {
        capacity = maxOrders;
        queue = new int[capacity];
        front = rear = -1;
        size = 0;
    }
 
    // Destructor to free the memory
    ~PizzaParlor() {
        delete[] queue;
    }
 
    // Function to place an order
    void placeOrder(int orderNumber) {
        if (size == capacity) {
            cout << "Sorry, the parlor is full. Cannot accept more orders!" << endl;
        } else {
            // Circularly add to the queue
            if (front == -1) {
                front = 0; // First order is placed
            }
            rear = (rear + 1) % capacity;
            queue[rear] = orderNumber;
            size++;
            cout << "Order " << orderNumber << " placed successfully!" << endl;
        }
    }
 
    // Function to serve an order
    void serveOrder() {
        if (size == 0) {
            cout << "No orders to serve!" << endl;
        } else {
            cout << "Serving Order " << queue[front] << endl;
            front = (front + 1) % capacity; // Circularly move front
            size--;
        }
    }
 
    // Function to view the orders in the queue
    void viewOrders() {
        if (size == 0) {
            cout << "No orders to view!" << endl;
        } else {
            cout << "Orders in the queue: ";
            int i = front;
            for (int j = 0; j < size; j++) {
                cout << queue[i] << " ";
                i = (i + 1) % capacity;
            }
            cout << endl;
        }
    }
};
 
int main() {
    int maxOrders;
    cout << "Enter the maximum number of orders the parlor can accept: ";
    cin >> maxOrders;
 
    PizzaParlor parlor(maxOrders);
    int choice, orderNumber;
 
    while (true) {
        cout << "\nPizza Parlor Menu:\n";
        cout << "1. Place an Order\n";
        cout << "2. Serve an Order\n";
        cout << "3. View Orders\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
 
        switch (choice) {
            case 1:
                cout << "Enter Order Number: ";
                cin >> orderNumber;
                parlor.placeOrder(orderNumber);
                break;
            case 2:
                parlor.serveOrder();
                break;
            case 3:
                parlor.viewOrders();
                break;
            case 4:
                cout << "Exiting the system...\n";
                return 0;
            default:
                cout << "Invalid choice! Please try again.\n";
        }
    }
 
    return 0;
}
