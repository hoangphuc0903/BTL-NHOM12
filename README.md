#include <iostream>
#include <vector>
#include <iomanip>
#include <limits>
#include <stdexcept>

using namespace std;

void line(int n){
    cout << setfill('-') << setw(n) << "-" << setfill(' ') << endl;
}

int nhapInt(string text){
    int x;
    while(true){
        cout << text;
        cin >> x;
        if(cin.fail()){
            cout << "Nhap sai! Vui long nhap so!\n";
            cin.clear();
            cin.ignore(
                numeric_limits<streamsize>::max(),
                '\n'
            );
        }else return x;
    }
}
string nhapString(string text){
    string s;
    cout << text;
    getline(cin >> ws, s);
    return s;
}


