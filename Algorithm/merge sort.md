



## Merge sort solution 1



## Merge sort solution 2



## count-array problem

merge sort可以保证，每一个元素和其他n-1个元素直接或间接比较过大小

那么 我们somehow, 能否边merge sort 边count 

Rule: whenever you want to add an element X from left side to the solution, we need to update X's counter by setting X{counter} to X (counter += j)

（总结：当谁小移谁的时候，凡是移动左边，count + j， 凡是移动右边，不更新count）



​														        4 (0)  1(0)  3(0)   2(0)

​								4 (0)  1(0)  														           3(0)   2(0)

​					4 (0) 					  1(0)  											3(0)   								2(0)

 ===========================================================================

