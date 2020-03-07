# LeetCode-javascript
## 栈
1. 用栈实现队列 - 
  **LeetCode第232题**
  ```

  var MyQueue = function() {
      this.stack1=[]
      this.stack2=[]
  };

  MyQueue.prototype.push = function(x) {
    this.stack2.push(x)
  };

  MyQueue.prototype.pop = function() {
    return this.stack2.shift()
  };

  MyQueue.prototype.peek = function() {
    return this.stack2[0]
  };


  MyQueue.prototype.empty = function() {
    return this.stack2.length===0
  };

  /**
   * Your MyQueue object will be instantiated and called as such:
   * var obj = new MyQueue()
   * obj.push(x)
   * var param_2 = obj.pop()
   * var param_3 = obj.peek()
   * var param_4 = obj.empty()
   */
  ```
2. 逆波兰表达式 - 
**leecode第150题**
  ```
  var evalRPN = function(tokens) {
      let stack = []
      for (var i=0; i<tokens.length; i++){
          if(tokens[i]!=='+' && tokens[i]!=='-' && tokens[i]!=='*' && tokens[i]!=='/'){
              stack.push(parseInt(tokens[i]))
          }else{
              let a,b;
          switch(tokens[i]){
              case '+':
                  a=stack.pop()
                  b=stack.pop()
                  stack.push(b+a)
                  break
              case '-':
                  a=stack.pop()
                  b=stack.pop()
                  stack.push(b-a)
                  break
              case '*':
                  a=stack.pop()
                  b=stack.pop()
                  stack.push(b*a)
                  break
              case '/':
                  a=stack.pop()
                  b=stack.pop()
                  stack.push(parseInt(b/a))
          }
          }
          if(i===tokens.length-1){
              return stack[0]
          }
      }
  };
  ```
3. 用队列模拟栈 - 
**leecode第225题**
  ```
  var MyStack = function() {
    this.queue1=[]
    this.queue2=[]
  };


  MyStack.prototype.push = function(x) {
    this.queue2.push(x)
  };


  MyStack.prototype.pop = function() {
    let queue1 = this.queue1
    let queue2 = this.queue2
    let result
    while(queue2.length>1){
      queue1.push(queue2.shift())
    }
    result = queue2.shift()
    while(queue1.length>0){
      queue2.push(queue1.shift())
    }
    return result
  };

  MyStack.prototype.top = function() {
    let queue1 = this.queue1
    let queue2 = this.queue2
    let result
    while(queue2.length>1){
      queue1.push(queue2.shift())
    }
    result = queue2[0]
    queue1.push(queue2.shift())
    while(queue1.length>0){
      queue2.push(queue1.shift())
    }
    return result
  };

  MyStack.prototype.empty = function() {
    return this.queue2.length===0
  };

  /**
   * Your MyStack object will be instantiated and called as such:
   * var obj = new MyStack()
   * obj.push(x)
   * var param_2 = obj.pop()
   * var param_3 = obj.top()
   * var param_4 = obj.empty()
   */
  ```
  4. 最小栈 - 
  **leetcode第155题**
   ```
  //牺牲空间换时间
  var MinStack = function() {
    this.stack = []
  };

  MinStack.prototype.push = function(x) {
    let n = parseInt(x)
    if(this.stack.length===0){
      this.stack.push({value:n, min:n})
      return;
    }
    let tmp=undefined
    if(n<this.stack.slice(-1)[0].min){
      tmp = n
    }
    this.stack.push({
      value: n,
      min: tmp===undefined? this.stack.slice(-1)[0].min: tmp
    })  //如果新值比较小的话设为新值

  };

  MinStack.prototype.pop = function() {

    return this.stack.pop().value
  };

  MinStack.prototype.top = function() {
    return this.stack.slice(-1)[0].value
  };

  MinStack.prototype.getMin = function() {
    return this.stack.slice(-1)[0].min
  };

  /**
   * Your MinStack object will be instantiated and called as such:
   * var obj = new MinStack()
   * obj.push(x)
   * obj.pop()
   * var param_3 = obj.top()
   * var param_4 = obj.getMin()
   */
  ```
  5. 有效的括号 - 
  LeetCode第20题
    ```
  var isValid = function(s) {
    let stack = []
    for(var i=0; i<s.length; i++){
      switch(s[i]){
        case ')':
          if(stack.slice(-1)[0]==='(') stack.pop()
          else stack.push(')')
          break
        case '}':
          if(stack.slice(-1)[0]==='{') stack.pop()
          else stack.push('}')
          break
        case ']':
          if(stack.slice(-1)[0]==='[') stack.pop()
          else stack.push(']')
          break
        default:
          stack.push(s[i])
      }
    }
    return stack.length===0
  };
  ```
  6. 下一个更大元素
  leetcode第503题
  ```
  var nextGreaterElements = function(nums) {
    let stack = []
    let result =Array.from({length: nums.length})
    for(let i=0; i<nums.length; i++) result[i]=-1
    for(i=0; i<nums.length*2; i++){
      let j = i%nums.length;
      while(stack.length!==0 && nums[j]>nums[stack.slice(-1)[0]]){  //如果即将入栈元素比栈顶元素大
        let tmp = stack.pop() //删掉栈顶元素
        result[tmp] = nums[j] //记录
      }
      stack.push(j)         //入栈
    }
    return result
  };
  ```
