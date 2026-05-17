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
class ConNguoi{
protected:
    string ten,sdt;
public:
    virtual void nhap() = 0;
    virtual void xuat() const = 0;
    string getTen() const { return ten; }
    virtual ~ConNguoi() {}
};
class KhachHang : public ConNguoi {
private:
    int diem;
    vector<string> lichSuChoi;
public:
    KhachHang(){
        diem = 0;
    }
    void nhap() override {
        ten = nhapString("Nhap ten khach hang: ");
        sdt = nhapString("Nhap so dien thoai: ");
    }
    void congDiem(double tien){
        diem += tien / 10000;
    }
    int getDiem() const{
        return diem;
    }
    string xepHang() const{
        if(diem >= 100)
            return "Gold";

        if(diem >= 50)
            return "Silver";

        return "Thuong";
    }
    double layGiamGia() const{
        if(xepHang() == "Gold")
            return 0.10;
        if(xepHang() == "Silver")
            return 0.05;
        return 0;
    }
    void themLichSu(string ls){
        lichSuChoi.push_back(ls);
    }
    void hienThiLichSu() const{
        cout << "\n===== LICH SU CHOI =====\n";
        if(lichSuChoi.empty()){
            cout << "Chua co lich su!\n";
            return;
        }
        for(string x : lichSuChoi){
            cout << "- " << x << endl;
        }
    }
    void xuat() const override{
        cout << "| "
             << left  << setw(15) << ten
             << "| "
             << left  << setw(12) << sdt
             << "| "
             << right << setw(8)  << diem
             << " | "
             << left  << setw(10) << xepHang()
             << " |\n";
    }
};
class NhanVien : public ConNguoi{
private:
    double luong;
    string chucVu;
public:
    void nhap() override{
        ten = nhapString("Nhap ten NV: ");
        sdt = nhapString("Nhap SDT NV: ");
        chucVu = nhapString("Nhap chuc vu: ");
        luong = nhapInt("Nhap luong: ");
    }
    void xuat() const override{
        cout << "| "
             << left  << setw(15) << ten
             << "| "
             << left  << setw(12) << sdt
             << "| "
             << left  << setw(12) << chucVu
             << "| "
             << right << setw(10)
             << fixed << setprecision(0)
             << luong
             << " |\n";
    }
};
class DoUong{
private:
    int ma;
    string ten;
    double gia;
public:
    void setDU(int m,string t,double g){
        ma = m;
        ten = t;
        gia = g;
    }
    int getMa() const { return ma; }
    string getTen() const { 
        return ten; 
    }
    double getGia() const { 
        return gia; 
    }
    void xuat() const{
        cout << "| "
             << left  << setw(5)  << ma
             << "| "
             << left  << setw(20) << ten
             << "| "
             << right << setw(10)
             << fixed << setprecision(0)
             << gia
             << " |\n";
    }
};
