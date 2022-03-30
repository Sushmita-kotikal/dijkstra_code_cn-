#include<stdio.h>
#include<conio.h>
#define INFINITY 9999
#define max 10

void djk(int g[max][max], int n, int startnode);
int main()
{
    int g[max][max],i,j,n,u;
    printf("enter the no of vertices :");
    scanf("%d",&n);
    printf("enter adjacent matrix:");
    for(i=0; i<n; i++)
        for(j=0; j<n; j++)
            scanf("%d",&g[i][j]);
    printf("enter the starting node:");
    scanf("%d",&u);
    djk(g,n,u);
    return 0;
}
void djk(int g[max][max], int n, int startnode)
{
    int cost[max][max],distance[max],pred[max];
    int visited[max],count,mindistance,nextnode,i,j;
    for(i=0; i<n; i++)
        for(j=0; j<n; j++)
            if(g[i][j]==0)
                cost[i][j]=INFINITY;
            else
                cost[i][j]=g[i][j];

    for(i=0; i<n; i++){
        distance[i]=cost[startnode][i];
        pred[i]=startnode;
        visited[i]=0;
    }
    distance[startnode]=0;
    visited[startnode]=1;
    count=1;

    while(count<n-1){
        mindistance=INFINITY;
        for(i=0;i<n;i++)
            if(distance[i]<mindistance&&!visited[i]){
                mindistance=distance[i];
                nextnode=i;
            }
        visited[nextnode]=1;
        for(i=0;i<n;i++)
            if(mindistance+cost[nextnode][i]<distance[i]){
                distance[i]=mindistance+cost[nextnode][i];
                pred[i]=nextnode;
               }
        count++;
    }
    for(i=0;i<n;i++)
        if(i!=startnode){
                printf("distance bet node %d=%d",i,distance[i]);
                printf("\n path %d",i);
                j=i;
                do{
                    j=pred[i];
                    printf("<-%d",j);
                }while(j!=startnode);
    }
}
