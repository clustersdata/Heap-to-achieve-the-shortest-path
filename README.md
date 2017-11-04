# Heap-to-achieve-the-shortest-path

Heap to achieve the shortest path

#include <iostream>
  
#include <string>
  
#include <stdlib.h>

#include <vector>;
  
using namespace std;

#define M 1001

#define LIM 2000000000


struct dd{ //最短距离

	int w,q;//w是距离值,q是堆中的相对位置
  
}d[M],d2[M];

struct node{

	int v,w;
  
};

int h[M],hs;

vector<node> g[M],g2[M];
  
void change_key(dd d[M],int v,int w){

	d[v].w=w;
  
	int i=d[v].q;
  
	while(i>1 && d[h[i/2]].w>d[h[i]].w){
  
		swap(h[i],h[i/2]);
    
		swap(d[h[i]].q,d[h[i/2]].q);
    
		i=i/2;
    
	}
  
}

inline void min_heaphy(dd d[M],int *a,int i,int s){//s 为堆大小

	int l=i*2,r=i*2+1;
  
	int miner=i;
  
	if (l<=s && d[a[i]].w>d[a[l]].w)
  
		miner = l;
    
    
	else miner=i;
  
	if (r<=s && d[a[miner]].w>d[a[r]].w)
  
		miner=r;
    
	if(miner!=i){
  
		swap(a[i],a[miner]);
    
		swap(d[a[i]].q,d[a[miner]].q);
    
		min_heaphy(d,a,miner,s);
    
	}
  
}

inline void init(dd d[M],int n,int s){  //初始化图和堆

	int i;
  
	hs=n;
  
	for(i=1;i<=n;i++){d[i].w=LIM;h[i]=d[i].q=i;}
  

	change_key(d,s,0);
  
}

inline void relax(dd d[M],int u,int v,int duv){

	if(d[v].w>d[u].w+duv) change_key(d,v,d[u].w+duv);
  
}

void dijkstra(vector<node> g[M],dd d[M],int n,int s){ //n is |V| && s is the source
  
	init(d,n,s);
  
	int i;
  
	while(hs!=0){
  
		int u=h[1];
    
		swap(h[1],h[hs]);
    
		swap(d[h[1]].q,d[h[hs]].q);
    
    
		hs--;
    
		min_heaphy(d,h,1,hs);
    
		for(i=0;i<g[u].size();i++) relax(d,u,g[u][i].v,g[u][i].w);
    
	}
  
}
