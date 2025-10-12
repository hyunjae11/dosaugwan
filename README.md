코드입니다 ⬇️


       #include <stdio.h>
       #include <string.h>
       #include <stdlib.h>
       
       #define BCOUNT 25
       
       typedef enum { N,O,S } Status;
       
       typedef struct {
           char bn[50];
           char bs[10];
       } Book;
       
       typedef struct {
           char mn[50];
           Status ms;
           int mo;
           char c[10];
       } M;
       
       Book b[BCOUNT] = {
           {"1984","대출 가능"},{"노인과 바다","대출 가능"},{"죄와 벌","대출 가능"},{"동물농장","대출 가능"},
           {"위대한 개츠비","대출 가능"},{"82년생 김지영","대출 가능"},{"채식주의자","대출 가능"},{"소년이 온다","대출 가능"},
           {"마지막 팬클럽","대출 가능"},{"7년의 밤","대출 가능"},{"연금술사","대출 가능"},{"내 이름은 빨강","대출 가능"},
           {"시간을 달리는 소녀","대출 가능"},{"클라우드 아틀라스","대출 가능"},{"모모","대출 가능"},{"셜록 홈즈 전집","대출 가능"},
           {"해리 포터","대출 가능"},{"나미야 잡화점의 기적","대출 가능"},{"기억 전달자","대출 가능"},{"더 마션","대출 가능"},
           {"유령생활기록부","대출 가능"},{"눈먼자들의 도시","대출 가능"},{"워렌버핏의 돈 관리법","대출 가능"},{"국어사전","대출 가능"},
           {"이스터Egg","대출 가능"}
       };
       
       M m;
       
       void im(){
           strcpy(m.mn,"SNB");
           m.ms=N; m.mo=0;
           sprintf(m.c,"%d",rand()%10000);
       }
       
       void sc(){
           printf("====== 도서증 ======\n");
           printf("이름: %s\n",m.mn);
           printf("회원상태: %s\n",m.ms==N?"정상":m.ms==O?"연체":"정지");
           printf("코드: %s\n",m.c);
           printf("==================\n");
       }
       
       void lb(){
           for(int i=0;i<BCOUNT;i++)
               printf("%d. 《%s》 상태: %s\n",i+1,b[i].bn,b[i].bs);
       }
       
       void bb(){
           if(m.ms==S){printf("회원 상태가 정지되어 대출 불가\n"); return;}
           int n;
           lb();
           printf("대출할 책 번호 입력: ");
           scanf("%d",&n); n--;
           if(n<0 || n>=BCOUNT){printf("잘못된 번호\n"); return;}
           if(strcmp(b[n].bs,"대출중")==0){printf("이미 대출중\n"); return;}
           strcpy(b[n].bs,"대출중");
           printf("《%s》 대출 완료\n",b[n].bn);
       }
       
       void rb(){
           int f=0;
           for(int i=0;i<BCOUNT;i++)
               if(strcmp(b[i].bs,"대출중")==0) f=1;
           if(!f){printf("대출중인 책 없음\n"); return;}
           int n;
           lb();
           printf("반납할 책 번호 입력: ");
           scanf("%d",&n); n--;
           if(n<0 || n>=BCOUNT || strcmp(b[n].bs,"대출중")!=0){printf("잘못된 입력\n"); return;}
           m.mo++;
           if(m.mo>=3) m.ms=S; else m.ms=O;
           strcpy(b[n].bs,"대출 가능");
           printf("《%s》 반납 완료\n",b[n].bn);
       }
       
       void rbk(){
           int i=rand()%BCOUNT;
           printf("추천 도서: 《%s》\n",b[i].bn);
       }
       
       int main(){
           srand(1);
           im();
           int c;
           while(1){
               system("cls");
               printf("\n1. 대출 \n2. 반납 \n3. 책 목록 \n4. 추천 \n5. 도서증 \n6. 종료\n선택: ");
               scanf("%d",&c);
               switch(c){
                   case 1: bb(); break;
                   case 2: rb(); break;
                   case 3: lb(); break;
                   case 4: rbk(); break;
                   case 5: sc(); break;
                   case 6: exit(0);
                   default: printf("잘못된 선택\n");
               }
               printf("\n계속하려면 엔터를 누르세요...");
               getchar(); getchar();
           }
       }


