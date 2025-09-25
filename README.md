# Triangle1

Given a triangle array, return the minimum path sum from top to bottom.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index i on the current row, you may move to either index i or index i + 1 on the next row.


import sys

class Solution(object):
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        if not triangle:
            return 0
        
        N = len(triangle)
        
        # Start from the second-to-last row (index N - 2)
        # and iterate upwards to row 0.
        for r in reversed(range(N - 1)):
            
            # Iterate through each element in the current row 'r'
            for i in range(len(triangle[r])):
                
                # Update the current element's value:
                # new value = current value + minimum of the two adjacent elements below it
                
                # The adjacent elements in the row below (r + 1) are:
                # 1. triangle[r + 1][i] 
                # 2. triangle[r + 1][i + 1]
                
                min_below = min(triangle[r + 1][i], triangle[r + 1][i + 1])
                
                triangle[r][i] = triangle[r][i] + min_below
                
        # After the loops finish, the element at the top (0, 0) 
        # holds the minimum path sum from top to bottom.
        return triangle[0][0]
