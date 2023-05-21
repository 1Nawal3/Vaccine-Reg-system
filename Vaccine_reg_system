#include <iostream>
#include <fstream>
#include <string.h>
#include <string>
#include <sstream>
#include <windows.h>
#include <locale.h>
#include <io.h> 
#include <fcntl.h> 
#include <ctype.h>
#include <vector>
#include <ctime>
#include <limits>
#include <cstddef>
#pragma warning(disable : 4996)
using namespace std;

// Kullanıcı prototipleri
struct VaccineSystem
{
	string              strMemberID;
	string              strMemberName;
	string              strMemberSurname;
	unsigned int	    intMemberAge;
	string              strMemberCity;
	unsigned int        intVaccineCount;
	string              strVaccineName;
}Patient;

struct VaccineDate
{
	int					intVaccineDay;
	int					intVaccineMonth;
	int					intVaccineYear;
}Date;

// Fonksiyon prototipleri
void PrintInfo();
void GetPatient();
void WriteInfo();
void UserID();
void CheckID();
void ReadInfo();
void EditPatient();
void SearchPatient();
void NewVaccine();

// main Fonksiyonu
int main()
{
	ofstream databaseFile;
	databaseFile.open("database.txt", ios::in | ios::out | ios::app);
	databaseFile.close();

	int choice;
	choice = -1;
	do
	{

		cout << "\n\t\t        ------WELCOME TO VACCINATION MANAGEMENT SYSTEM------           \n\n";
		cout << "\t********************************************************************************\n"
			<< "\t********************************************************************************\n"
			<< "\t***  1- New patient registration                                             ***\n"
			<< "\t***  2- View all patients                                                    ***\n"
			<< "\t***  3- Search a patient                                                     ***\n"
			<< "\t***  4- Edit a patient info                                                  ***\n"
			<< "\t***  5- New vaccination record                                               ***\n"
			<< "\t***  6- -                                                                    ***\n"
			<< "\t***  7- -                                                                    ***\n"
			<< "\t***  0- Exit                                                                 ***\n"
			<< "\t********************************************************************************\n"
			<< "\t********************************************************************************\n";

		cout << "\t***  Enter choice: ";
		cin >> choice;
		cout << "\t********************************************************************************" << endl;
		switch (choice)
		{
		case 1:
			system("CLS");
			GetPatient();
			UserID();
			CheckID();
			PrintInfo();
			WriteInfo();
			break;
		case 2:
			system("CLS");
			ReadInfo();
			break;
		case 3:
			system("CLS");
			SearchPatient();
			break;
		case 4:
			system("CLS");
			EditPatient();
			break;
		case 5:
			system("CLS");
			NewVaccine();
			break;
		case 0:
			system("CLS");
			cout << "\t********************************************************************************\n";
			cout << "\t***                 The system has been successfully exited.                 ***\n";
			cout << "\t********************************************************************************\n";
			break;
		default:
			system("CLS");
			cout << "\n\t***  The choice you entered was not valid,                                   ***\n";
			cout << "\t***  please enter a valid option.                                            ***\n";
			break;
		}
	} while (choice);

	return 0;
}

// PrintInfo Fonksiyonu
void PrintInfo()
{
	// Veritabanına yeni kaydedilmiş hasta bilgileri ekrana bastırılır.
	system("CLS");
	cout << endl;
	cout << "\n\t***  New patient information has been saved in the database successfully!    ***\n";
	cout << endl;
	cout << "\t***  ID: \t \t \t" << Patient.strMemberID << endl;
	cout << "\t***  Name: \t \t \t" << Patient.strMemberName << endl;
	cout << "\t***  Surname: \t \t \t" << Patient.strMemberSurname << endl;
	cout << "\t***  Age: \t \t \t" << Patient.intMemberAge << endl;
	cout << "\t***  City: \t \t \t" << Patient.strMemberCity << endl;
	cout << "\t***  Last Vac. Date: \t \t" << Date.intVaccineDay << "/" << Date.intVaccineMonth << "/" << Date.intVaccineYear << endl;
	cout << "\t***  Vac. Dose No.: \t \t" << Patient.intVaccineCount << endl;
	cout << "\t***  Vac. Name: \t \t" << Patient.strVaccineName << endl;
}

// UserID Fonksiyonu
void UserID()
{
	// Veritabanına girilen yeni hasta bilgilerine has bir ID numarası üretilir.
	string tempID;
	constexpr int CHAR_LENGTH = 1;

	// İki adet rastgele harf ve iki adet rastgele rakam üretilir.
	srand(time(NULL));
	const char arrayNum[10] = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9' };
	char randLetter;
	char randLetter2;
	int randNum;
	int randNum2;

	randLetter = 'A' + rand() % 26;
	randLetter2 = 'A' + rand() % 26;
	randNum = rand() % 10;
	randNum2 = rand() % 10;

	string tmpLetter(CHAR_LENGTH, randLetter);
	string tmpLetter2(CHAR_LENGTH, randLetter2);
	string tmpNum = to_string(randNum);
	string tmpNum2 = to_string(randNum2);

	// Elde edilen harfler ve rakamlar tempID işaretçisine atılır.
	tempID = tmpLetter + tmpLetter2 + tmpNum + tmpNum2;
	// tempID işaretçisindeki veri, structure yapısı içerisine atılır.
	Patient.strMemberID = tempID;
}

// CheckID Fonksiyonu
void CheckID()
{
	// TXT dosyasının içerisinde bulunan bilgiler okunur.
	ifstream databaseReadFile("database.txt");

	// Dosya açma hata kontrolü
	if (!databaseReadFile) {
		cout << "\n\t***  Can't open file: database.txt!                                          ***\n";
		exit(1);
	}

	// ID numarasının bulunduğu satır line değişkenine atanacaktır.
	string line;

	// While döngüsü içerisinde veritabanı içerisinde eş ID numarası aranır.
	// ID numarası bulunursa yeni bir ID üretilir.
	// ID numarası bulunamazsa üretilen adı kullanıcıya atanır.
	while (getline(databaseReadFile, line))
	{
		size_t Position = (line).find(Patient.strMemberID);
		if (Position != string::npos)
		{
			return UserID();
		}
		else if (Position == string::npos)
		{
			break;
		}
		// Veritabanı dosyası kapatılır.
		databaseReadFile.close();
	}
}

// WriteInfo Fonksiyonu
void WriteInfo()
{
	// Dosyaya yazma işlemi için akış oluşturma (Dosya append modunda açıldı. Bu sayede eski verilerin üzerine yeni veriler yazılmadı.)
	ofstream databaseWriteFile("database.txt", ios::app);

	// Dosya açma hata kontrolü
	if (!databaseWriteFile) {
		cout << "Can't open file: database.txt!" << endl;
		exit(1);
	}

	// Dosyaya kullanıcının girdiği yeni veriler eklendi.
	databaseWriteFile << Patient.strMemberID << " " << Patient.strMemberName << " " << Patient.strMemberSurname << " " << Patient.intMemberAge << " " << Patient.strMemberCity << " " << Date.intVaccineDay << "/" << Date.intVaccineMonth << "/" << Date.intVaccineYear << " " << Patient.intVaccineCount << " " << Patient.strVaccineName << endl;

	// İşlem yapılan dosya kapatılır.
	databaseWriteFile.close();
}

// ReadInfo Fonksiyonu
void ReadInfo()
{
	// TXT dosyasının çıktısını almak için kullanılan bir string dizisi oluşturuldu.
	string ReadInfo;

	// TXT dosyasının içerisinde bulunan bilgiler okunur.
	ifstream databaseReadFile("database.txt");

	// Dosya açma hata kontrolü
	if (!databaseReadFile) {
		cout << "Can't open file: database.txt!" << endl;
		exit(1);
	}

	// Dosyanın satır satır ve boşluklara duyarlı olmaması için getline() fonksiyonu kullanılarak bir while döngüsü içerisinde okunur.
	cout << "\n\t\t                   ------PATIENT INFORMATION------           \n\n";
	cout << "\t********************************************************************************\n";
	cout << "\t***  ID   Name  Surname Age  City   Last Vac. Date  Vac. Dose No.  Vac. Name ***\n";
	cout << "\t********************************************************************************\n";
	while (getline(databaseReadFile, ReadInfo)) {
		// TXT dosyasının içerisindeki bilgilerin ekrandaki çıktısı
		cout << "\t    " << ReadInfo << endl;
	}
	cout << endl;

	// İşlem yapılan dosya kapatılır.
	databaseReadFile.close();
}

// GetPatient Fonksiyonu
void GetPatient()
{
	// Kullanıcı, Structure sayesinde yeni bir kullanıcı yaratır.
	cout << endl;
	cout << "\n\t\t        ------ADD NEW PATIENT------           \n\n";
	cout << endl;
	cout << "\t*** Please enter the patient's name: \t\t\t";
	cin >> Patient.strMemberName;
	Patient.strMemberName[0] = toupper(Patient.strMemberName[0]);
	cout << "\t*** Please enter the patient's surname: \t\t";
	cin >> Patient.strMemberSurname;
	Patient.strMemberSurname[0] = toupper(Patient.strMemberSurname[0]);
	cout << "\t*** Please enter the patient's age: \t\t\t";
	cin >> Patient.intMemberAge;
	cout << "\t*** Please enter the city where the patient lives: \t";
	cin >> Patient.strMemberCity;
	Patient.strMemberCity[0] = toupper(Patient.strMemberCity[0]);
	Date.intVaccineDay = 01;
	Date.intVaccineMonth = 06;
	Date.intVaccineYear = 2020;
	Patient.intVaccineCount = 0;
	Patient.strVaccineName = "NULL";

	cin.sync();
}

// EditPatient Fonksiyonu
void EditPatient()
{
	system("CLS");

	// TXT dosyasının içerisinde bulunan bilgiler okunur.
	fstream databaseReadFile("database.txt", ios::in | ios::out);

	// Dosya açma hata kontrolü
	if (!databaseReadFile) {
		cout << "\n\t***  Can't open file: database.txt!                                          ***\n";
		exit(1);
	}

	// Kullanıcıdan hastanın sahip olduğu ID numarasını girmesi istenir.
	string patientID;
	cout << "\n\n\n\t*** Please enter the patient's ID: ";
	cin >> patientID;

	// ID numarasının bulunduğu satır line değişkenine atanacaktır.
	string line;
	// Veritabanında işlem yapılacak satır indisini saklar. (Örn. 3. satır)
	int currentLineNumber;
	currentLineNumber = 0;
	// int currentLineNumber = 0;

	// While döngüsü içerisinde spesifik pozisyonda kullanıcının girdiği ID numarası aranır.
	// ID numarası bulunursa tüm satır line değişkenine atılır.
	// line değişkeni ekrana bastırılır.
	cout << endl;
	cout << "\n\t\t                   ------PATIENT INFORMATION------                   \n\n";
	cout << "\t********************************************************************************\n";
	cout << "\t***  ID   Name  Surname Age  City   Last Vac. Date  Vac. Dose No.  Vac. Name ***\n";
	cout << "\t********************************************************************************\n";

	while (getline(databaseReadFile, line))
	{
		// Kullanıcı tarafından girilen ID'nin bulunduğu pozisyon aranır.
		size_t Position = line.find(patientID);
		if (Position != string::npos)
		{
			// Elde edilen kullanıcı bilgilerine sahip satır ekrana bastırılır.
			cout << "\n\t***  " << line << endl;

			int updateChoice;

			cout << "\n\t\t              ------UPDATE PATIENT DATA MENU------              \n\n";
			cout << "\t********************************************************************************\n"
				<< "\t********************************************************************************\n"
				<< "\t***  1- Update name of a patient                                             ***\n"
				<< "\t***  2- Update surname of a patient                                          ***\n"
				<< "\t***  3- Update age of a patient                                              ***\n"
				<< "\t***  4- Update the city where the patient lives                              ***\n"
				<< "\t***  9- Return to main menu                                                  ***\n"
				<< "\t********************************************************************************\n"
				<< "\t********************************************************************************\n";

			cout << "\t***  Enter choice: ";
			cin >> updateChoice;
			cout << "\t********************************************************************************" << endl;

			// İsim Değiştirme Fonksiyonu
			if (updateChoice == 1)
			{
				databaseReadFile.seekg(line.find(patientID), ios::beg);

				// String içerisinde boşluk aramak için gerekli olan komutlar
				string whitespace(" ");
				size_t found = line.find(whitespace);

				// line stringi 3 parçaya bölünür.
				// 1. kısım, işlem yapılacak bölmeden öncesidir. beforeTheLine içerisinde saklanır.
				// 2. kısım, işlem yapılacak bölmedir. name içerisinde saklanır.
				// 3. kısım, işlem yapılacak bölmeden sonrasıdır. restOfLine içerisinde saklanır.
				string beforeTheLine = line.substr(0, found);
				string name = line.substr(found + 1, line.substr(found + 1, line.length()).find(" "));
				string restOfLine = line.substr(beforeTheLine.length() + name.length() + 2, line.length());

				system("CLS");
				// String içerisinden elde edilen isim ekrana bastırılır.
				cout << "\n\t***  Patient's name: \t \t \t" << name << endl;
				// Kullanıcıdan değiştirilmesini istediği ismi girmesi istenir.
				string newPatientName;
				cout << "\n\t***  Enter the new name of the patient: ";
				cin >> newPatientName;

				// updatedLine değişkeni içerisinde parçalanmış bölmeler yeni isim eklenerek tekrardan birleştirilir.
				string updatedLine = beforeTheLine + " " + newPatientName + " " + restOfLine;

				// Dosyadaki veritabanı okunur ve güncellenir.
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Okunan veriler bir vectorun içerisinde saklanır.
				vector<string> fileLineDatas;
				// Geçici kullanılan, işlem yapılacak satırı içerisinde saklar.
				string readLine;
				// Geçici kullanılan, veritabanında işlem yapılacak satır indisini saklayacak değişken (Örn. 3. satır)
				int readLineNumber = 0;

				// Düzenlenen satır eğer satır indisleri eşleşme sağlarsa vector içerisine yazılır.
				// Aksi durumda readLineNumber == currentLineNumber eşleşmesi sağlanana kadar readLineNumber birer artırılır.
				while (getline(databaseReadFile, readLine)) {
					if (readLineNumber == currentLineNumber) {
						fileLineDatas.push_back(updatedLine);
					}
					else {
						fileLineDatas.push_back(readLine);
					}
					readLineNumber++;
				}
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Veritabanının içi tamamen temizlenir.
				databaseReadFile.clear();
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Vector içerisinde bulunan tüm içerik dosyanın içerisine tekrardan yazılır.
				for (int i = 0; i < fileLineDatas.size(); i++)
				{
					databaseReadFile.write((fileLineDatas[i] + "\n").c_str(), fileLineDatas[i].length() + 1);
				}

				// İşlem yapılan dosya kapatılır.
				databaseReadFile.close();
				system("CLS");
				cout << "\n\t***  Patient information has been successfully updated!                      ***\n";
				cout << "\n\t***  " << updatedLine << endl;
			}

			// Soyisim değiştirme fonksiyonu
			if (updateChoice == 2)
			{
				databaseReadFile.seekg(line.find(patientID), ios::beg);

				// String içerisinde boşluk aramak için gerekli olan komutlar
				string whitespace(" ");
				size_t found = line.find(whitespace);
				size_t found2 = line.find(" ", found + 1, 1);

				// line stringi 3 parçaya bölünür.
				// 1. kısım, işlem yapılacak bölmeden öncesidir. beforeTheLine içerisinde saklanır.
				// 2. kısım, işlem yapılacak bölmedir. surname içerisinde saklanır.
				// 3. kısım, işlem yapılacak bölmeden sonrasıdır. restOfLine içerisinde saklanır.
				string beforeTheLine = line.substr(0, found2);
				string surname = line.substr(found2 + 1, line.substr(found2 + 1, line.length()).find(" "));
				string restOfLine = line.substr(beforeTheLine.length() + surname.length() + 2, line.length());

				system("CLS");
				// String içerisinden elde edilen soyisim ekrana bastırılır.
				cout << "\n\t***  Patient's surname: \t \t \t" << surname << endl;
				// Kullanıcıdan değiştirilmesini istediği soyismi girmesi istenir.
				string newPatientSurname;
				cout << "\n\t***  Enter the new name of the patient: ";
				cin >> newPatientSurname;

				// updatedLine değişkeni içerisinde parçalanmış bölmeler yeni soyisim eklenerek tekrardan birleştirilir.
				string updatedLine = beforeTheLine + " " + newPatientSurname + " " + restOfLine;

				// Dosyadaki veritabanı okunur ve güncellenir.
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Okunan veriler bir vectorun içerisinde saklanır.
				vector<string> fileLineDatas;
				// Geçici kullanılan, işlem yapılacak satırı içerisinde saklar.
				string readLine;
				// Geçici kullanılan, veritabanında işlem yapılacak satır indisini saklayacak değişken (Örn. 3. satır)
				int readLineNumber = 0;

				// Düzenlenen satır eğer satır indisleri eşleşme sağlarsa vector içerisine yazılır.
				// Aksi durumda readLineNumber == currentLineNumber eşleşmesi sağlanana kadar readLineNumber birer artırılır.
				while (getline(databaseReadFile, readLine)) {
					if (readLineNumber == currentLineNumber) {
						fileLineDatas.push_back(updatedLine);
					}
					else {
						fileLineDatas.push_back(readLine);
					}
					readLineNumber++;
				}
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Veritabanının içi tamamen temizlenir.
				databaseReadFile.clear();
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Vector içerisinde bulunan tüm içerik dosyanın içerisine tekrardan yazılır.
				for (int i = 0; i < fileLineDatas.size(); i++)
				{
					databaseReadFile.write((fileLineDatas[i] + "\n").c_str(), fileLineDatas[i].length() + 1);
				}

				// İşlem yapılan dosya kapatılır.
				databaseReadFile.close();
				system("CLS");
				cout << "\n\t***  Patient information has been successfully updated!                      ***\n";
				cout << "\n\t***  " << updatedLine << endl;
			}

			// Yaş değiştirme fonksiyonu
			if (updateChoice == 3)
			{
				databaseReadFile.seekg(line.find(patientID), ios::beg);

				// String içerisinde boşluk aramak için gerekli olan komutlar
				string whitespace(" ");
				size_t found = line.find(whitespace);
				size_t found2 = line.find(" ", found + 1, 1);
				size_t found3 = line.find(" ", found2 + 2, 1);

				// line stringi 3 parçaya bölünür.
				// 1. kısım, işlem yapılacak bölmeden öncesidir. beforeTheLine içerisinde saklanır.
				// 2. kısım, işlem yapılacak bölmedir. age içerisinde saklanır.
				// 3. kısım, işlem yapılacak bölmeden sonrasıdır. restOfLine içerisinde saklanır.
				string beforeTheLine = line.substr(0, found3);
				string age = line.substr(found3 + 1, line.substr(found3 + 1, line.length()).find(" "));
				string restOfLine = line.substr(beforeTheLine.length() + age.length() + 2, line.length());

				system("CLS");
				// String içerisinden elde edilen yaş ekrana bastırılır.
				cout << "\n\t***  Patient's age: \t \t \t" << age << endl;
				// Kullanıcıdan değiştirilmesini istediği yaşı girmesi istenir.
				string newPatientAge;
				cout << "\n\t***  Enter the new name of the patient: ";
				cin >> newPatientAge;

				// updatedLine değişkeni içerisinde parçalanmış bölmeler yeni yaş eklenerek tekrardan birleştirilir.
				string updatedLine = beforeTheLine + " " + newPatientAge + " " + restOfLine;

				// Dosyadaki veritabanı okunur ve güncellenir.
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Okunan veriler bir vectorun içerisinde saklanır.
				vector<string> fileLineDatas;
				// Geçici kullanılan, işlem yapılacak satırı içerisinde saklar.
				string readLine;
				// Geçici kullanılan, veritabanında işlem yapılacak satır indisini saklayacak değişken (Örn. 3. satır)
				int readLineNumber = 0;

				// Düzenlenen satır eğer satır indisleri eşleşme sağlarsa vector içerisine yazılır.
				// Aksi durumda readLineNumber == currentLineNumber eşleşmesi sağlanana kadar readLineNumber birer artırılır.
				while (getline(databaseReadFile, readLine)) {
					if (readLineNumber == currentLineNumber) {
						fileLineDatas.push_back(updatedLine);
					}
					else {
						fileLineDatas.push_back(readLine);
					}
					readLineNumber++;
				}
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Veritabanının içi tamamen temizlenir.
				databaseReadFile.clear();
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Vector içerisinde bulunan tüm içerik dosyanın içerisine tekrardan yazılır.
				for (int i = 0; i < fileLineDatas.size(); i++)
				{
					databaseReadFile.write((fileLineDatas[i] + "\n").c_str(), fileLineDatas[i].length() + 1);
				}

				// İşlem yapılan dosya kapatılır.
				databaseReadFile.close();
				system("CLS");
				cout << "\n\t***  Patient information has been successfully updated!                      ***\n";
				cout << "\n\t***  " << updatedLine << endl;
			}

			// Şehir Güncelleme Fonksiyonu
			if (updateChoice == 4)
			{
				databaseReadFile.seekg(line.find(patientID), ios::beg);

				// String içerisinde boşluk aramak için gerekli olan komutlar
				string whitespace(" ");
				size_t found = line.find(whitespace);
				size_t found2 = line.find(" ", found + 1, 1);
				size_t found3 = line.find(" ", found2 + 2, 1);
				size_t found4 = line.find(" ", found3 + 2, 1);

				// line stringi 3 parçaya bölünür.
				// 1. kısım, işlem yapılacak bölmeden öncesidir. beforeTheLine içerisinde saklanır.
				// 2. kısım, işlem yapılacak bölmedir. city içerisinde saklanır.
				// 3. kısım, işlem yapılacak bölmeden sonrasıdır. restOfLine içerisinde saklanır.
				string beforeTheLine = line.substr(0, found4);
				string city = line.substr(found4 + 1, line.substr(found4 + 1, line.length()).find(" "));
				string restOfLine = line.substr(beforeTheLine.length() + city.length() + 2, line.length());

				system("CLS");
				// String içerisinden elde edilen şehir ekrana bastırılır.
				cout << "\n\t***  Patient's age: \t \t \t" << city << endl;
				// Kullanıcıdan değiştirilmesini istediği şehiri girmesi istenir.
				string newPatientCity;
				cout << "\n\t***  Enter the new name of the patient: ";
				cin >> newPatientCity;

				// updatedLine değişkeni içerisinde parçalanmış bölmeler yeni şehir eklenerek tekrardan birleştirilir.
				string updatedLine = beforeTheLine + " " + newPatientCity + " " + restOfLine;

				// Dosyadaki veritabanı okunur ve güncellenir.
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Okunan veriler bir vectorun içerisinde saklanır.
				vector<string> fileLineDatas;
				// Geçici kullanılan, işlem yapılacak satırı içerisinde saklar.
				string readLine;
				// Geçici kullanılan, veritabanında işlem yapılacak satır indisini saklayacak değişken (Örn. 3. satır)
				int readLineNumber = 0;

				// Düzenlenen satır eğer satır indisleri eşleşme sağlarsa vector içerisine yazılır.
				// Aksi durumda readLineNumber == currentLineNumber eşleşmesi sağlanana kadar readLineNumber birer artırılır.
				while (getline(databaseReadFile, readLine)) {
					if (readLineNumber == currentLineNumber) {
						fileLineDatas.push_back(updatedLine);
					}
					else {
						fileLineDatas.push_back(readLine);
					}
					readLineNumber++;
				}
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Veritabanının içi tamamen temizlenir.
				databaseReadFile.clear();
				databaseReadFile.seekp(0);
				databaseReadFile.seekg(0);

				// Vector içerisinde bulunan tüm içerik dosyanın içerisine tekrardan yazılır.
				for (int i = 0; i < fileLineDatas.size(); i++)
				{
					databaseReadFile.write((fileLineDatas[i] + "\n").c_str(), fileLineDatas[i].length() + 1);
				}

				// İşlem yapılan dosya kapatılır.
				databaseReadFile.close();
				system("CLS");
				cout << "\n\t***  Patient information has been successfully updated!                      ***\n";
				cout << "\n\t***  " << updatedLine << endl;
			}

			// Çıkış Fonksiyonu
			if (updateChoice == 9)
			{
				// Hasta bilgileri ile ilgili düzenlemeler sona erdiğinde ana menüye dönüş yapılır.
				break;
				system("CLS");
			}
		}
		// Satır indisi artırılır.
		currentLineNumber++;
	}
}

// SearchPatient Fonksiyonu
void SearchPatient() {

	// TXT dosyasının içerisinde bulunan bilgiler okunur.
	fstream databaseReadFile("database.txt", ios::in | ios::out | ios::binary);

	// Dosya açma hata kontrolü
	if (!databaseReadFile) {
		cout << "\n\t***  Can't open file: database.txt!                                          ***\n";
		exit(1);
	}

	// Kullanıcıdan hastanın sahip olduğu ID numarasını girmesi istenir.
	string* patientID = new string;
	cout << "\n\t***  Please enter the patient's ID: ";
	cin >> *patientID;

	// ID numarasının bulunduğu satır line değişkenine atanacaktır.
	string* line = new string;

	// While döngüsü içerisinde spesifik pozisyonda kullanıcının girdiği ID numarası aranır.
	// ID numarası bulunursa tüm satır line değişkenine atılır.
	// line değişkeni ekrana bastırılır.
	cout << endl;
	cout << "\n\t\t                   ------PATIENT INFORMATION------           \n\n";
	cout << "\t********************************************************************************\n";
	cout << "\t***  ID   Name  Surname Age  City   Last Vac. Date  Vac. Dose No.  Vac. Name ***\n";
	cout << "\t********************************************************************************\n";

	while (getline(databaseReadFile, *line))
	{
		// Kullanıcı tarafından girilen ID'nin bulunduğu pozisyon aranır.
		size_t Position = (*line).find(*patientID);
		if (Position != string::npos)
		{
			cout << "\n\t***  " << *line << endl;

			databaseReadFile.close();
		}
	}
}

// NewVaccine Fonksiyonu
void NewVaccine()
{
	system("CLS");

	cout << "\t********************************************************************************\n";
	cout << "\t***                   ------NEW VACCINE REGISTRATION------                   ***\n";
	cout << "\t********************************************************************************\n";

	// TXT dosyasının içerisinde bulunan bilgiler okunur.
	fstream databaseReadFile("database.txt", ios::in | ios::out);

	// Dosya açma hata kontrolü
	if (!databaseReadFile) {
		cout << "\n\t***  Can't open file: database.txt!                                          ***\n";
		exit(1);
	}

	// Kullanıcıdan hastanın sahip olduğu ID numarasını girmesi istenir.
	string patientID;

	cout << "\n\n\n\t*** Please enter the patient's ID: ";
	cin >> patientID;

	// ID numarasının bulunduğu satır line değişkenine atanacaktır.
	string line;

	// Veritabanında işlem yapılacak satır indisini saklar. (Örn. 3. satır)
	int currentLineNumber = 0;

	// While döngüsü içerisinde spesifik pozisyonda kullanıcının girdiği ID numarası aranır.
	// ID numarası bulunursa tüm satır line değişkenine atılır.
	// line değişkeni ekrana bastırılır.
	cout << endl;
	cout << "\n\t\t                   ------PATIENT INFORMATION------                   \n\n";
	cout << "\t********************************************************************************\n";
	cout << "\t***  ID   Name  Surname Age  City   Last Vac. Date  Vac. Dose No.  Vac. Name ***\n";
	cout << "\t********************************************************************************\n";

	while (getline(databaseReadFile, line))
	{
		// Kullanıcı tarafından girilen ID'nin bulunduğu pozisyon aranır.
		size_t Position = line.find(patientID);
		if (Position != string::npos)
		{
			// Elde edilen kullanıcı bilgilerine sahip satır ekrana bastırılır.
			cout << "\n\t***  " << line << endl;

			int vaccineChoice;

			cout << "\n\t\t                     ------CHOOSE A VACCINE------                      \n\n";
			cout << "\t********************************************************************************\n"
				<< "\t********************************************************************************\n"
				<< "\t***  1- X Vaccine				                             ***\n"
				<< "\t***  2- Y Vaccine						             ***\n"
				<< "\t***  9- Return to main menu						     ***\n"
				<< "\t********************************************************************************\n"
				<< "\t********************************************************************************\n";

			cout << "\t***  Enter choice: ";
			cin >> vaccineChoice;
			cout << "\t********************************************************************************" << endl;

			// X Aşısı Fonksiyonu
			if (vaccineChoice == 1)
			{
				databaseReadFile.seekg((line).find(patientID), ios::beg);

				// String içerisinde boşluk aramak için gerekli olan komutlar
				string whitespace(" ");
				size_t found = (line).find(whitespace);
				size_t found2 = (line).find(" ", found + 1, 1);
				size_t found3 = (line).find(" ", found2 + 1, 1);
				size_t found4 = (line).find(" ", found3 + 1, 1);
				size_t found5 = (line).find(" ", found4 + 1, 1);
				size_t found6 = (line).find("/", found5 + 1, 1);
				size_t found7 = (line).find("/", found6 + 1, 1);
				size_t found8 = (line).find(" ", found7 + 1, 1);
				size_t found9 = (line).find(" ", found8 + 1, 1);

				string beforeTheLine = (line).substr(0, found5);
				string day = (line).substr(found5 + 1, (line).substr(found5 + 1, (line).length()).find("/"));
				string month = (line).substr(found6 + 1, (line).substr(found6 + 1, (line).length()).find("/"));
				string year = (line).substr(found7 + 1, (line).substr(found7 + 1, (line).length()).find(" "));
				string vaccount = (line).substr(found8 + 1, (line).substr(found8 + 1, (line).length()).find(" "));
				string vacname = (line).substr(found9 + 1, (line).substr(found9 + 1, (line).length()).find(" "));

				system("CLS");

				// String içerisinden elde edilen hasta bilgisi ekrana bastırılır.
				cout << "\n\t***  Patient info: " << (line) << "\n\n\n";

				// Güncel zaman elde edilir.
				time_t now = time(0);
				tm* ltm = localtime(&now);

				// Şimdiki zaman
				int* curDay = new int;
				int* curMonth = new int;
				int* curYear = new int;

				*curDay = ltm->tm_mday;
				*curMonth = 1 + ltm->tm_mon;
				*curYear = 1900 + ltm->tm_year;

				// Veritabanında hastanın sahip olduğu zaman
				int dataDay;
				int dataMonth;
				int dataYear;

				dataDay = stoi(day);
				dataMonth = stoi(month);
				dataYear = stoi(year);

				string strCurDay = to_string(*curDay);
				string strCurMonth = to_string(*curMonth);
				string strCurYear = to_string(*curYear);

				day = strCurDay;
				month = strCurMonth;
				year = strCurYear;

				// Son aşı vurulma süresinin üzerinden 30 gün geçip geçmediği kontrol edilir.
				int totalDay = (360 * (*curYear - dataYear) + 30 * (*curMonth - dataMonth) + (*curDay - dataDay));

				vacname = "X";
				int vacCount;
				vacCount = stoi(vaccount);
				vacCount = vacCount + 1;
				vaccount = to_string(vacCount);

				if (totalDay > 30 && vacname == "X")
				{
					// updatedLine değişkeni içerisinde parçalanmış bölmeler yeni isim eklenerek tekrardan birleştirilir.
					string updatedLine = beforeTheLine + " " + day + "/" + month + "/" + year + " " + vaccount + " " + vacname + "   ";

					cout << "\n\n" << updatedLine << "\n\n";

					// Dosyadaki veritabanı okunur ve güncellenir.
					databaseReadFile.seekp(0);
					databaseReadFile.seekg(0);

					// Okunan veriler bir vectorun içerisinde saklanır.
					vector<string> fileLineDatas;
					// Geçici kullanılan, işlem yapılacak satırı içerisinde saklar.
					string readLine;
					// Geçici kullanılan, veritabanında işlem yapılacak satır indisini saklayacak değişken (Örn. 3. satır)
					int readLineNumber = 0;

					// Düzenlenen satır eğer satır indisleri eşleşme sağlarsa vector içerisine yazılır.
					// Aksi durumda readLineNumber == currentLineNumber eşleşmesi sağlanana kadar readLineNumber birer artırılır.
					while (getline(databaseReadFile, readLine)) {

						cout << "\n\n" << readLine << "\n\n";
						cout << "\n\n" << updatedLine << "\n\n";

						if (readLineNumber == currentLineNumber) {
							fileLineDatas.push_back(updatedLine);
						}
						else {
							fileLineDatas.push_back(readLine);
						}
						readLineNumber++;
					}
					databaseReadFile.seekp(0);
					databaseReadFile.seekg(0);

					// Veritabanının içi tamamen temizlenir.
					databaseReadFile.clear();
					databaseReadFile.seekp(0);
					databaseReadFile.seekg(0);

					// Vector içerisinde bulunan tüm içerik dosyanın içerisine tekrardan yazılır.
					for (int i = 0; i < fileLineDatas.size(); i++)
					{
						databaseReadFile.write((fileLineDatas[i] + "\n").c_str(), fileLineDatas[i].length() + 1);
					}

					// İşlem yapılan dosya kapatılır.
					databaseReadFile.close();
					system("CLS");
					cout << "\n\t***  Patient information has been successfully updated!                      ***\n";
					cout << "\n\t***  " << updatedLine << endl;
				}
				else
				{
					cout << "\t********************************************************************************\n"
						<< "\t***  It has not been 30 days since the vaccination period!                   ***\n"
						<< "\t***  or                                                                      ***\n"
						<< "\t***  You've had a different vaccine before.                                  ***\n"
						<< "\t********************************************************************************\n";
					break;
				}
			}

			// Y Aşısı Fonksiyonu
			if (vaccineChoice == 2)
			{
				databaseReadFile.seekg((line).find(patientID), ios::beg);

				// String içerisinde boşluk aramak için gerekli olan komutlar
				string whitespace(" ");
				size_t found = (line).find(whitespace);
				size_t found2 = (line).find(" ", found + 1, 1);
				size_t found3 = (line).find(" ", found2 + 1, 1);
				size_t found4 = (line).find(" ", found3 + 1, 1);
				size_t found5 = (line).find(" ", found4 + 1, 1);
				size_t found6 = (line).find("/", found5 + 1, 1);
				size_t found7 = (line).find("/", found6 + 1, 1);
				size_t found8 = (line).find(" ", found7 + 1, 1);
				size_t found9 = (line).find(" ", found8 + 1, 1);

				string beforeTheLine = (line).substr(0, found5);
				string day = (line).substr(found5 + 1, (line).substr(found5 + 1, (line).length()).find("/"));
				string month = (line).substr(found6 + 1, (line).substr(found6 + 1, (line).length()).find("/"));
				string year = (line).substr(found7 + 1, (line).substr(found7 + 1, (line).length()).find(" "));
				string vaccount = (line).substr(found8 + 1, (line).substr(found8 + 1, (line).length()).find(" "));
				string vacname = (line).substr(found9 + 1, (line).substr(found9 + 1, (line).length()).find(" "));

				system("CLS");

				// String içerisinden elde edilen hasta bilgisi ekrana bastırılır.
				cout << "\n\t***  Patient info: " << (line) << "\n\n\n";

				// Güncel zaman elde edilir.
				time_t now = time(0);
				tm* ltm = localtime(&now);

				// Şimdiki zaman
				int* curDay = new int;
				int* curMonth = new int;
				int* curYear = new int;

				*curDay = ltm->tm_mday;
				*curMonth = 1 + ltm->tm_mon;
				*curYear = 1900 + ltm->tm_year;

				// Veritabanında hastanın sahip olduğu zaman
				int dataDay;
				int dataMonth;
				int dataYear;

				dataDay = stoi(day);
				dataMonth = stoi(month);
				dataYear = stoi(year);

				string strCurDay = to_string(*curDay);
				string strCurMonth = to_string(*curMonth);
				string strCurYear = to_string(*curYear);

				day = strCurDay;
				month = strCurMonth;
				year = strCurYear;

				// Son aşı vurulma süresinin üzerinden 30 gün geçip geçmediği kontrol edilir.
				int totalDay = (360 * (*curYear - dataYear) + 30 * (*curMonth - dataMonth) + (*curDay - dataDay));

				vacname = "Y";
				int vacCount;
				vacCount = stoi(vaccount);
				vacCount = vacCount + 1;
				vaccount = to_string(vacCount);

				if (totalDay > 30 && vacname == "Y")
				{
					// updatedLine değişkeni içerisinde parçalanmış bölmeler yeni isim eklenerek tekrardan birleştirilir.
					string updatedLine = beforeTheLine + " " + day + "/" + month + "/" + year + " " + vaccount + " " + vacname + "   ";

					cout << "\n\n" << updatedLine << "\n\n";

					// Dosyadaki veritabanı okunur ve güncellenir.
					databaseReadFile.seekp(0);
					databaseReadFile.seekg(0);

					// Okunan veriler bir vectorun içerisinde saklanır.
					vector<string> fileLineDatas;
					// Geçici kullanılan, işlem yapılacak satırı içerisinde saklar.
					string readLine;
					// Geçici kullanılan, veritabanında işlem yapılacak satır indisini saklayacak değişken (Örn. 3. satır)
					int readLineNumber = 0;

					// Düzenlenen satır eğer satır indisleri eşleşme sağlarsa vector içerisine yazılır.
					// Aksi durumda readLineNumber == currentLineNumber eşleşmesi sağlanana kadar readLineNumber birer artırılır.
					while (getline(databaseReadFile, readLine)) {
						if (readLineNumber == currentLineNumber) {
							fileLineDatas.push_back(updatedLine);
						}
						else {
							fileLineDatas.push_back(readLine);
						}
						readLineNumber++;
					}
					databaseReadFile.seekp(0);
					databaseReadFile.seekg(0);

					// Veritabanının içi tamamen temizlenir.
					databaseReadFile.clear();
					databaseReadFile.seekp(0);
					databaseReadFile.seekg(0);

					// Vector içerisinde bulunan tüm içerik dosyanın içerisine tekrardan yazılır.
					for (int i = 0; i < fileLineDatas.size(); i++)
					{
						databaseReadFile.write((fileLineDatas[i] + "\n").c_str(), fileLineDatas[i].length() + 1);
					}

					// İşlem yapılan dosya kapatılır.
					databaseReadFile.close();
					system("CLS");
					cout << "\n\t***  Patient information has been successfully updated!                      ***\n";
					cout << "\n\t***  " << updatedLine << endl;
				}
				else
				{
					cout << "\t********************************************************************************\n"
						<< "\t***  It has not been 30 days since the vaccination period!                   ***\n"
						<< "\t***  or                                                                      ***\n"
						<< "\t***  You've had a different vaccine before.                                  ***\n"
						<< "\t********************************************************************************\n";
					break;
				}
			}

			// Çıkış Fonksiyonu
			if (vaccineChoice == 9)
			{
				// Hasta bilgileri ile ilgili düzenlemeler sona erdiğinde ana menüye dönüş yapılır.
				system("CLS");
				break;
			}
		}
		// Satır indisi artırılır.
		currentLineNumber++;
	}
}
