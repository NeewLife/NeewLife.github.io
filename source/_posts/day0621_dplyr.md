---
title: "6장"
output:
  html_document:
    keep_md: true
date: '2022-06-21 09:30:00'
---




# 6장
## 데이터 전처리를 위한 도구(p.98)
- dplyr : 10GB 이내, 매우 쉬움, 처리속도 느림
- data.table : 50GB 이상, 어려움, 처리속도 빠름


- dplyr 라이브러리 불러오기


```r
install.packages("dplyr",repos = "http://cran.us.r-project.org")
library(dplyr)
```


- %>% : 파이프 연산자(코드와 코드를 이어줌 (ctrl+shift+m))

```r
mpg1 <- read.csv("mpg1.csv")
str(mpg1)
```

```
## 'data.frame':	234 obs. of  5 variables:
##  $ manufacturer: chr  "audi" "audi" "audi" "audi" ...
##  $ trans       : chr  "auto" "manual" "manual" "auto" ...
##  $ drv         : chr  "f" "f" "f" "f" ...
##  $ cty         : int  18 21 20 21 16 18 18 18 16 20 ...
##  $ hwy         : int  29 29 31 30 26 26 27 26 25 28 ...
```

```r
data2 <- mpg1 %>% 
  select(drv,cty,hwy) %>% 
  filter(drv == "f")        # filter : 조건에 맞는 행 추출
```
  
- 파이프 연산자 안 쓸 경우

```r
data3 <- select(mpg1, drv, cty, hwy)
data3 <- filter(data3, drv == "f")  #이렇게 쭉 이어 붙여야 한다..
```

- rename() : 변수 이름 바꿔주기

```r
#기존데이터 <- 새 데이터 %>% rename(새 이름1=기존 이름1, 새 이름2=기존 이름2,...)
```

- count() : table()함수와 같지만 count()함수는 데이터프레임
- table()함수는 테이블 형태로 출력

```r
count(mpg1, trans)  #mpg1의 데이터 중 trans 항목의 빈도 수
```

```
##    trans   n
## 1   auto 157
## 2 manual  77
```

```r
class(count(mpg1, trans)) # count()는 데이터프레임 형태
```

```
## [1] "data.frame"
```
- table() 함수는 데이터세트$변수 이다.

```r
table(mpg1$trans)  #mpg1의 데이터 중 trans 항목의 빈도 수
```

```
## 
##   auto manual 
##    157     77
```

```r
class(table(mpg1$trans)) # table()은 테이블 형태
```

```
## [1] "table"
```

- select : 필요한 열 추출

```r
#새 데이터세트 <- 데이터세트 %>% select(열1, 열2, ...)
mpg1_1 <- mpg1 %>% select(manufacturer, trans,cty)  #manufacturer,trans,cty 열만 추출
```
- 열 삭제 응용(select 함수 안에 -c 함수로 삭제할 열을 입력)

```r
mpg1_2 <- mpg1 %>% select(-c(cty,hwy))  #cty,hwy 열이 삭제됨
```

- slice : 필요한 행 추출

```r
mpg1 %>% slice(1,4,5)  #1,4,5번 행을 추출한다. 연속적인 행이면 a:b로도 가능
```

```
##   manufacturer trans drv cty hwy
## 1         audi  auto   f  18  29
## 2         audi  auto   f  21  30
## 3         audi  auto   f  16  26
```
- filter : 조건에 맞는 행 추출
예시1

```r
mpg1_hd1 <- mpg1 %>% filter(manufacturer=="hyundai") #manufacturer가 'hyundai'인 행을 추출한다.
```
- 예시2

```r
mpg1 %>% filter(cty==max(cty))      #cty의 최댓값 함수를 바로 대입하거나,
```

```
##   manufacturer  trans drv cty hwy
## 1   volkswagen manual   f  35  44
```

```r
max(mpg1$cty)                       #cty의 최댓값을 구한 뒤
```

```
## [1] 35
```

```r
mpg1 %>% filter(cty==35)            #cty의 최댓값이 35일 때, cty의 값이 35인 행을 추출한다.
```

```
##   manufacturer  trans drv cty hwy
## 1   volkswagen manual   f  35  44
```
- 비교값이 다른 데이터 추출

```r
mpg1_hd2 <- mpg1 %>% filter(manufacturer != "hyundai")  #manufacturer가 'hyundai'가 아닌 행을 추출한다.
```
- 비교값이 크거나 작은 데이터 추출

```r
mpg1_hd3 <- mpg1 %>%filter(cty < mean(cty))  #cty값이 평균 미만인 자동차들을 추출한다.
```
- 1사분위수와 비교

```r
quantile(mpg1$cty) 
```

```
##   0%  25%  50%  75% 100% 
##    9   14   17   19   35
```

```r
mpg1_hd4 <- mpg1 %>% filter(cty<=14)  #cty값이 cty값의 1사분위값보다 작거나 같은 자동차들을 추출한다.
```
- 크거나 같거나 수학연산자를 사용한다.(<=, >, !=, ...)

- 'manufacturer=="honda"|manufacturer=="nissan"|manufacturer=="subaru"|manufacturer=="toyota"'는
- 'manufacturer %in% c("honda", "nissan", "subaru", "toyota")'로 묶어도 된다.

```r
# %in% c()로 한번에 묶기
# %>% 이 아니라 %in% 이다.
mpg1_hd5 <- mpg1 %>% filter(manufacturer %in% c("honda", "nissan", "subaru", "toyota")) 
```

- glimpse() : 데이터 미리보기
- mutate() : 새로운 파생변수 항목 만들기

```r
# 여러 조건들을 한 뒤에 데이터 미리보기
# "%>% glimpse()" 대신 "<- iris2" 쓰면 작업한 데이터가 바로 iris2로 저장된다.
iris %>%
  filter(Species == "setosa") %>% 
  select(Sepal.Length, Sepal.Width) %>% 
  filter(Sepal.Length > 5.0) %>% 
  mutate(total = Sepal.Length + Sepal.Width) %>% glimpse()
```

```
## Rows: 22
## Columns: 3
## $ Sepal.Length <dbl> 5.1, 5.4, 5.4, 5.8, 5.7, 5.4, 5.1, 5.7, 5.1, 5.4, 5.1, 5.…
## $ Sepal.Width  <dbl> 3.5, 3.9, 3.7, 4.0, 4.4, 3.9, 3.5, 3.8, 3.8, 3.4, 3.7, 3.…
## $ total        <dbl> 8.6, 9.3, 9.1, 9.8, 10.1, 9.3, 8.6, 9.5, 8.9, 8.8, 8.8, 8…
```
- &를 이용하여 반복되는 함수를 줄인다

```r
#바로 위의 함수와 같은 함수지만 filter를 &로 정리했다.
#여러 조건일 때 &는 and, |는 or, !는 not
iris %>%
  filter(Species == "setosa" & Sepal.Length > 5.0) %>% 
  select(Sepal.Length, Sepal.Width) %>% 
  mutate(total = Sepal.Length + Sepal.Width)
```

```
##    Sepal.Length Sepal.Width total
## 1           5.1         3.5   8.6
## 2           5.4         3.9   9.3
## 3           5.4         3.7   9.1
## 4           5.8         4.0   9.8
## 5           5.7         4.4  10.1
## 6           5.4         3.9   9.3
## 7           5.1         3.5   8.6
## 8           5.7         3.8   9.5
## 9           5.1         3.8   8.9
## 10          5.4         3.4   8.8
## 11          5.1         3.7   8.8
## 12          5.1         3.3   8.4
## 13          5.2         3.5   8.7
## 14          5.2         3.4   8.6
## 15          5.4         3.4   8.8
## 16          5.2         4.1   9.3
## 17          5.5         4.2   9.7
## 18          5.5         3.5   9.0
## 19          5.1         3.4   8.5
## 20          5.1         3.8   8.9
## 21          5.1         3.8   8.9
## 22          5.3         3.7   9.0
```

- group_by(trans) : trans 변수안의 범주로 행을 분류한다.
- summarise(m = mean(cty)) : cty의 평균을 m이라는 변수에 넣는다.

```r
#'group_by()' 함수랑 'summarise()' 함수는 한 세트로 생각
mpg1 %>% 
  group_by(trans) %>% 
  summarise(avg     = mean(cty)   # 평균
            , total = sum(cty)    # 총합
            , med   = median(cty) # 중간값
            , count = n())        # 빈도
```

```
## # A tibble: 2 × 5
##   trans    avg total   med count
##   <chr>  <dbl> <int> <int> <int>
## 1 auto    16.0  2507    16   157
## 2 manual  18.7  1438    18    77
```
- n() : 데이터숫자를 세어 빈도를 알려준다.(count함수와 비슷함.)

- count() 함수와 summarise(n=n()) 함수는 결과값은 같지만,
count()함수는 summarise()함수같이 여러 명령을 수행할 수 없고,
summarise(n=n())함수는 여러 명령을 수행할 수 있다.


```r
count(mpg1, trans)  #짧지만 여러 명령은 불가능..
```

```
##    trans   n
## 1   auto 157
## 2 manual  77
```

```r
mpg1 %>% 
  group_by(trans) %>% 
  summarise(n=n())  #summarise(n=n()) 함수가 더 길지만, 여러 명령을 붙일 때 빛을 본다.
```

```
## # A tibble: 2 × 2
##   trans      n
##   <chr>  <int>
## 1 auto     157
## 2 manual    77
```

- group_by() + summarise(n())+ mutate()의 조합

```r
mpg1 %>% 
  group_by(trans) %>%       #trans범주로 분류
  summarise(n=n()) %>%      #trans범주별 데이터 빈도 구하기
    mutate(total=sum(n),    #trans범주별 빈도의 총계 구하기
          pct=n/total*100)  #trans범주별 비율 구하기
```

```
## # A tibble: 2 × 4
##   trans      n total   pct
##   <chr>  <int> <int> <dbl>
## 1 auto     157   234  67.1
## 2 manual    77   234  32.9
```

- if, else : if에 조건과 명령문을 쓰고, else에 다른 명령을 쓴다.

```r
#if(조건) {명령문A} else {명령문B}
#"조건이 참이면 명령문A를 수행하고, 아니면 명령문B를 수행하라"
```
- ifelse() : if조건에 참이면 수행하고, 거짓이면 else를 해라. if+else

```r
a <- c(1,3,4,6,9)
ifelse(a%%2==0, "짝수", "홀수")  #ifelse 함수는 벡터연산 가능
```

```
## [1] "홀수" "홀수" "짝수" "짝수" "홀수"
```


  
  
