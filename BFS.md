## 909.蛇梯棋
### 给你一个大小为 n x n 的整数矩阵 board ，方格按从 1 到 n*n 编号，编号遵循 转行交替方式 ，从左下角开始 （即，从 board[n - 1][0] 开始）每一行交替方向。玩家从棋盘上的方格 1 （总是在最后一行、第一列）开始出发。每一回合，玩家需要从当前方格 curr 开始出发，按下述要求前进：选定目标方格 next ，目标方格的编号符合范围 [curr + 1, min(curr + 6, n2)] 。该选择模拟了掷 六面体骰子 的情景，无论棋盘大小如何，玩家最多只能有 6 个目的地。传送玩家：如果目标方格 next 处存在蛇或梯子，那么玩家会传送到蛇或梯子的目的地。否则，玩家传送到目标方格 next 。 当玩家到达编号 n2 的方格时，游戏结束。r 行 c 列的棋盘，按前述方法编号，棋盘格中可能存在 “蛇” 或 “梯子”；如果 board[r][c] != -1，那个蛇或梯子的目的地将会是 board[r][c]。编号为 1 和 n2 的方格上没有蛇或梯子。注意，玩家在每回合的前进过程中最多只能爬过蛇或梯子一次：就算目的地是另一条蛇或梯子的起点，玩家也 不能 继续移动。举个例子，假设棋盘是 [[-1,4],[-1,3]] ，第一次移动，玩家的目标方格是 2 。那么这个玩家将会顺着梯子到达方格 3 ，但 不能 顺着方格 3 上的梯子前往方格 4 。返回达到编号为 n2 的方格所需的最少移动次数，如果不可能，则返回 -1。
### 模板代码
```
class Solution {
    public int snakesAndLadders(int[][] board) {
        int n = board.length;
        int step = 0;
        Queue<Integer> queue = new LinkedList<>();
        boolean visited[] = new boolean[n * n];
        queue.offer(1);// 将数值放入队列，非坐标
        while (!queue.isEmpty()) {
            step++;// 没遍历一层，步数加1
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int head = queue.poll();
                for (int k = 1; k < 7 && k + head <= n*n; k++) {
                    int new_x = k + head;
                    int[] temp = convert(n, new_x-1);
                    int x = board[temp[0]][temp[1]] < 0 ? new_x : board[temp[0]][temp[1]];// 如果遇见蛇或梯子则跳转
                    if (x == n * n)
                        return step;
                    if (visited[x])
                        continue;
                    
                    visited[x] = true;
                    queue.offer(x);

                }
            }
        }
        return -1;
    }

    public int[] convert(int n, int id) {
        int row = id / n;
        int col = id % n;
        // 偶数行从右往左
        if (row % 2 != 0)
            col = n - 1 - col;
        return new int[] { n - 1 - row, col };
    }
}
```
