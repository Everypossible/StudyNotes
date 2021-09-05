# 广东工业大学数据结构AnyView参考答案

## 1、第一章

1. ![image-20210902201634767](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210902201634767.png)

    ```c
    #include "allinclude.h"  //DO NOT edit this line
    void Descend(int &a, int &b, int &c)  // 通过交换，令 a >= b >= c
    {   // Add your code here
        if(a < b){
          swap(a, b);
        }
        if(a < c){
          swap(a,c);
        }
        if(b < c){
          swap(b,c);
        }
    }
    
    void swap(int a, int b){
      int c;
      c = a;
      a = b;
      b = a;
    }
    ```

    

2. ![image-20210902201916117](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210902201916117.png)

    ```c
    #include "allinclude.h"  //DO NOT edit this line
    float Polynomial(int n, int a[], float x0) 
    {   // Add your code here
      float result=0;
      for(int i = 0; i <= n; i++){
        result += a[i]*pow((x0),i);
      }
      return result;
    }
    ```

    

3. 。。。

4. ![image-20210902202052317](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210902202052317.png)

    ```c
    #include "allinclude.h"  //DO NOT edit this line
    Status Series(int a[], int n) { 
        // Add your code here
        if(n == 0){
          return ERROR;
        }
        int result=1, res = 1;
        for(int k = 1; k <= n; k++){
          res = 1;
          for(int j = 1; j <= k; j++){
            res = res * j;
          }
          res = res*pow(2,k);
          if(res > MAXINT){
            return EOVERFLOW;
          }
          a[k-1] = res;
        }
        return OK;
    
    }
    ```

    

5. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905091522410.png" alt="image-20210905091522410" style="zoom: 67%;" />

    ```c
    #include "allinclude.h"
    void printName(stuType student[], int index[], int n)
    { 
      for(int i = 0; i < n; i++){
            printf("%s\n", student[index[i]].name);
      }
    }
    ```

    

6. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905091723185.png" alt="image-20210905091723185" style="zoom:67%;" />

    ````c
    #include "allinclude.h"
    float highestScore(stuType *student[], int n)
    {  // Add your code here
        float max=0;
        for(int i = 0; i < n; i++){
          if(max < student[i]->score){
            max = student[i]->score;
          }
        }
        return max;
    }
    ````

    

7. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905091832784.png" alt="image-20210905091832784" style="zoom:67%;" />

    ```c
    #include "allinclude.h"
    void printFirstName_HighestScore(stuType *student[], int n)
    {  // Add your code here
        stuType *studentMax=NULL;
        float scoreMax=0;
        for(int i = 0; i < n; i++){
          if(scoreMax < student[i]->score){
            studentMax = student[i];
            scoreMax = student[i]->score;
          }
        }
        for (int i = 0; i < 4; i++) {
          printf("%c", studentMax->name[i]);
        }
        printf("\n%.2f\n",  studentMax->score);
    }
    ```

    

8. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905092214101.png" alt="image-20210905092214101" style="zoom:67%;" />

    ```c
    #include "allinclude.h"
    void printLastName_HighestScore(stuType *student[], int n)
    {  // Add your code here
        stuType *studentMax=NULL;
        float scoreMax=0;
        for(int i = 0; i < n; i++){
          if(scoreMax <= student[i]->score){
            studentMax = student[i];
            scoreMax = student[i]->score;
          }
        }
        for (int i = 0; i < 4; i++) {
          printf("%c", studentMax->name[i]);
        }
        printf("\n%.2f\n",  studentMax->score);
    }
    ```

    

9. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905092344369.png" alt="image-20210905092344369" style="zoom:67%;" />

    ```c
    #include "allinclude.h"  //DO NOT edit this line
    void A() {
    	printf("X\n");
    }
    void B() {
    	printf("Y\n");
    }
    
    int main()
    {
    	void (*funcp)(); //定义函数指针
    
    	funcp = A;
    	(*funcp)(); // 实际上调用了A( );
    
    	funcp = B;
    	(*funcp)(); // 实际上调用了B( );
    
    	return 0;
    }
    ```

    

10. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905092428811.png" alt="image-20210905092428811" style="zoom:67%;" />

    ```c
    #include "allinclude.h"  //DO NOT edit this line
    void hello() 
    { 
    	printf("Hello world!\n"); 
    }
    
    void runFun(void (*pFun)()) 
    {
    	pFun();  //函数指针;
    }
    
    
    int main()
    {
    	runFun(hello);  //hello是实际要调用的函数
    
    	return 0;
    }
    ```

    

11. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905092514568.png" alt="image-20210905092514568" style="zoom:67%;" />

     ````c
     #include "allinclude.h"
     StrSequence* reverseStr(StrSequence* strSeq)
     /*返回一个结构体，该结构体将strSeq中的字符串逆序存放*/
     {  // Add your code here
         int length    = strSeq->length;
         ElemType *str = (ElemType*)malloc(length);
         for(int i = length-1; i >= 0; i--){
           str[length-1-i] = strSeq->elem[i];
         }
         
         StrSequence *res = (StrSequence*)malloc(sizeof(StrSequence));
         res->elem   = str;
         res->length = length;
         return res;
     }
     ````

     

12. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905092747752.png" alt="image-20210905092747752" style="zoom:67%;" />

     ```c
     #include "allinclude.h"  //DO NOT edit this line
     Status CreateSequence(Sequence &S, int n, ElemType *a) { 
       if(n <= 0) return ERROR;
        S.length = n;
        S.elem = a;
        return OK;
     }
     ```

     

13. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905092937216.png" alt="image-20210905092937216" style="zoom:67%;" />

     ```c
     #include "allinclude.h"  //DO NOT edit this line
     LinkList MakeNode(ElemType x) { 
         // Add your code here
         LNode *head=(LNode*)malloc(sizeof(LNode));
         head->data = x;
         head->next = NULL;
         return head;
     }
     ```

     

14. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905093041765.png" alt="image-20210905093041765" style="zoom:67%;" />

     ```c
     #include "allinclude.h"  //DO NOT edit this line
     LinkList CreateLinkList(ElemType x, ElemType y) { 
         // Add your code here
     
         LNode *head,*p;
         head=(LNode*)malloc(sizeof(LNode));
         p=(LNode*)malloc(sizeof(LNode));
         if(head!=NULL){
             head->data=x;
             head->next=p;
             }
         if(p!=NULL){
             p->data=y;
             p->next=NULL;
             }
         return head; 
         return NULL; // This is a temporary code. Change it if necessary.
     }
     ```

     

15. <img src="C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210905093128791.png" alt="image-20210905093128791" style="zoom:67%;" />

     ```c
     #include "allinclude.h"  //DO NOT edit this line
     LinkList CreateOrdLList(ElemType x, ElemType y) { 
         // Add your code here
         LNode *head, *p;
         head = (LNode*)malloc(sizeof(LNode));
         p    = (LNode*)malloc(sizeof(LNode));
         
         head->next = p;
         p->next = NULL;
         if(x < y){
           head->data = x;
           p->data = y;
         } else {
           head->data = y;
           p->data = x;
         }
         return head;
     }
     ```

     

16. 

