# polynomials-using-arrays
#include<stdio.h>
#include<stdlib.h>
struct polynomial
{
    int highpow;
    int coef[100];
};
typedef struct  polynomial poly;
poly* create()
{
    poly *p;
    int i;
    p=(poly*)malloc(sizeof(poly));
    printf("enter high power of the polynomial:");
    scanf("%d",&p->highpow);
    for (i=p->highpow;i>=0;i--)
    {
        printf("enter coef of %d:",i);
        scanf("%d",&p->coef[i]);
    }
    return p;
}
poly* add(poly *p1,poly *p2)
{
    poly *p3;
    int i;
    p3=(poly*)malloc(sizeof(poly));
    p3->highpow=max(p1->highpow,p2->highpow);
    for (i=p3->highpow;i>=0;i--)
    {
        p3->coef[i]=p1->coef[i]+p2->coef[i];
    }
    return p3;
}
poly* multiply(poly *p1,poly *p2)
{
    poly  *p3;
    int i,j;
    p3=(poly*)malloc(sizeof(poly));
    p3->highpow=p1->highpow+p2->highpow;
    for (i=p1->highpow;i>=0;i--)
    {
        for(j=p2->highpow;j>=0;j--)
        {
            p3->coef[i+j]=p3->coef[i+j]+p1->coef[i]*p2->coef[j];
        }
    }
    return p3;
}
int max(int x,int y)
{
    return (x>y?x:y);
}
void display(poly *p)
{
   int i;
   for (i=p->highpow;i>=0;i--)
   {
       printf("%d x^%d +",p->coef[i],i);
   }

}
void main()
{

    int k;
    poly *p1,*p2,*p;
    p1=create();
    p2=create();
    while(1)
    {
     printf("enter k value:");
     scanf("%d",&k);
     switch(k)
     {

        case 1:p=add(p1,p2);
               break;
        case 2:p=multiply(p1,p2);
               break;
        case 3:display(p);
               break;
        case 4:exit(0);
     }
}
}
