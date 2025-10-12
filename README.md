코드입니다 ⬇️


    #include <stdio.h>
    #include <string.h>
    
    #define MAX_BOOKS 5
    
    struct Book {
        char title[50];
        int iB;
    };
    
    struct User {
        char name[30];
        int hC;
    };
    
    void sM();
    void bB(struct Book books[], int n);
    void rB(struct Book books[], int n);
    void sB(struct Book books[], int n);
    void rcmB();
    void mC(struct User *u);
    
    int main() {
        struct Book books[MAX_BOOKS] = {
            {"해리포터와 마법사의 돌", 0},
            {"데미안", 0},
            {"죄와 벌", 0},
            {"어린 왕자", 0},
            {"토지", 0}
        };

    struct User u = {"", 0};
    int ch;

    while (1) {
        sM();
        printf("번호 선택: ");
        scanf("%d", &ch);
        getchar();

        switch (ch) {
            case 1:
                bB(books, MAX_BOOKS);
                break;
            case 2:
                rB(books, MAX_BOOKS);
                break;
            case 3:
                sB(books, MAX_BOOKS);
                break;
            case 4:
                rcmB();
                break;
            case 5:
                mC(&u);
                break;
            case 0:
                printf("프로그램을 종료합니다.\n");
                return 0;
            default:
                printf("잘못된 입력입니다.\n");
        }
    }
    }
    
    void sM() {
        printf("\n=== 도서관 프로그램 ===\n");
        printf("1. 대출\n");
        printf("2. 반납\n");
        printf("3. 책 목록\n");
        printf("4. 추천 도서\n");
        printf("5. 도서증\n");
        printf("0. 종료\n");
    }
    
    void bB(struct Book books[], int n) {
        int i;
        printf("\n--- 대출 가능한 책 목록 ---\n");
        for (i = 0; i < n; i++) {
            if (!books[i].iB)
                printf("%d. %s\n", i + 1, books[i].title);
        }

    printf("대출할 책 번호 입력: ");
    scanf("%d", &i);

    if (i < 1 || i > n) {
        printf("잘못된 번호입니다.\n");
        return;
    }

    if (books[i - 1].iB) {
        printf("이미 대출 중인 책입니다.\n");
    } else {
        books[i - 1].iB = 1;
        printf("'%s' 책을 대출했습니다. 반납 기간은 1주일입니다.\n", books[i - 1].title);
    }
    }
    
    void rB(struct Book books[], int n) {
        int i;
        printf("\n--- 반납 가능한 책 목록 ---\n");
        for (i = 0; i < n; i++) {
            if (books[i].iB)
                printf("%d. %s\n", i + 1, books[i].title);
        }

    printf("반납할 책 번호 입력: ");
    scanf("%d", &i);

    if (i < 1 || i > n) {
        printf("잘못된 번호입니다.\n");
        return;
    }

    if (!books[i - 1].iB) {
        printf("이 책은 대출되지 않았습니다.\n");
    } else {
        books[i - 1].iB = 0;
        printf("'%s' 책을 반납했습니다.\n", books[i - 1].title);
    }
    }
    
    void sB(struct Book books[], int n) {
        printf("\n--- 전체 책 목록 ---\n");
        for (int i = 0; i < n; i++) {
            printf("%d. %s (%s)\n", i + 1, books[i].title,
                   books[i].iB ? "대출 중" : "대출 가능");
        }
    }
    
    void rcmB() {
        printf("\n오늘의 추천 도서: 『1984』 - 조지 오웰\n");
    }
    
    void mC(struct User *u) {
        if (u->hC == 0) {
            printf("\n도서증이 없습니다. 새로 만드시겠습니까? (y/n): ");
            char c;
            scanf(" %c", &c);
            getchar();
            if (c == 'y' || c == 'Y') {
                printf("이름 입력: ");
                fgets(u->name, sizeof(u->name), stdin);
                u->name[strcspn(u->name, "\n")] = '\0';
                u->hC = 1;
                printf("%s님의 도서증이 발급되었습니다.\n", u->name);
            } else {
                printf("도서증 발급이 취소되었습니다.\n");
            }
        } else {
            printf("\n--- 도서증 정보 ---\n");
            printf("이름: %s\n", u->name);
            printf("회원 상태: 정상\n");
        }
    }
