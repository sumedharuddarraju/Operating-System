//  Write a C program to implement  Round Robin Scheduling Algorithm.

#include <stdio.h>
#include <stdbool.h>
int main()
{
    int i,j,n;
    printf("Enter no of processes : ");
    scanf("%d",&n);
    int bt[n],wt[n],tt[n],tq;
    int sum_wt=0,sum_tt=0;
    float awt=0.0,att=0.0;
    printf("Enter the burst times : ");
    for(i=0;i<n;i++)
    {
        scanf("%d",&bt[i]);
    }
    printf("Enter the time quantum : ");
    scanf("%d",&tq);
    
    int rem_bt[n];
    for(i=0;i<n;i++)
    {
        rem_bt[i]=bt[i];
    }
    
    int t=0;
    while(1)
    {
        bool done = true;
        for(i=0;i<n;i++)
        {
            if(rem_bt[i]>0)
            {
                done=false;
            
                if(rem_bt[i]>tq)
                {
                    t=t+tq;
                    rem_bt[i]=rem_bt[i]-tq;
                }
                else
                {
                    t=t+rem_bt[i];
                    wt[i]=t-bt[i];
                    rem_bt[i]=0;
                }
            }
        }
        if(done==true)
        {
            break;
        }
    }
    for(i=0;i<n;i++)
    {
        tt[i]=wt[i]+bt[i];
    }
    for(i=0;i<n;i++)
    {
        sum_wt+=wt[i];
    }
     for(i=0;i<n;i++)
    {
        sum_tt+=tt[i];
    }
    awt=(float)sum_wt/n;
    att=(float)sum_tt/n;
    printf("Process\tBurst time\tWaiting time\tTurn around time\n");
    for(i=0;i<n;i++)
    {
        printf("P[%d]\t\t%d\t\t%d\t\t%d\n",i+1,bt[i],wt[i],tt[i]);
    }
    printf("Average waiting time: %0.2fms\n", awt);
    printf("Average turnaround time: %0.2fms\n", att);
    
    return 0;
}

