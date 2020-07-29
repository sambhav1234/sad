# sad
c programme
#include <stdio.h>
#include <stdlib.h>

struct element{
int i;
int j;
int x;


};

struct sparse{
int n;
int m;
int num;

struct element *ele;


};


void create(struct sparse *s)
{
    printf("enter dimension of ");
    scanf("%d %d",&s->m,&s->n);
    printf("enter no. of non zero");
    scanf("%d",&s->num);
    s->ele=(struct element *)malloc(s->num*sizeof(struct element));

    for(int i=0;i<s->num;i++)
    {

        scanf("%d %d %d",&s->ele[i].i,&s->ele[i].j,&s->ele[i].x);
    }



}

struct sparse * add(struct sparse *s1,struct sparse *s2)
{
    struct sparse *sum;
    if(s1->m!=s2->m&&s1->n!=s2->n)
        return 0;
sum=(struct sparse *)malloc(sizeof(struct sparse));
    sum->ele=(struct element*)malloc((s1->num+s2->num)*sizeof(struct element));

    int i=0;
    int j=0;
    int k=0;
    while(i<s1->num&&j<s2->num)
    {


        if(s1->ele[i].i<s2->ele[j].i)
            sum->ele[k++]=s1->ele[i++];
        else if(s1->ele[i].i>s2->ele[j].i)
            sum->ele[k++]=s2->ele[j++];
        else{

            if(s1->ele[i].j<s2->ele[j].j)
                sum->ele[k++]=s1->ele[i++];
            else if(s1->ele[i].j>s2->ele[j].j)
                sum->ele[k++]=s2->ele[j++];
            else{
                sum->ele[k].i=s1->ele[i].i;
                sum->ele[k].j=s1->ele[i].j;
                sum->ele[k++].x=s1->ele[i++].x+s2->ele[j++].x;
            }
        }
    }
    for(;i<s1->num;i++)sum->ele[k++]=s1->ele[i++];

    for(;j<s2->num;j++)sum->ele[k++]=s2->ele[j++];

    sum->m=s1->m;
    sum->n=s1->n;
    sum->num=k;

    return sum;


}

void display(struct sparse s)
{
    int k=0;
    for(int i=0;i<s.m;i++)
    {
        for(int j=0;j<s.n;j++)
        {
            if(i==s.ele[k].i&&j==s.ele[k].j)
                printf("%d ",s.ele[k++].x);
            else printf("0 ");
        }
        printf("\n");

    }

}


int main()
{
struct sparse s1,s2,*s3;

 create(&s1);
 create(&s2);



 printf("First Matrix\n");
 display(s1);
 printf("Second Matrix\n");
 display(s2);
  s3=add(&s1,&s2);
 printf("Sum Matrix");
 display(*s3);
}
