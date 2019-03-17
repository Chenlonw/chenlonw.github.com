---
layout: post
title:  "Say Hello to Fortran 90"
excerpt: "recently I need to transform some code from fortran to C, This is just a glance of Fortran"
date:   2016-08-24
categories: [tutorial]
comments: true
---

> This note records the basic programming grammar with Fortran 90

---

#### Basics
```
写作格式区别为 Fixed format 和 free format.
Fixed format 不同字节的地方有不同的含义，是为了早起打洞程序录入准备的;
Free format 是现在的fortran 通用格式。
```

+ comments by `!`
+ 每行132个字符, 每行末尾如果是 `&` 表示下行还会连接
+ Fortran is **case insensitive**

------

#### Appendix My test code block
```fortran
!---A fortran.90 notes for primary learners
! this is a primary notes about learning
! fortran90 code by gfortran complier
! Auther : Chenlong Wang 
! Tongji University & NTNU
! 2014.10.24
! Email: clwang88@gmail.com
!
! Reference:
! 1. http://wenku.baidu.com/link?url=GxtpCOgD3yN35d7x5hHFVoJvEMsI0n6aOkv8ZmIMhJHrFAQiYTYm2SOOKlNyouto8dEScpG4h6POosQIxF43cHIuVv0X2HCRpbPAxjBNxyy
! 2. <Fortran 90 程序设计教程> 刘卫国 2003
!
!Free format (the other one is fixed format)
!Variables type: Integer, Real, complex, character, logical
!Fortran doesn't distinguish the upper or lower case of input variables
!Fortran doesn't need ; to finish a line of code, just start from a new line
!The application of variables should ahead of all the excutable codes
!STOP means the program terminated, END (END Program/ END program main) means the code writing is finished

program main
 IMPLICIT NONE !fortran has an implicit rule: variable name start with i-n will be regarded as integer

 integer :: a !applicate an variable
 integer :: i, j !type (category argument), attributes :: variable name
 integer :: day
 logical :: log1, log2
 complex :: cplx=(1.9, 2.0)
 real(8), parameter :: pi=3.1415926535d0 !define a const variable with double precision
 real :: tmp
 real :: average
 real , dimension (3) :: m, n, l !define an array
 real , dimension (2,2) :: mat1 !define an array index from x(1:2) z(1:2) has 4 elements
 real , dimension (1:3, 2:4) :: mat2 !define an array index from x(1:3) z(2:4)
 real , dimension(:,:), allocatable :: vx !define a dynamic array 
 integer :: nx=5
 integer :: nz=10
 real funt !take care the function name shoud applied in program
 real linefun !line function
 real ::x
 linefun(x) = 3*x + x**2

 type staff !define a struct
 character(15) Sname
 logical :: sex
 real :: salary
 end type

 type(staff) :: s1=staff("chlwang", .true. , 2000.0) ! you cant put it after excutable lines
 type(staff) :: s2=staff("jbcheng", .true. , 10000.0)

 write(*,*) "Hello World !!" !the first * is choose destination the second is sheet control 
 print *, & !& means this line isn't finished
 "Hello World !!"

 print *, a

 !---test the parameter function of fortran
 print *, pi

 !---the matrix operation in fortran
 m=2.000 !fortran can initial the array directly by '=' operator
 n=4.000

 print *,"m=", m
 print *,"n=", n

 l=m*n
 print *,"m*n=", l

 l=m+n
 print *,"m+n=", l

 l=sin(m)
 print *,"sin(m)=", l

 print *, 'up and low bound of array # in dimension i'
 print *, ubound(l)
 print *, lbound(mat1,1)
 print *, lbound(mat2)

 tmp=dot_product(m,n) !some similar intrinsic commond like matmul transpose
 print *,"inner product of m and n", tmp

 !---alloc and delete an array
 allocate(vx(nx, nz))
 vx = 0
 deallocate(vx)

 !---if syntax
 write (*,*) "chech if a is a positive or negative num"
 write (*,*) "please input a!"
 read (*,*) a
 if (a>0) then
 print *,"a is a positive number"
 else if (a==0) then
 print *,"a is zero"
 else
 print *,"a is a negative number"
 end if

 !---Do syntax
 print *, "Do syntax"
 do i=1,10,2 !e1(1) start number, e2(10) end number, e3(2) increment number
 print *, i
 end do

 !---Do while syntax
 print *, "Do while syntax"
 i = 1
 do while (i<10)
 print *, i
 i = i + 3
 end do

 !---case syntax
 print *, "Case syntax"
 write (*,*) "please input 1-3"
 read (*,*) day

 selectcase(day)
 case(1)
 print *, "mon"
 case(2)
 print *, "tue"
 case(3)
 print *, "wed"
 case default
 print *, "wrong"
 end select

 !---I/O in fortran 
 100 format(/i4, 3xf4.1, 3xf4.1) !'/' means change a new line ; 'i' means integer, 'x' means space, 'f'means float 4.1 means 4 positions
 !!!
 !!! for integer type: r i/b w r means repeat times(default is 1), i means decimal b means binary,&
 !!! w means width, if w is not long enough, it will use ** to instead of 
 !!! for real type: r f/e W.w r repeat times, f=real e=exponent W width of width, w width of decimal places (when no '.' in your number)
 !!! if . is aviable in your number the w will not works any more
 !!!
 !100 format(/i2, 2f4.1) 
 open (1, file="out", status='unknown')
 write (1, 100) a, m(2), n(1)
 !write (1, "(i4, 2(f4.1, f4.1))") a, m(2), n(1) !/another choice
 close (1)

 !---logical variable in fortran
 print *, 'check if the input number between (-PI, PI)'
 read *, tmp
 log1 = tmp>=-pi .and. tmp<=pi ! logic variables and logical operators .and. .or. .not. .eqv. .neqv.
 if (log1) then
 print *, 'Yes!'
 else
 print *, 'No!'
 end if

 !---use of line function
 print *, 'calculation of 3x+x^2'
 print *, LINEFUN(tmp)

 !---use of function
 !print *, 'calculation of 3x+x^2'
 print *, funt(tmp)

 !---use the subroutines
 call sub(1.0d0) !if the type of variable should matched with your subroutine

 !---use the subroutines the formal parameter and actual use a same inner memory
 call init(mat1)
 do i=1,2
 do j=1,2
 print *, mat1(i,j)
 enddo
 enddo

 !---use struct in fortran 
 average = (s1%salary + s2%salary)/2.0 !quotation of struct
 print *, "the average salary of s1 and s2 is:", average

 !--- the File I/O in fortran 
 open (10, FILE="A.txt", form="formatted", access="sequential", action="write") !formatted in/out put
 write (10, '(xi3)') 911
 write (10, '(xa7)') 'welcome'
 close (10)

 open (11, FILE="B.txt", form="unformatted", access="sequential",action="write") !unformatted i/o
 write (11) 911
 write (11) 'welcome'
 close (11)

 !open (12, FILE="C.txt", form="binary", access="sequential", status="unknown") 
 !write (12) 911
 !write (12) 'welcome'

end program main

REAL FUNCTION FUNT(x)
 implicit none
 real ::x
 FUNT = 3 * x + x ** 2
 END FUNCTION FUNT

subroutine sub(x)
 implicit none
 real(8) :: x
 write (*,*) "x = ", x
 end subroutine sub

subroutine init(x)
 implicit none
 real , dimension (2,2) :: x
 x = 2.3
 end subroutine init
```


