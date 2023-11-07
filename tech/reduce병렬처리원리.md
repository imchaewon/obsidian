이미지자료/reduce병렬처리원리.png 참고

int a = Stream.of(1,2,3,4,5,6,7,8,9,10).parallel().reduce(0,(i,j)->{
	System.out.println(Thread.currentThread().getName() + " : " + i + "-" + j + "="+(i-j));
	return i-j;
});
System.out.println(a);





ForkJoinPool.commonPool-worker-1 : 0-2=-2
ForkJoinPool.commonPool-worker-2 : 0-1=-1
ForkJoinPool.commonPool-worker-2 : -1--2=1 ★
ForkJoinPool.commonPool-worker-2 : 1-1=0 ★

-1        -2        -3        -4
  (-1)-(-2)			  (-3)-(-4)
	  1				  	  1
	  		 (1)-(1)
	  		 	0





main : 0-3=-3
ForkJoinPool.commonPool-worker-1 : 0-2=-2
main : 0-1=-1
ForkJoinPool.commonPool-worker-2 : 0-4=-4
main: -1 + -2 = -3 ★
ForkJoinPool.commonPool-worker-3 : 0-5=-5
ForkJoinPool.commonPool-worker-3: -4 + -5 = -9 ★
ForkJoinPool.commonPool-worker-3: -3 + -9 = -12 ★
ForkJoinPool.commonPool-worker-3: -3 + -12 = -15 ★

-1        -2        -3        -4        -5
  (-1)-(-2)						(-4)-(-5)
	  1								1
						   (-3)-(1)
							  -4
				 (1)-(-4)
				 	5





main : 0-4=-4
ForkJoinPool.commonPool-worker-1 : 0-2=-2
ForkJoinPool.commonPool-worker-6 : 0-3=-3
ForkJoinPool.commonPool-worker-2 : 0-1=-1
ForkJoinPool.commonPool-worker-6 : -2--3=1 ★
ForkJoinPool.commonPool-worker-6 : -1-1=-2 ★
ForkJoinPool.commonPool-worker-1 : 0-5=-5
main : 0-6=-6
main : -5--6=1 ★
main : -4-1=-5 ★
main : -2--5=3 ★

-1        -2        -3        -4        -5        -6
			(-2)-(-3)					  (-5)-(-6)
				1							  1
	   (-1)-(1)						(-4)-(1)
	      -2							-5
	      				(-2)-(-5)
	      					3





main : 0-6=-6
main : 0-5=-5
main : -5--6=1 ★
ForkJoinPool.commonPool-worker-5 : 0-3=-3
ForkJoinPool.commonPool-worker-7 : 0-7=-7
main : 0-8=-8
ForkJoinPool.commonPool-worker-2 : 0-2=-2
ForkJoinPool.commonPool-worker-8 : 0-4=-4
ForkJoinPool.commonPool-worker-4 : 0-1=-1
ForkJoinPool.commonPool-worker-8 : -3--4=1 ★
main : -7--8=1 ★
main : 1-1=0 ★
ForkJoinPool.commonPool-worker-4 : -1--2=1 ★
ForkJoinPool.commonPool-worker-4 : 1-1=0 ★
ForkJoinPool.commonPool-worker-4 : 0-0=0 ★


-1        -2        -3        -4        -5        -6        -7        -8
  (-1)-(-2)			  (-3)-(-4)			  (-5)-(-6)			  (-7)-(-8)
	  1					  1				  	  1					  1
			 (1)-(1)					  	  		 (1)-(1)
				0						  	  		 	0
								(0)-(0)
								   0





main : 0-7=-7
ForkJoinPool.commonPool-worker-1 : 0-6=-6
ForkJoinPool.commonPool-worker-7 : 0-3=-3
ForkJoinPool.commonPool-worker-3 : 0-5=-5
ForkJoinPool.commonPool-worker-1 : -6--7=1 ★
ForkJoinPool.commonPool-worker-5 : 0-1=-1
ForkJoinPool.commonPool-worker-8 : 0-4=-4
ForkJoinPool.commonPool-worker-2 : 0-2=-2
main : 0-10=-10
ForkJoinPool.commonPool-worker-6 : 0-9=-9
ForkJoinPool.commonPool-worker-4 : 0-8=-8
ForkJoinPool.commonPool-worker-6 : -9--10=1 ★
ForkJoinPool.commonPool-worker-6 : -8-1=-9 ★
ForkJoinPool.commonPool-worker-2 : -1--2=1 ★
ForkJoinPool.commonPool-worker-8 : -4--5=1 ★
ForkJoinPool.commonPool-worker-8 : -3-1=-4 ★
ForkJoinPool.commonPool-worker-8 : 1--4=5 ★
ForkJoinPool.commonPool-worker-6 : 1--9=10 ★
ForkJoinPool.commonPool-worker-6 : 5-10=-5 ★


-1        -2        -3        -4        -5        -6        -7        -8        -9        -10
  (-1)-(-2)						(-4)-(-5)			(-6)-(-7)					  (-9)-(-10)
	  1								1				1							  1
						   (-3)-(1)											 (-8)-(1)
							  -4											 	-9
				  (1)-(-4)											(1)-(-9)
					 5												   10
					 					   (5)-(10)
					 					   	 -5























