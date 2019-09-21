---
title: Leetcode 3 无重复字符的最长子串
date: 2019-09-21 18:26:43
categories:
- Leetcode
tags:
- Leetcode
- Javascript
---
尝试解答：

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    let letterMap = {}
    let longestLength = 0
    for(let firstIndex = 0; firstIndex < s.length; firstIndex++) {
        let currentLength = 0
        for(let secondIndex = firstIndex; secondIndex < s.length; secondIndex++) {
            if(letterMap[s[secondIndex]]){
                letterMap = {}
                break;
            } else {
                letterMap[s[secondIndex]] = true
                currentLength ++
                if(currentLength > longestLength) {
                    longestLength = currentLength
                }                
            }
        }
    }
    return longestLength
};
```

这个解答无论时空复杂度均爆表……还需要后续优化。