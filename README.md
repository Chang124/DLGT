#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <conio.h>
#include <ctype.h>

typedef struct list add;

struct list {
    char name[40];
    char num[20];
    char gmail[40];
    int cf[1];
    add* next;
};

int i=1,size=0;

void Insert(add** head) { //ch=1
FILE *fptr;
fptr = fopen("finalnhap.txt", "w");
    add* temp=(add*)malloc(sizeof(add));
    printf("\n\n\n\t\tContact Name: ");
    gets(temp->name);
    system("cls");
    printf("\n\n\n\t\tContact Name: ");
    gets(temp->name);
    system("cls");
    printf("\n\n\n\t\t\tMobile Number: ");
    gets(temp->num);
    system("cls");
    printf("\n\n\n\t\t\tGmail ID: ");
    gets(temp->gmail);
    system("cls");
    printf("\n\n\n\t\tClose friend(1.yes/2.no): ");
    gets(temp->cf);
    system("cls");
    temp->next = NULL;
    size++;
//    if(size == 5) {
//        system("cls");
//        printf("\n\n\n\t\t\tPhone Memory is full!!!");
//        printf("\n\t\tIf you want to add more contact,You have to delete some contact from your list...\n\n\n");
//        return;
//    } else {
        if(*head == NULL) {
            *head = temp;
            system("cls");
            printf("\n\n\t\t\t\t\tDone!!!\n\n");
            return;
        } else {
            add* p = *head; 
            while(p->next != NULL) {
                p = p->next;
            }
            p->next = temp;
            system("cls");
            printf("\n\t\t\t\t\tDone!!!\n\n");
        }
        fclose(fptr);
        return;
    }

void Delete(add** head) { //ch=2
FILE *fptr;
fptr = fopen("finalnhap.txt", "a");
    char ch[40];
    printf("\n\t\tContact name : ");
    gets(ch);
    system("cls");
    printf("\n\t\tContact name : ");
    gets(ch);
    system("cls");
    
    if(*head == NULL) {
        system("cls");
        printf("\n\t\t\t\t\tNo Contact exists in this Phone Book List!\n\n");
        return;
    } else {
        if(strcmp(((*head)->name),ch) == 0) {
            add*p=*head;
            *head = (*head)->next;
            free(p);
            printf("\n\t\t\t\t\tDone!!!\n\n\n\n");
            return;
        } else {
            add*p = *head;
            while(p->next != NULL) {
                if(strcmp((p->next->name),ch) == 0) {
                    p->next = p->next->next;
                    size--;
                    return;
                }
                p = p->next;
            }
            system("cls");
            printf("\n\t\t\t\t\tInvalid Contact!!!\n\n");
fclose(fptr);

        }
    }
}

void Display(add* head) { //ch=3
FILE *fptr;
fptr = fopen("finalnhap.txt", "r");

    if(head == NULL) {
        system("cls");
        printf("\n\n\n\t\tNo Contact exists in this Phone Book List!");
        return;

    } else {
        add*p = head;
        while(p != NULL) {
            printf("\n\t\t\t\t%d.%c%s",i,32,p->name);
            printf("\n\t\t\t-------------------------");
            printf("\n\t\t\tNumber : %s",p->num);
            printf("\n\t\t\tGmail ID : %s",p->gmail);
            printf("\n\t\t\tClose friend : %s",p->cf);

        
        }
            p = p->next;
            i++;
        }
    i=1;
    return;
        fclose(fptr);
    }

void Search(add*head) { //ch=4
FILE *fptr;
fptr = fopen("finalnhap.txt", "r");
    char ch[40];
    printf("\n\n\n\t\tContact name : ");
    gets(ch);
    system("cls");
    printf("\n\n\n\t\tContact name : ");
    gets(ch);
    system("cls");
    if(head == NULL) {
        system("cls");
        printf("\n\n\n\t\tNo Contact exists in this Phone Book List!!!\n\n");
        return;
    } else {
        add*p = head;
        while(p != NULL) {
            if(strcmp((p->name),ch) == 0) {
                system("cls");
                printf("\n\t\t\t%s",p->name);
                printf("\n\t\t-------------------------");
                printf("\n\t\tNumber : %s",p->num);
                printf("\n\t\tGmail ID : %s",p->gmail);
                printf("\n\t\tClose friend(1.yes/2.no) : %s\n\n",p->cf);
                return;
            }
            p = p->next;
        }
        system("cls");
        printf("\n\n\n\t\tThis Contact is not exists in the list!");
fclose(fptr);

    }
}

int main() {
    add* head=NULL;
    char c[40];
    //             mainhome:
    //             system("cls");
    //             printf("\n\t\t|!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!|");
    //             printf("\n\t\t|                  !!!!!!!!!!!!!!!!!!!!!!!!!!!!                 |");
    //             printf("\n\t\t|!!!!!!!!!!!!!!!!!!! WELCOME TO OUR PHONE BOOK !!!!!!!!!!!!!!!!!|");
    //             printf("\n\t\t|                  !!!!!!!!!!!!!!!!!!!!!!!!!!!!                 |");
    //             printf("\n\t\t|!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!|\n\n\n");

    while(1) {
        printf("\n\n\t\t\t\t\t\tMenu");
        printf("\n\t\t\t-------------------------------------------------");
        printf("\n\t\t\t1)Create A Contact\t\t2)Remove A Contact");
        printf("\n\t\t\t3)Show The Contact List\t\t4)Find A Contact");
        printf("\n\t\t\t-1)Quit");
        printf("\n\t\t\t");
        int ch;
        scanf("%d",&ch);
        if(ch == -1) {
            break;
        } else {
             switch(ch) {
                case 1: system("cls"); //Insert Function
                        Insert(&head);
                        break;

                case 2: system("cls"); //Delete Funtion
                        Delete(&head);
                        break;

                case 3: system("cls"); //Display Funtion
                        Display(head);
                        break;

                case 4: system("cls"); // Search Function
                        Search(head);
                        break;

                default: printf("\n\t\tInvalid Choice!Try again!!!"); //Incorrect choice
                         break;
            }
        }
    }
}
