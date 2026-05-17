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
class BanBida{
private:
    int ma;
    string loai;
    double gia;
    bool trangThai;
    string tenKhach;
    int hMo,pMo;
    int hDong,pDong;
    vector<pair<string,double>> dsNuoc;
public:
    BanBida(){
        trangThai = false;
        hMo = 0;
        pMo = 0;
    }
    bool getTrangThai() const{
        return trangThai;
    }
    void setBan(int m,string l,double g){
        ma = m;
        loai = l;
        gia = g;
    }

    int getMa() const{ return ma; }
    int getHMo() const{ return hMo; }
    int getPMo() const{ return pMo; }
    int getHDong()const{ return hDong; }
    int getPDong()const{ return pDong; }
    string getLoai()const{ return loai; }
    string getTenKhach() const{
        return tenKhach;
    }
    vector<pair<string,double>> getDSNuoc() const{
        return dsNuoc;
    }
    double getGia() const{
        return gia;
    }

    void xuat() const{
        cout << "| "
             << left  << setw(5)  << ma
             << "| "
             << left  << setw(15) << loai
             << "| "
             << right << setw(10)
             << fixed << setprecision(0)
             << gia
             << " | "
             << left  << setw(18) << tenKhach
             << "| "
             << left  << setw(12)
             << (trangThai ? "Dang choi" : "Con trong")
             << " |\n";
    }
    void xuatChiTiet(){
        line(50);
        cout << "Ma ban      : " << ma << endl;
        cout << "Loai ban    : " << loai << endl;
        cout << "Gia / gio   : " << gia << endl;
        if(trangThai){
            cout << "Khach       : "
                 << tenKhach << endl;
            cout << "Trang thai  : Dang choi\n";
            cout << "Gio mo      : ";
            if(hMo < 10) cout << "0";
            cout << hMo << ":";
            if(pMo < 10) cout << "0";
            cout << pMo << endl;
            cout << "\nDo uong da goi:\n";
            if(dsNuoc.empty()){
                cout << "Khong co\n";
            }else{
                for(auto x : dsNuoc){
                    cout << "- "
                         << x.first
                         << " : "
                         << x.second
                         << " VND\n";
                }
            }
        }else{
            cout << "Trang thai  : Con trong\n";
        }
        line(50);
    }

    void moBan(string ten,int h,int p){
        if(trangThai)
            throw runtime_error("Ban dang su dung!");
        tenKhach = ten;
        hMo = h;
        pMo = p;
        trangThai = true;
    }
    
    void themDoUong(string ten,double tien){
        dsNuoc.push_back({ten,tien});
    }

    double dongBan(int h,int p){
        if(!trangThai)
            throw runtime_error("Ban chua mo!");
        hDong = h;
        pDong = p;
        int mo =
            hMo * 60 + pMo;
        int dong =
            hDong * 60 + pDong;
        int tongPhut =
            dong - mo;
        if(tongPhut <= 0)
            tongPhut = 60;
        double soGio =
            tongPhut / 60.0;
        double tong =
            soGio * gia;
        for(auto x : dsNuoc)
            tong += x.second;
        dsNuoc.clear();
        trangThai = false;
        tenKhach = "";
        return tong;
    }
};

class HoaDon{
private:
    int maHD,maBan;
    int hMo,pMo;
    int hDong,pDong;
    double tongTien;
public:
    HoaDon(int mhd,
           int mb,
           int hm,
           int pm,
           int hd,
           int pd,
           double tong){
        maHD = mhd;
        maBan = mb;
        hMo = hm;
        pMo = pm;
        hDong = hd;
        pDong = pd;
        tongTien = tong;
    }
    double getTongTien() const{
        return tongTien;
    }
    void xuat() const{
        string tg;
        if(hMo < 10) tg += "0";
        tg += to_string(hMo) + ":";
        if(pMo < 10) tg += "0";
        tg += to_string(pMo);
        tg += " - ";
        if(hDong < 10) tg += "0";
        tg += to_string(hDong) + ":";
        if(pDong < 10) tg += "0";
        tg += to_string(pDong);
        cout << "| "
             << left  << setw(5)  << maHD
             << "| "
             << left  << setw(5)  << maBan
             << "| "
             << left  << setw(13) << tg
             << "| "
             << right << setw(12)
             << fixed << setprecision(0)
             << tongTien
             << " |\n";
    }
};
