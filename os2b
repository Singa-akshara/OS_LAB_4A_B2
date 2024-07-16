#include <stdio.h>
#include <stdbool.h>

void findTurnaroundTime(int processes[], int n, int bt[], int wt[], int tat[]) {
    for (int i = 0; i < n; i++) {
        tat[i] = bt[i] + wt[i];
    }
}

void findWaitingTime(int processes[], int n, int bt[], int wt[], int quantum) {
    int rem_bt[n];
    for (int i = 0; i < n; i++) {
        rem_bt[i] = bt[i];
    }
    int t = 0;

    while (1) {
        bool done = true;
        for (int i = 0; i < n; i++) {
            if (rem_bt[i] > 0) {
                done = false;
                if (rem_bt[i] > quantum) {
                    t += quantum;
                    rem_bt[i] -= quantum;
                } else {
                    t += rem_bt[i];
                    wt[i] = t - bt[i];
                    rem_bt[i] = 0;
                }
            }
        }
        if (done == true)
            break;
    }
}

void findAvgTime(int processes[], int n, int bt[], int quantum) {
    int wt[n], tat[n], total_wt = 0, total_tat = 0;

    findWaitingTime(processes, n, bt, wt, quantum);
    findTurnaroundTime(processes, n, bt, wt, tat);

    printf("\nProcess ID\tBurst Time\tWaiting Time\tTurnaround Time\n");

    for (int i = 0; i < n; i++) {
        total_wt += wt[i];
        total_tat += tat[i];
        printf("%d\t\t%d\t\t%d\t\t%d\n", processes[i], bt[i], wt[i], tat[i]);
    }

    printf("\nAverage waiting time = %f", (float)total_wt / n);
    printf("\nAverage turnaround time = %f\n", (float)total_tat / n);
}

int main() {
    int n, quantum;

    printf("Enter the Number of Processes: ");
    scanf("%d", &n);

    int processes[n], burst_time[n];

    printf("\nEnter the quantum time: ");
    scanf("%d", &quantum);

    for (int i = 0; i < n; i++) {
        printf("\nEnter the process ID: ");
        scanf("%d", &processes[i]);
        printf("Enter the Burst Time: ");
        scanf("%d", &burst_time[i]);
    }

    findAvgTime(processes, n, burst_time, quantum);
    return 0;
}
