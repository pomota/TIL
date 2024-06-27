## Tensor Manipulation 2
### View (Reshape)
cf) shape: (깊이, 행, 열) -> 늘어난 차원이 앞에 추가됨

```
t = torch.FloatTensor([[0,1,2],[3,4,5]],[[6,7,8],[9,10,11]])
t.shape # torch.size([2,2,3])
t.view([-1,1,3]) # torch.size([4,1,3]) # -1은 모르는 숫자 의미 (총 개수로 맞춰줌)
```

### Squeeze
불필요한 차원 제거
```
ft = torch.FloatTensor([0],[1],[2]) # (3,1)
ft.squeeze() # (3,)
ft.squeeze(dim= ) # 특정 dim 없애기, 해당 dimension에 1이 있을 경우 없앰
```

### Unsqueeze
squeeze 반대 -> dimension을 반드시 명시해줘야 함
```
ft.unsqueeze(0) # dimension 0에 1을 넣어라 (3,) -> (1,3)
ft.view(1,-1)
ft.unsqueeze(1) # (3,) -> (3,1)
ft.unsqueeze(-1) # -1 dimension, 마지막 dimension을 의미
```

### Type Casting
tensor의 type을 바꿔줌
```
lt = torch.LongTensor([1,2,3,4])
lt.float()
bt = toch.ByteTensor([True,False]) # boolean
bt.long() bt.float() # 0과 1로 대체
```

### Concatenate
```
x # (2,2)
y # (2,2)
torch.cat([x,y], dim=0) # (4,2)
torch.cat([x,y], dim=1) # (2,4)
```

### Stacking
concatenating을 단축시켜놓은 것
```
x, y ,z # (2,)
torch.stack([x,y,z]) # (3,2)
torch.stack([x,y,z],dim=1) # (2,3) 3이 dim=1로 
```

### Ones and Zeros
```
x = torch.FloatTensor([0,1,2],[2,1,0])
torch.ones_like(x) # 1로 가득찬 tensor
torch.zeros_like(x) # 0으로 가득찬 tensor
```
- 연산은 같은 device에서 선언된 것끼리 가능 (CPU, GPU, multiple GPU)
- ones_like, zeros_like는 같은 device에 tensor를 선언

### In-place Operation
```
x.mul_(y) # 메모리를 새로 선언하지 않고 기존의 tensor에 넣음
```
