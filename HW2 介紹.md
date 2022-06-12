# 老鼠走迷宮
老鼠走迷宮是遞迴求解的基本題型，例如，在二維陣列中使用 2 表示迷宮牆壁，1 表示老鼠的行走路徑，以程式求出由入口至出口的一條路徑；進一步地，若入口至出口路徑可能不只一條，列出全部路。

## 解法思路
老鼠的走法有上、左、下、右四個方向，每前進一格後，選一個未造訪方向進行遞迴，無法前進時退回，選擇下一個可前進方向，如此在陣列中依序測試四個方向，直到走到出口為止，也就是說，先判斷哪些方向可以走, 把可以走的方向放到 stack 中, 再 pop 出來。
```
Procedure GO(maze[])
    VISIT(maze, START_I, START_J, END_I, END_J)
    
Procedure VISIT(maze[], i, j, end_i, end_j)
    IF maze[i][j] == 0
        maze[i][j] = 1
        IF maze[end_i][end_j] == 0
           IF !(VISIT(maze, i, j + 1, end_i, end_j) OR 
                VISIT(maze, i + 1, j, end_i, end_j) OR
                VISIT(maze, i, j - 1, end_i, end_j) OR 
                VISIT(maze, i - 1, j, end_i, end_j))
               maze[i][j] = 0
    RETURN maze[end_i][end_j] == 1
```
求全部路徑的話，只要在老鼠走至出口時顯示經過的路徑，然後退回重新選擇下個方向遞迴就可以了：
```
Procedure GO(maze[])
    VISIT(maze, START_I, START_J, END_I, END_J)
    
Procedure VISIT(maze[], i, j, end_i, end_j)
    IF maze[i][j] == 0
        maze[i][j] = 1
        IF maze[end_i][end_j] == 1
            PRINT maze
        ELSE
            VISIT(maze, i, j + 1, end_i, end_j)
            VISIT(maze, i + 1, j, end_i, end_j)
            VISIT(maze, i, j - 1, end_i, end_j)
            VISIT(maze, i - 1, j, end_i, end_j)
        maze[i][j] = 0
```
## 實作
```
入口處是一隻老鼠，0是他可以走的路，2是牆壁，走過的路會被改寫為1，如此一直走到出口才能吃到可口的乳酪。另外這圖片是給使用者方便了解用的，實際的迷宮印出來會是其他的圖形。
至於求所有路徑看起來複雜但其實更簡單，只要在老鼠走至出口時顯示經過的路徑，然後退回上一格重新選擇下一個位置繼續遞迴就可以了，不過這樣比求單一路徑還要簡單。
```
## 參考資料
```
1. https://openhome.cc/zh-tw/algorithm/basics/maze/#google_vignette (程式碼，知識介紹參考)
```
