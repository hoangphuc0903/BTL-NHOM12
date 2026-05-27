// ==========================================
// QUAN LY QUAN BIDA FULL OOP
// DEV-C++
// ==========================================
#include<windows.h>
#include<iostream>
#include<vector>
#include<iomanip>
#include<string>
#include<limits>
#include<algorithm>
#include<cctype>

using namespace std;

HANDLE h = GetStdHandle(STD_OUTPUT_HANDLE);

void mau(int color){

    SetConsoleTextAttribute(h,color);
}

void line(int n){

    mau(11);

    for(int i=0;i<n;i++){

        cout << char(205);
    }

    cout << endl;

    mau(7);
}

int nhapInt(string text){

    int x;

    while(true){

        cout << text;

        cin >> x;

        if(cin.fail()){

            cout << "Nhap sai!\n";

            cin.clear();

            cin.ignore(
                numeric_limits<streamsize>::max(),
                '\n'
            );
        }
        else{

            return x;
        }
    }
}

double nhapDouble(string text){

    double x;

    while(true){

        cout << text;

        cin >> x;

        if(cin.fail()){

            cout << "Nhap sai!\n";

            cin.clear();

            cin.ignore(
                numeric_limits<streamsize>::max(),
                '\n'
            );
        }
        else{

            return x;
        }
    }
}

string nhapString(string text){

    string s;

    cout << text;

    getline(cin >> ws,s);

    return s;
}

void title(string text){

    mau(14);

    line(60);

    cout << "\t" << text << endl;

    line(60);

    mau(7);
}

// ==========================================
// KHACH HANG
// ==========================================

class KhachHang{

private:

    string ten;
    string gioiTinh;
    string sdt;

    int diem;

public:

    KhachHang(){

        diem = 0;
    }

    void nhap(){

        ten =
            nhapString(
                "Nhap ten KH: "
            );

        gioiTinh =
            nhapString(
                "Nhap gioi tinh: "
            );

        sdt =
            nhapString(
                "Nhap SDT: "
            );
    }

    string getTen(){

        return ten;
    }

    void congDiem(double tongTien){

        diem += tongTien / 10000;
    }

    void xuat(){

        cout
        << "| "
        << left
        << setw(20)
        << ten
        << "| "
        << setw(12)
        << gioiTinh
        << "| "
        << setw(15)
        << sdt
        << "| "
        << setw(10)
        << diem
        << " |\n";
    }
};

// ==========================================
// NHAN VIEN
// ==========================================

class NhanVien{

private:

    string ten;
    string gioiTinh;
    string chucVu;

    int ca1;
    int ca2;
    int ca3;
    
    bool daTraLuong;

    string ngayTraLuong;

public:

    NhanVien(){

    ca1 = 0;
    ca2 = 0;
    ca3 = 0;

    daTraLuong = false;

    ngayTraLuong = "Chua tra";
}

    void nhap(){

        ten =
            nhapString(
                "Nhap ten NV: "
            );

        gioiTinh =
            nhapString(
                "Nhap gioi tinh: "
            );

        while(true){

            cout
            << "\n===== CHUC VU =====\n";

            cout
            << "1. Quan ly\n";

            cout
            << "2. Thu ngan\n";

            cout
            << "3. Phuc vu\n";

            chucVu =
                nhapString(
                    "Nhap chuc vu: "
                );

            for(int i=0;i<chucVu.length();i++){

                chucVu[i] =
                    tolower(chucVu[i]);
            }

            if(
                chucVu == "quan ly"
                ||
                chucVu == "thu ngan"
                ||
                chucVu == "phuc vu"
            ){

                break;
            }

            cout
            << "Chuc vu khong hop le!\n";
        }

cout
<< "\n===== DANG KY CA =====\n";

cout
<< "1. Ca 1 : 7h -> 12h\n";

cout
<< "2. Ca 2 : 12h -> 17h\n";

cout
<< "3. Ca 3 : 17h -> 22h\n";

int soLuongCa;

while(true){

    soLuongCa =
        nhapInt(
            "Nhap so luong ca muon dang ky (1-3): "
        );

    if(soLuongCa >= 1 && soLuongCa <= 3){

        break;
    }

    cout
    << "So luong khong hop le!\n";
}

for(int i=1;i<=soLuongCa;i++){

    int ca;

    while(true){

        ca =
            nhapInt(
                "Chon ca thu "
                + to_string(i)
                + " (1-3): "
            );

        if(ca == 1 && ca1 == 0){

            ca1 = 1;

            break;
        }

        else if(ca == 2 && ca2 == 0){

            ca2 = 1;

            break;
        }

        else if(ca == 3 && ca3 == 0){

            ca3 = 1;

            break;
        }

        else{

            cout
            << "Ca khong hop le hoac da chon!\n";
        }
    }
}
 }

    int tongCa(){

        return ca1 + ca2 + ca3;
    }

    double tinhLuong(){

    int soGio =
        tongCa() * 5;

    string cv = chucVu;

    for(int i=0;i<cv.length();i++){

        cv[i] = tolower(cv[i]);
    }

    if(cv == "quan ly"){

        return soGio * 40000;
    }

    return soGio * 25000;
}
void traLuong(){

    if(daTraLuong){

        cout
        << "Nhan vien da duoc tra luong!\n";

        return;
    }

    ngayTraLuong =
        nhapString(
            "Nhap ngay tra luong: "
        );

    daTraLuong = true;

    cout
    << "Tra luong thanh cong!\n";
}
string getTrangThaiLuong(){

    if(daTraLuong){

        return "Da tra";
    }

    return "Chua tra";
}

    void xuat(){

        cout
        << "| "
        << left
        << setw(20)
        << ten
        << "| "
        << setw(10)
        << gioiTinh
        << "| "
        << setw(15)
        << chucVu
        << "| "
        << setw(8)
        << ca1
        << "| "
        << setw(8)
        << ca2
        << "| "
        << setw(8)
        << ca3
        << "| "
        << setw(10)
        << tongCa()
        << "| "
        << setw(15)
		<< tinhLuong()
		<< "| "
		<< setw(12)
		<< getTrangThaiLuong()
		<< "| "
		<< setw(15)
		<< ngayTraLuong
		<< " |\n";
    }
};

// ==========================================
// DO UONG
// ==========================================

class DoUong{

private:

    int ma;

    string ten;

    double giaLe;
    double giaLoc;

    int tonLe;
    int tonLoc;

    int daBanLe;
    int daBanLoc;

public:

    void setDU(
        int m,
        string t,
        double gl,
        double gloc,
        int tle,
        int tloc
    ){

        ma = m;

        ten = t;

        giaLe = gl;

        giaLoc = gloc;

        tonLe = tle;

        tonLoc = tloc;

        daBanLe = 0;

        daBanLoc = 0;
    }

    int getMa(){

        return ma;
    }

    string getTen(){

        return ten;
    }

    double getGiaLe(){

        return giaLe;
    }

    double getGiaLoc(){

        return giaLoc;
    }

    int getTonLe(){

        return tonLe;
    }

    int getTonLoc(){

        return tonLoc;
    }

    int getDaBanLe(){

        return daBanLe;
    }

    int getDaBanLoc(){

        return daBanLoc;
    }

    void banLe(int sl){

        if(sl > tonLe){

            cout
            << "Khong du nuoc le!\n";

            return;
        }

        tonLe -= sl;

        daBanLe += sl;
    }

    void banLoc(int sl){

        if(sl > tonLoc){

            cout
            << "Khong du nuoc loc!\n";

            return;
        }

        tonLoc -= sl;

        daBanLoc += sl;
    }

    void xuat(){

        cout
        << "| "
        << left
        << setw(5)
        << ma
        << "| "
        << setw(20)
        << ten
        << "| "
        << setw(10)
        << giaLe
        << "| "
        << setw(10)
        << giaLoc
        << "| "
        << setw(10)
        << tonLe
        << "| "
        << setw(10)
        << tonLoc
        << " |\n";
    }
};

// ==========================================

struct MonNuoc{

    string ten;

    string loai;

    int soLuong;

    double thanhTien;
};

// ==========================================
// BAN BIDA
// ==========================================

class BanBida{

private:

    int ma;

    string loai;

    double giaGio;

    bool trangThai;

    string tenKhach;

    vector<MonNuoc> dsNuoc;

public:

    BanBida(){

        trangThai = false;
    }

    void setBan(
        int m,
        string l,
        double g
    ){

        ma = m;

        loai = l;

        giaGio = g;
    }

    int getMa(){

        return ma;
    }

    bool getTrangThai(){

        return trangThai;
    }

    double getGia(){

        return giaGio;
    }

    vector<MonNuoc>& getDSNuoc(){

        return dsNuoc;
    }

    void moBan(string ten){
        if(trangThai){

            cout
            << "Ban dang choi!\n";

            return;
        }

        tenKhach = ten;

        trangThai = true;
    }

    void themNuoc(
        string ten,
        string loai,
        int sl,
        double tien
    ){
		
        MonNuoc m;

        m.ten = ten;

        m.loai = loai;

        m.soLuong = sl;

        m.thanhTien = tien;

        dsNuoc.push_back(m);
    }

    double tinhTienNuoc(){

        double tong = 0;

        for(int i=0;i<dsNuoc.size();i++){

            tong += dsNuoc[i].thanhTien;
        }

        return tong;
    }

    void dongBan(){

        trangThai = false;

        tenKhach = "";

        dsNuoc.clear();
    }

    void xuat(){

	    cout
	    << "| "
	    << left
	    << setw(5)
	    << ma
	    << "| "
	    << setw(15)
	    << loai
	    << "| "
	    << setw(12)
	    << giaGio
	    << "| "
	    << setw(15)
	    << tenKhach
	    << "| ";
	
	    if(trangThai){
	
	        mau(12);
	
	        cout
	        << setw(15)
	        << "Dang choi";
	
	        mau(7);
	    }
	    else{
	
	        mau(10);
	
	        cout
	        << setw(15)
	        << "Con trong";
	
	        mau(7);
	    }
	
	    cout << " |\n";
	}
	
	string getTenKhach(){

    return tenKhach;
}
};
// ==========================================
// HOA DON
// ==========================================

class HoaDon{

private:

    int maHD;

    int maBan;

    double tienBan;

    double tienNuoc;

    double tongTien;

public:

    HoaDon(
        int mhd,
        int mb,
        double tb,
        double tn,
        double tong
    ){

        maHD = mhd;

        maBan = mb;

        tienBan = tb;

        tienNuoc = tn;

        tongTien = tong;
    }

    void xuat(){

        cout
        << "| "
        << left
        << setw(5)
        << maHD
        << "| "
        << setw(8)
        << maBan
        << "| "
        << setw(15)
        << tienBan
        << "| "
        << setw(15)
        << tienNuoc
        << "| "
        << setw(15)
        << tongTien
        << " |\n";
    }
};

// ==========================================
// TAI KHOAN
// ==========================================

class TaiKhoan{

public:

    string user;

    string pass;

    string role;
};

// ==========================================
// QUAN LY
// ==========================================

class QuanLy{

private:

    vector<BanBida> dsBan;

    vector<DoUong> dsDU;

    vector<KhachHang> dsKH;

    vector<NhanVien> dsNV;

    vector<HoaDon> dsHD;

    vector<TaiKhoan> dsTK;

    string quyen;

    double doanhThu;

public:

    QuanLy(){

        doanhThu = 0;

        khoiTaoBan();

        khoiTaoDU();

        khoiTaoTK();
    }

    // ======================================

    void khoiTaoTK(){

        TaiKhoan a;

        a.user = "admin";
        a.pass = "123";
        a.role = "admin";

        dsTK.push_back(a);

        TaiKhoan b;

        b.user = "nv";
        b.pass = "123";
        b.role = "nhanvien";

        dsTK.push_back(b);
    }

    // ======================================

    bool dangNhap(){

        string u,p;

        cout
        << "User: ";

        cin >> u;

        cout
        << "Pass: ";

        cin >> p;

        for(int i=0;i<dsTK.size();i++){

            if(
                dsTK[i].user == u
                &&
                dsTK[i].pass == p
            ){

                quyen =
                    dsTK[i].role;

                return true;
            }
        }

        return false;
    }

    // ======================================

    string getQuyen(){

        return quyen;
    }

    // ======================================

    void khoiTaoBan(){

        int ma = 1;

        for(int i=0;i<3;i++){

            BanBida b;

            b.setBan(
                ma++,
                "Libre",
                50000
            );

            dsBan.push_back(b);
        }

        for(int i=0;i<4;i++){

            BanBida b;

            b.setBan(
                ma++,
                "Pool",
                60000
            );

            dsBan.push_back(b);
        }
    }

    // ======================================

    void khoiTaoDU(){

        DoUong a,b,c;

        a.setDU(
            1,
            "Coca",
            15000,
            70000,
            100,
            30
        );

        b.setDU(
            2,
            "Sting",
            15000,
            70000,
            100,
            30
        );

        c.setDU(
            3,
            "Bo Huc",
            20000,
            90000,
            80,
            20
        );

        dsDU.push_back(a);
        dsDU.push_back(b);
        dsDU.push_back(c);
    }

    // ======================================

    void hienThiBan(){

        mau(11);

		line(80);

		mau(7);

        cout
        << "| "
        << left
        << setw(5)
        << "Ma"
        << "| "
        << setw(15)
        << "Loai"
        << "| "
        << setw(12)
        << "Gia gio"
        << "| "
        << setw(15)
        << "Khach"
        << "| "
        << setw(15)
        << "Trang thai"
        << " |\n";

        line(80);

        for(int i=0;i<dsBan.size();i++){

            dsBan[i].xuat();
        }

        line(80);
    }

    // ======================================

    void moBan(){
		cout << "\n===== DANH SACH BAN =====\n";

		hienThiBan();
        int ma =
            nhapInt(
                "Nhap ma ban: "
            );

        for(int i=0;i<dsBan.size();i++){

            if(dsBan[i].getMa() == ma){

                if(dsBan[i]
                   .getTrangThai()){

                    cout
                    << "Ban dang choi!\n";

                    return;
                }

                string ten =
                    nhapString(
                        "Nhap ten khach: "
                    );

                dsBan[i].moBan(ten);

                cout
                << "Mo ban thanh cong!\n";

                return;
            }
        }

        cout
        << "Khong tim thay ban!\n";
    }

    // ======================================

    void themNuoc(){
		cout << "\n===== DANH SACH BAN =====\n";

    	hienThiBan();
        int maBan =
            nhapInt(
                "Nhap ma ban: "
            );
		cout << "\n===== DANH SACH NUOC =====\n";

		hienThiDoUong();
        int maNuoc =
            nhapInt(
                "Nhap ma nuoc: "
            );

        for(int i=0;i<dsBan.size();i++){

            if(dsBan[i].getMa() == maBan){

                if(!dsBan[i]
                    .getTrangThai()){

                    cout
                    << "Ban chua mo!\n";

                    return;
                }

                for(int j=0;j<dsDU.size();j++){

                    if(dsDU[j].getMa()
                       == maNuoc){

                        cout
                        << "1. Nuoc le\n";

                        cout
                        << "2. Nuoc loc\n";

                        int loai =
                            nhapInt(
                                "Nhap loai: "
                            );

                        int sl =
                            nhapInt(
                                "Nhap so luong: "
                            );

                        if(loai == 1){

                            dsDU[j].banLe(sl);

                            dsBan[i].themNuoc(
                                dsDU[j].getTen(),
                                "Le",
                                sl,
                                sl
                                *
                                dsDU[j]
                                .getGiaLe()
                            );
                        }
                        else{

                            dsDU[j].banLoc(sl);

                            dsBan[i].themNuoc(
                                dsDU[j].getTen(),
                                "Loc",
                                sl,
                                sl
                                *
                                dsDU[j]
                                .getGiaLoc()
                            );
                        }

                        cout
                        << "Them nuoc thanh cong!\n";

                        return;
                    }
                }
            }
        }

        cout
        << "Khong tim thay!\n";
    }

    // ======================================

    void dongBan(){
    	cout << "\n===== DANH SACH BAN =====\n";
		hienThiBan();
        int ma =
            nhapInt(
                "Nhap ma ban: "
            );

        for(int i=0;i<dsBan.size();i++){

            if(dsBan[i].getMa() == ma){

                if(!dsBan[i]
                    .getTrangThai()){

                    cout
                    << "Ban chua mo!\n";

                    return;
                }

                int gio =
                    nhapInt(
                        "Nhap so gio choi: "
                    );

                double tienBan =
                    gio
                    *
                    dsBan[i]
                    .getGia();

                double tienNuoc =
                    dsBan[i]
                    .tinhTienNuoc();

                double tong =
                    tienBan
                    +
                    tienNuoc;

                doanhThu += tong;
				
				string tenKH = dsBan[i].getTenKhach();

				for(int k=0;k<dsKH.size();k++){
				
				    if(dsKH[k].getTen() == tenKH){
				
				        dsKH[k].congDiem(tong);
				
				        break;
				    }
				}
				
                HoaDon hd(
                    dsHD.size()+1,
                    ma,
                    tienBan,
                    tienNuoc,
                    tong
                );

                dsHD.push_back(hd);

                mau(14);

				cout
				<< "\n===== HOA DON =====\n";
				
				mau(7);

                cout
                << "Tien ban : "
                << tienBan
                << endl;

                cout
                << "Tien nuoc: "
                << tienNuoc
                << endl;

                cout
                << "Tong tien: "
                << tong
                << endl;

                dsBan[i].dongBan();

                return;
            }
        }

        cout
        << "Khong tim thay ban!\n";
    }

    // ======================================

    void hienThiDoUong(){

        mau(11);

		line(90);
		
		mau(7);

        cout
        << "| "
        << left
        << setw(5)
        << "Ma"
        << "| "
        << setw(20)
        << "Ten nuoc"
        << "| "
        << setw(10)
        << "Gia le"
        << "| "
        << setw(10)
        << "Gia loc"
        << "| "
        << setw(10)
        << "Ton le"
        << "| "
        << setw(10)
        << "Ton loc"
        << " |\n";

        line(90);

        for(int i=0;i<dsDU.size();i++){

            dsDU[i].xuat();
        }

        line(90);
    }

    // ======================================

    void themKhachHang(){

        KhachHang kh;

        kh.nhap();

        dsKH.push_back(kh);

        cout
        << "Them KH thanh cong!\n";
    }

    // ======================================

    void hienThiKhachHang(){

        mau(11);

		line(80);
		
		mau(7);

        cout
        << "| "
        << left
        << setw(20)
        << "Ten KH"
        << "| "
        << setw(12)
        << "Gioi tinh"
        << "| "
        << setw(15)
        << "SDT"
        << "| "
        << setw(10)
        << "Diem"
        << " |\n";

        line(80);

        for(int i=0;i<dsKH.size();i++){

            dsKH[i].xuat();
        }

        line(80);
    }

    // ======================================

    void timKhachHang(){

        string key =
            nhapString(
                "Nhap ten can tim: "
            );

        for(int i=0;i<key.length();i++){

            key[i] =
                tolower(key[i]);
        }

        bool check = false;

        for(int i=0;i<dsKH.size();i++){

            string ten =
                dsKH[i].getTen();

            for(int j=0;j<ten.length();j++){

                ten[j] =
                    tolower(ten[j]);
            }

            if(
                ten.find(key)
                != string::npos
            ){

                dsKH[i].xuat();

                check = true;
            }
        }

        if(!check){

            cout
            << "Khong tim thay!\n";
        }
    }

    // ======================================

    void themNhanVien(){

        NhanVien nv;

        nv.nhap();

        dsNV.push_back(nv);

        cout
        << "Them NV thanh cong!\n";
    }

    // ======================================

    void hienThiNhanVien(){

        mau(11);

		line(165);
		
		mau(7);

			cout
			<< "| "
			<< left
			<< setw(5)
			<< "STT"
			<< "| "
			<< setw(20)
			<< "Ten NV"
			<< "| "
			<< setw(10)
			<< "Gioi tinh"
			<< "| "
			<< setw(15)
			<< "Chuc vu"
			<< "| "
			<< setw(8)
			<< "Ca 1"
			<< "| "
			<< setw(8)
			<< "Ca 2"
			<< "| "
			<< setw(8)
			<< "Ca 3"
			<< "| "
			<< setw(10)
			<< "Tong ca"
			<< "| "
			<< setw(15)
			<< "Luong"
			<< "| "
			<< setw(12)
			<< "Trang thai"
			<< "| "
			<< setw(15)
			<< "Ngay tra"
			<< " |\n";
			
			line(165);
        for(int i=0;i<dsNV.size();i++){

		    cout
		    << "| "
		    << left
		    << setw(5)
		    << i + 1;
		
		    dsNV[i].xuat();
		}

        line(120);
    }

    // ======================================

    void hienThiHoaDon(){

        mau(11);

		line(70);

		mau(7);

        cout
        << "| "
        << left
        << setw(5)
        << "Ma"
        << "| "
        << setw(8)
        << "Ban"
        << "| "
        << setw(15)
        << "Tien ban"
        << "| "
        << setw(15)
        << "Tien nuoc"
        << "| "
        << setw(15)
        << "Tong"
        << " |\n";

        line(70);

        for(int i=0;i<dsHD.size();i++){

            dsHD[i].xuat();
        }

        line(70);
    }

    // ======================================

    void thongKeDoanhThu(){

        cout
        << "Tong doanh thu: "
        << doanhThu
        << endl;
    }

    // ======================================

    void thongKeTonKho(){

        line(60);

        for(int i=0;i<dsDU.size();i++){

            cout
            << dsDU[i].getTen()
            << " | Ton le: "
            << dsDU[i].getTonLe()
            << " | Ton loc: "
            << dsDU[i].getTonLoc()
            << endl;
        }

        line(60);
    }

    // ======================================

    void thongKeNuocDaBan(){

        line(60);

        for(int i=0;i<dsDU.size();i++){

            cout
            << dsDU[i].getTen()
            << " | Da ban le: "
            << dsDU[i].getDaBanLe()
            << " | Da ban loc: "
            << dsDU[i].getDaBanLoc()
            << endl;
        }

        line(60);
    }
    void traLuongNhanVien(){

    if(quyen != "admin"){

        cout
        << "Chi admin moi duoc tra luong!\n";

        return;
    }

    if(dsNV.empty()){

        cout
        << "Chua co nhan vien!\n";

        return;
    }

    hienThiNhanVien();

    int stt =
        nhapInt(
            "Nhap vi tri nhan vien can tra luong: "
        );

    if(stt < 1 || stt > dsNV.size()){

        cout
        << "Khong hop le!\n";

        return;
    }

    dsNV[stt - 1].traLuong();
}
};

// ==========================================
// MAIN
// ==========================================

int main(){

    QuanLy ql;

    cout
    << "===== DANG NHAP =====\n";

	mau(14);

	cout << "Dang nhap";
	
	for(int i=0;i<5;i++){
	
	    cout << ".";
	
	    Sleep(300);
	}
	
	cout << endl;
	
	mau(7);

    if(!ql.dangNhap()){

        cout
        << "Dang nhap that bai!\n";

        return 0;
    }

    int chon;

    do{

        system("cls");
        
        mau(11);

		cout << "========================================\n";
		cout << "          QUAN LY QUAN BIDA             \n";
		cout << "========================================\n";
		
		mau(7);

		title("QUAN LY QUAN BIDA");

        mau(10);
		cout << "1. Danh sach ban\n";
		
		mau(11);
		cout << "2. Mo ban\n";
		
		mau(12);
		cout << "3. Dong ban / thanh toan\n";
		
		mau(13);
		cout << "4. Danh sach do uong\n";
		
		mau(14);
		cout << "5. Them nuoc vao ban\n";
		
		mau(6);
		cout << "6. Them khach hang\n";
		
		mau(9);
		cout << "7. Tim khach hang\n";
		
		mau(5);
		cout << "8. Danh sach khach hang\n";
		
		mau(3);
		cout << "9. Them nhan vien\n";
		
		mau(2);
		cout << "10. Danh sach nhan vien\n";
		
		mau(12);
		cout << "11. Danh sach hoa don\n";
		
		mau(14);
		cout << "12. Thong ke doanh thu\n";
		
		mau(11);
		cout << "13. Thong ke ton kho\n";
		
		mau(10);
		cout << "14. Thong ke nuoc da ban\n";
		
		mau(13);
		cout << "15. Tra luong nhan vien\n";
		
		mau(4);
		cout << "0. Thoat\n";
		
		mau(7);

        line(60);

        chon =
            nhapInt(
                "Nhap lua chon: "
            );

        switch(chon){

        case 1:

            ql.hienThiBan();

            break;

        case 2:

            ql.moBan();

            break;

        case 3:

            ql.dongBan();

            break;

        case 4:

            ql.hienThiDoUong();

            break;

        case 5:

            ql.themNuoc();

            break;

        case 6:

            ql.themKhachHang();

            break;

        case 7:

            ql.timKhachHang();

            break;

        case 8:

            ql.hienThiKhachHang();

            break;

        case 9:

            if(
                ql.getQuyen()
                != "admin"
            ){

                cout
                << "Chi admin moi duoc them!\n";

                break;
            }

            ql.themNhanVien();

            break;

        case 10:

            ql.hienThiNhanVien();

            break;

        case 11:

            ql.hienThiHoaDon();

            break;

        case 12:

            if(
                ql.getQuyen()
                != "admin"
            ){

                cout
                << "Chi admin moi duoc xem!\n";

                break;
            }

            ql.thongKeDoanhThu();

            break;

        case 13:

            ql.thongKeTonKho();

            break;

        case 14:

            ql.thongKeNuocDaBan();

            break;
        case 15:

  		  ql.traLuongNhanVien();

  			  break;

        case 0:

            cout
            << "Thoat chuong trinh!\n";

            break;

        default:

            cout
            << "Lua chon khong hop le!\n";
        }
		system("pause");
    }while(chon != 0);

    return 0;
}
