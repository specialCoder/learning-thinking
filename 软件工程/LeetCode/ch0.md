简单入门
===================

数组去重
-------------------

> 使用map实现数组去重
> 时间复杂度O(n)

```javascript
const solution = (arr)=>{
    const r = [];
    const map = {};
    for(let i=0;i<arr.length;i++){
        const value = arr[i];
        if(!map[value]){
            r.push(value);
            map[value] = 1;
        }
    }
    return r;
}
```

测试用例

```javascript
input: [1,1,22,3,4,55,66,3]

output:[1,22,3,4,55,66]

```