#include"pch.h"
#include <graphics.h>  
#include <conio.h>
#include <stdio.h>
#define BLOCK_SIZE 20 // 每個小格子的長寬大小
#define HEIGHT 30 // 高度上一共30個小格子
#define WIDTH 40 //  寬度上一共40個小格子 
// 全局變量定義

char moveDirection;  //  小蛇的一定方向
int isFailure = 0; //  是否遊戲失敗
class Food {
private:
	int food_i, food_j; //  食物的位置
public:
	Food(int x, int y) {
		this->food_i = x;
		this->food_j = y;
	}
	Food() {
		this->food_i = 0;
		this->food_j = 0;
	}
	void Setfood(int x, int y) {
		this->food_i = x;
		this->food_j = y;
	}
	int Get_food_X() {
		return this->food_i;
	}
	int Get_food_Y() {
		return this->food_j;
	}
};
class Snake_Head {
private:
	int x, y; //  食物的位置
public:
	Snake_Head(int x, int y) {
		this->x = x;
		this->y = y;
	}
	Snake_Head() {
		this->x = 15;
		this->y = 15;//如果未設定蛇頭 將位於15,15起始
	}
	void SetHead(int x, int y) {
		this->x = x;
		this->y = y;
	}
	int Get_Head_X() {
		return this->x;
	}
	int Get_Head_Y() {
		return this->y;
	}
};
class Snake_Tail {
private:
	int x, y; //  食物的位置
public:
	Snake_Tail(int x, int y) {
		this->x = x;
		this->y = y;
	}
	Snake_Tail() {
		this->x = 15;
		this->y = 15;//如果未設定蛇頭 將位於15,15起始
	}
	void SetTail(int x, int y) {
		this->x = x;
		this->y = y;
	}
	int Get_Tail_X() {
		return this->x;
	}
	int Get_Tail_Y() {
		return this->y;
	}
};
class Snake_Game {
private:
	Food food;
	Snake_Head old_head, new_head;
	Snake_Tail tail;

public:
	int Blocks[HEIGHT][WIDTH] = { 0 }; //  二維陣列，用於記錄所有的遊戲地圖
	void moveSnake() // 移動小蛇及相關處理函數
	{
		int i, j;
		for (i = 0; i < HEIGHT; i++) // 對行遍歷 
			for (j = 0; j < WIDTH; j++) // 對列遍歷
				if (Blocks[i][j] > 0) // 大於0的為小蛇元素 
					Blocks[i][j]++; //  讓其+1
		//int oldTail_i, oldTail_j, oldHead_i, oldHead_j; // 定義變量，儲存界舊蛇尾、蛇頭舊座標  
		int max = 0; // 用於紀錄最大值 
		for (i = 0; i < HEIGHT; i++) //  對行列遍歷
		{
			for (j = 0; j < WIDTH; j++) //  
			{
				if (max < Blocks[i][j]) //  如果當前元素值比max大
				{
					max = Blocks[i][j]; // 更新max的值
					/*
					oldTail_i = i; //  紀錄最大值的座標，就是舊蛇尾的位置
					oldTail_j = j; //
					*/
					tail.SetTail(i, j);
				}
				if (Blocks[i][j] == 2) // 找到數值為2 
				{
					/*
					oldHead_i = i; //  數值為2恰好是舊蛇頭的位置
					oldHead_j = j; //
					*/
					old_head.SetHead(i, j);
				}
			}
		}
		/*
		int newHead_i = oldHead_i; // 設定變量儲存新蛇頭的位置
		int newHead_j = oldHead_j;
		*/
		new_head.SetHead(old_head.Get_Head_X(), old_head.Get_Head_Y());
		//  根據用戶按鍵，設定新蛇頭的位置
		if (moveDirection == 'w') // 向上一定
			/*newHead_i = oldHead_i - 1;*/
			new_head.SetHead(old_head.Get_Head_X() - 1, old_head.Get_Head_Y());
		else if (moveDirection == 's') // 向下移動
			/*newHead_i = oldHead_i + 1;*/
			new_head.SetHead(old_head.Get_Head_X() + 1, old_head.Get_Head_Y());
		else if (moveDirection == 'a') // 向左移動
			/*newHead_j = oldHead_j - 1;*/
			new_head.SetHead(old_head.Get_Head_X(), old_head.Get_Head_Y() - 1);
		else if (moveDirection == 'd') // 向右移動
			/*newHead_j = oldHead_j + 1;*/
			new_head.SetHead(old_head.Get_Head_X(), old_head.Get_Head_Y() + 1);

		//  如果蛇頭超出邊界，或者蛇頭碰到蛇身，遊戲失敗
		if (new_head.Get_Head_X() >= HEIGHT || new_head.Get_Head_X() < 0 || new_head.Get_Head_Y() >= WIDTH || new_head.Get_Head_Y() < 0
			|| Blocks[new_head.Get_Head_X()][new_head.Get_Head_Y()]>0)
		{
			isFailure = 1; //  遊戲失敗
			return; // 函數返回
		}

		Blocks[new_head.Get_Head_X()][new_head.Get_Head_Y()] = 1;  // 新蛇頭位置數值為1 
		if (new_head.Get_Head_X() == food.Get_food_X() && new_head.Get_Head_Y() == food.Get_food_Y()) //  如果新蛇頭正好碰到食物
		{
			/*
			food_i = rand() % (HEIGHT - 5) + 2; //  食物重新隨機位置
			food_j = rand() % (WIDTH - 5) + 2; //
			*/  //改成下面這行 然後 food是class我將它設定有x 與 y 並設定 設置食物的函數 可以上去看一下函式使用方法
			food.Setfood(rand() % (HEIGHT - 5) + 2, rand() % (WIDTH - 5) + 2);
			// 不對舊蛇尾處理，相當於蛇的長度+1
		}
		else // 新蛇頭没有碰到食物
			Blocks[tail.Get_Tail_X()][tail.Get_Tail_Y()] = 0; // 舊蛇尾變成空白，不吃食物時保持蛇的長度不變
	}

	void startup()  //  初始化函數
	{
		int i;
		Blocks[HEIGHT / 2][WIDTH / 2] = 1; // 畫面中間畫蛇頭，數字為1
		for (i = 1; i <= 4; i++) //  向左依次4個蛇身，數值依次為2,3,4,5
			Blocks[HEIGHT / 2][WIDTH / 2 - i] = i + 1;
		moveDirection = 'd';  //  初始向右移動
		/*food_i = rand() % (HEIGHT - 5) + 2; //  初始化随機食物位置
		food_j = rand() % (WIDTH - 5) + 2; //  */
		food.Setfood(rand() % (HEIGHT - 5) + 2, rand() % (WIDTH - 5) + 2);	//存到class中的食物
		initgraph(WIDTH*BLOCK_SIZE, HEIGHT*BLOCK_SIZE); //  新開畫面
		setlinecolor(RGB(200, 200, 200)); // 設置線條顏色
		BeginBatchDraw(); // 開始批量繪製
	}

	void show()  // 繪製函數
	{
		cleardevice(); // 清除畫面
		int i, j;
		for (i = 0; i < HEIGHT; i++) //  對二維陣列的地圖設定
		{
			for (j = 0; j < WIDTH; j++)
			{
				if (Blocks[i][j] > 0) // 當地圖大於0表示是蛇，這裡讓蛇的身體颜色色調改變
					setfillcolor(HSVtoRGB(Blocks[i][j] * 10, 0.9, 1));
				else
					setfillcolor(RGB(150, 150, 150)); // 元素為0表示為空，顏色為灰色
				   // 在對應位直處，以對應颜色繪製小方格
				fillrectangle(j*BLOCK_SIZE, i*BLOCK_SIZE,
					(j + 1)*BLOCK_SIZE, (i + 1)*BLOCK_SIZE);
			}
		}
		setfillcolor(RGB(0, 255, 0)); //  食物為綠色
		//  繪製食物小方塊
		fillrectangle(food.Get_food_Y()*BLOCK_SIZE, food.Get_food_X()*BLOCK_SIZE,
			(food.Get_food_Y() + 1)*BLOCK_SIZE, (food.Get_food_X() + 1)*BLOCK_SIZE);
		if (isFailure) //  如果遊戲失敗
		{
			setbkmode(TRANSPARENT); // 文字字體透明    
			settextcolor(RGB(255, 0, 0));// 設定文字颜色
			settextstyle(80, 0, _T("宋體")); //  設定文字大小、樣式
			outtextxy(240, 220, _T("遊戲失敗")); //  輸出文字内容
		}
		FlushBatchDraw(); // 批量繪製
	}

	void updateWithoutInput() // 與輸入無關的更新函數
	{
		if (isFailure) //  如果遊戲失敗，函數返回
			return;
		static int waitIndex = 1; // 靜態局部變量，初始化時為1
		waitIndex++; // 每一幀+1
		if (waitIndex == 10) // 如果等於10才執行，這樣小蛇每隔10幀移動一次
		{
			moveSnake(); //  調用小蛇移動函數
			waitIndex = 1; // 再變成1
		}
	}

	void updateWithInput()  // 和輸入有關的更新函數
	{
		if (_kbhit() && isFailure == 0)  //  如果有按鍵輸入，並且不失敗
		{
			char input = _getch(); //  獲得按鍵輸入
			if (input == 'a' || input == 's' || input == 'd' || input == 'w') // 如果是asdw 
			{
				moveDirection = input;  //設定移動方向
				moveSnake(); // 調用小蛇移動函數
			}
		}
	}
};


int main() //  主函數
{
	Snake_Game game;
	game.startup();  // 初始化函數，僅執行一次 
	while (1)   // 一直循環
	{
		game.show();  // 進行繪製
		game.updateWithoutInput(); // 和輸入無關的更新 
		game.updateWithInput();    // 和輸入有關的更新
	}
	return 0;
}
