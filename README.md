#include <iostream>
#include <string>
using namespace std;

class Product {
private:
    string PID;
    string name;
    int quantity;
    double price;

public:
    // Constructor m?c ð?nh
    Product() {
        this->PID = "";
        this->name = "";
        this->quantity = 0;
        this->price = 0.0;
    }

    // Constructor có tham s?
    Product(string PID, string name, int quantity, double price) {
        this->PID = PID;
        this->name = name;
        this->setQuantity(quantity);
        this->setPrice(price);
    }

    // Getter
    string getPID() const { return this->PID; }
    string getName() const { return this->name; }
    int getQuantity() const { return this->quantity; }
    double getPrice() const { return this->price; }

    // Setter
    void setPID(string PID) { this->PID = PID; }
    void setName(string name) { this->name = name; }

    void setQuantity(int quantity) {
        if (quantity < 0) this->quantity = 0;
        else this->quantity = quantity;
    }

    void setPrice(double price) {
        if (price < 0) this->price = 0;
        else this->price = price;
    }

    // Nh?p d? li?u
    void input() {
        cout << "Product ID: ";
        getline(cin, this->PID);

        cout << "Product Name: ";
        getline(cin, this->name);

        cout << "Quantity: ";
        cin >> this->quantity;

        cout << "Price: ";
        cin >> this->price;
        cin.ignore();

        setQuantity(this->quantity);
        setPrice(this->price);
    }

    // Tính t?ng ti?n
    double totalPrice() const {
        return this->quantity * this->price;
    }

    // Xu?t d? li?u
    void print() const {
        cout << "Product{ID=" << PID
             << ", Name=" << name
             << ", Quantity=" << quantity
             << ", Price=" << price
             << ", Total=" << totalPrice()
             << "}" << endl;
    }
};
