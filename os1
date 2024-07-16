#include <stdio.h>
int n, i, j, pos, temp, choice, total = 0;
int Burst_time[20], Arrival_time[20], Waiting_time[20], Turn_around_time[20], process[20];
float avg_Turn_around_time = 0, avg_Waiting_time = 0;

void FCFS()
{
    int total_waiting_time = 0, total_turnaround_time = 0;
    int current_time = 0;

    for (i = 0; i < n - 1; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if (Arrival_time[i] > Arrival_time[j])
            {
                temp = Arrival_time[i];
                Arrival_time[i] = Arrival_time[j];
                Arrival_time[j] = temp;

                temp = Burst_time[i];
                Burst_time[i] = Burst_time[j];
                Burst_time[j] = temp;

                temp = process[i];
                process[i] = process[j];
                process[j] = temp;
            }
        }
    }

    Waiting_time[0] = 0;
    current_time = Arrival_time[0] + Burst_time[0];

    for (i = 1; i < n; i++)
    {
        if (current_time < Arrival_time[i])
        {
            current_time = Arrival_time[i];
        }
        Waiting_time[i] = current_time - Arrival_time[i];
        current_time += Burst_time[i];
        total_waiting_time += Waiting_time[i];
    }

    printf("\nProcess\t\tArrival Time\tBurst Time\tWaiting Time\tTurnaround Time");
    for (i = 0; i < n; i++)
    {
        Turn_around_time[i] = Burst_time[i] + Waiting_time[i];
        total_turnaround_time += Turn_around_time[i];
        printf("\nP[%d]\t\t%d\t\t%d\t\t%d\t\t%d", process[i], Arrival_time[i], Burst_time[i], Waiting_time[i], Turn_around_time[i]);
    }

    avg_Waiting_time = (float)total_waiting_time / n;
    avg_Turn_around_time = (float)total_turnaround_time / n;
    printf("\nAverage Waiting Time: %.2f", avg_Waiting_time);
    printf("\nAverage Turnaround Time: %.2f\n", avg_Turn_around_time);
}

void SJF()
{
    int total_waiting_time = 0, total_turnaround_time = 0;
    int completed = 0, current_time = 0, min_index;
    int is_completed[20] = {0};

    while (completed != n)
    {
        int min_burst_time = 9999;
        min_index = -1;

        for (i = 0; i < n; i++)
        {
            if (Arrival_time[i] <= current_time && is_completed[i] == 0)
            {
                if (Burst_time[i] < min_burst_time)
                {
                    min_burst_time = Burst_time[i];
                    min_index = i;
                }
                if (Burst_time[i] == min_burst_time)
                {
                    if (Arrival_time[i] < Arrival_time[min_index])
                    {
                        min_burst_time = Burst_time[i];
                        min_index = i;
                    }
                }
            }
        }

        if (min_index != -1)
        {
            Waiting_time[min_index] = current_time - Arrival_time[min_index];
            current_time += Burst_time[min_index];
            Turn_around_time[min_index] = current_time - Arrival_time[min_index];
            total_waiting_time += Waiting_time[min_index];
            total_turnaround_time += Turn_around_time[min_index];
            is_completed[min_index] = 1;
            completed++;
        }
        else
        {
            current_time++;
        }
    }

    printf("\nProcess\t\tArrival Time\tBurst Time\tWaiting Time\tTurnaround Time");
    for (i = 0; i < n; i++)
    {
        printf("\nP[%d]\t\t%d\t\t%d\t\t%d\t\t%d", process[i], Arrival_time[i], Burst_time[i], Waiting_time[i], Turn_around_time[i]);
    }

    avg_Waiting_time = (float)total_waiting_time / n;
    avg_Turn_around_time = (float)total_turnaround_time / n;
    printf("\n\nAverage Waiting Time = %.2f", avg_Waiting_time);
    printf("\nAverage Turnaround Time = %.2f\n", avg_Turn_around_time);
}

int main()
{
    printf("Enter the total number of processes: ");
    scanf("%d", &n);
    printf("\nEnter Arrival Time and Burst Time:\n");
    for (i = 0; i < n; i++)
    {
        printf("P[%d] Arrival Time: ", i + 1);
        scanf("%d", &Arrival_time[i]);
        printf("P[%d] Burst Time: ", i + 1);
        scanf("%d", &Burst_time[i]);
        process[i] = i + 1;
    }
    while (1)
    {
        printf("\n-----MAIN MENU-----\n");
        printf("1. FCFS Scheduling\n2. SJF Scheduling\n");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);
        switch (choice)
        {
        case 1:
            FCFS();
            break;
        case 2:
            SJF();
            break;
        default:
            printf("Invalid Input!!!\n");
        }
    }
    return 0;
}
