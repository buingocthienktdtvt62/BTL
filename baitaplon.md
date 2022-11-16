#include<iostream>
#include <sstream>
#include <fstream>
#include <stdlib.h>
//#include<string.h>
#include <conio.h>
//#include <string>
#include<stdio.h>
#include<vector>
#include <bits/stdc++.h>
#define MAX_LENGTH 100
#define stringify( name ) #name 
#include <windows.h>
using namespace std;

struct SinhVien {
	int maSo;
	string ten, lop, ngaySinh;
	double anten, tinHieu, tinHoc, lapTrinh, tiengAnh, diemRenLuyen, tBC;
};
typedef struct SinhVien SV;

struct Node {
	SV data;
	Node* next;
};
typedef struct Node NODE;

struct LinkedList {
	NODE* pHead;
	NODE* pTail;
};
typedef struct LinkedList LINKED_LIST;

void KhoiTao(LINKED_LIST& ds) {
	ds.pHead = NULL;
	ds.pTail = NULL;
}
//Ham ktra empty:
bool kiemTraRong(LINKED_LIST ds) {
	if (ds.pHead == NULL) {
		return true;
	}
	return !true;
}
//Ham tao Node:
NODE* taoNode(SV x) {
	NODE* p;
	p = new NODE;
	if (p == NULL) {
		cout << "ERROR" << endl;
		return NULL;
	}
	p->data = x;
	p->next = NULL;
	return p;
}
//Ham add SV vao cuoi danh sach:
void chenCuoi(LINKED_LIST& ds, NODE* p) {
	if (ds.pHead == NULL) {
		ds.pHead = p;
		ds.pTail = p;
	}
	else {
		ds.pTail->next = p;
		ds.pTail = p;
	}
}

void xoaDau(LINKED_LIST& ds) {
	//tao node p
	NODE* p = new NODE;
	//gan p bang node pHead dau tien cua danh sach 
	p = ds.pHead;
	//thay doi lai pHead cua danh sach
	ds.pHead = ds.pHead->next;
	//gan node p ban dau tro den NULL
	p->next = NULL;
	//xoa node p
	delete p;
	cout << "DELETED~!!" << endl;
}
//Ham xoa SV cuoi danh sach:
void xoaCuoi(LINKED_LIST& ds)
{
	//duyet cac phan tu co trong danh sach
	for (NODE* k = ds.pHead; k != NULL; k = k->next)
	{
		//neu duyet den phan tu pTail cuoi trong danh sach
		if (k->next == ds.pTail)
		{
			//xoa phan tu cuoi
			delete ds.pTail;
			//tro phan tu truoc phan tu cuoi ve NULL
			k->next = NULL;
			//thay doi lai phan tu cuoi pTail cua danh sach
			ds.pTail = k;
			cout << "DELETED~!!" << endl;
		}
	}
}
//Ham chinh textcolor:
void TextColor(int x) {
	HANDLE h = GetStdHandle(STD_OUTPUT_HANDLE);
	SetConsoleTextAttribute(h, x);
}

//Cac ham kiem tra nhap diem:
double stringToDouble(string s) {
	stringstream geek(s);
	int diem;
	geek >> diem;
	return diem;
}
int stringToInt(string s) {
	stringstream geek(s);
	int diem;
	geek >> diem;
	return diem;
}
bool kiemTraNhapSo(string s) {
	std::string::const_iterator it = s.begin();
	while (it != s.end() && std::isdigit(*it)) ++it;
	return !s.empty() && it == s.end();
}
bool kiemTraNhapDiem(string s) {
	bool check = kiemTraNhapSo(s);
	if (!check) {
		return false;
	}
	int diem = stringToInt(s);
	if (diem >= 0 && diem <= 10) {
		return true;
	}
	return false;
}
double nhapDiem() {
	string s;
nhaplai:
	cin >> s;
	bool check = kiemTraNhapDiem(s);
	if (!check) {
		TextColor(4);
		cout << "Nhap lai:";
		TextColor(7);
		goto nhaplai;
	}
	return stringToDouble(s);
}
//Ham ktra Maso khi nhap:
int nhapMaSo(LINKED_LIST& ds, int size) {
	int maSo;
nhaplai:
	cin >> maSo;
	for (NODE* k = ds.pHead; k != NULL; k = k->next) {
		if (maSo == k->data.maSo) {
			TextColor(4);
			cout << "AVAILABLE!!" << endl;
			cout << "Nhap lai:";
			TextColor(7);
			goto nhaplai;
		}
	}
	return maSo;
}
//Ham nhap:
void Nhap(LINKED_LIST& ds, int size) {
	cout << "NHAP THONG TIN SINH VIEN" << endl;
	SV x;
	cout << "Ma sinh vien : ";
	x.maSo = nhapMaSo(ds,size);
	cout << "Ten sinh vien : ";
	cin >> x.ten;
	cout << "Lop : ";
	cin >> x.lop;
	cout << "Ngay sinh  : ";
	cin >> x.ngaySinh;
	cout << "Diem ren luyen : ";
	cin >> x.diemRenLuyen;
	cout << "Anten : ";
	x.anten = nhapDiem();
	cout << "Tin hieu : ";
	x.tinHieu = nhapDiem();
	cout << "Tin Hoc : ";
	x.tinHoc = nhapDiem();
	cout << "Lap trinh : ";
	x.lapTrinh = nhapDiem();
	cout << "Tieng anh : ";
	x.tiengAnh = nhapDiem();
	cout << "TBC:" << (x.tBC = (x.anten + x.tinHieu + x.tinHoc + x.lapTrinh + x.tiengAnh) / 5);
	cout << endl << endl;
	NODE* p = new NODE;
	p = taoNode(x);
	chenCuoi(ds, p);
}
//ham support cho Ham in danh sach:
void displaySinhVien(SV sv) {
	cout << "Ma sinh vien : " << sv.maSo << " | ";
	cout << "Ten sinh vien : " << sv.ten << " | ";
	cout << "Lop : " << sv.lop << " | ";
	cout << "Ngay sinh : " << sv.ngaySinh << " | ";
	cout << "Diem ren luyen : " << sv.diemRenLuyen << " | ";
	cout << "Anten : " << sv.anten << " | ";
	cout << "Tin hieu : " << sv.tinHieu << " | ";
	cout << "Tin Hoc : " << sv.tinHoc << " | ";
	cout << "Lap trinh : " << sv.lapTrinh << " | ";
	cout << "Tieng anh : " << sv.tiengAnh << " | ";
	cout << "Tbc:" << sv.tBC << " . " << endl;
}
//Ham in danh sach:
void xuatDanhSachSV(LINKED_LIST ds) {
	for (NODE* p = ds.pHead; p != NULL; p = p->next) {
		displaySinhVien(p->data);
	}
}
//Ham xoa tat ca SV trong danh sach:
void xoaAll(LINKED_LIST& ds, int size) {
	//duyet toan bo danh sach
	for (NODE* k = ds.pHead; k != NULL; k = k->next)
	{
		//tao node p gan bang phan tu dau danh sach
		NODE* p = ds.pHead;
		//gan phan tu dau danh sach bang p->next
		ds.pHead = p->next;
		//xoa di node p
		delete p;
	}
	//gan phan tu cuoi danh sach ve NULL
	ds.pTail = NULL;
}
//Ham tinh do dai cua danh sach:
int Size(LINKED_LIST& ds) {
	int size = 0;
	for (NODE* k = ds.pHead; k != NULL; k = k->next) {
		size++;
	}
	return size;
}
//Ham xoa SV theo maso:
void xoaMaSv(LINKED_LIST& ds) {
	NODE* p = new NODE;
	SV x;
	p = taoNode(x);
	cout << "SV NEED TO BE DELETE: ";
	int maSo;
	cin >> maSo;

	if (ds.pHead->data.maSo == maSo) {
		//goi ham xoa dau
		xoaDau(ds);
		//ket thuc ham
		return;
	}

	//neu data bang voi pTail->data thi xoa cuoi
	if (ds.pTail->data.maSo == maSo) {
		//goi ham xoa cuoi
		xoaCuoi(ds);
		//ket thuc ham
		return;
	}

	for (NODE* k = ds.pHead; k != NULL; k = k->next) {
		if (k->data.maSo == maSo) {
			p->next = k->next;
			delete k;
			cout << "DELETED~!!" << endl;
			return;
		}
		else {
			TextColor(4);
			cout << "NON-EXIST" << endl;
			TextColor(7);
		}
		p = k;
	}
}
//Ham kiem tra ton tai SV:
void kiemTraTonTaiSv(LINKED_LIST& ds, int size) {
	NODE* p = new NODE;
	SV x;
	p = taoNode(x);
	cout << "SV NEED TO BE CHECK: ";
	cin >> p->data.maSo;
	for (NODE* k = ds.pHead; k != NULL; k = k->next) {
		if (k->data.maSo == p->data.maSo) {
			TextColor(4);
			cout << "EXIST" << endl;
			TextColor(7);
		}
		else {
			TextColor(4);
			cout << "NON-EXIST" << endl;
			TextColor(7);
		}
	}
}
//Ham menu dung de chinh sua:
void menuChinhSuaSinhVien() {
	TextColor(4);
	cout << "1. Ho ten: " << endl;
	cout << "2. Lop: " << endl;
	cout << "3. Ngay sinh: " << endl;
	cout << "4. Diem: " << endl;
	cout<<"0. ESC."<<endl;
	TextColor(7);
}
void menuMonhoc() {
	TextColor(2);
	cout << "1. Diem ren luyen:"<<endl;
	cout << "2. Anten: " << endl;
	cout << "3. Tin Hieu: " << endl;
	cout << "4. Tin Hoc: " << endl;
	cout << "5. Lap Trinh: " << endl;
	cout << "6. Tieng Anh: " << endl;
	cout<<"0. ESC."<<endl;
	TextColor(7);
}
void chinhSuaSV(LINKED_LIST& ds, int size) {
	NODE* p = new NODE;
	SV x;
	p = taoNode(x);
	cout << "SV NEED TO BE EDIT: ";
	cin >> p->data.maSo;
	for (NODE* k = ds.pHead; k != NULL; k = k->next) {
		if (k->data.maSo != p->data.maSo) {
			TextColor(4);
			cout << "NON-EXIST" << endl;
			TextColor(7);
		}
		else {
			p = k;
			do {
				system("cls");
				int a;
				menuChinhSuaSinhVien();
				TextColor(4);
				cout << "CONTENT TO EDIT: ";
				TextColor(7);
				cin >> a;
				switch (a) {
				case 1: {
					cout << "Nhap ho ten: ";
					cin >> p->data.ten;
					cout << "EDITED." << endl;
					break;
				}
				case 2: {
					cout << "Nhap lop: ";
					cin >> p->data.lop;
					cout << "EDITED." << endl;
					break;
				}
				case 3: {
					cout << "Nhap ngay sinh: ";
					cin >> p->data.ngaySinh;
					cout << "EDITED." << endl;
					break;
				}
				case 4: {
				    do {
				        system("cls");
				        int b;
				        menuMonhoc();
				        TextColor(4);
				        cout << "CONTENT TO EDIT: ";
				        TextColor(7);
				        cin >> b;
				        switch (b) {
				        case 1: {
					     cout << "Diem ren luyen: ";
					     cin >> p->data.diemRenLuyen;
					     cout << "EDITED." << endl;
					     break;
				    }
						case 2: {
					     cout << "Anten: ";
					     cin >> p->data.anten;
					     cout << "EDITED." << endl;
					     break;
				    }
				        case 3: {
					    cout << "Tin Hieu: ";
					    cin >> p->data.tinHieu;
					    cout << "EDITED." << endl;
					    break;
				    }
				        case 4: {
					    cout << "Tin Hoc: ";
					    cin >> p->data.tinHoc;
					    cout << "EDITED." << endl;
					    break;
				    }
				        case 5: {
				        cout << "Lap Trinh: ";
					    cin >> p->data.lapTrinh;
					    cout << "EDITED." << endl;
					    break;
				    }
				        case 6: {
				        cout << "Tieng Anh: ";
					    cin >> p->data.tiengAnh;
					    cout << "EDITED." << endl;
					    break;
				    }
				        case 0: {
					    return;
				    }
				        default:
					    break;
				    }
				    cout << "**** Nhan phim bat ky de luu thong tin ****";
				    char ch = _getch();
			        }while (true);
				break;
				}
				case 0: {
					return;
				}
				default:
					break;
				}
				cout << "**** Nhan phim bat ky de luu thong tin ****";
				char ch = _getch();
			} while (true);
		}
	}
}
//Ham tiem kiem SV:
void timKiemSv(LINKED_LIST& ds, int size) {
	NODE* p = new NODE;
	SV x;
	p = taoNode(x);
	TextColor(4);
	cout << "SV NEED TO BE FIND: ";
	TextColor(7);
	cin >> p->data.maSo;
	for (NODE* k = ds.pHead; k != NULL; k = k->next) {
		if (k->data.maSo == p->data.maSo) {
			xuatDanhSachSV(ds);
		}
		else {
			TextColor(4);
			cout << "NON-EXIST" << endl;
			TextColor(7);

		}
	}
}
//Ham sap xep SV:
void sapXep(LINKED_LIST& ds, int size) {
	for (Node* i = ds.pHead; i != NULL; i = i->next) {
		Node* q = i;
		for (Node* j = i->next; j != NULL; j = j->next) {
			if (q->data.tBC > j->data.tBC) {
				q = j;
			}
			else if (q->data.tBC == j->data.tBC) {
				if (q->data.ten > j->data.ten) {
					q = j;
				}
			}
		}
		SV tmp = q->data;
		q->data = i->data;
		i->data = tmp;
	}
	xuatDanhSachSV(ds);
}
//Menu chinh:
void mainMenu() {
	TextColor(4);
	cout << "     ********************************************* " << endl;
	TextColor(4);
	cout << "     * ";TextColor(2);cout<<"1.Nhap thong tin Sinhvien.                ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"2.In danh sach Sinhvien.                  ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"3.Tong Sinh vien hien tai.                ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"4.Xoa tat ca sinh vien.                   ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"5.Chinh sua Sinh vien.                    ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"6.Tim Sinh Vien (theo Maso).              ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"7.Xoa 1 Sinh vien (theo Maso).            ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     * ";TextColor(2);cout<<"8.Sap xep Sinh vien (theo TBC va ten).    ";TextColor(4);cout<<"* " << endl;TextColor(4);
	cout << "     ********************************************* " << endl;
	TextColor(7);
}
//Ham main:
int main() {
	LINKED_LIST ds;
	int size = 0;
	int choose;
	KhoiTao(ds);
	do {
		mainMenu();
		TextColor(4);
		cout << " YOUR CHOOSE IS(Nhap '0' se thoat): ";
		TextColor(7);
		cin >> choose;
		cout << "-----------------------------------------------------------------------------------------------------------------------------------------------------------" << endl;
		switch (choose) {
		case 1: {
			Nhap(ds, size);
			++size;
			break;
		}
		case 2: {
			if (kiemTraRong(ds) == true) {
				cout << "ISEMPTY" << endl;
			}
			else {
				cout << "LIST OF SINH VIEN: " << endl;
				xuatDanhSachSV(ds);
			}
			break;
		}
		case 3: {
			cout << "TOTAL SINH VIEN: " << size << endl;
			break;
		}
		case 4: {
			if (kiemTraRong(ds) == true) {
				cout << "ISEMPTY!!!. CAN NOT DELETE." << endl;
			}
			else {
				xoaAll(ds, size);
				size = 0;
				cout << "DELETED." << endl;
			}
			break;
		}
		case 5: {
			if (kiemTraRong(ds) == !true) {
				chinhSuaSV(ds, size);
			}
			else {
				cout << "ISEMPTY!!!. CAN NOT EDIT!!!" << endl;
			}
			break;
		}
		case 6: {
			if (kiemTraRong(ds) == !true) {
				timKiemSv(ds, size);
			}
			else {
				cout << "ISEMPTY!!!. CAN NOT FIND!!!!" << endl;
			}
			break;
		}
		case 7: {
			if (kiemTraRong(ds) == !true) {
				xoaMaSv(ds);
			}
			else {
				cout << "ISEMPTY!!!" << endl;
			}
			break;
		}
		case 8: {
			if (kiemTraRong(ds) == !true) {
				sapXep(ds, size);
				cout << "SORTED." << endl;
			}
			else {
				cout << "ISEMPTY!!!. CAN NOT SORT" << endl;
			}
			break;
		}
		}
		cout << "**** Nhan phim bat ky de tiep tuc ****";
		char ch = _getch();
		system("cls");
	} while (choose != 0);
}
