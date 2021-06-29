#include<iostream>
#include<istream>
#include<iomanip>
#include<string>
#include<cmath>
#include <cstdlib>
#include<conio.h>
#include<Windows.h>
#include<stdio.h>
#include<stdlib.h>
#include<fstream>
using namespace std;
const int width = 70, height = 20; //這是因為我的遊戲面積長寬固定 所以用const
int x, y, seedX, seedY, score;		//X Y為蛇的生成位置 SeedX seedY為種子生成位置
int bodyX[80], bodyY[30];			//蛇身體的座標
int Tail = 0;							//蛇的身體長度
int level = 0;
int record;
bool gameover = false;
int control = 0;		//控制方向 
fstream file;
//enum List { stop = 0, LEFT, RIGHT, UP, DOWN }; List snake;	//選擇要走哪步 參考網路用法
//stop=0 --> left = 1 -->right =2 --> up=3 --> down=4 接續數字	//列舉函數 參考https://openhome.cc/Gossip/CppGossip/enumType.html 
void gotoxy(int xpos, int ypos)		//游標函數 利用游標點清空畫面		
{						//得到游標位置主控權https://blog.wildsky.cc/posts/c-code-note/
	COORD scrn;									//定義一個座標結構
	HANDLE hOuput = GetStdHandle(STD_OUTPUT_HANDLE); // 得到標準輸出的處理
	scrn.X = xpos; scrn.Y = ypos;				//座標賦予值
	SetConsoleCursorPosition(hOuput, scrn);		//設置控制台游標到指定座標
}
void begin() {			//起始動作 初始化遊戲設定
	srand(time(NULL));
	gameover = false;
	x = (rand() % 66) + 3;
	y = (rand() % 20);
	seedX = (rand() % 66) + 3;
	seedY = (rand() % 20);
	score = 0;
	Tail = 0;
	for (int i = 0; i < width; i++) {
		if (i < 30) {
			bodyX[i] = 0;
			bodyY[i] = 0;
		}
		else
			bodyX[i] = 0;
	}
	level = 0;
	control = 0;
}
void initial() {			//遊戲開始選單

	char a[10];
	cout << "╔═════════════════════════  << 貪吃蛇遊戲 >>  ════════════════════════╗" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                            1 . 開 始 遊 戲                          ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                           2 . 結 束 程 式                           ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║              ┌────────────────── 請注意 ──────────────────┐	      ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║			    控制方法為使用數字鍵	 	      ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "║              └────────────────────────────────────────────┘         ║" << endl;
	cout << "║                                                                     ║" << endl;
	cout << "╚═════════════════════════════════════════════════════════════════════╝" << endl;
	file.open("Record.txt", ios::in);	//開啟檔案 並讀取
	file.read(a, size(a));		//讀檔 ( 將檔案存入字元 , 字元長度 )
	record = atoi(a);			//將字元轉成int整數型態
	cout << "                          目前歷史最高分數為:" << record << endl;
	file.close();
}
void gameend() {			//死亡背景

	cout << "╔═════════════════════════  << 貪吃蛇遊戲 >>  ═════════════════════════╗" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║		  	     你輸了! 結束遊戲	                       ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "║                                                                      ║" << endl;
	cout << "╚══════════════════════════════════════════════════════════════════════╝" << endl;
}
void pause() {			//暫停遊戲
	int sec = 10;
	while (sec >= 0) {
		//system("cls");
		gotoxy(0, 0);
		cout << "╔═════════════════════════  << 貪吃蛇遊戲 >>  ═════════════════════════╗" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║		  	      ~~暫停遊戲~~	                       ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "║                                                                      ║" << endl;
		cout << "╚══════════════════════════════════════════════════════════════════════╝" << endl;
		sec--;	//倒數計時
		Sleep(50);
	}
	cout << "按任意鍵一下繼續" << endl;
}
void background() {			//設定遊戲背景
	gotoxy(0, 0);			//非標準函式庫 原本用CLS會發現閃屏很嚴重
	for (int i = 0; i <= width; i++) {		//上面的框框
		if (i == 0)
			cout << "╔";
		else if (i == width)
			cout << "╗";
		else
			cout << "═";
	}
	cout << endl;
	for (int i = 0; i <= height; i++) {						//中間的框框
		for (int j = 0; j <= width; j++) {
			if (j == 0 || j == width) {
				cout << "║";
			}
			else {
				if (j == x && i == y) {						//如果蛇的位置相等 
					cout << "O";
				}
				else if (j == seedX && i == seedY) {		//如果種子的位置相等 
					cout << "S";
				}
				else {										//如果沒有遇到種子與身體 
					bool print = false;
					for (int k = 0; k < Tail; k++) {
						if (j == bodyX[k] && i == bodyY[k]) {	//如果座標X Y 與 蛇的身體座標相同 
							cout << "O";
							print = true;
						}
					}
					if (!print)		 
						cout << " ";
				}
			}
		}
		cout << endl;
	}
	for (int i = 0; i <= width; i++) {			//下面的框框
		if (i == 0)
			cout << "╚";
		else if (i == width)
			cout << "╝";
		else
			cout << "═";
	}
	cout << endl << "分數 : " << score << endl;
	cout << "遊戲規則: 1.使用數字鍵控制方向 4( <- ) 5( v ) 6( -> ) 8( ^ )" << endl;
	cout << "          2.行進間不能使蛇突然相反 會導致蛇失控咬傷自己 自殺!" << endl;
	cout << "          3.按下數字鍵中的" << " 3 " << "可暫停遊戲 按任意鍵繼續" << endl;
	cout << "          4.分數超過某個門檻 速度會開始放慢且不可穿牆喔 ^ ^ " << endl;
	//cout << seedX<<" "<<seedY << endl; //測試種子出現位置
	return;
}
void input() {   //.https://twpug.net/docs/ccfaq/node311.html //如果使用方向鍵
	if (_kbhit()) {		//當輸入為空時回傳0值則=略過下方執行  若非空值只要輸入鍵盤上的一鍵則會回傳非0值進入下方switch 
	//使用kbhit (keyboard hit)會檢查是否輸入任何按鍵 不會像getch暫停等待輸入 
		switch (_getch())		//選擇按下的鍵
		{
		case '8':
			control = 1;
			break;
		case '5':
			control = 2;
			break;
		case'4':
			control = 3;
			break;
		case  '6':
			control = 4;
			break;
		case '3':
			system("CLS");
			pause();
			_getch();
			system("CLS");
			break;
		default:
			break;
		}
	}
}
void logic() {
	int prevX = bodyX[0];	//將上一個蛇頭的X暫存置X
	int prevY = bodyY[0];	////將上一個蛇頭的Y暫存置X
	int prev2X, prev2Y;
	bodyX[0] = x;	//設定蛇頭X
	bodyY[0] = y;	//設定蛇頭Y
	for (int i = 1; i < Tail; i++) {	//身體的每一截
		prev2X = bodyX[i];			//前一截的身體暫存2X
		prev2Y = bodyY[i];			//前一截的身體暫存2Y
		bodyX[i] = prevX;			//剛存X1的給下一個身體的i位置
		bodyY[i] = prevY;			//剛存Y1的給下一個身體的i位置
		prevX = prev2X;				//X2再存去前一個X1
		prevY = prev2Y;				//Y2再存去前一個Y1
	}
	switch (control)		//選擇剛剛control的值
	{
	case 3:
		x--;
		break;
	case 4:
		x++;
		break;
	case 1:
		y--;
		break;
	case 2:
		y++;
		break;
	default:
		break;
	}
	if (level > 1)		//等級判別 等級大於1及不可穿牆
	{
		if (x >= width) {
			x--;
			control = 3;
		}
		else if (x < 2) {
			x++;
			control = 4;
		}
		if (y > height) {
			y--;
			control = 1;
		}
		else if (y < 0) {
			y++;
			control = 2;
		}
	}
	else
	{
		if (x > width - 1)		//如果超過牆
			x = 2;
		else if (x < 2)
			x = width;
		if (y > height)
			y = 0;
		else if (y < 0)
			y = height;
	}
	for (int k = 0; k < Tail; k++) {
		if (x == bodyX[k] && y == bodyY[k]) {	//判斷蛇頭去撞到身體
			system("CLS");
			gameend();
			Sleep(5000);
			gameover = true;
			break;
		}
	}
	if (x == seedX && y == seedY) {
		score += 10;
		srand(time(NULL));
		seedX = (rand() % 66) + 3;
		seedY = rand() % 20;
		Tail++;
		if (score > 300) {		//分數超過門檻
			level = 1;
			if (score > 600) {
				level = 2;
				if (score > 900) {
					level = 3;
					if (score > 1200) {
						level++;
					}
				}
			}
		}
	}
	if (record < score) {	
		record = score;		
		file.open("Record.txt", ios::trunc);	//清空檔案
		file.close();
		file.open("Record.txt", ios::out);	//寫入檔案
		file << score;   //將分數寫入
		file.close();	
	}
}
void time() {
	if (level == 0) {	//分數越高 越慢 
		Sleep(80);
	}
	else if (level == 1) {
		Sleep(120);
	}
	else if (level == 2) {
		Sleep(200);
	}
	else {		//等級3以上
		Sleep(300);
	}
}
int main() {

	int n;
	while (true)					//讓遊戲介面一直顯示
	{
		system("CLS");
		initial();					//印出遊戲介面選單
		gameover = false;
		n = _getch();
		if (n == '1') {
			begin();
			while (!gameover) {
				background();		//背景
				time();				//等級決定時間快慢
				input();			//輸入
				logic();			//運作邏輯
			}
		}
		else if (n == '2') {
			cout << "結束遊戲" << endl;
			break;
		}
		else {
			cout << "輸入錯誤請重新輸入" << endl;
			Sleep(1000);
		}
		file.close();
	}
	system("PAUSE");
	return 0;
}
