# game
Untuk memenuhi tugas akhir UAS praktikum pemograman

```bash
#include<iostream>
#include<windows.h>
#include<string>
using namespace std;

void HUD();
void Combat();
void CombatHUD();
void Moving();
void CreateMonster();
void LevelUp();

string name = " ", race = " ", sex = " ";
int level = 0, xp = 0, darah = 0, totalDarah = 0, nextLevel = 0, maxDarah = 0, heal = 0;
int monsterHp = 0;
int monsterXp = 0;
int monsterLevel = 0;

string monsterName[] = { "Goblin", "Dwarf", "Ogre", "Witch", "Wizard", };
int monsterLainName = 5;
string monsterLain = " ";

int counter = 3;
int main(){
	
	level = 1;
	xp = 0;
	nextLevel = 76;
	darah = 100;
	totalDarah = darah;
	maxDarah = totalDarah;
	// membuat karakter
	cout << "\n   _________________________________________________________________________________ \n";
	cout << "  | ####  ######  ######## ##    ##    ###    ####    ##      ##    ###    ######## |\n";
	cout << "  | ##  ##    ## ##       ##   ##    ## ##    ##     ##  ##  ##   ## ##   ##     ## |\n";
	cout << "  | ##  ##       ##       ##  ##    ##   ##   ##     ##  ##  ##  ##   ##  ##     ## |\n";
	cout << "  | ##   ######  ######   #####    ##     ##  ##     ##  ##  ## ##     ## ########  |\n";
	cout << "  | ##        ## ##       ##  ##   #########  ##     ##  ##  ## ######### ##   ##   |\n";
	cout << "  | ##  ##    ## ##       ##   ##  ##     ##  ##     ##  ##  ## ##     ## ##    ##  |\n";
	cout << "  |####  ######  ######## ##    ## ##     ## ####     ###  ###  ##     ## ##     ## |\n";
	cout << "  |_________________________________________________________________________________|\n";

	cout << "\nMasukan Nama Karakter: ";
	cin >> name;
	
	cout << "masukan Jenis Karakter: ";
	cin >> race;
	
	cout << "Masukan Gender Karakter: ";
	cin >> sex;
	
	
	for (int i = 0; i < counter; i++) {
		if (i == 0)
			cout << "Membuat Karakter.\n";
		if (i == 1)
			cout << "Membuat Karakter..\n";
		if (i == 2)
			cout << "Membuat Karakter...\n";
		Sleep(500);
		system("cls");
	}
	
	
	system("pause");
	
	HUD();
	Moving();

	system("pause");

	return 0;
}

void HUD() {
	Sleep(500);
	system("cls");
	cout << "\nNama		: " << name;
	cout << "\ndarah		: " << totalDarah;
	cout << "\njenis		: " << race;
	cout << "\nGender		: " << sex;
	cout << "\nlevel		: " << level;
	cout << "\nXp		: " << xp;
	cout << "\nxp to level	: " << nextLevel << endl;

	Moving();
}

void CombatHUD() {
	Sleep(500);
	system("cls");
	cout << "Name: " << name;
	cout << "		|		Monster Name: " << monsterLain;
	cout << "\nHealth:  " << totalDarah;
	cout << "		| 		Monster Health " << monsterHp;
	cout << "\nlevel: " << level;
	cout << "		|		Monster Level: " << monsterLevel << endl;

}

void Combat() {

	CombatHUD();

	int playerAttack;
	int playerDamage = 8;
	int monsterAttack = 6 * monsterLevel / 2;

	if (totalDarah >= 1 && monsterHp >= 1) {
		cout << "\n";
		cout << "1. Serang\n";
		cout << "2. Tahan\n";
		cout << "3. LARIIIII\n";
		cout << "\n";
		cin >> playerAttack;

		if(playerAttack == 1){
			//menyerang
			cout << "Menyerang...prosess" << playerDamage;
			cout << " ke " << monsterLain << endl;
			monsterHp = monsterHp - playerDamage;
			Sleep(1000);
			CombatHUD();
			if(monsterHp >= 1) {
				cout << "\n";
				cout << "Monster sedang Menyerang..\n";
				totalDarah = totalDarah - monsterAttack;
				cout << "anda terluka parah " << monsterAttack;
				cout << " hp " << totalDarah << endl;
				
				if (totalDarah <= 0) {
					totalDarah = 0;
				}
			}
			else if (monsterHp <= 0) {
				monsterHp = 0;
				LevelUp();
				cout << "\n";
				cout << "anda kalah nak" << monsterLain;
				cout << "hadiah anda dengan" << monsterXp << "xp.\n!Selamat nak!\n";
				Sleep(1000);
				
			}
			Sleep(1000);
			Combat();
		}
		else if (playerAttack == 2){
			//Block
			cout << "Blocking\n";
			int i = rand() % 100 + 1;
			if (i >= 50) {
				cout << "Anda ngeblok serangan!\n";
				heal = level * 10 / 2;
				cout << "Anda mengisi Hp " << heal << endl;
				totalDarah += heal;
				Sleep(1000);
				Combat();
			}
			else {
				cout << "Anda gagal ngeblok serangan lawan..\n";
				totalDarah -= monsterAttack;
				cout << "Anda diserang dari belakang!" << monsterAttack;
				cout << " hp saat ini " << totalDarah << endl;
				Sleep(1000);
				Combat();
			}
		}
		else if (playerAttack == 3) {
			//kabur
			cout << "Anda mencoba kabur\n";
			int x = rand() % 100 + 1;
			if (x >= 50 ) {
				cout << "Anda berhasil Kaburrrr\n";
				HUD();
			}
			else {
				cout << "Anda gagal Kabur \n";
				cout << "Monster menyiksa Anda!\n";
				totalDarah -= monsterAttack + 10;
				cout << "anda babak belur " << monsterAttack + 10;
				cout << "darah anda saat ini" << totalDarah << endl;
				Sleep(1000);
				Combat();
			}
		}
		
		else {
		cout << "salah nomor\n";
		Sleep(500);
		Combat();
		}
	}
	if(totalDarah <= 1) {
		system("cls");
		cout << "Anda mati anjay \nLevel Anda sekarang: " << level << "Anda mati oleh" << monsterLain << endl;
		Sleep(2000);
		exit(0);
	}

	if(monsterHp <= 1) {
	
	}
}

void Moving() {

	int choice;

	cout << "\n\n";
	cout << "1. Maju kedepan\n";
	cout << "2. Istirahat\n";
	cout << "3. Kembali kebelakang\n";
	cout << "\n";

	cin >> choice;

	if (choice == 1) {
		int temp = rand() % 100 + 1;
		cout << "kamu Sedang maju kedepan...\n";
		if (temp >= 50) {
			//encounter a monster
			CreateMonster();
			string tempName = monsterName[rand() % monsterLainName];
			cout << "Ada! " << tempName << "! persiapkan untuk bertarung!!\n";
			monsterLain = tempName;
			Sleep(1000);
			Combat();
		}
		cout << "yang Anda cari tidak ada\n";
		Sleep(1000);
		HUD();

	}
	else if (choice == 2) {
		cout << "Anda ingin buat kemah untuk malam ini\n";
		if(totalDarah <= 99) {
			totalDarah += 10 * level;
		}
		cout << "Anda dapat beristirahat sekarang. mengisi darah sekarang" << totalDarah << endl;
		Sleep(1000);
		HUD();

	}
	else if (choice == 3) {
		int temp = rand() % 100 + 1;
		cout << "Anda mundur kebelakang...\n";
		if (temp >=50) {
			CreateMonster();
			string tempName = monsterName[rand()% monsterLainName];
			cout << "Ada " << tempName << "! persiapkan untuk bertarung\n";
			monsterLain = tempName;
			Sleep(1000);
			Combat();
		}
	}
	else {
		cout << "salah nomor! ulangi\n";
		Sleep(500);
		Moving();
	}
}

void CreateMonster() {
	monsterHp = 30;
	monsterLevel = (rand() % 3) + level;

	
	monsterLevel =(rand() % 3) + level;
	

	// disini mungkin nilainya nanti diubah
	monsterHp = (rand() % 30) * monsterLevel;
	monsterXp = monsterHp;

	if (monsterHp == 0)
		CreateMonster();
	if (monsterLevel == 0)
		CreateMonster();
}

void LevelUp() {
	xp = xp + monsterXp;
	if (xp >= nextLevel) {
		level++;
		nextLevel = nextLevel * 3 / 2;
		totalDarah = totalDarah + 20;
		maxDarah = totalDarah;
		cout << "tunggu levelnya naik anjay!, level anda sekarang " << level << endl;
		cout << "total darah anda naik 20 poin! Total darah anda" << totalDarah << endl;
		Sleep(2000);
		HUD();  
	}
}
```
