1.#include<stdio.h>

 struct Week{
   char day[100];
   int date;
   char actdisp[100];
 };

 struct Week day[7];
  
   void read(){
       for(int i = 1;i<=7;i++){
       printf("Enter the date for week:\n");
       scanf("%d",&day[i].date);

       printf("Enter the Day for week:\n");
       scanf("%s",day[i].day);

       printf("Enter the activity discreption:\n");
       scanf("%s",day[i].actdisp);
    }
   }

    void display(){
      printf("------------Calendar---------\n");

      for(int i = 1; i<=7; i++){
         printf("Date:%d, \t Day:%s, \t ActivityDEScription:%s \n",day[i].date,day[i].day,day[i].actdisp);
      }

    }

     int main(){

         read();
         display();

         return 0;
     }


     

     2.#include<stdio.h>
#include<stdlib.h>
char str[100],pat[100],rep[100],ans[100];
int i=0,j=0,m=0,c=0,k,flag=0;

 void strs(){
    while(str[c]!='\0'){
        if(str[m]==pat[i]){
              i++;
              m++;
              if(pat[i]=='\0'){
                flag=1;
                for(k=0;rep[k]!='\0';k++,j++){
                    ans[j]=rep[k];
                }
                i=0;
                c=m;
              }
        }else{
            ans[j]=str[c];
            j++;
            c++;
            m=c;
            i=0;
        }
    }
    ans[j]='\0';
 }

 void main(){
    printf("Enter the string:\n");
    gets(str);
    printf("Enter the pattern:\n");
    gets(pat);
    printf("Enter the replacement:\n");
    gets(rep);
    strs();
    if(flag==1){
        printf("%s",ans);
    }else{
        printf("not working");
    }
 }


 3.#include<stdio.h>

#include<stdlib.h>

#include<string.h>

#define MAX 100

 int s[MAX];

 int top=-1;



 void push();

 void pop();

 void display();

 void palindrome();



 int main(){

    int ch;

    while(1){

        printf("\nENTER THE CHOICE\n 1.Push\n 2.pop\n 3.display \n 4.palindrome\n");

        scanf("%d",&ch);



        switch(ch){

            case 1 : push();break;

            case 2 : pop();break;

            case 3 : display();break;

            case 4 : palindrome();break;

        }

    }

    return 0;

 }



 void push(){

    int x;



    if(top==MAX-1){

        printf("Overflow");

    }else{

    printf("Enter to push element:");

    scanf("%d",&x);

    top=top+1;

    s[top]=x;

 }

 }

  

 void pop(){

    if(top==-1){

       printf("Underflow");

    }else{

    printf("The poped element is :%d",s[top]);

    top=top-1;

 }

 }



 void display(){

    for(int i=top;i>=0;i--){

        printf("|%d|\n",s[i]);

    }

 }

  void palindrome(){



    char a[10],b[10];

    printf("Enter the str\n");

    fflush(stdin);

    gets(a);

    strcpy(b,a);

    strrev(b);

    if(strcmp(a,b)==0){

    printf("this is palindrome");

    }else{

    printf("This is not palindrome");

  }

  }



  4.#include<stdio.h>
#include<ctype.h>
#include<string.h>

 char infix[100],postfix[100];
int top=-1;

void push(char c){
         infix[++top]=c;
    }
char pop(){
    return infix[top--];
}
int precedence(char c){
    switch(c){
        case '^':return 3;
        case '*':
        case '/':return 2;
        case '+':
        case '-':return 1;
        defalut:return-1; 
    }
}
 int isoperator(char c){
    return(c=='+' || c=='-' || c=='*' || c=='/' || c=='^');
 }

  void convert(){
    int i=0,j=0;
    while(infix[i]!='\0'){
         if(isalnum(infix[i])){
            postfix[j++]=infix[i++];
         }else if (infix[i]=='('){
                 push(infix[i++]);
         }else if(infix[i]==')'){
                while(infix[top]!='(')
                    postfix[j++]==pop();
                    pop();
                    i++;
                }
                else{
                    while(top>=0&&precedence(infix[top])>=precedence(infix[i]))
                        postfix[j++]=pop();
                        push(infix[i++]);
                }
    }
    while(top>=0)
         postfix[j++]=pop();
         postfix[j]='\0';
  }

   void main(){
    printf("Enter INFfix exp:");
    scanf("%s",infix);
    convert();
    printf("postfix exp:%s",postfix);
   }




   5.a  #include<stdio.h>
#include<ctype.h>
#include<math.h>

 int i,top=-1,op1,op2,res,s[20];
 char postfix[20],symb;

void push(int item){
    s[++top]=item;
}
int pop(){
    return (s[top--]);
}

 void main(){
    printf("Enter postfix expression:");
    scanf("%s",postfix);

    for(int i=0;postfix[i]!='\0';i++){
        symb=postfix[i];
        if(isdigit(symb)){
            push(symb-'0');
        }else{
            op2=pop();
            op1=pop();

                 switch(symb){
                    case '+':push(op1+op2);
                             break;
                    case '-':push(op1-op2);
                             break;
                    case '*':push(op1*op2);
                             break;
                    case '/':push(op1/op2);
                             break;
                    case '^':push(pow(op1,op2));
                             break;
                 }
        }
    }
    res=pop();
    printf("Result:%d",res);
 }



 5.b  #include<stdio.h>
#include<stdlib.h>
void towerOfHanoi(int n,char fromTower,char toTower,char auxTower){
    if(n==1){
        printf("\nMove disc 1 from tower %c to tower %c\n",fromTower,toTower);
        return;
    }
    towerOfHanoi(n-1,fromTower,auxTower,toTower);
    printf("\nMove disc %d from tower %c to tower %c\n",n,fromTower,toTower);
    towerOfHanoi(n-1,auxTower,toTower,fromTower);
}
int main(){
    int n;
    printf("\nEnter the no. of disks\n");
    scanf("%d",&n);
    printf("\nThe steps to be performed\n");
    towerOfHanoi(n,'a','c','b');
}




6.#include<stdio.h>
#include<stdlib.h>
#define MAX 5
char q[MAX];
int f=0,r=0;
void insert(){
    char e;
    if((r+1)%MAX==f){
        printf("\nQueue Overflow\n");
        return;
    }
    printf("\nEnter element to be inserted\n");
    scanf("\n%c",&e);//Very important line
    r=(r+1)%MAX;
    q[r]=e;
}
void delete(){
    if(f==r){
        printf("\nQueue Underflow\n");
        return;
    }
    f=(f+1)%MAX;
    printf("\nThe element being dequeued is %c\n",q[f]);
}
void display(){
    if(f==r){
        printf("\nEmpty Queue\n");
        return;
    }
    int i=f;
    printf("\nThe elements of the queue are:\n");
    while(i!=r){
        i=(i+1)%MAX;
        printf("%c ",q[i]);
    }
}
int main(){
    int ch;
    printf("\nMENU\n1.Insert\n2.Delete\n3.Display\n4.Exit\n");
    while(1){
        printf("\nEnter your choice\n");
        scanf("%d",&ch);
        switch(ch){
            case 1: insert();
                    break;
            case 2: delete();
                    break;
            case 3: display();
                    break;
            case 4: exit(0);
        }
    }
}


7.#include <stdio.h>
#include <stdlib.h>

struct node
{
    struct node *link;
    char name[25], usn[15], programme[10];
    int sem;
    int ph_no;
} *newnode, *head = NULL, *temp, *tail,*prev;

void create(){
    newnode = (struct node *)malloc(sizeof(struct node));
    newnode->link = NULL;
    printf("\nEnter Name:");
    scanf("%s", newnode->name);
    printf("Enter USN:");
    scanf("%s", newnode->usn);
    printf("Enter Programme:");
    scanf("%s", newnode->programme);
    printf("Enter Sem:");
    scanf("%d", &newnode->sem);
    printf("Enter Phone Number:");
    scanf("%d", &newnode->ph_no);
  if (head == NULL){    
      tail = temp = head = newnode;
    }
  else{
      temp->link = newnode;
      temp=temp->link;
    }
}

int insertfront(){
	
    newnode = (struct node *)malloc(sizeof(struct node));
    newnode->link = NULL;
    printf("\nEnter Name:");
    scanf("%s", newnode->name);
    printf("Enter USN:");
    scanf("%s", newnode->usn);
    printf("Enter Programme:");
    scanf("%s", newnode->programme);
    printf("Enter Sem:");
    scanf("%d", &newnode->sem);
    printf("Enter Phone Number:");
    scanf("%d", &newnode->ph_no);
      newnode->link = head;
      head = newnode;
}
int delfront(){
    temp = head;
    head = temp->link;
    free(temp);
}
int insertend(){
    newnode = (struct node *)malloc(sizeof(struct node));
    printf("\nEnter Name:");
    scanf("%s", newnode->name);
    printf("Enter USN:");
    scanf("%s", newnode->usn);
    printf("Enter Programme:");
    scanf("%s", newnode->programme);
    printf("Enter Sem:");
    scanf("%d", &newnode->sem);
    printf("Enter Phone Number:");
    scanf("%d", &newnode->ph_no);
    temp=head;
    while(temp->link!=NULL){
        temp=temp->link;
    }
    temp->link=newnode;
    newnode->link=NULL;
}

int delend(){
    temp = head;
while (temp->link != NULL){
        prev = temp;
        temp = temp->link;
}
        prev->link = NULL;
        tail = prev;
        free(temp);
    }
void display(){
    if(head==NULL){
       printf("List is empty");
    }else{
        temp = head;
        
    while (temp != NULL){
  printf("\nDetails of Student\n");
  printf("|Name:%s|Usn:%s|Programme:%s|Sem:%d|Phone Number:%d|", temp->name, temp->usn, temp->programme, temp->sem, temp->ph_no);
        temp = temp->link;
        }
}}
int main(){
   int i, m, ch;
    while (1){
     printf("\nSingle linkedlist for Student details\n\n1.Create\n2.Insert at front\n3.Delete at front\n4.Insert at end\n5.Delete at end\n6.Display\n7.Exit\nEnter your choice:");
     scanf("%d", &ch);
        switch (ch)
    {
        case 1: printf("\nEnter No. of students:");
                scanf("%d", &m);
              for (i=0; i<m;i++){
                     create();
                     }
                   break;
        case 2:insertfront();break;
        case 3:delfront();break;
        case 4:insertend();break;
        case 5:delend();break;
        case 6:display();break;
        case 7:exit(0);
       default:printf("\ninvalid choice\n");break;
      }
   }
}


8.#include<string.h>
#include<stdio.h>
#include<stdlib.h>
struct stud
{
    char ssn[11],name[15],desg[15],phno[11],dept[15];
    float sal;
    struct stud *next,*prev;
}*f=NULL,*r=NULL,*t=NULL;
void ins(int ch)
{
    t=(struct stud*)malloc(sizeof(struct stud));
    printf("\nEnter SSN:");
    scanf("%s",t->ssn);
    printf("Enter Name:");
    scanf("%s",t->name);
    printf("Enter Dept:");
    scanf("%s",t->dept);
    printf("Enter desg:");
    scanf("%s",t->desg);
    printf("Enter Phno:");
    scanf("%s",t->phno);
    printf("Enter salary:");
    scanf("%f",&t->sal);
    t->next=t->prev=NULL;
    if(!r)
        f=r=t;
    else
    {
        if(ch)
        {
            r->next=t;
            t->prev=r;
            r=t;
        }
        else
        {
            t->next=f;
            f->prev=t;
            f=t;
        }
    }
}
void del(int ch)
{
    if(!f)
        printf("\nList Empty");
    else
    {
        struct stud *t1;
        if(f==r)
        {
            t1=f;
            f=r=NULL;
        }
        else if(ch)
        {
            t1=r;
            r=r->prev;
            r->next=NULL;
        }
        else
        {
            t1=f;
            f=f->next;
            f->prev=NULL;
        }
        printf("\nElement deleted is:\n");
        printf("\nSSN:%s\nName:%s\nDept:%s\nDesg:%s\nPhno:%s\nSalary:%f\n",t1->ssn,t1->name,t1->dept,t1->desg,t1->phno,t1->sal);
        free(t1);
    }
}
void disp()
{
    if(!f)
        printf("\nList Empty!!!");
    else
        printf("\nList elements are:\n");
    for(t=f;t;t=t->next)
       printf("\nSSN:%s\nName:%s\nDept:%s\nDesg:%s\nPhno:%s\nSalary:%f\n",t->ssn,t->name,t->dept,t->desg,t->phno,t->sal);
}
void main()
{
    
    while(1)
    {
        int ch,n,i;
    printf("\n........Menu..........,\n");
    printf("1.Create\n");
    printf("2.Display\n");
    printf("3.Insert at end\n");
    printf("4.Delete at end\n");
    printf("5.Insert at beg\n");
    printf("6.Delete at beg\n");
    printf("7.Exit\n");
        printf("\nEnter choice:");
        scanf("%d",&ch);
        switch(ch)
        {
            case 1: printf("\nEnter no. of nodes:");
                    scanf("%d",&n);
                    for(i=0;i<n;i++)
                        ins(0);
                    break;
            case 2:disp();break;
            case 3:ins(1);break;
            case 4:del(1);break;
            case 5:ins(0);break;
            case 6:del(0);break;
            case 7:exit(0);
            default:printf("\nInvalid choice!!!!");
        }
    }

}



9.#include <stdio.h>
#include <stdlib.h>
#include<math.h>
typedef struct polynomial
{
    float coeff;
    int x,y,z;
    struct polynomial *next;
}poly;
poly *p1,*p2,*p3;
poly* readpoly()
{
    poly *temp=(poly*)malloc(sizeof(poly));
    printf("\nEnter coeff:");
    scanf("%f",&temp->coeff);
    printf("Enter x expon:");
    scanf("%d",&temp->x);
    printf("Enter y expon:");
    scanf("%d",&temp->y);
    printf("Enter z expon:");
    scanf("%d",&temp->z);
    return temp;
}
poly* create()
{
    int n,i;
    printf("\nEnter no. of terms:");
    scanf("%d",&n);
    poly *temp=(poly*)malloc(sizeof(poly)),*t1=temp;
    for(i=0;i<n;i++,t1=t1->next)
      t1->next=readpoly();
    t1->next=temp;
    return temp;
}
void evaluate()
{
    float sum=0;
    int x,y,z;
    poly *t=p1->next;
    printf("\nEnter x,y&z:\n");
    scanf("%d",&x);
    scanf("%d",&y);
    scanf("%d",&z);
    while(t!=p1)
    {
      sum+=t->coeff*pow(x,t->x)*pow(y,t->y)*pow(z,t->z);
      t=t->next;
    }
    printf("\nSum=%f",sum);
}
void display(poly *p)
{
    poly *t=p->next;
    while(t!=p)
    {
      if(t!=p->next&&t->coeff>0)
        putchar('+');
      printf("%.1fx^%dy^%dz^%d",t->coeff,t->x,t->y,t->z);
      t=t->next;
    }
}
poly* attach(float coeff,int x,int y,int z,poly *p)
{
    poly *t=(poly*)malloc(sizeof(poly));
    t->coeff=coeff;
    t->x=x;
    t->y=y;
    t->z=z;
    p->next=t;
    return t;
}
poly* add()
{
    printf("\nPolynomial1:\n");
    p1=create();
    printf("\nPolynomial2:\n");
    p2=create();
    int flag;
    poly *t1=p1->next,*t2=p2->next,*t3;
    p3=(poly*)malloc(sizeof(poly));
    t3=p3;
    while(t1!=p1&&t2!=p2)
    {
        if(t1->x>t2->x)
          flag=1;
        else if(t1->y<t2->y)
          flag=-1;
        else if(t1->z==t2->z)
          flag=0;
        switch(flag)
        {
            case 0:t3=attach(t1->coeff+t2->coeff,t1->x,t1->y,t1->z,t3);
                   t1=t1->next;
                   t2=t2->next;
                   break;
            case 1:t3=attach(t1->coeff,t1->x,t1->y,t1->z,t3);
                   t1=t1->next;
                   break;
            case -1:t3=attach(t2->coeff,t2->x,t2->y,t2->z,t3);
                    t2=t2->next;
                    break;
        }
    }
    for(;t1!=p1;t1=t1->next)
        t3=attach(t1->coeff,t1->x,t1->y,t1->z,t3);
    for(;t2!=p2;t2=t2->next)
        t3=attach(t2->coeff,t2->x,t2->y,t2->z,t3);
    t3->next=p3;
    return p3;
}
int main()
{
   int ch;
   printf("\n1.Represent and evaluate polynomial\n2.Add 2 polynomials\n3.Exit\nEnter choice:");
   scanf("%d",&ch);
   switch(ch)
   {
       case 1:p1=create();
              display(p1);
              evaluate();
              break;
       case 2:p3=add();
              printf("\nPolynomial1:\n");
              display(p1);
              printf("\nPolynomial2:\n");
              display(p2);
              printf("\nP1+P2:\n");
              display(p3);
              break;
       case 3:exit(0);
       default:printf("\nInvalid choice...!");
   }
    return 0;

}




10.#include<stdio.h>
#include<stdlib.h>
typedef struct tree* treeptr;
typedef struct tree{
    int data;
    treeptr llink;
    treeptr rlink;
}tree;
int f=0;
void inOrder(treeptr root){
    if(root){
        inOrder(root->llink);
        printf("%d ",root->data);
        inOrder(root->rlink);
    }
}
void preOrder(treeptr root){
    if(root){
        printf("%d ",root->data);
        preOrder(root->llink);
        preOrder(root->rlink);
    }
}
void postOrder(treeptr root){
    if(root){
        postOrder(root->llink);
        postOrder(root->rlink);
        printf("%d ",root->data);
    }
}
void search(treeptr root,int data){
    if(root){
        if(data<root->data)
            search(root->llink,data);
        else if(data>root->data)
            search(root->rlink,data);
        else{
            f=1;
            return;
        }
    }
}
treeptr newNode(int data){
    treeptr temp=(treeptr)malloc(sizeof(*temp));
    temp->data=data;
    temp->llink=temp->rlink=NULL;
    return temp;
}
treeptr insert(treeptr root,int data){
    if(!root)
        return newNode(data);
    if(data<root->data)
        root->llink=insert(root->llink,data);
    if(data>root->data)
        root->rlink=insert(root->rlink,data);
    return root;
}
treeptr findMin(treeptr root){
    while(root->llink!=NULL)
        root=root->llink;
    return root;
}
treeptr delete(treeptr root,int data){
    if(!root)
        return NULL;
    if(root->data==data){
        if((!root->llink)&&(!root->rlink))
            return NULL;
        else if(root->llink&&!root->rlink)
            return root->llink;
        else if(root->rlink&&!root->llink)
            return root->rlink;
        else{
            int min=findMin(root->rlink)->data;
            root->data=min;
            root->rlink=delete(root->rlink,min);
        }
    }
    else if(data<root->data)
        root->llink=delete(root->llink,data);
    else
        root->rlink=delete(root->rlink,data);
    return root;
}
int main(){
    treeptr root=NULL;
    int a[]={6,9,5,2,8,15,24,14,7,8,5,2};
    int i,n,ch;
    for(i=0;i<12;i++)
        root=insert(root,a[i]);
    printf("\nMENU:\n1.Inorder\n2.PreOrder\n3.PostOrder\n4.Search\n5.Delete\n6.Exit");
    while(1){
        printf("\nEnter your choice:\n");
        scanf("%d",&ch);
        switch(ch){
            case 1: inOrder(root);
                    break;
            case 2: preOrder(root);
                    break;
            case 3: postOrder(root);
                    break;
            case 4: printf("\nEnter element to be searched:\n");
                    scanf("%d",&n);
                    search(root,n);
                    if(f==0)
                        printf("\nElement not found\n");
                    else
                        printf("\nElement found\n");
                    break;
            case 5: printf("\nEnter element to be deleted\n");
                    scanf("%d",&n);
                    root=delete(root,n);
                    break;
            case 6: exit(0);
        }
    }
}




11.  #include <stdio.h>
#include <stdlib.h>
int a[20][20],q[20],visited[20],reach[20],n,f=0,r=-1,count=0;
void bfs(int v)
{
    int i;
    for(i=1;i<=n;i++)
      if(a[v][i]&&!visited[i])
      {
        visited[i]=1;
        q[++r]=i;
      }
      if(f<=r)
        bfs(q[f++]);
}
void dfs(int v)
{
    int i;
    reach[v]=1;
    for(i=1;i<=n;i++)
      if(a[v][i]&&!reach[i])
      {
        printf("%d->%d\n",v,i);
        count++;
        dfs(i);
      }
}
int main()
{
    int v,ch,i,j;
    printf("\nenter no. of vertices:");
    scanf("%d",&n);
    for(i=1;i<=n;i++)
      reach[i]=visited[i]=q[i]=0;
    printf("\nEnter graph data in matrix form:\n");
    for(i=1;i<=n;i++)
      for(j=1;j<=n;j++)
        scanf("%d",&a[i][j]);
    printf("\n1.BFS\n2.DFS\n3.Exit\nEnter choice:");
    scanf("%d",&ch);
    switch(ch)
    {
        case 1:printf("\nEnter vertex:");
               scanf("%d",&v);
               bfs(v);
               printf("\nThe nodes that are reacheble from %d are:\n",v);
               for(i=1;i<=n;i++)
                  if(visited[i])
                    printf("%d ",i);
               break;
        case 2:dfs(1);
               if(count==n-1)
                  printf("\ngraph is connected");
               else
                  printf("\ngraph is not connected");
               break;
        case 3:exit(0);
        default:printf("\nInvalid choice");
    }
    return 0;

}




     
   12.  #include<stdio.h>
#include<stdlib.h>

int key[20],n,m;
int *ht,index;
int count = 0;

void insert(int key)
{
            index = key % m;
            while(ht[index] != -1)
            {
                         index = (index+1)%m;
            }
            ht[index] = key;
            count++;
 }

void display()
{
           int i;
           if(count == 0)
          {
                         printf("\nHash Table is empty");
                         return;
           }

           printf("\nHash Table contents are:\n ");
           for(i=0; i<m; i++)
                      printf("\n T[%d] --> %d ", i, ht[i]);
}


void main()
{
         int i;
         printf("\nEnter the number of employee  records (N) :   ");
         scanf("%d", &n);

         printf("\nEnter the two digit memory locations (m) for hash table:   ");
         scanf("%d", &m);

         ht = (int *)malloc(m*sizeof(int));
         for(i=0; i<m; i++)
                     ht[i] = -1;

         printf("\nEnter the four digit key values (K) for N Employee Records:\n  ");
         for(i=0; i<n; i++)
                    scanf("%d", &key[i]);

         for(i=0;i<n;i++)
        {
                   if(count == m)
                   {
                        printf("\n~~~Hash table is full. Cannot insert the record %d key~~~",i+1);
                        break;
                   }
                   insert(key[i]);
    }

            //Displaying Keys inserted into hash table
             display();
}
