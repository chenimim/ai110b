# HW2 CODE
## (1)單一路徑
```
#include <stdlib.h>
#define SIZE 7

typedef struct {
    int x; 
    int y;
} Point;

Point pt(int, int);
int visit(int[][SIZE], Point, Point);
void print(int[][SIZE]);

int main(void) { 
    int maze[SIZE][SIZE] = {{2, 2, 2, 2, 2, 2, 2}, 
                            {2, 0, 0, 0, 0, 0, 2}, 
                            {2, 0, 2, 0, 2, 0, 2}, 
                            {2, 0, 0, 2, 0, 2, 2}, 
                            {2, 2, 0, 2, 0, 2, 2}, 
                            {2, 0, 0, 0, 0, 0, 2}, 
                            {2, 2, 2, 2, 2, 2, 2}}; 

    if(!visit(maze, pt(1, 1), pt(5, 5))) {
        printf("\n沒有找到出口！\n"); 
    }
    print(maze);
    
    return 0; 
}

Point pt(int x, int y) {
    Point p = {x, y};
    return p;
}

int visit(int maze[][SIZE], Point start, Point end) {
    if(!maze[start.x][start.y]) {
         maze[start.x][start.y] = 1;
         if(!maze[end.x][end.y] && 
            !(visit(maze, pt(start.x, start.y + 1), end) || 
              visit(maze, pt(start.x + 1, start.y), end) ||
              visit(maze, pt(start.x, start.y - 1), end) || 
              visit(maze, pt(start.x - 1, start.y), end))) {
                 maze[start.x][start.y] = 0;
         }
    }
    return maze[end.x][end.y];
    
}

void print(int maze[][SIZE]) {
    int i, j;
    for(i = 0; i < SIZE; i++) { 
        for(j = 0; j < SIZE; j++) switch(maze[i][j]) {
            case 0 : printf("  "); break;
            case 1 : printf("◇"); break;
            case 2 : printf("█"); 
        }
        printf("\n"); 
    }     
}
```
## (2)全部路徑
```
#include <stdio.h>
#include <stdlib.h>
#define SIZE 9

typedef struct {
    int x; 
    int y;
} Point;

Point pt(int, int);
void visit(int[][SIZE], Point, Point, void (*)(int[][SIZE]));
void print(int[][SIZE]);

int main(void) { 
    int maze[SIZE][SIZE] = {{2, 2, 2, 2, 2, 2, 2, 2, 2},
                            {2, 0, 0, 0, 0, 0, 0, 0, 2},
                            {2, 0, 2, 2, 0, 2, 2, 0, 2},
                            {2, 0, 2, 0, 0, 2, 0, 0, 2},
                            {2, 0, 2, 0, 2, 0, 2, 0, 2},
                            {2, 0, 0, 0, 0, 0, 2, 0, 2},
                            {2, 2, 0, 2, 2, 0, 2, 2, 2},
                            {2, 0, 0, 0, 0, 0, 0, 0, 2},
                            {2, 2, 2, 2, 2, 2, 2, 2, 2}}; 

    visit(maze, pt(1, 1), pt(7, 7), print);

    return 0; 
}

Point pt(int x, int y) {
    Point p = {x, y};
    return p;
}

void visit(int maze[][SIZE], Point start, 
           Point end, void (*take)(int[][SIZE])) {
    if(!maze[start.x][start.y]) {
         maze[start.x][start.y] = 1;
         if(maze[end.x][end.y]) {
             take(maze);
         }
         else {
             visit(maze, pt(start.x, start.y + 1), end, take);
             visit(maze, pt(start.x + 1, start.y), end, take);
             visit(maze, pt(start.x, start.y - 1), end, take);
             visit(maze, pt(start.x - 1, start.y), end, take);
         }
         maze[start.x][start.y] = 0;
    }
}

void print(int maze[][SIZE]) {
    int i, j;
    for(i = 0; i < SIZE; i++) { 
        for(j = 0; j < SIZE; j++) switch(maze[i][j]) {
            case 0 : printf("  "); break;
            case 1 : printf("◇"); break;
            case 2 : printf("█"); 
        }
        printf("\n"); 
    }     
}
```
## 參考資料
```
老鼠走迷宮:https://openhome.cc/zh-tw/algorithm/basics/maze/#google_vignette
```
