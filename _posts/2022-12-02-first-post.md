---
title: 전산 언어II 프로젝트
layout: post
post-image: /cpp_fitness.jpg
description: 이번에 구현해본 전산언어 프로젝트에 대해. 이 프로젝트는 구조체와 메모리 동적할당, 파일 입출력등의 기능등을 사용하였다. 
tags:
- 전산 언어 II
- cpp
- 프로젝트
---

# 전산언어 II 

## 피트니스 회원관리 프로그램


---

## 구현한 주요 기능
1. [회원등록](#회원-등록)
2. [등록된 회원 조회](#등록된-회원-조회)
3. [생일 회원 조회](#생일-회원-조회) 
4. [회원 정보 출력](#회원-정보-출력)
5. [회원 탈퇴](#회원-탈퇴) 
6. [파일 입출력](#파일-입출력)
7. [파일 분할](#파일-분할)

---

**본론으로 들어가기전 피트니스 회원 관리 프로그램에는 총 6개의 주요 기능이 있다. 각각 별도의 함수로 구현을 하였다. 필자는 visual studio 2022버전을 사용하였다.**

**전체 코드는 밑에 링크로 달아두겠다.** 


본론
===


 
### 회원 등록

회원 등록기능을 선택한다면 먼저 회원의 락커룸(회원코드)를 등록한다. 등록 후 회원의 정보인 성함, 전화 번호, 주소 마지막으로 생년월일을 등록한다. 

총 등록할 수 있는 회원의 수는 50명이다. 회원의 정보는 모두 구조체에 저장한다. 
그리고 만약 락커룸(회원 코드)에 먼저 등록된 회원이 있다면 더 이상 등록이 되지 않게 설계하였다.

>회원 등록 함수코드이다.


```cpp
void regis(Information* infor)
{
	int num1=0;

	printf("\n<<회원등록을 선택하셨습니다.>> \n");
	printf("[락커룸 번호]  및 [회원코드]등록\n");
	do {

		do
		{
			printf("몇번째 락커룸:"); scanf_s("%d", &num1);
			if (num1 < 1 || num1>50)
			{
				printf("다시입력해주세요. \n");
			}
		} while (num1 < 1 || num1>50);
		if (infor[num1 - 1].name != NULL)
		{
			puts("락커룸에 회원이 존재합니다. ");
			puts("다른락커룸을 선택해주세요. ");
			
		}
	} while (infor[num1 - 1].name != NULL);
}
```


위에 보이는 것처럼 먼저 락커룸(회원코드)를 입력하여 num1에 저장한다. 이 num1의 값을 do~while문을 값 경계 검사를 1부터 50사이값까지 한다. 값 경계검사를 통과하면, 그 um1을 가지고 구조체에 접근한다.

두번째 do~while문을 이용하여 조건을 검사한다. 락커룸(회원코드)에 먼저 등록된 회원이 있는지 검사한다. 만약 먼저 등록된 회원이 있다면 락커룸번호부터 다시 입력해야 한다. 

모든 조건을 통과하면 회원의 정보를 입력한다. 

>회원 정보 입력코드이다. 


```cpp
printf("<<%d번째 락커룸 회원성명>>: ", num1);
	num1 -= 1;
	getchar();

	infor[num1].name = (char*)malloc(sizeof(char) * 20);
	gets_s(infor[num1].name,sizeof(char)*20);

	printf("<회원전화번호입력>: ");
	infor[num1].num = (char*)malloc(sizeof(char) * 25);
	gets_s(infor[num1].num, sizeof(char)*25);


	printf("<회원주소입력>: ");
	infor[num1].adr = (char*)malloc(sizeof(char) * 30);
	gets_s(infor[num1].adr, sizeof(char)*30);
	
	
	do {
		printf("<회원생년입력(1900~2022)>: "); scanf_s("%d", &infor[num1].year);
	} while (infor[num1].year < 1900 || infor[num1].year > 2022);
	do {
		printf("<회원생월입력(1월~12월)>: "); scanf_s("%d", &infor[num1].month);
	} while (infor[num1].month < 1 || infor[num1].month > 12);
	do {
		printf("<회원생일입력(1일~31일)>: "); scanf_s("%d", &infor[num1].day);
	} while (infor[num1].day < 1 || infor[num1].day > 31);
	printf("-----회원 등록완료----- \n");
}
```



구조체를 배열로 선언, 0~49의 크기이기 때문에 num1을 -1을 해준다. 그리고 문자열인 성함, 전화번호, 주소를 메모리 동적할당(malloc)으로 메모리크기를 할당해준다. 
그리고 입력된 문자열을 키보드로 입력받아(gets) 각 구조체에 저장한다. 

그후 생년월일을 입력한다. 각각 do~while문을 이용해서 보는 것처럼 값 경계 검사를 실시하였다. 모두 입력하면 회원 등록이 성공한다.

---

### 등록된 회원 조회

등록된 회원 조회기능을 선택한다면 락커룸 칸과 락커룸 넘버가 함께 뜬다. [회원 등록](#회원-등록)기능에서 등록을 하였다면
회원의 이름이 출력된다. 비어 있는 락커룸이라면 빈칸이 출력된다. 

현재 등록되어 있는 총 회원의 수와 등록할 수 있는 회원의 수도 함깨 조회된다. 

>회원 조회함수 코드이다.


```cpp
void list(Information* infor)
{
	int i, num3;

	printf("\n회원조회를 선택하셨습니다.\n");
	num3 = 0;
	for (i = 0; i < SIZE; i++)
	{
		if (infor[i].name == NULL)
		{
			printf("%3d.[%7c]\t", i + 1, '\0');
			num3++;
		}
		else
		{
			printf("%3d.[%4s]\t", i + 1, infor[i].name);
		}
		if ((i + 1) % 5 == 0)
		{
			puts(" ");
		}
	}
	printf("\n");
	printf("등록된 회원의 수는 %d명입니다. \n그리고 등록할 수 있는 회원의 수는 %d입니다. \n", SIZE - num3, num3);
}
```

for문을 이용하여 먼저 모든 구조체배열을 출력하거나 비교한다. 

모든 구조체의 문자열은 NULL로 초기화를 하였기 때문에 if문을 사용하여 NULL과 비교한다. 만약 NULL일시 '\0'이 출력되며 빈칸이 된다.


NULL이 아닐시 그 구조체에 저장된 성함이 출력된다. for문에 사용한 i를 이용하여 락커룸번호도 함께 출력된다. 그리고 5로 나눈 나머지가 0일때 줄 바꿈을 하도록 if문을 설계하였다. 

---
### 생일 회원 조회

생일 회원 조회기능을 선택하면 먼저 몇 월달의 생일을 회원을 조회 할 것인지 입력한다. 그 달에 생일인 회원이 있다면, 회원의 성함과 나이가 함께 출력된다. 
만약 그 달에 생일인 회원이 없다면, 생일인 회원이 없다는 문구와 함께 출력되지 않는다. 

>생일회원조회 함수코드이다.


```cpp
void BDAY(Information* infor) 
{
	int num3, i;
	int check = 0;
	printf("\n<<생일 회원조회를 선택하셨습니다.>> \n");
	printf("몇월생인지 입력해주세요.: ");
	scanf_s("%d", &num3);
	printf("%d월생은", num3);

	for (i = 0; i <= SIZE; i++)
	{
		if (num3 == infor[i].month)
		{
			printf(" %s입니다. \n", infor[i].name);
			printf("나이는 %d입니다. \n", (2022 - infor[i].year)+1);
			check++;

		}
	}
	
	if (check == 0)
	{
		printf("없습니다.\n");
	}
}

```

생일회원조회 함수 코드다. 먼저 몇월생을 조회할 것인지 입력한다. 입력한 값을 num3에 저장한다. 그리고 for문을 이용하여 모든 구조체에 접근한다.

if문을 이용하여 num3값과 구조체에 저장된 생월과의 값과 비교한다. 그 값이 동일하다면 그 회원의 성함, 나이가 출력된다. 후위증가인 check가 증가한다.
만약 동일한 값이 없다면, check의 값이 증가하지 않아 if문이 실행된다. 생일을 입력할 때 do~while로 값 경계검사를 했으면 더 좋을 것 같다. 

---

### 회원 정보 출력


이 함수는 회원의 정보를 출력한다. 회원의 정보를 출력할려면 성함으로 회원을 조회 또는 회원코드로조회 중 택 1을 하여 정보를 조회한다. 

성함을 입력하면 입력된 성홤과 등록된 성함을 비교하여 같은 성함이 있다면 정보를 출력한다. 없다면 출력이 안된다. 

회원 코드로 조회를 선택하면 입력한 회원 코드에 회원이 등록되어 있따면 정보가 출력된다. 

>회원정보출력 코드

먼저 기능선택 코드이다. 
```cpp
void MemberINfor(Information* infor)
{
	int num3, i, num1 = 0;
	char ch1[10];
	printf("\n<<회원정보 출력을 선택하셨습니다.>> \n");
	do
	{
		printf("<1. 성함으로 검색> 또는 <2. 회원코드로 검색>"); scanf_s("%d", &num3);
		if (num3 > 2 || num3 < 1)
		{
			printf("다시 입력해주세요. \n");
		}
	} while (num3 > 2 || num3 < 1);
```

do~while을 이용하여 값 경계검사를 진행하였다. 

1번 기능인 성함으로 검색기능이다. 

```cpp
if (num3 == 1)
	{
		getchar();
		printf("성함을 입력하세요: ");
		gets_s(ch1, sizeof(ch1));
		for (i = 0; i < SIZE; i++)
		{
			if (infor[i].name != NULL && !strcmp(ch1, infor[i].name))
			{
				printf("\n락커룸넘버: [%d]\n", i + 1);
				printf("성함: %s\n", infor[i].name);
				printf("전화번호: %s\n", infor[i].num);
				printf("주소: %s\n", infor[i].adr);
				printf("생년월일: %d년 %d월 %d일\n", infor[i].year, infor[i].month, infor[i].day);
				num1++;
				break;
			}
		}
		if (num1 == 0)
		{
			printf("%s회원이 존재하지 않습니다. \n", ch1);
		}
	}
```
먼저 getchar를 이용하여 입력버퍼를 비워주었다. strcmp를 이용하여 입력된 성함과 등록된 성함을 비교 후 같으면 참의 값이 반환되도록 not을 붙여 주었다. 
그리고 만약 회원이 존재하지 않을 시 num1를 이용하여 카운트 후 if문이 실행되도록 설계하였다. 

2번 기능인 회원코드로 검색이다.

```cpp
	else if (num3 == 2)
	{
		printf("회원코드를 입력하세요.[락커룸 넘버]\n");
		do
		{
			printf("몇번째 락커룸:"); scanf_s("%d", &num1);
			if (num1 < 0 || num1>50)
			{
				printf("다시입력해주세요. \n");
			}
		} while (num1 < 0 || num1>50);
		printf("\n락커룸넘버: [%d]\n", num1);
		num1 -= 1;
		if (infor[num1].name == NULL)
		{
			printf("%d번라커룸은 빈 락커룸입니다. \n", num1 + 1);

		}
		else if (infor[num1].name != NULL)
		{
			printf("성함: %s\n", infor[num1].name);
			printf("전화번호: %s\n", infor[num1].num);
			printf("주소: %s\n", infor[num1].adr);
			printf("생년월일: %d년 %d월 %d일\n", infor[num1].year, infor[num1].month, infor[num1].day);
		}

```

do~while로 값 경계 검사를 진행하였다. NULL로 초기화를 하였으니, NULL과 비교한다. 등록된 락커룸이면 회원의 정보가 출력된다. 

---
### 회원 탈퇴

회원 탈퇴도 회원 정보 조회와 같은 매커니즘이다. 

메모리 동적할당이 되어 있기 때문에 할당해준 메모리를 풀어준 뒤 다시 NULL로 초기화 한다. 나머지 정수형 변수는 0으로 초기화 한다. 

여기서는 간단하게 메모리 동적할당만 보고 가겠다. 

```cpp
free(infor[i].name);
free(infor[i].adr);
free(infor[i].num);
```

이런 식으로 할당된 메모리를 풀어준 뒤 초기화 해주면 된다. 

---
### 파일 입출력

현재 등록된 회원들의 정보를 파일에 저장한다. 필자는 .txt파일에 저장해 주었다. 

>파일 입출력 코드 

```cpp
void Customer_list(Information* infor)
{
	int i, j;
	char str[20];
	FILE* fp;
	printf("파일 입출력 선택!!\n");
	fp = fopen("data.txt", "wt");
	if (fp == NULL)
	{
		puts("파일 오픈 실패!");
		system("pause");
		return;
	}
	else
	{
		puts("파일 출력성공!");
	}
	for (i = 0; i < SIZE; i++)
	{
		if (infor[i].name != NULL)
		{
			fprintf(fp, "<<<<<<<<등록된 %d번째 회원>>>>>>>>>\n", i + 1);
			fprintf(fp, "성함:%s\n", infor[i].name);
			fprintf(fp, "주소:%s\n", infor[i].adr);
			fprintf(fp, "전화번호:%s\n", infor[i].num);
			fprintf(fp, "생년월일: %d년%d월%d일생\n", infor[i].year, infor[i].month, infor[i].day);
		}
	}
	fclose(fp);
}
```
data.txt파일에 저장해 줄 것이다. 파일을 쓰기 모드로 열어준다. if문을 활용하여 파일이 열리지 않았을 때를 대비한다. 

for문과 if문을 활용하여 값을 비교후 fprintf를 활용하여 파일에 저장한다. 

---
### 파일 분할

2개의 헤더파일과 2개의 cpp파일로 총 4개의 파일로 분할 하였다. 구조체와 함수 선언은 헤더 파일로 만들었다. main함수와 나머지 기능들의 코드는 cpp파일로 만들었다. 

전체 코드 링크: <https://github.com/woojinw0rld/steady/tree/main/fitness.cpp>

[전체 코드 링크](https://github.com/woojinw0rld/steady/tree/main/fitness.cpp)