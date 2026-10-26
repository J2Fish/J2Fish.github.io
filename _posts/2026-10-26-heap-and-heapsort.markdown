---
layout:     post
title:      "heap and heap_sort"
subtitle:   "heap_practice"
date:       2026-10-26 21:33
author:     "J2Fish"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - algorithm
    - data_structure
    - C++
---


Heap is a special type of binary tree that every father point will bigger than both its son point
Natually,when we set the index "1" as head, heap can easily use index to indicate the fa-son relationship with this formula like binary tree:
 `son_left = fa_idx*2, son_right = fa_idx*2+1 //first_idx = 1`
Something I must note is that the ```upinsert()``` should compare whether its father bigger than itself ,on the contrary ```downinsert``` should compare weather itself bigger than its son.

Heap_sort just use the ```pop()``` to pop every element in the list, and the final list will be ordered.

Following is the whole codes:
``` C++
#include <iostream>
using namespace std;
class heap{
    private:
        int list[10000];
        int ptr = 0;
        bool type = true; //true 大根, false 小根
    public:
        heap(bool type): type(type){
            for (int i = 0; i < 10000; i++) list[i] = -1;
        }
        void insert(int value){
            ptr++;
            list[ptr] = value;
            this->up(ptr);
            
        }
        void up(int idx){
            int self = idx;
            while (true){
                int fa = self/2;
                if (fa <= 0) break;
                if (this->compare(fa, self)){
                    int temp = list[fa];
                    list[fa] = list[self];
                    list[self] = temp;
                    self = fa;
                    fa = self/2;
                }
                else break;
            }
        }

        void down(int idx){
            int self = idx;
            while (true){
                // this->range();
                // cout << '\n';
                int son_l = self*2;
                int son_r = self*2+1;
                int son = compare(son_l, son_r) ? son_r : son_l;
                if (son > ptr) break;
                if (!this->compare(son, self)){
                    int temp = list[son];
                    list[son] = list[self];
                    list[self] = temp;
                    self = son;
                }
                else break;
            }
        }

        bool compare(int other, int self){
            if (type)
                return list[other] < list[self];
            else
                return !(list[other] < list[self]);
        }

        void pop(){
            int temp = list[1];
            list[1] = list[ptr];
            list[ptr] = temp;
            //cout << list[1] << ',' << ptr << '\n';
            ptr--;
            this->down(1);
        }

        void dfs(){
            cout << "111" << '\n';
        }

        void range(){
            for (int i = 1; list[i] != -1; i++){
                cout << list[i] << '\t';
            }
        }
};

int main(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    heap h(true);
    for (int i = 0; i < 10; i++){
        h.insert(i);
    }
    h.range();
    cout << '\n';
    for (int i = 0; i < 10; i++){
        h.pop();
    }
    h.range();
    return 0;
}
```

Next essasy will focus on some specific algorithm problem
