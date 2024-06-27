## Linear regression
### Data 정의
공부 시간 - 성적 예측

Training/Test dataset

torch.tensor의 형태, 입력과 출력을 따로 저장
```
x_train = torch.FloatTensor([1],[2],[3])
y_train = torch.FloatTensor([2],[4],[6])
```

### Hypothesis
y = Wx + b (weight, bias)
- W와 b 0으로 초기화 (항상 출력 0 예측)
- requires_grad = True (학습할 것임)

```
W = torch.zeros(1, requires_grad=True)
b = torch.zeros(1, requires_grad=True)
hypothesis = x_train * W + b
```

### Compute Loss
Mean Squared Error
![image](https://github.com/pomota/TIL/assets/132712212/37568ec1-d14b-4f69-a5a4-0bd11c8b499b)
```
cost = torch.mean((hypothesis - y_train)**1)
```

### Gradient descent
W와 b를 학습시킴
- `torch.optim` 라이브러리 사용
- lr은 learning rate

항상 있는 3단계
1. zero_grad(): gradient 초기화
2. backward(): gradient 계산
3. step(): 개선

```
optimizer = optim.SGD([W,b], lr=0.01)

optimizer.zero_grad()
optimizer.backward()
optimizer.step()
```

### 전체 코드
```
x_train = torch.FloatTensor([[1],[2],[3]])
y_train = torch.FloatTensor([[2],[4],[6]])

W = torch.zeros(1, requires_grad=True)
b = torch.zeros(1, requires_grad=True)

optimizer = optim.SGD([W,b],lr=0.01)

nb_epochs = 1000
for epoch in range(1, nb_epochs+1):
  hypothesis = x_train * W + b
  cost = torch.mean((hypothesis-y_train)**2)

  optimizer.zero_grad()
  optimizer.backward()
  optimizer.step()
```
