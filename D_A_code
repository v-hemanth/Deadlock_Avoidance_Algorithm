#include <stdio.h>

int max_resource(int *array[10], int size,int restricted_index) {
    int index = 0,i;
    if (restricted_index == 0)
        index = 1;
        for(i = 0; i < size; ++i) {
            if ((*(array[index]) < *(array[i]) ) && i!=restricted_index)
                index = i;
        }
    return index;
}




int compare(int work[6], int need[6], int no_of_resources) {
    int flag = 0,i;
    for ( i = 0; i < no_of_resources; ++i) {

        if (work[i] < need[i]) {
            ++flag;
        }
    }
    return flag;
}


int adding_resource(int work[6],int allocation[6],int need[6],int no_of_resources) {
    int i;
    for (i = 0; i < no_of_resources; ++i) {
            work[i] += allocation[i];
            need[i] += allocation[i];
            allocation[i] = 0;
    }
}



void extra_resources(int work[6], int need[6], int no_of_resources, int flag[6]) {
    int j,i;

    for (j = 0; j < no_of_resources; ++j) {
            flag[j] = 0;
    }
    for (i = 0; i < no_of_resources; ++i) {
        if (work[i] < need[i]) {
            flag[i] = 1;
        }
    }
}



int main() {
    int	allocation[10][6],	maximum[10][6], need[10][6],work[6],allocated_processes[10],safe_sequence[10], total_resources[6],m,i1,i;

    for (m = 0; m < 10; ++m) {
        allocated_processes[m] = 0;
        safe_sequence[m] = 0;
    }


    for (i1 = 0; i1 < 6; ++i1) {
            total_resources[i1] = 0;
    }
    int no_of_processes, no_of_resources;
    int *resources[6][10],j;
    printf("Enter The Number Of Processes(<=10) : ");
    scanf("%d", &no_of_processes);
    printf("Enter	The	Number	Of	Resources(<=6)	:	");
    scanf("%d", &no_of_resources);
    printf("Enter The Allocation Matrix : \n");
    for (i = 0; i < no_of_processes; i++) {
        for (j = 0; j < no_of_resources; j++) {
            scanf("%d",	&allocation[i][j]);
            total_resources[j] += allocation[i][j];
        }
}

printf("Enter The Maximum Matrix : \n");
for (i = 0; i < no_of_processes; i++) {
    for(j = 0; j < no_of_resources; j++) {
        scanf("%d", &maximum[i][j]);
    }
}

printf("Enter Work Matrix(The Resources Left) : ");
int l;
for (l = 0; l < no_of_resources; ++l) {
    scanf("%d",&work[l]);
    total_resources[l] += work[l];
}

printf("The Need Matrix is : \n");
for (i = 0; i < no_of_processes; i++) {
    for ( j = 0; j < no_of_resources; j++) {
        need[i][j] = maximum[i][j] - allocation[i][j];
        printf("%d ",need[i][j]);
    }
    printf("\n");
}

int k;
for ( k = 0; k < no_of_resources; ++k) {
    for (i = 0; i < no_of_processes; ++i) {
        resources[k][i] = &allocation[i][k];
    }
}

int current_total_resource[6],z=0,safe_state = 1,unsafe_process=-1,j1;
for (j1 = 0; j1 < no_of_processes; ++j1) {
    z = 0;
    while(z < no_of_resources){
        current_total_resource[z] = total_resources[z] - allocation[j1][z];
        z++;
    }

    if(compare(current_total_resource,need[j1],no_of_resources)!=0) {
    safe_state = 0;
    unsafe_process = j1;
    break;
    }
}

i = 0;
int process_executed = 0;
while(1 && safe_state)//If the system is in safe state generate the sequence of executing
{
int current_executions = 0;
if(i==0)
{

    for (j = 0; j < no_of_processes; ++j) {

        if((compare(work,need[j],no_of_resources)==0)&&(allocated_processes[j]==0))
        {
        adding_resource(work,allocation[j],need[j],no_of_resources);
        allocated_processes[j] = 1;
        ++current_executions;
        safe_sequence[process_executed++] = j;
        }
    }
}

else
{

for (j = 0; j < no_of_processes; ++j) {

if((compare(work,need[j],no_of_resources)==i)&&(allocated_processes[j]==0))
{
    int extra_resource[6];       //Array that generates the required resources by the J th Process

    extra_resources(work,need[j],no_of_resources,extra_resource);

    for (k = 0; k < no_of_resources; ++k) {
        if(extra_resource[k]) {
            int	process_no	= max_resource(resources[k],no_of_processes,j);
            printf("ProcessNo[%d] Preempted\n",process_no);
            adding_resource(work,allocation[process_no],need[process_no], no_of_resources);
            ++current_executions;
             i = 0;
        }
    }
}
}


if(i!=0)
++i;

if(i==0)
break;

}
//If none of the process executed in the current loop change the value of i to 1
if(current_executions==0 && i==0)
    i=1;
//If all the processes have executed break from the loop if(process_executed==no_of_processes)
break;
//If the system is in a safe state generate the safe sequence
}

if(safe_state)

{
int n;
    for	(n	=	0;	n	<	no_of_processes;	++n)	{
        printf("ProcessNo[%d]->",safe_sequence[n]);
    }
}
else
{
printf("Resources Demanded Exceed Total Available Resources\n System in Unsafe State\n");
printf("Unsafe Process is : %d",unsafe_process);
}

}

