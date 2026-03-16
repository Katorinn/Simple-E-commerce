//QuangAnh
#include <iostream>
#include <vector>
using namespace std;

class Product {
public:
    int id;
    string name;
    int stock;
};

class CartLine {
public:
    int customerId;
    int productId;
    int qty;
};

class OrderItem {
public:
    int productId;
    int qty;
};

class Order {
public:
    string orderId;
    int customerId;
    string date;
    vector<OrderItem> items;
};

vector<Product> products;
vector<CartLine> cart;
vector<Order> orders;

bool productExists(int productId) {
    for (auto p : products)
        if (p.id == productId)
            return true;
    return false;
}

bool addToCart(int customerId, int productId, int qty) {

    if (!productExists(productId) || qty <= 0)
        return false;

    for (auto &c : cart) {
        if (c.customerId == customerId && c.productId == productId) {
            c.qty += qty;
            return true;
        }
    }

    CartLine newLine;
    newLine.customerId = customerId;
    newLine.productId = productId;
    newLine.qty = qty;

    cart.push_back(newLine);
    return true;
}

bool removeFromCart(int customerId, int productId) {

    for (int i = 0; i < cart.size(); i++) {
        if (cart[i].customerId == customerId &&
            cart[i].productId == productId) {

            cart.erase(cart.begin() + i);
            return true;
        }
    }

    return false;
}

string checkout(int customerId, string date) {

    vector<CartLine> customerCart;

    for (auto c : cart)
        if (c.customerId == customerId)
            customerCart.push_back(c);

    if (customerCart.empty())
        return "false";

    for (auto item : customerCart) {
        for (auto &p : products) {
            if (p.id == item.productId && p.stock < item.qty)
                return "false";
        }
    }

    Order newOrder;
    newOrder.orderId = "ORD" + to_string(orders.size() + 1);
    newOrder.customerId = customerId;
    newOrder.date = date;

    for (auto item : customerCart) {

        OrderItem oi;
        oi.productId = item.productId;
        oi.qty = item.qty;

        newOrder.items.push_back(oi);

        for (auto &p : products)
            if (p.id == item.productId)
                p.stock -= item.qty;
    }

    orders.push_back(newOrder);

    for (int i = cart.size() - 1; i >= 0; i--)
        if (cart[i].customerId == customerId)
            cart.erase(cart.begin() + i);

    return newOrder.orderId;
}

void showCart(int customerId) {
    cout << "Cart:\n";
    for (auto c : cart)
        if (c.customerId == customerId)
            cout << "Product " << c.productId << " Qty " << c.qty << endl;
}

int main() {

    products.push_back({101, "Keyboard", 10});
    products.push_back({102, "Mouse", 5});

    int choice;
    int customerId = 1;

    do {
        cout << "\n1.Add to cart\n";
        cout << "2.Remove from cart\n";
        cout << "3.Show cart\n";
        cout << "4.Checkout\n";
        cout << "5.Exit\n";
        cout << "Choose: ";
        cin >> choice;

        if (choice == 1) {
            int pid, qty;
            cin >> pid >> qty;
            cout << addToCart(customerId, pid, qty) << endl;
        }

        if (choice == 2) {
            int pid;
            cin >> pid;
            cout << removeFromCart(customerId, pid) << endl;
        }

        if (choice == 3) {
            showCart(customerId);
        }

        if (choice == 4) {
            cout << checkout(customerId, "2026-03-09") << endl;
        }

    } while (choice != 5);
}



//QuangAnh
//Thang
#include<iostream > 
#include<string> 
#include<bits/stdc++.h> 
#include <vector> 																				
using namespace std ;
 class product{
  private :
  	string id ;
  	string name ;
  	double price ;
	int stock ;
	  // dac diem cua san pham
	public :
		 product(){} 
	product (string id , string name ,double price , int stock ) {
	
    this -> id=id ;															
    this -> name=name;
 this -> price=price;
 this ->stock ;}
 
 
    string 	getid(){
    return id;
}

string getname(){
    return name;
}

double getprice(){
    return price;
}

int getstock(){
    return stock;// thay doi khi mua 
}

void setstock(int s){
    stock = s;
}
};
	
	 // vector dung de luu danh sach 
	
	 // in dach sach san pham
	 void showproduct (vector<product>&products){
	  
	 for (int i =0 ; i < products.size(); i++) {
	 
	 cout <<products[i].getname() <<endl; }}
	 // tao class cartiteam de co the mua nhieu 1 san pham nhieu lan 
	 class cartiteam {
	 	private :
		 product prod ;
	   	int quanlity  ;
		 public :
		cartiteam (product prod , int quanlity)	{
		
		this -> prod = prod;// ten bien trung nhau nen phai dung thís -> de name = name 
		this -> quanlity = quanlity ;
	}
		product getproduct () {
			return prod ;
			 
		}
		double getquanlity () {
			return quanlity ; 
		}
		// de chuong trinh ngung neu het so hang 
	
		
		}; 
		// them san pham vao cart
		vector<cartiteam> cart;
		void addtocart(vector<product>&products , vector<cartiteam>&cart) 
		{ string id ;
		int qty ; 
		cout <<"nhap ID san pham :" ;
		cin>>id ;
		cout <<"nhap so luong san pham can mua :" ;
		cin >>qty;
		for (int i = 0 ; i < products.size(); i++) // tim trong gio hang 
		{if (products[i].getid() ==id ){if (products[i].getstock() < qty ){cout << "so luong khong du\n" ;
		return ;
		 
		}
		cartiteam iteam(products[i],qty); // tao cartiteam gom san pham va so luong mua  
		cart.push_back(iteam) ;
		products[i].setstock(products[i].getstock()-qty );// so luong trong kho = so luong cu - so luong moi mua  
		cout <<" da them vao gio hang \n ";
		return ;
		}
		
		}
			cout <<"khong tim thay san pham ";
		}
		 
			
		
		int main () {
			vector<product> products;
		products.push_back (product("01","laptop",21000000,5)) ;
	 products.push_back (product("02","smart phone",17000000,10 )) 
	 ;
	 products.push_back (product ("03","legotoy",7000000,30 )) ;
	 products.push_back (product ("04","mouse",800000,40 )) ;
	 products.push_back (product("05","keyboard" ,1000000,30)) ;
	 addtocart(products,cart);}
	 
	  
	  
    
	
	 
	  
 


 


//Thang
//QuanAnh
#include <iostream>
#include <fstream>
#include <vector>
#include <sstream>
#include <cstdlib>
using namespace std;

struct Product
{
    int id;
    string name;
    int price;
    int stock;
};

void showMenu()
{
    cout << "\n====== SHOP MENU ======\n";
    cout << "1. Show products\n";
    cout << "2. Save products to CSV\n";
    cout << "3. Exit\n";
    cout << "Choose: ";
}

void showProducts(vector<Product> products)
{
    cout << "\n------ PRODUCT LIST ------\n";

    for (int i = 0; i < products.size(); i++)
    {
        cout << "ID: " << products[i].id << endl;
        cout << "Name: " << products[i].name << endl;
        cout << "Price: " << products[i].price << endl;
        cout << "Stock: " << products[i].stock << endl;
        cout << "------------------------\n";
    }
}

void saveProductsCSV(vector<Product> products)
{
    ofstream file("products (1)");

    for (int i = 0; i < products.size(); i++)
    {
        file << products[i].id << ","
             << products[i].name << ","
             << products[i].price << ","
             << products[i].stock << endl;
    }

    file.close();

    cout << "Data saved to products.csv\n";
}

vector<Product> loadProductsCSV()
{
    vector<Product> products;

    ifstream file("products.csv");

    string line;

    while (getline(file, line))
    {
        Product p;

        stringstream ss(line);
        string temp;

        getline(ss, temp, ',');
        p.id = atoi(temp.c_str());

        getline(ss, p.name, ',');

        getline(ss, temp, ',');
        p.price = atoi(temp.c_str());

        getline(ss, temp, ',');
        p.stock = atoi(temp.c_str());

        products.push_back(p);
    }

    file.close();

    return products;
}

int main()
{
    vector<Product> products = loadProductsCSV();

    int choice;

    do
    {
        showMenu();
        cin >> choice;

        switch (choice)
        {
        case 1:
            showProducts(products);
            break;

        case 2:
            saveProductsCSV(products);
            break;

        case 3:
            cout << "Goodbye!\n";
            break;

        default:
            cout << "Invalid choice\n";
        }

    } while (choice != 3);

    return 0;
}
    } while (choice != 3);

    return 0;
}
//QuocAnh
