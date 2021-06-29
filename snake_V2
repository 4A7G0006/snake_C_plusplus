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
#define width 60
#define height 20
void gotoxy(int xpos, int ypos)		//游標函數 利用游標點清空畫面		
{						//得到游標位置主控權https://blog.wildsky.cc/posts/c-code-note/
	COORD scrn;									//定義一個座標結構
	HANDLE hOuput = GetStdHandle(STD_OUTPUT_HANDLE); // 得到標準輸出的處理 //Handle是一個指標指向函數(pointer to void) 用於取得console控制權 //STD_OUTPUT_HANDLE 標準輸出之 handle，通常指的是螢幕
	scrn.X = xpos; scrn.Y = ypos;				//座標賦予值 設定螢幕的x y座標基本上從0,0開始
	SetConsoleCursorPosition(hOuput, scrn);		//設置控制台游標到指定座標 由剛剛上面設定的 輸出處理 與座標設定 讓畫面清空
}
class HEAD {
private:
	int x, y;
public:
	HEAD(int a, int b) {//設定參數建構元 一樣設定參數給類別的變數值
		x = a;
		y = b;
	}
	HEAD() {	//建構元 設定兩變數 x座標y座標
		x = 0;	//設定為0
		y = 0;	//設定為0
	}
	void setPoint(int a, int b) {	//設定傳入參數為座標
		x = a;
		y = b;
	}
	int getX() {	//得到X座標
		return x;
	}
	int getY() {			//得到Y座標
		return y;
	}
};
class Snake_game {
private:
	int seedX, seedY, Tail, level, control, score;
	HEAD snakee;
	int TNT_x[100][2] = { 0 }, TNT_y[100][2] = { 0 };	//炸彈x 炸彈y 座標
	int bodyX[80], bodyY[30];			//蛇身體的座標

public:
	int bomb_num;
	bool now;
	Snake_game() {
		seedX = 0;
		seedY = 0;
		score = 0;
		bomb_num = 2;
		Tail = 0;
		control = 0;
		score = 0;
		level = 0;
		now = false;
		snakee.setPoint(rand() % (width - 2) + 1, rand() % (height - 2) + 1);
		for (int i = 0; i < width; i++) {	//身體所有數字清空
			if (i < 30) {
				bodyX[i] = 0;
				bodyY[i] = 0;
			}
			else
				bodyX[i] = 0;
		}
		grow_rand();
	}
	void grow_rand() {	//亂數生成 炸彈 與 種子

		srand(time(NULL));

		for (int i = 0; i < bomb_num; i++) {
			//for (int a = 1; a < i; a++) {
			//	if (TNT_x[i][0] == TNT_x[a][0] || TNT_x[i][0] == TNT_x[a ][0])//避免炸彈重疊與交錯x軸處理
			//		TNT_x[i][0] = rand() % (width - 2) + 1;
			//	if (TNT_y[i][0] == TNT_y[a+1][0] || TNT_y[i][0] == TNT_y[a + 1][0])//避免炸彈重疊與交錯y軸處理
			//		TNT_y[i][0] = rand() % (height - 2) + 1;
			//}
			TNT_x[i][0] = rand() % (width - 2) + 1;
			TNT_x[i][1] = TNT_x[i][0] + 1;
			TNT_y[i][0] = rand() % (height - 2) + 1;
			TNT_y[i][1] = TNT_y[i][0] + 1;
		}
		bool re = true;
		while (re) {	//判斷點數是否與炸彈重複到
			re = false;
			seedX = rand() % (width - 1) + 1;	//預設亂數從0開始所以 +2 避掉0與牆壁
			seedY = rand() % (height - 1) + 1;
			for (int i = 0; i < bomb_num; i++) {
				for (int j = 0; j < 2; j++) {
					for (int k = 0; k < 2; k++) {
						if (seedX == TNT_x[i][j] && seedY == TNT_y[i][k]) {
							re = true;
						}
					}
				}
			}
		}
	}
	bool logic() {
		int prevX = bodyX[0];	//將上一個蛇頭的X暫存置X
		int prevY = bodyY[0];	////將上一個蛇頭的Y暫存置X
		int prev2X, prev2Y;
		bodyX[0] = snakee.getX();	//設定蛇頭X
		bodyY[0] = snakee.getY();	//設定蛇頭Y
		for (int i = 1; i < Tail; i++) {	//身體的每一截
			prev2X = bodyX[i];			//前一截的身體暫存2X
			prev2Y = bodyY[i];			//前一截的身體暫存2Y
			bodyX[i] = prevX;			//剛存X1的給下一個身體的i位置
			bodyY[i] = prevY;			//剛存Y1的給下一個身體的i位置
			prevX = prev2X;				//X2再存去前一個X1
			prevY = prev2Y;				//Y2再存去前一個Y1
		}//簡單來說 就是因為吃到種子 身體的部分都要因為把頭塞到第0個位置 後面都要往後
		switch (control) {		//選擇剛剛control的值
		case 3:		//透過控制方向的數值決定移動方向
			snakee.setPoint(snakee.getX() - 1, snakee.getY());		//向左
			break;
		case 4:
			snakee.setPoint(snakee.getX() + 1, snakee.getY());		//向右
			break;
		case 1:
			snakee.setPoint(snakee.getX(), snakee.getY() - 1);		//向上
			break;
		case 2:
			snakee.setPoint(snakee.getX(), snakee.getY() + 1);		//向下
			break;
		default:
			break;
		}
		if (snakee.getX() > width - 1)		//如果超過牆
			now = dead();
		else if (snakee.getX() < 1)
			now = dead();
		if (snakee.getY() > height - 1)
			now = dead();
		else if (snakee.getY() < 1)
			now = dead();
		for (int k = 0; k < Tail; k++) {
			if (snakee.getX() == bodyX[k] && snakee.getY() == bodyY[k]) {	//判斷蛇頭去撞到身體
				now = dead();
				break;
			}
		}
		for (int i = 0; i < bomb_num; i++) {		//判斷炸彈出現
			for (int n = 0; n < 2; n++) {	//碰到[0][o] [1][o]
				for (int o = 0; o < 2; o++) {//碰到[n][0] [n][1]
					if (snakee.getX() == TNT_x[i][n] && snakee.getY() == TNT_y[i][o]) {	//如果吃到炸彈
						now = dead();
						break;
					}
				}
			}

		}
		if (snakee.getX() == seedX && snakee.getY() == seedY) {
			score += 10;
			grow_rand();	//隨機生成
			Tail++;			//尾巴++
			if (score >= 20 + level) {	//每越一階門檻
				cout << "等級提升+1" << endl;
				bomb_num += 1;		//炸彈數多一
				level = score;	//門檻值更新
			}
		}
		return now;
	}

	void initial() {
		gotoxy(0, 0);
		for (int i = 0; i < height; i++) {
			for (int j = 0; j < width; j++) {
				if (i == 0 || i == height - 1 || j == 0 || j == width - 1) {
					cout << "0";
				}
				else {
					if (i == (height / 2) && j == ((width / 2) - 3)) {
						cout << "開 始 遊 戲";
						j += 10;
					}
					else { cout << " "; }
				}
			}
			cout << endl;
		}
		cout << "目前分數為:" << score << endl;
	}
	void background() {

		gotoxy(0, 0);
		for (int i = 0; i <= height; i++) {						//中間的框框
			for (int j = 0; j <= width; j++) {
				if (j == 0 || j == width || i == 0 || i == height) {
					cout << "0";
				}
				else {

					if (j == snakee.getX() && i == snakee.getY()) {						//如果蛇的位置相等 
						cout << "O";
					}
					else if (j == seedX && i == seedY) {		//如果種子的位置相等 
						cout << "P";
					}
					else {										//如果沒有遇到種子與身體 
						bool print = false;
						for (int l = 0; l < bomb_num; l++) {	//判斷炸彈位置 如果一樣位置 就印出X
							for (int m = 0; m < 2; m++) {
								for (int n = 0; n < 2; n++) {
									if (j == TNT_x[l][m] && i == TNT_y[l][n]) {
										cout << "X";
										print = true;
									}
								}
							}

						}
						for (int k = 0; k < Tail; k++) {
							if (j == bodyX[k] && i == bodyY[k]) {	//如果座標X Y 與 蛇的身體座標相同 
								cout << "O";
								print = true;
							}
						}
						if (!print)		//如果沒有印出任何相關 X O  print=false時 印出空格
							cout << " ";
					}
				}
			}
			cout << endl;
		}
		cout << endl << "分數 : " << score << endl;
		cout << "遊戲規則: 1.使用數字鍵控制方向 4( <- ) 5( v ) 6( -> ) 8( ^ )" << endl;
		cout << "          2.行進間不能使蛇突然相反 會導致蛇失控咬傷自己 自殺!" << endl;
		cout << "          3.分數超過某個門檻 炸彈會開始變多 !!! " << endl;
		cout << "          4.遊戲中出現的X為炸彈請小心走喔 不然會踩到就掰掰了~" << endl;
	}
	void GameEnd() {			//死亡背景

		for (int i = 0; i < height; i++) {
			for (int j = 0; j < width; j++) {
				if (i == 0 || i == height - 1 || j == 0 || j == width - 1) {
					cout << "0";
				}
				else {
					if (i == (height / 2) && j == ((width / 2) - 8)) {
						cout << "你輸了 結束遊戲!";
						j += 15;
					}
					else { cout << " "; }
				}
			}
			cout << endl;
		}
	}
	bool dead() {
		system("CLS");
		GameEnd();
		Sleep(5000);
		return true;
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
			default:
				break;
			}
		}
	}

};
int main() {

	int n;
	bool gameover = false;
	Snake_game snake;
	system("mode con cols=65 lines=30");	//控制螢幕輸出大小 固定為80*30
	snake.initial();					//印出遊戲介面選單
	gotoxy(0, 0);
	n = _getch();
	while (!gameover) {
		snake.background();		//背景
		Sleep(90);
		snake.input();			//輸入
		gameover = snake.logic();			//運作邏輯
	}
	system("PAUSE");
	return 0;
}
