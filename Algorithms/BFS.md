# 问题本质
<mark>在一幅“图”中找到从起点start到终点target的最近距离</mark>
# 框架
```
int BFS(Node start, Node target){
    Queue<Node> q;
    Set<Node> visited;//避免走回头路

    q.offer(start);//将起点加入队列
    visited.add(start);
    int step=0;//记录扩散的步数

    while( q not empty){
        int size=q.size();
        /*将当前队列中的所有节点向四周扩散*/
        for(int i=0;i<size;i++){
            Node cur=q.poll();
            //是否到达终点
            if (cur is target)
                return step;
            //将cur的相邻节点加入队列
            for (Node :cur.adj){
                if(x not in visited){
                    q.offer(x);
                    visited.add(x);
                }
            }
        }
        //更新步数
        step++;
    }
}
```
# 实例
## 二叉树的最小深度
```
def minDepth(root):
    if not root:
        return 0
    q=list()
    q.append(root)
    depth=1
    while q:
        size=len(q)
        for i in range(size):
            cur=q[0]
            q=q[1:]
            if not cur.left and not cur.right:
                return depth
            if cur.left:
                q.append(cur.left)
            if cur.right:
                q.append(cur.right)
        depth+=1
    return depth
```
## 揭开密码锁的最小次数