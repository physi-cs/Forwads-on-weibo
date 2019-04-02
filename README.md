#include<vector>
#include<queue>
#include<cstdio>
#include<cstring>
using namespace std;
const int maxn=1010;
const int INF=1000000000;
int n,l;
struct user{
    int num;//编号
    int floor;//层数
};
int G[maxn][maxn]={0};//邻接矩阵存储关注关系
bool inq[maxn];
int BFS(int u){//对编号u的顶点所在连通集遍历
    int count=0;
    queue<user> q;
    user start;
    start.num=u;
    start.floor=0;
    q.push(start);
    inq[u]=true;
    while(!q.empty()){
        user top=q.front();
        q.pop();
        int o=top.num;
        for(int v=0;v<n;v++){
            user next;
            next.num=v;
            next.floor=top.floor+1;
            if(inq[v]==false&&G[o][v]!=0&&next.floor<=l){
                q.push(next);
                inq[v]=true;
                count++;
            }
        }
    }
    return count;
}
int main(){
    int k;int t;
    scanf("%d%d",&n,&l);
    for(int i=0;i<n;i++){
        scanf("%d",&k);
        for(int j=0;j<k;j++){
            scanf("%d",&t);
            G[t][i]=1;
        }
    }
    int m;
    scanf("%d",&m);
    int a;
    for(int x=0;x<m;x++){
        memset(inq,false,sizeof(inq));
        scanf("%d",&a);
        printf("%d\n",BFS(a));

    }
    return 0;
}
