//QuangAnh




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

//QuocAnh
