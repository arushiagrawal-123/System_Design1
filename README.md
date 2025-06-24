# System_Design1

``` cpp
    struct Item {
    double price;
    int quantity;
};

class ShoppingCart {
private:
    unordered_map<string, Item> cart;

public:
    void addItem(string name, double price, int quantity) {
        if (cart.find(name) != cart.end()) {
            cart[name].quantity += quantity; // If item exists, increase quantity
        } else {
            cart[name] = {price, quantity};
        }
        cout << quantity << " " << name << "(s) added to cart.\n";
    }

    void removeItem(string name) {
        if (cart.find(name) != cart.end()) {
            cart.erase(name);
            cout << name << " removed from cart.\n";
        } else {
            cout << name << " not found in cart.\n";
        }
    }

    void updateItem(string name, int quantity) {
        if (cart.find(name) != cart.end()) {
            cart[name].quantity = quantity;
            cout << name << " quantity updated to " << quantity << ".\n";
        } else {
            cout << name << " not found in cart.\n";
        }
    }

    void displayCart() {
        cout << "\nItems in cart:\n";
        if (cart.empty()) {
            cout << "Cart is empty.\n";
            return;
        }
        double total = 0;
        cout << left << setw(15) << "Item"
             << setw(10) << "Price"
             << setw(10) << "Qty"
             << "Subtotal\n";

        for (auto &entry : cart) {
            string name = entry.first;
            double price = entry.second.price;
            int qty = entry.second.quantity;
            double subtotal = price * qty;
            total += subtotal;
            cout << left << setw(15) << name
                 << setw(10) << price
                 << setw(10) << qty
                 << subtotal << endl;
        }
        cout << "Total Amount: ₹" << total << "\n";
    }

    double getTotal() {
        double total = 0;
        for (auto &entry : cart) {
            total += entry.second.price * entry.second.quantity;
        }
        return total;
    }
};
int main() {
    ShoppingCart cart;

    cart.addItem("Apple", 10.5, 3);
    cart.addItem("Milk", 45, 2);
    cart.addItem("Bread", 25, 1);

    cart.displayCart();

    cart.updateItem("Milk", 3);       
    cart.removeItem("Bread");         

    cart.displayCart();

    cout << "\nTotal amount to pay: ₹" << cart.getTotal() << endl;

    return 0;
}
