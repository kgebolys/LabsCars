#include <iostream>
//#include <conio.h>
#include <string>
#include <random>
#include <ctime>
#include <sstream>
#include <vector>
 
using namespace std;
 
//https://stackoverflow.com/questions/13445688/how-to-generate-a-random-number-in-c
std::random_device dev;
std::mt19937 rng(dev());
std::uniform_int_distribution<std::mt19937::result_type> cenaRnd(5000, 150000);
 
void wypisz(); //funkcja zaprzyjażniona z dwoma klasami
 
class Car {
    friend class Customer;
    friend void wypisz();
 
    string brand;
    string model;
    int price;
 
    
 
public:
 
    Car() { price = -1; };
 
    Car(string a, string b) {
        brand = a;
        model = b;
        price = cenaRnd(rng);
    }
 
    string getBrand() {
        return brand;
    };
 
    string getModel() {
        return model;
    };
 
    double getPrice() {
        return price;
    };
 
    void setBrand(string brand) {
        this->brand = brand;
    };
 
    void setModel(string model) {
        this->model = model;
    };
 
    void setPrice(double price) {
        this->price = price;
    };
};
 
class Customer {
private:
    friend void wypisz();
    int ID;
public:
    static int counter;
    int limit = 3;
    int carsAmount = 0;
    Car* cars = nullptr;
 
    Customer(Car cars[]) {
        ID = counter;
        counter++;
        cout << "\nWywolano konstruktor sparametryzowany dla " << "Customer ID: " << ID << endl;;
        this->cars = new Car[limit];
 
 
        for (int i = 0; i < limit; i++) {
            this->cars[i].brand = cars[i].brand;
            this->cars[i].model = cars[i].model;
            this->cars[i].price = cars[i].price;
        };
    };
 
    Customer() {
        ID = counter;
        counter++;
        cout << "\nWywolano konstruktor domyslny dla " << "Customer ID: " << ID << endl;
        this->cars = new Car[limit];
    };
 
    Customer(const Customer& customer) {
        ID = counter;
        counter++;
        cout << "\nWywolano konstruktor kopiujacy " << "Customer ID: " << ID << endl; 
        this->cars = new Car[limit];
 
        //const short carsAmount = (sizeof(customer.cars) / sizeof(*customer.cars));
        /*cout << carsAmount << "asdsadsadasdsadas" << "\n"; */
        for (int i = 0; i < limit; i++) {
            this->cars[i].brand = customer.cars[i].brand;
            this->cars[i].model = customer.cars[i].model;
            this->cars[i].price = customer.cars[i].price;
        };     
    }
 
    ~Customer() {
        counter--;
        cout << "\nWywolano destruktor ";
        cout << ID;
        delete[] this->cars;
    };
 
    void addCar(Car& car) {
        this->cars[0].brand = car.brand;
        this->cars[0].model = car.model;
        this->cars[0].price = car.price;
    }
 
    void addCar(Car& car, int i) {
        this->cars[i].brand = car.brand;
        this->cars[i].model = car.model;
        this->cars[i].price = car.price;
    }
 
    void modifyPrice() {
        for (int i = 0; i < limit; i++) {
            this->cars[i].setPrice(cenaRnd(rng));
        };
    }
 
    int getId() {
        return ID;
    };
 
    void coutAllInfo() {
        cout << "Customer ID: " << ID << endl;
        coutCars();
    }
 
    void coutCars() {
        for (int i = 0; i < limit; i++) {
            if(cars[i].getPrice() != -1)
                cout << "Brand: " << cars[i].getBrand() << " Model: " << cars[i].getModel() << " price: " << cars[i].getPrice() << "$" << endl;
        };
    };
};
 
int Customer::counter = 0;
 
//Zmienne do przetestowania dostępu do prywantch pól dla zaprzyjaźniownej funkcji wypisz()
Customer* Kupiec_0 = new Customer();
Car* Auto_0 = new Car();
 
int main() {
 
    Car c1("Fiacik", "Bravo");
   
    string model[10] = { "Fiacik","Audi","BMW","Ford","Kia","Alfa Rome", "Seat","Peugeot","Renault","Jaguar"};
    string marka[10] = {"Bravo","A4","3","Focus","Rio","159","Ibiza","307","307","XE"};
    Car cars[10] { {"Fiacik", "Bravo"}, {"Audi", "A4"}, {"BMW", "3"}, {"Ford", "Focus"}, {"Kia", "Rio"},
    {"Alfa Romeo", "159"}, {"Seat", "Ibiza"}, {"Peugeot", "307"}, {"Renault", "307"}, {"Jaguar", "XE"} };
 
    Car first3cars[3];
    //tworzymy kupców
    Customer *Kupiec_1 = new Customer();
    Customer *Kupiec_2 = new Customer(cars);
    //kopiowanie danych kupca 2 do kupca 3
    Customer *Kupiec_3 = new Customer(*Kupiec_2);
 
    cout << "Ilosc klientow: " << Customer::counter << "\n";
 
    Kupiec_1->coutAllInfo();
    Kupiec_2->coutAllInfo();
    Kupiec_3->coutAllInfo();
 
    cout << endl;
 
    Kupiec_1->addCar(c1);
 
    Kupiec_2->modifyPrice();
 
    cout << "Kupcy po dodaniu i zmianie" << endl;
 
    Kupiec_1->coutAllInfo();
    Kupiec_2->coutAllInfo();
    Kupiec_3->coutAllInfo();
 
    srand((int)time(0));
    
    //kasowanie kupców
 
    delete Kupiec_1;
    delete Kupiec_2;
    delete Kupiec_3;
    
    cout << endl;
 
    cout << "Ilosc klientow: " << Customer::counter;
 
    Customer *customers = new Customer[100];
 
    for (int i = 0; i < 100; i++) {
        int r = (rand() % 4);
        for (int j = 0; j < r; j++) {
            int markaModelRnd = (rand() % 10);
            Car* car = new Car(model[markaModelRnd], marka[markaModelRnd]);
            customers[i].addCar(*car, j);
        }
    };
 
    for (int j = 0; j < 100; j++) {
        customers[j].coutAllInfo();
    }
 
    delete Kupiec_0;
 
    delete[] customers;
    
    cout << endl;
     
    cout << "Ilosc klientow: " << Customer::counter << "\n";
}
 
 
void wypisz()
{
    Kupiec_0->ID;
    Auto_0->model;
}
